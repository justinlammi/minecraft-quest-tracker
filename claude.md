# Minecraft Quest Tracker - Project Context

## Project Overview

This is a **family-friendly Minecraft-themed quest/chore tracker** designed to gamify daily tasks for children. The system uses Firebase Realtime Database to provide instant synchronization across all devices, allowing parents to manage quests while children interact with a fun, engaging display interface.

**Key Value Proposition:** Transform mundane chores into exciting Minecraft quests with real-time emerald tracking, achievement goals, and celebration animations.

### Target Users
- **Children:** View and complete daily quests on a display (DakBoard, tablet, or browser)
- **Parents:** Manage quests, set goals, and track progress through an admin panel

## Architecture

### Tech Stack
- **Frontend:** Pure vanilla HTML5, CSS3, JavaScript ES6+
- **Backend:** Firebase Realtime Database (NoSQL cloud database)
- **Deployment:**
  - **Display:** DakBoard Custom HTML widget (embedded, no public hosting)
  - **Admin:** Local file access only (file:// protocol)
- **No Build Process:** Files run directly in browser - no compilation needed

### Current Deployment Strategy (v2.2)

**Security-First Approach:**
This deployment eliminates all public exposure while maintaining full functionality.

**Display File (`minecraft-quest-tracker.html`):**
- Entire HTML source embedded in DakBoard Custom HTML widget
- DakBoard renders the widget on their private display
- No URL, no hosting, no public access
- Firebase connection happens client-side from the widget
- Updates require re-pasting HTML source into widget

**Admin File (`minecraft-quest-tracker-admin.html`):**
- Saved to local computers/devices only
- Accessed via `file:///path/to/file.html` in browser
- Bookmarked for easy access
- Can be synced via private cloud storage (Google Drive, Dropbox) for multi-device access
- Never exposed to public internet

**Benefits of This Approach:**
1. Zero attack surface - no public URLs to discover
2. Complete privacy - HTML source never leaves user's control
3. Simple - no authentication/authorization complexity needed
4. Secure - requires physical device access to admin
5. Functional - Firebase sync works perfectly from both embedded widget and local file

**Trade-offs:**
- Display updates require manual widget re-paste (rare - only when Firebase config changes or features added)
- Admin access requires local file (acceptable for single-family use)
- No remote admin without additional setup (intentional security choice)

### Real-time Synchronization
All three HTML files connect to the same Firebase Realtime Database using listeners:
```javascript
database.ref('chores').on('value', (snapshot) => { ... });
database.ref(`completions/${todayKey}`).on('value', (snapshot) => { ... });
database.ref('settings/reward').on('value', (snapshot) => { ... });
```

When any device updates the database, all connected devices receive updates instantly.

## File Structure

### Core Application Files

#### 1. `minecraft-quest-tracker.html` (~18.5 KB)
**Purpose:** Child-facing display interface

**Key Features:**
- Shows daily quests in Minecraft-themed UI
- Click/tap quests to mark complete
- Real-time emerald counter with celebration animations
- Progress bar toward achievement goal
- Dynamic encouragement messages based on progress
- Auto-reloads at midnight for new day

**Important Code Locations:**
- Firebase config: Lines ~367-377
- Quest rendering: `loadChores()` function
- Completion logic: `toggleChore()` function
- Celebration animation: `showCelebration()` function
- Midnight auto-reload: Lines ~345-350

#### 2. `minecraft-quest-tracker-admin.html` (~26.5 KB)
**Purpose:** Parent management interface

**Key Features:**
- CRUD operations for quests (Create, Read, Update, Delete)
- 16 Minecraft-themed emoji selector (⛏️, ⚔️, 🛡️, 💎, etc.)
- Set achievement goals (name and points)
- View daily statistics dashboard
- Reset completions if needed
- Preview button to open display file

**Important Code Locations:**
- Firebase config: Lines ~525-535
- Add quest: `addChore()` function
- Edit quest: `editChore()` function
- Delete quest: `deleteChore()` function
- Emoji picker: Lines ~300-330

#### 3. `minecraft-initialize-data.html` (~11.7 KB)
**Purpose:** One-time setup utility

**Key Features:**
- Loads 6 sample Minecraft-themed quests
- Sets default achievement goal (100 emeralds)
- Clear all data function
- Firebase configuration verification

**Sample Quests Loaded:**
- ⛏️ MINE YOUR BED (10 emeralds)
- 🪥 MORNING POTION (5 emeralds)
- 🪥 NIGHT POTION (5 emeralds)
- 🍽️ CLEAR CRAFTING TABLE (5 emeralds)
- 🧸 COLLECT DROPPED ITEMS (10 emeralds)
- 👕 GATHER ARMOR (5 emeralds)

**Important Code Locations:**
- Firebase config: Lines ~183-193
- Sample data: `sampleChores` array

### Documentation Files

#### `README.md` (21.4 KB)
Comprehensive user guide covering:
- Quick start (15-45 minute setup)
- Deployment options (GitHub Pages vs Raspberry Pi)
- Daily usage instructions
- Customization guide (colors, sizes, messages)
- 20+ quest ideas by category
- Troubleshooting (12 common issues)
- Database structure documentation
- Security and privacy notes

#### `FIREBASE-SETUP.md` (16.3 KB)
Step-by-step Firebase configuration guide:
- Firebase console setup (15 steps)
- Database creation and location selection
- Security rules configuration
- Configuration copying instructions
- Verification procedures
- Free tier limits and costs

## Database Schema

### Structure
```
firebase-realtime-database/
├── chores/
│   ├── {questId}/
│   │   ├── name: string          # Quest name (e.g., "MINE YOUR BED")
│   │   ├── points: number        # Emerald value (e.g., 10)
│   │   ├── icon: string          # Emoji icon (e.g., "⛏️")
│   │   └── createdAt: timestamp  # Creation timestamp
│
├── completions/
│   ├── {YYYY-MM-DD}/             # Date key (e.g., "2025-11-11")
│   │   ├── {questId}: boolean    # true if completed today
│
└── settings/
    └── reward/
        ├── name: string          # Achievement name (e.g., "DIAMOND SWORD")
        └── points: number        # Goal emeralds (e.g., 100)
```

### Date Key Format
All three files use the same date format:
```javascript
getTodayKey() {
    const today = new Date();
    return `${today.getFullYear()}-${String(today.getMonth() + 1).padStart(2, '0')}-${String(today.getDate()).padStart(2, '0')}`;
}
// Returns: "2025-11-11"
```

## Firebase Configuration

### Location in Files
Firebase config objects appear in all three HTML files:
- `minecraft-quest-tracker.html`: Lines ~367-377
- `minecraft-quest-tracker-admin.html`: Lines ~525-535
- `minecraft-initialize-data.html`: Lines ~183-193

### Configuration Structure
```javascript
const firebaseConfig = {
    apiKey: "...",
    authDomain: "...",
    databaseURL: "...",           // CRITICAL: Realtime Database URL
    projectId: "...",
    storageBucket: "...",
    messagingSenderId: "...",
    appId: "...",
    measurementId: "..."
};
```

**IMPORTANT:** All three files must have identical Firebase configs for proper operation.

## Key Development Patterns

### Real-time Listeners
Always use `.on('value')` for continuous sync:
```javascript
database.ref('chores').on('value', (snapshot) => {
    const chores = snapshot.val() || {};
    // Update UI
});
```

### Quest Completion Toggle
```javascript
async function toggleChore(choreId) {
    const todayKey = getTodayKey();
    const completionRef = database.ref(`completions/${todayKey}/${choreId}`);
    const snapshot = await completionRef.once('value');
    const isCompleted = snapshot.val() || false;
    await completionRef.set(!isCompleted);
    // Celebration animations happen automatically via listener
}
```

### Progress Calculation
```javascript
const percentage = Math.min((currentEmeralds / goalEmeralds) * 100, 100);
```

### Dynamic Messages by Progress
- **100%+:** "ACHIEVEMENT UNLOCKED!"
- **75-99%:** "ALMOST THERE! SO CLOSE!"
- **50-74%:** "HALFWAY! KEEP GOING!"
- **25-49%:** "GREAT START! MINE ON!"
- **0-24%:** Random from 10 hardcoded encouraging messages

## Styling & Theming

### Minecraft Visual Theme
- **Font:** "Press Start 2P" (Google Fonts - pixel-perfect retro font)
- **Background:** 16x16px grass block pattern
- **Colors:** Minecraft-inspired palette
  - Background: `#8B4513` (brown/dirt)
  - Quest items: `#2d5016` (dark grass green)
  - Completed: `#FFD700` (gold/achievement yellow)
  - Buttons: `#4a752c` (grass green)

### Key CSS Variables (if adding)
Consider these for future customization:
```css
:root {
    --minecraft-grass: #2d5016;
    --minecraft-gold: #FFD700;
    --minecraft-emerald: #50C878;
    --minecraft-dirt: #8B4513;
}
```

## Security Model

### Current Setup: Secure Local Deployment
- **Authentication:** None (family/private use)
- **Security Rules:** `{".read": true, ".write": true}` (test mode)
- **Display Access:** Embedded in DakBoard widget - no public URL
- **Admin Access:** Local file:// only - never exposed publicly
- **Access Control:** Physical device security + obscure Firebase database URL

### Security Advantages of Current Deployment
1. **Display HTML never hosted publicly** - source code embedded directly in DakBoard widget
2. **Admin panel never exposed** - local file access only (file:// protocol)
3. **No attack surface** - no public URLs to discover or exploit
4. **Firebase API keys are public by design** - they identify the project, not authenticate users
5. **Database URL is long and random** - unlikely to be discovered without access to HTML source
6. **Perfect for family/private use** - maximum privacy with minimal complexity

### For Future Multi-Family or Public Use
If you want to expand access while maintaining security:
- Add Firebase Authentication (email/password or Google Sign-In)
- Update security rules to require authentication: `{".read": "auth != null", ".write": "auth != null"}`
- Implement user-specific data paths: `/users/{userId}/chores/`
- Host admin panel with authentication required

## Important Features to Preserve

### 1. Midnight Auto-Reload
Display file automatically reloads at midnight to show fresh quest list:
```javascript
const now = new Date();
const night = new Date(now.getFullYear(), now.getMonth(), now.getDate() + 1, 0, 0, 0);
const msToMidnight = night.getTime() - now.getTime();
setTimeout(() => location.reload(), msToMidnight);
```

### 2. Celebration Animations
Random celebration emojis (💎⭐🎉🏆✨) fly up the screen when quests complete:
```javascript
function showCelebration() {
    const emojis = ['💎', '⭐', '🎉', '🏆', '✨'];
    // Creates floating animation elements
}
```

### 3. 16 Minecraft Emojis
Admin panel restricts icons to these themed emojis:
```
⛏️ (pickaxe), ⚔️ (sword), 🛡️ (shield), 💎 (diamond),
🌲 (tree), 🔥 (fire), 🪓 (axe), 🏹 (bow),
🧙 (wizard), 🐷 (pig), 🐔 (chicken), 🐑 (sheep),
🪨 (rock), ⭐ (star), 🎯 (target), 🏆 (trophy)
```

### 4. Last Updated Timestamp
Display shows "Last Update: X seconds/minutes ago" with auto-refresh every 10 seconds.

## Common Workflows

### Parent Adds New Quest
1. Open `minecraft-quest-tracker-admin.html`
2. Fill in quest name, emerald value, select emoji
3. Click "Add Quest"
4. Firebase updates `/chores/{newId}`
5. Display file instantly shows new quest

### Child Completes Quest
1. View `minecraft-quest-tracker.html` on display
2. Tap/click quest item
3. Firebase updates `/completions/{today}/{questId}` to `true`
4. Celebration animation plays
5. Emerald counter increases
6. Progress bar updates
7. All displays sync instantly

### Reset for New Day
Completions are stored by date (`/completions/2025-11-11/`), so:
- Old completions remain in database (for history/tracking)
- New day automatically shows uncompleted quests
- Emerald totals persist across days toward achievement goal

## Development Guidelines

### Making Changes

1. **Modifying Quest Display:**
   - Edit `minecraft-quest-tracker.html`
   - Find `loadChores()` function for rendering logic
   - Maintain Minecraft theming (fonts, colors, emojis)
   - **IMPORTANT:** After changes, re-paste entire HTML source into DakBoard widget

2. **Changing Admin Features:**
   - Edit `minecraft-quest-tracker-admin.html`
   - Emoji picker logic: Lines ~300-330
   - Stats calculation: `updateStats()` function
   - Save updated file to local locations (overwrite existing)
   - Bookmarks will automatically use updated version

3. **Updating Firebase Config:**
   - **MUST update all three HTML files identically**
   - Search for `firebaseConfig` in each file
   - Replace entire object including all keys
   - **CRITICAL:** Re-paste display file into DakBoard widget after config change

4. **Customizing Styles:**
   - CSS is embedded in `<style>` tags in each file
   - Look for `.minecraft-*` classes
   - Maintain Press Start 2P font for authenticity
   - Display changes require DakBoard widget re-paste

### Testing Locally

1. Open HTML files directly in browser (file:// protocol works)
2. Test Firebase connection in browser console
3. Use admin panel to add/edit/delete quests
4. Open display file to verify real-time updates
5. Check browser console for Firebase errors

### Deployment Checklist

- [ ] Firebase project created and database enabled
- [ ] Security rules set (test mode for family use)
- [ ] Firebase config copied to all three HTML files
- [ ] `minecraft-initialize-data.html` run once to load sample data
- [ ] Display HTML source embedded in DakBoard Custom HTML widget
- [ ] DakBoard widget tested and rendering correctly
- [ ] Admin file saved to permanent local location on both computers
- [ ] Admin panel bookmarked (file:// URL) on both computers
- [ ] Optional: Admin file uploaded to shared cloud storage for mobile access

## Dependencies

### External Resources
```html
<!-- Firebase SDK v9.22.0 (Compat mode) -->
<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
```

### Browser Compatibility
- Chrome (recommended)
- Firefox
- Safari
- Edge
- Modern mobile browsers (iOS Safari, Chrome Mobile)

**Minimum Requirements:** ES6 support, CSS Grid, Flexbox

## Troubleshooting Tips

### Common Issues

1. **Firebase not connecting:**
   - Check browser console for errors
   - Verify `databaseURL` ends with `.firebaseio.com`
   - Confirm security rules allow read/write

2. **Quests not syncing:**
   - Ensure all three files have identical Firebase config
   - Check internet connection
   - Verify database is in test mode

3. **Emojis not displaying:**
   - Some platforms may not support all emojis
   - Use fallback: ⛏️ works universally
   - Avoid complex emoji sequences

4. **Midnight reload not working:**
   - Check system clock is correct
   - Browser tab must stay open
   - Consider external auto-refresh (DakBoard feature)

## Future Enhancement Ideas

- [ ] Add Firebase Authentication for multi-family use
- [ ] Create weekly/monthly achievement tracking
- [ ] Add sound effects for quest completion
- [ ] Implement quest streaks (completed X days in a row)
- [ ] Create parent notification system (email/SMS when goal reached)
- [ ] Add bonus/penalty multipliers
- [ ] Create quest templates/categories
- [ ] Add data export for tracking long-term progress
- [ ] Implement quest scheduling (specific days of week)
- [ ] Create achievement badges system

## Version Information

- **Current Version:** v2.2
- **Last Updated:** January 2025
- **Recent Changes:**
  - Enhanced security: DakBoard widget deployment (no public hosting)
  - Local-only admin access for maximum privacy
  - Removed GitHub Pages deployment
  - Added cumulative emerald tracking with goal-based resets
  - Updated all documentation for secure deployment approach
  - Enhanced troubleshooting for DakBoard widget issues

---

**Note for Claude:** This is a complete, working application with no build process. Files can be edited directly. Always test changes in all three HTML files to ensure consistency. The project prioritizes simplicity and family-friendliness over technical complexity.