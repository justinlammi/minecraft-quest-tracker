# ⛏️ Minecraft Quest Tracker

Transform your child's daily chores into exciting Minecraft quests! A gamified chore tracking system with a Minecraft theme, perfect for displaying on a DakBoard or any screen.

![Minecraft Quest Tracker](https://img.shields.io/badge/Status-Active-success)
![Firebase](https://img.shields.io/badge/Firebase-Realtime%20Database-orange)
![License](https://img.shields.io/badge/License-MIT-blue)

---

## ✨ Features

### For Kids
- 🎮 **Minecraft-themed interface** with blocky design and familiar icons
- 💎 **Earn emeralds** by completing quests (chores)
- 🏆 **Achievement system** with progress tracking
- 🎉 **Celebration animations** when quests are completed
- 📊 **Visual progress bar** showing advancement toward goals
- ⚡ **Real-time updates** - changes appear instantly
- 🔄 **Auto-resets daily** at midnight

### For Parents
- 📱 **Easy admin panel** - manage quests from your computer
- ✏️ **Edit quests** - change names, points, and icons on the fly
- 🎨 **Customizable icons** - choose from 16 Minecraft-themed emojis
- 📈 **Track progress** - see daily completion stats
- 🌐 **Cloud-based** - Firebase syncs across all devices
- 🔒 **Secure deployment** - display embedded in DakBoard, admin local-only
- 🔄 **Quick reset** - clear today's completions if needed
- 💾 **Persistent data** - emeralds accumulate toward achievements

---

## 📦 What's Included

### Main Files

1. **minecraft-quest-tracker.html** (Display File)
   - Shows on your DakBoard or display screen
   - Compact quest design - fits more quests on screen
   - Touch-enabled checkboxes for completion
   - Real-time sync with Firebase

2. **minecraft-quest-tracker-admin.html** (Admin Panel)
   - Manage all quests and settings
   - Edit existing quests (name, points, icon)
   - Add new quests
   - Set achievement goals
   - View today's statistics
   - Large, easy-to-use edit modal

3. **minecraft-initialize-data.html** (Setup Tool)
   - One-time setup utility
   - Loads 6 sample Minecraft-themed quests
   - Sets default achievement goal
   - Quick start for testing

### Documentation

4. **README.md** (This file)
   - Complete project overview
   - Setup and usage instructions

5. **FIREBASE-SETUP.md**
   - Detailed Firebase configuration guide
   - Step-by-step database setup
   - Security rules configuration

6. **MINECRAFT-README.md**
   - Original comprehensive guide
   - Quest ideas and suggestions
   - Troubleshooting tips

---

## 🚀 Quick Start Guide

### Prerequisites
- Google account (for Firebase)
- Web browser (Chrome, Firefox, Safari, Edge)
- Text editor (Notepad, TextEdit, VS Code, etc.)
- **For deployment:**
  - DakBoard account or display device with custom HTML widget support
  - Computer to save and access admin panel locally

### Setup Time
- **Firebase setup**: 15-20 minutes (one-time)
- **Testing**: 5-10 minutes
- **DakBoard widget setup**: 5-10 minutes
- **Total**: 25-40 minutes

---

## 📋 Step-by-Step Setup

### Step 1: Set Up Firebase Database

1. **Create Firebase Project**
   - Go to [Firebase Console](https://console.firebase.google.com)
   - Click "Add project"
   - Name it (e.g., "minecraft-quest-tracker")
   - Disable Google Analytics (optional)
   - Click "Create project"

2. **Create Realtime Database**
   - In Firebase Console, click "Realtime Database"
   - Click "Create Database"
   - Choose location (United States recommended)
   - Start in **Test mode**
   - Click "Enable"

3. **Configure Security Rules**
   - Go to "Rules" tab in Realtime Database
   - Replace with:
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
   - Click "Publish"

4. **Get Firebase Configuration**
   - Click the gear icon → Project Settings
   - Scroll down to "Your apps"
   - Click the web icon `</>`
   - Register your app (nickname: "Quest Tracker")
   - Copy the firebaseConfig object

### Step 2: Configure Your Files

1. **Update Display File** (minecraft-quest-tracker.html)
   - Open in text editor
   - Find line ~367: `const firebaseConfig = {`
   - Replace with your Firebase config
   - Save file

2. **Update Admin File** (minecraft-quest-tracker-admin.html)
   - Open in text editor
   - Find line ~525: `const firebaseConfig = {`
   - Replace with your Firebase config
   - Save file

3. **Update Initialize File** (minecraft-initialize-data.html)
   - Open in text editor
   - Find line ~183: `const firebaseConfig = {`
   - Replace with your Firebase config
   - Save file

### Step 3: Load Sample Data

1. Open `minecraft-initialize-data.html` in browser
2. Click "✨ CRAFT SAMPLE QUESTS" button
3. Confirm the action
4. You should see: "✅ QUESTS CRAFTED!"

**Sample quests loaded:**
- ⛏️ MINE YOUR BED (10 emeralds)
- 🪥 MORNING POTION (5 emeralds)
- 🪥 NIGHT POTION (5 emeralds)
- 🍽️ CLEAR CRAFTING TABLE (5 emeralds)
- 🧸 COLLECT DROPPED ITEMS (10 emeralds)
- 👕 GATHER ARMOR (5 emeralds)

**Achievement:** 💎 DIAMOND TREASURE - 100 emeralds

### Step 4: Test Everything

1. **Test Display**
   - Open `minecraft-quest-tracker.html` in browser
   - You should see all sample quests
   - Click on a quest to complete it
   - Watch the celebration animation
   - See emeralds increase

2. **Test Admin Panel**
   - Open `minecraft-quest-tracker-admin.html` in browser
   - Verify all quests appear
   - Click "EDIT" on a quest
   - Change the name
   - Click "SAVE"
   - Check that display updates in real-time

3. **Test Real-Time Sync**
   - Keep both files open in separate browser windows
   - Complete a quest in the display
   - Watch it update in the admin panel
   - Edit a quest in admin
   - Watch it update in display

### Step 5: Deploy to DakBoard

**Deployment Strategy:**
- **Display**: Embed HTML source directly in DakBoard Custom HTML widget (secure, no public hosting)
- **Admin Panel**: Save locally on your computers (file:// access only)

---

#### **Part A: DakBoard Widget Setup (Display)**

1. **Copy Display File Source Code**
   - Open `minecraft-quest-tracker.html` in your text editor
   - Select all content (Ctrl+A / Cmd+A)
   - Copy to clipboard (Ctrl+C / Cmd+C)

2. **Create DakBoard Custom HTML Widget**
   - Log in to your DakBoard account
   - Go to your screen settings
   - Click "Add Block" or "+"
   - Select "Custom HTML" widget
   - Paste the entire HTML source code
   - Set refresh rate: 60 seconds (recommended)
   - Position and size as desired
   - Click "Save"

3. **Test the Widget**
   - Preview your DakBoard screen
   - Verify quests appear correctly
   - Try clicking/tapping a quest to complete it
   - Confirm celebration animation plays
   - Check emerald counter updates

**Benefits of Widget Embedding:**
- ✅ No public URL exposure
- ✅ Source code never hosted publicly
- ✅ Works on any DakBoard-compatible device
- ✅ Auto-refreshes keep display current
- ✅ Direct Firebase connection (no intermediate server)

---

#### **Part B: Local Admin Access**

1. **Save Admin File Locally**
   - Save `minecraft-quest-tracker-admin.html` to a permanent location on your computer
   - **Suggested locations:**
     - Windows: `C:\Users\YourName\Documents\minecraft-admin.html`
     - Mac: `/Users/YourName/Documents/minecraft-admin.html`
     - Cloud sync: Dropbox, Google Drive, OneDrive folder for access from multiple devices

2. **Create Bookmarks**
   - Open `minecraft-quest-tracker-admin.html` in your browser (file:// protocol)
   - **Windows example:** `file:///C:/Users/YourName/Documents/minecraft-admin.html`
   - **Mac example:** `file:///Users/YourName/Documents/minecraft-admin.html`
   - Bookmark the page in your browser
   - Optional: Add to browser favorites bar for quick access
   - Repeat on your spouse's computer

3. **Test Admin Panel**
   - Click your bookmark to open admin panel
   - Verify all quests appear
   - Try editing a quest
   - Check that DakBoard display updates in real-time
   - Test adding/deleting quests

4. **Mobile Access (Optional)**
   - Email the admin HTML file to yourself
   - Save to phone's file storage or cloud app
   - Open in mobile browser when needed
   - Works offline once Firebase data is cached

**Benefits of Local Admin:**
- ✅ Zero public exposure
- ✅ No authentication needed (physical device security)
- ✅ Works without internet (after initial Firebase connection)
- ✅ No hosting costs
- ✅ Complete privacy and control

---

## 💡 Daily Usage

### For Your Child

**Morning:**
1. Look at the display
2. See today's quests
3. Complete chores throughout the day
4. Tap each quest when done
5. Watch emeralds grow!

**Evening:**
1. Show you their progress
2. Celebrate completed quests together
3. Watch achievement progress bar

**Midnight:**
- Quests automatically reset for tomorrow
- Emeralds stay saved toward achievement goal

### For Parents

**Daily Management (30 seconds):**
1. Open admin panel on phone/computer
2. Check completion stats
3. Add/edit quests as needed

**Weekly Tasks:**
- Change achievement goals
- Add variety to quests
- Celebrate milestone achievements

**As Needed:**
- Edit quest names for clarity
- Adjust emerald values
- Reset day if there's a mistake
- Add seasonal or special quests

---

## 🎨 Customization

### Change Quest Names

Use the admin panel:
1. Click "EDIT" button next to quest
2. Type new name
3. Click "SAVE"

**Ideas:**
- MINE YOUR BED → Make Your Bed
- MORNING POTION → Brush Teeth AM
- COLLECT DROPPED ITEMS → Pick Up Toys
- GATHER ARMOR → Put Dirty Clothes Away

### Adjust Emerald Values

Based on difficulty:
- **Easy tasks (5 emeralds)**: Brush teeth, wash hands
- **Medium tasks (10 emeralds)**: Make bed, clean room
- **Hard tasks (15-20 emeralds)**: Homework, extra chores

### Pick Different Icons

Available icons in admin panel:
- ⛏️ Pickaxe
- ⚔️ Sword
- 🛡️ Shield
- 💎 Diamond
- 🪓 Axe
- 🔱 Trident
- 🏹 Bow
- 🗡️ Dagger
- 🛏️ Bed
- 🪥 Toothbrush
- 🍽️ Plate
- 🧹 Broom
- 📚 Books
- 🎒 Backpack
- 🧸 Teddy Bear
- 👕 Shirt

### Set Achievement Goals

**Starter goals (new users):**
- 50 emeralds - Easy first achievement
- 100 emeralds - Standard week goal
- 150 emeralds - Challenge week

**Advanced goals:**
- 200 emeralds - Two-week goal
- 300+ emeralds - Monthly goal
- Custom rewards tied to emerald counts

**Achievement names:**
- DIAMOND TREASURE
- EMERALD CHAMPION
- QUEST MASTER
- MINING LEGEND
- BLOCK BUILDER
- CRAFT KING/QUEEN

---

## 🎯 Quest Ideas by Category

### Morning Routine (5 emeralds each)
- Make bed
- Brush teeth
- Get dressed
- Eat breakfast
- Pack backpack

### After School (5-10 emeralds)
- Hang up jacket/backpack
- Homework time
- Practice instrument
- Reading time
- Snack cleanup

### Evening Routine (5 emeralds each)
- Set table
- Clear dishes
- Bath/shower
- Brush teeth
- Lay out clothes for tomorrow

### Room & House (10-15 emeralds)
- Tidy bedroom
- Make bed
- Put away laundry
- Vacuum room
- Organize toys

### Special/Bonus Quests (15-25 emeralds)
- Help sibling
- Extra chore
- Good behavior report
- Kind deed
- Try new food
- Complete challenge

---

## 🔧 Advanced Customization

### Change Colors

Edit the display file CSS:
- Background: Line 19-23 (grass block pattern)
- Quest items: Line 189-215
- Achievement section: Line 76-92

### Adjust Quest Size

In display file:
- Quest padding: Line 196 (currently `12px 14px`)
- Quest margin: Line 197 (currently `10px`)
- Icon size: Line 236 (currently `28px`)
- Font sizes: Lines 250, 260

### Modify Messages

In display file JavaScript (lines 392-403):
```javascript
const minecraftMessages = [
    "AWESOME MINING! ⛏️",
    "KEEP DIGGING! 💪",
    // Add your own messages here!
];
```

### Add More Emojis

In admin file JavaScript (line 454):
```javascript
const emojis = ['⛏️', '⚔️', '🛡️', /* add more here */];
```

---

## 📱 Access Admin Panel

### Recommended: Local File Access
**Current deployment uses this method for security**

- Save `minecraft-quest-tracker-admin.html` to a permanent location
- Bookmark the file:// URL in your browser
- Open when needed from bookmarks/favorites
- Works on both computers via file sync (Google Drive, Dropbox, OneDrive)
- Zero security risk - file never exposed publicly

### Mobile Access Options

**Option 1: Save to Cloud Storage**
- Upload admin HTML to Google Drive, Dropbox, or iCloud
- Access from phone's cloud storage app
- Open in mobile browser
- Syncs automatically when you update the file

**Option 2: Email to Yourself**
- Email file as attachment to yourself
- Save to phone storage
- Open in mobile browser when needed
- Manual updates required

**Option 3: Local Storage Apps**
- Use file manager app (Files on iOS, My Files on Android)
- Save admin HTML file
- Tap to open in browser
- Works offline after initial Firebase connection

### Future Option: Add Authentication (Advanced)
If you later want remote web access with security:
- Implement Firebase Authentication
- Host admin panel with password protection
- See CLAUDE.md for implementation guidance

---

## 🐛 Troubleshooting

### Display Shows "Loading quests..."

**Problem:** Can't connect to Firebase

**Solutions:**
1. Check Firebase config is correct in display file
2. Verify database URL format: `https://PROJECT-ID-default-rtdb.firebaseio.com`
3. Check security rules allow reading
4. Check internet connection

### Quests Don't Update When Clicked

**Problem:** Can't write to Firebase

**Solutions:**
1. Check Firebase config is correct
2. Verify security rules allow writing
3. Check browser console for errors (press F12)
4. Refresh the page

### Admin Panel Can't Edit Quests

**Problem:** Edit button doesn't work or modal won't open

**Solutions:**
1. Check JavaScript console for errors (press F12)
2. Make sure you're using the updated admin file
3. Clear browser cache and reload
4. Try different browser

### Edit Modal Has Scrollbar

**Problem:** Older version of admin file

**Solution:**
- Use the latest file: `minecraft-quest-tracker-admin.html`
- This version has the scrollbar hidden

### Emeralds Not Accumulating

**Problem:** Progress resets unexpectedly

**Solutions:**
1. Check if someone clicked "Reset Today" button
2. Verify Firebase data is persisting
3. Check system clock isn't changing dates
4. Completions reset at midnight (this is normal)

### Display Won't Show on DakBoard Widget

**Problem:** Custom HTML widget not rendering

**Solutions:**
1. Verify you pasted the ENTIRE HTML source code (including `<!DOCTYPE html>` and closing `</html>`)
2. Check Firebase config is correctly embedded in the pasted code
3. Test the HTML file in a regular browser first (open locally)
4. Ensure DakBoard refresh rate is set (60 seconds recommended)
5. Check DakBoard widget size is adequate (minimum 400x600px recommended)
6. Try removing and re-adding the widget
7. Clear DakBoard cache and reload screen

### DakBoard Widget Shows "Loading quests..."

**Problem:** Firebase connection issue in embedded widget

**Solutions:**
1. Verify Firebase config in HTML source has correct `databaseURL`
2. Check internet connection on DakBoard device
3. Confirm Firebase security rules allow reading: `".read": true`
4. Test by opening the HTML file directly in a browser
5. Check browser console for Firebase errors (if accessible)
6. Ensure external scripts can load (Firebase SDK from CDN)

### Changes Not Showing in DakBoard Widget

**Problem:** Updated HTML but widget shows old version

**Solutions:**
1. DakBoard caches widget content
2. Edit the widget and paste updated HTML source
3. Save widget changes
4. Force refresh: remove widget, wait 30 seconds, re-add with new source
5. Check that you copied the updated HTML file (not old version)
6. Clear DakBoard cache in settings
7. Wait for auto-refresh cycle (based on refresh rate setting)

---

## 📊 Database Structure

Your Firebase Realtime Database stores data in this structure:

```
minecraft-quest-tracker/
├── chores/
│   ├── chore_1234567890/
│   │   ├── name: "MINE YOUR BED"
│   │   ├── points: 10
│   │   ├── icon: "⛏️"
│   │   └── createdAt: 1234567890000
│   └── chore_1234567891/
│       ├── name: "MORNING POTION"
│       └── ...
├── completions/
│   ├── 2025-01-15/
│   │   ├── chore_1234567890: true
│   │   └── chore_1234567891: false
│   └── 2025-01-16/
│       └── ...
└── settings/
    └── reward/
        ├── name: "DIAMOND TREASURE"
        └── points: 100
```

---

## 🔒 Security Notes

### Current Secure Deployment
Your setup prioritizes privacy and security:

**Display (DakBoard Widget):**
- HTML source embedded directly in DakBoard
- Never hosted on public internet
- No URL for outsiders to discover
- Only accessible via your DakBoard account

**Admin Panel (Local Files):**
- Saved locally on your computers only
- Accessed via file:// protocol (never on web)
- Requires physical access to your devices
- Can be synced via private cloud storage (Google Drive, Dropbox)

**Firebase Database:**
- Test mode rules (read/write allowed)
- Long, random database URL (unlikely to be discovered)
- No sensitive personal data stored (just quest names and completions)
- Firebase API key is public by design (normal for client-side apps)

### Why This Is Secure
1. **No public attack surface** - neither display nor admin panel are publicly accessible
2. **Physical security** - admin requires access to your actual computers
3. **Private widget** - DakBoard widgets are private to your account
4. **Minimal data exposure** - even if database URL was discovered, only chore names are visible
5. **Perfect for family use** - right level of security without complexity

### For Future Public or Multi-Family Use
If you later want to share with other families securely:

1. **Add Firebase Authentication:**
   ```json
   {
     "rules": {
       ".read": "auth != null",
       ".write": "auth != null"
     }
   }
   ```

2. **Implement User-Specific Data:**
   - Separate data paths per family: `/families/{familyId}/chores/`
   - Add login UI to admin panel
   - Each family sees only their own data

### Privacy
- No personal data is collected
- No analytics or tracking
- All data stays in your Firebase project
- You control all data
- No third parties have access

---

## 💾 Backup Your Data

### Manual Backup
1. Go to Firebase Console
2. Open Realtime Database
3. Click on the three dots (⋮) 
4. Select "Export JSON"
5. Save file to your computer

### Restore from Backup
1. Open Firebase Console
2. Click three dots (⋮)
3. Select "Import JSON"
4. Choose your backup file

**Recommended:** Back up weekly or before major changes

---

## 🔄 Updates and Maintenance

### Firebase Free Tier Limits
- **Storage**: 1 GB
- **Downloads**: 10 GB/month
- **Simultaneous connections**: 100

**Your usage:** Tiny! This project uses:
- ~10 KB of storage
- Minimal bandwidth
- 1-2 connections at a time

You'll never hit these limits with home use.

### Browser Compatibility
- ✅ Chrome (recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Edge
- ✅ Mobile browsers

### Raspberry Pi Requirements
- **OS**: Raspberry Pi OS (any version)
- **Browser**: Chromium (included)
- **Internet**: Required for Firebase
- **Power**: Standard Pi power supply

---

## 🎓 Teaching Moments

Use this tracker to teach:
- **Responsibility**: Completing tasks independently
- **Goal setting**: Working toward achievements
- **Math**: Adding emeralds, calculating progress
- **Time management**: Prioritizing daily tasks
- **Technology**: Understanding cloud apps
- **Cause and effect**: Actions → Rewards

---

## 🌟 Success Tips

### Getting Started
1. **Start small**: Begin with 3-4 easy quests
2. **Make it achievable**: Set first goal at 50 emeralds
3. **Be consistent**: Check daily for first week
4. **Celebrate wins**: Make achievement unlocking special
5. **Adjust as needed**: Fine-tune based on what works

### Keeping Interest
- Change quest names monthly
- Add seasonal quests (holidays, summer)
- Tie achievements to real rewards
- Let child help pick new quests
- Make special "bonus quest" days
- Create week-long challenges

### When It's Not Working
- Lower emerald goals
- Simplify quest names
- Add more exciting icons
- Reduce number of daily quests
- Increase emerald values
- Make completion more fun (do together)

---

## 📞 Support

### Questions?
- Check MINECRAFT-README.md for detailed info
- Review FIREBASE-SETUP.md for database help
- Read this README troubleshooting section

### Common Resources
- [Firebase Documentation](https://firebase.google.com/docs)
- [DakBoard Support](https://blog.dakboard.com/diy-wall-display/)
- [Raspberry Pi Forums](https://forums.raspberrypi.com/)

---

## 📝 Version History

### v2.2 (Current)
- 🔒 Enhanced security: Display embedded in DakBoard widget (no public hosting)
- 🏠 Local-only admin access for maximum privacy
- 📝 Updated documentation for secure deployment approach
- 🛡️ Removed public GitHub Pages deployment
- 💎 Added cumulative emerald tracking with goal-based resets
- 📚 Enhanced troubleshooting for DakBoard widget deployment

### v2.1
- 🎨 Fine-tuned quest display sizing
- 📏 Improved readability with optimized spacing
- 🔧 Added weekday/weekend quest filtering
- ⚡ Enhanced cache prevention

### v2.0
- ✨ Added edit functionality to admin panel
- 🎨 Optimized quest display size (medium compact)
- 📏 Enlarged edit modal with no scrollbar
- 🔧 Improved spacing and layout
- 📱 Better mobile responsiveness

### v1.0 (Original)
- 🎮 Initial Minecraft-themed quest tracker
- 💎 Emerald point system
- 🏆 Achievement tracking
- 🔄 Auto-reset daily
- 📊 Admin panel with stats

---

## 📄 License

This project is free to use and modify for personal use. Attribution appreciated but not required.

**Built with:**
- Firebase Realtime Database
- Vanilla JavaScript
- Press Start 2P font (Google Fonts)
- Love for Minecraft and organized kids! ⛏️💚

---

## 🎉 Have Fun!

Remember: The goal is to make chores fun and build responsibility. Don't stress about perfection—adjust and adapt to what works for your family. Happy questing! 🎮

---

**Made with ❤️ for parents and kids who love Minecraft**

**Deployment:** DakBoard widget (display) + Local files (admin) = Maximum security & privacy

*Last updated: January 2025*
