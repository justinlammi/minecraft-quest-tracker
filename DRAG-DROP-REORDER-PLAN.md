# Drag-and-Drop Quest Reordering Implementation Plan

## Overview
Add drag-and-drop functionality to the admin panel to allow parents to reorder quests. The custom order will persist to Firebase and sync across all devices including the display.

## Current State

### Quest Data Structure (Firebase)
```javascript
chores/
  {questId}/
    name: string
    points: number
    icon: string
    daysActive: string ('all' | 'weekday' | 'weekend')
    createdAt: timestamp
    // No sortOrder field currently exists
```

### Current Rendering Behavior
- Quests display in insertion order (order they were created)
- No explicit sorting logic
- Both admin and display files iterate through quests without ordering

## Implementation Plan

### Phase 1: Update Data Model

#### 1.1 Add `sortOrder` Field to New Quests
**File:** `minecraft-quest-tracker-admin.html`
**Function:** `addQuest()` (around line 680)

**Change:**
```javascript
// BEFORE:
database.ref(`chores/${questId}`).set({
    name: name,
    points: points,
    icon: selectedEmoji,
    daysActive: selectedDaysActive,
    createdAt: Date.now()
});

// AFTER:
const maxSortOrder = quests.reduce((max, q) => Math.max(max, q.sortOrder || 0), -1);

database.ref(`chores/${questId}`).set({
    name: name,
    points: points,
    icon: selectedEmoji,
    daysActive: selectedDaysActive,
    createdAt: Date.now(),
    sortOrder: maxSortOrder + 1  // NEW - add to end of list
});
```

#### 1.2 Initialize Sort Order for Existing Quests
Add a migration function and button to admin panel.

**Add function:**
```javascript
function initializeSortOrder() {
    if (!confirm('INITIALIZE SORT ORDER FOR ALL QUESTS?')) return;

    database.ref('chores').once('value')
        .then(snapshot => {
            const data = snapshot.val();
            if (!data) {
                alert('NO QUESTS TO INITIALIZE');
                return;
            }

            const updates = {};
            Object.keys(data).forEach((key, index) => {
                if (data[key].sortOrder === undefined) {
                    updates[`chores/${key}/sortOrder`] = index;
                }
            });

            if (Object.keys(updates).length === 0) {
                alert('ALL QUESTS ALREADY HAVE SORT ORDER');
                return;
            }

            return database.ref().update(updates);
        })
        .then(() => {
            showSuccess('✅ SORT ORDER INITIALIZED!');
        })
        .catch(error => {
            alert('ERROR: ' + error.message);
        });
}
```

**Add button to Quick Actions section** (after line 523):
```html
<button onclick="initializeSortOrder()" class="btn-secondary" style="margin-left: 10px;">🔢 INITIALIZE ORDER</button>
```

### Phase 2: Implement Drag-and-Drop UI

#### 2.1 Add Drag-and-Drop State Variables
**File:** `minecraft-quest-tracker-admin.html`
**Location:** After existing variables (around line 602)

```javascript
let draggedElement = null;
let draggedIndex = null;
```

#### 2.2 Update `renderQuests()` Function
**File:** `minecraft-quest-tracker-admin.html`
**Function:** `renderQuests()` (around line 832)

**Changes:**
1. Sort quests by `sortOrder` before rendering
2. Add drag-and-drop attributes to each quest item
3. Add drag handle visual indicator

```javascript
function renderQuests() {
    const container = document.getElementById('questsList');

    if (quests.length === 0) {
        container.innerHTML = `
            <div class="empty-state">
                <div class="empty-state-icon">📜</div>
                <p>NO QUESTS YET.<br>CRAFT YOUR FIRST!</p>
            </div>
        `;
        return;
    }

    container.innerHTML = '';

    // SORT BY sortOrder BEFORE RENDERING
    const sortedQuests = [...quests].sort((a, b) => (a.sortOrder || 0) - (b.sortOrder || 0));

    sortedQuests.forEach((quest, index) => {
        const isCompleted = completions[quest.id] || false;

        const item = document.createElement('div');
        item.className = 'quest-list-item';

        // ADD DRAG-AND-DROP ATTRIBUTES
        item.draggable = true;
        item.dataset.questId = quest.id;
        item.dataset.index = index;

        // ADD DRAG EVENT LISTENERS
        item.addEventListener('dragstart', handleDragStart);
        item.addEventListener('dragover', handleDragOver);
        item.addEventListener('drop', handleDrop);
        item.addEventListener('dragend', handleDragEnd);
        item.addEventListener('dragleave', handleDragLeave);

        item.innerHTML = `
            <div class="drag-handle" title="Drag to reorder">⋮⋮</div>
            <div class="quest-info">
                <div class="quest-emoji">${quest.icon || '⛏️'}</div>
                <div class="quest-details">
                    <h3>${quest.name} ${isCompleted ? '✅' : ''}</h3>
                    <div class="quest-emeralds">💎 ${quest.points} EMERALDS • ${getDaysActiveLabel(quest.daysActive)}</div>
                </div>
            </div>
            <div class="quest-actions">
                <button onclick="editQuest('${quest.id}')" class="btn-warning">EDIT</button>
                <button onclick="deleteQuest('${quest.id}')" class="btn-danger">DELETE</button>
            </div>
        `;
        container.appendChild(item);
    });
}
```

#### 2.3 Add Drag-and-Drop Event Handlers
**File:** `minecraft-quest-tracker-admin.html`
**Location:** Before `renderQuests()` function

```javascript
function handleDragStart(e) {
    draggedElement = this;
    draggedIndex = parseInt(this.dataset.index);
    this.style.opacity = '0.5';
    e.dataTransfer.effectAllowed = 'move';
    e.dataTransfer.setData('text/html', this.innerHTML);
}

function handleDragOver(e) {
    if (e.preventDefault) {
        e.preventDefault(); // Necessary to allow drop
    }
    e.dataTransfer.dropEffect = 'move';

    // Visual feedback
    if (this !== draggedElement) {
        this.classList.add('drag-over');
    }

    return false;
}

function handleDragLeave(e) {
    this.classList.remove('drag-over');
}

function handleDrop(e) {
    if (e.stopPropagation) {
        e.stopPropagation(); // Stops browser from redirecting
    }

    if (draggedElement !== this) {
        const dropIndex = parseInt(this.dataset.index);

        // Reorder the quests array
        const sortedQuests = [...quests].sort((a, b) => (a.sortOrder || 0) - (b.sortOrder || 0));
        const draggedQuest = sortedQuests[draggedIndex];
        sortedQuests.splice(draggedIndex, 1);
        sortedQuests.splice(dropIndex, 0, draggedQuest);

        // Update sortOrder for all quests
        const updates = {};
        sortedQuests.forEach((quest, index) => {
            updates[`chores/${quest.id}/sortOrder`] = index;
        });

        // Persist to Firebase
        database.ref().update(updates)
            .then(() => {
                showSuccess('✅ QUEST ORDER SAVED!');
            })
            .catch(error => {
                alert('ERROR SAVING ORDER: ' + error.message);
            });
    }

    this.classList.remove('drag-over');
    return false;
}

function handleDragEnd(e) {
    this.style.opacity = '1';

    // Remove all drag-over styling
    document.querySelectorAll('.quest-list-item').forEach(item => {
        item.classList.remove('drag-over');
    });
}
```

#### 2.4 Add CSS Styles for Drag-and-Drop
**File:** `minecraft-quest-tracker-admin.html`
**Location:** In `<style>` section, after `.quest-list-item` styles (around line 231)

```css
/* Drag handle */
.drag-handle {
    font-size: 20px;
    color: #FFF;
    cursor: grab;
    user-select: none;
    padding: 0 10px;
    text-shadow: 2px 2px 0 #000;
}

.quest-list-item[draggable="true"] {
    cursor: move;
}

.quest-list-item[draggable="true"]:active .drag-handle {
    cursor: grabbing;
}

/* Drag feedback */
.quest-list-item.drag-over {
    border-top: 6px solid #FFFF00 !important;
    margin-top: 8px;
}
```

#### 2.5 Update Quest List Item Layout
The `.quest-list-item` class needs to accommodate the drag handle.

**Modify existing CSS** (around line 222):
```css
.quest-list-item {
    background: #8B8B8B;
    padding: 15px;
    margin-bottom: 12px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 4px solid #555;
    box-shadow: inset 0 0 0 2px #A0A0A0, 0 4px 0 #3E3E3E;
    gap: 10px;  /* ADD THIS */
}
```

### Phase 3: Update Display File

#### 3.1 Sort Quests by Order in Display
**File:** `minecraft-quest-tracker.html`
**Function:** `renderQuests()` (around line 506)

**Change:**
```javascript
// BEFORE:
quests.forEach(quest => {
    // Filter by day type
    const daysActive = quest.daysActive || 'all';
    if (daysActive !== 'all' && daysActive !== dayType) {
        return;
    }
    // ... rendering logic
});

// AFTER:
// Sort by sortOrder before rendering
const sortedQuests = [...quests].sort((a, b) => (a.sortOrder || 0) - (b.sortOrder || 0));

sortedQuests.forEach(quest => {
    // Filter by day type
    const daysActive = quest.daysActive || 'all';
    if (daysActive !== 'all' && daysActive !== dayType) {
        return;
    }
    // ... rendering logic
});
```

## Testing Checklist

### Initial Setup
- [ ] Run `initializeSortOrder()` function once to add sortOrder to existing quests
- [ ] Verify all quests have sortOrder field in Firebase console

### Admin Panel Testing
- [ ] Create new quest → should appear at bottom of list
- [ ] Drag quest up → should move and save new position
- [ ] Drag quest down → should move and save new position
- [ ] Drag quest to top → should become first quest
- [ ] Drag quest to bottom → should become last quest
- [ ] Edit quest → order should remain unchanged
- [ ] Delete quest → remaining quests should maintain order

### Display File Testing
- [ ] Open display → quests appear in custom order
- [ ] Reorder in admin → display updates in real-time
- [ ] Refresh display → custom order persists

### Edge Cases
- [ ] Drag quest onto itself → no change
- [ ] Rapid dragging → no duplicate sortOrder values
- [ ] Multiple devices → order syncs correctly
- [ ] Empty list → no errors

## Rollback Plan

If drag-and-drop causes issues:

1. **Remove sortOrder sorting** from both files
2. **Quests will revert to insertion order** (creation time)
3. **No data loss** - all quest data remains intact

## Future Enhancements

- [ ] Add touch/mobile drag-and-drop support (consider SortableJS library)
- [ ] Add smooth animation during reorder
- [ ] Add "Reset to Default Order" button
- [ ] Add visual ghost/placeholder during drag
- [ ] Add keyboard shortcuts (Ctrl+↑/↓) for reordering

## Notes

- Drag-and-drop only affects **admin panel** (parent interface)
- Display file simply **respects the saved order**
- Firebase handles **real-time sync** automatically
- **No external libraries** required for basic implementation
- Works on **desktop browsers** (touch support requires additional work)
