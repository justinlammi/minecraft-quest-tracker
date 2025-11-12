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
- 📱 **Easy admin panel** - manage quests from any device
- ✏️ **Edit quests** - change names, points, and icons on the fly
- 🎨 **Customizable icons** - choose from 16 Minecraft-themed emojis
- 📈 **Track progress** - see daily completion stats
- 🌐 **Cloud-based** - access from anywhere
- 🚀 **GitHub Pages ready** - free web hosting included
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
- **For deployment, one of:**
  - GitHub account (for GitHub Pages - recommended)
  - Raspberry Pi with DakBoard (for local deployment)
  - Any device that can display web pages

### Setup Time
- **Firebase setup**: 15-20 minutes (one-time)
- **Testing**: 5-10 minutes
- **Deployment (GitHub Pages)**: 5-10 minutes
- **Deployment (Raspberry Pi)**: 10-15 minutes
- **Total**: 25-45 minutes depending on deployment method

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

### Step 5: Deployment Options

Choose the deployment method that works best for you:

---

#### **Option A: GitHub Pages (Recommended - Easy & Free)**

**Best for:** Easy setup, accessible from anywhere, automatic updates when you push changes

**Live Example:** https://justinlammi.github.io/minecraft-quest-tracker/minecraft-quest-tracker.html

1. **Create GitHub Repository**
   - Go to https://github.com/new
   - Repository name: `minecraft-quest-tracker`
   - Set to Public (required for free GitHub Pages)
   - Click "Create repository"

2. **Upload Your Files**
   ```bash
   # In your project folder
   git init
   git add minecraft-quest-tracker.html
   git add minecraft-quest-tracker-admin.html
   git add minecraft-initialize-data.html
   git add README.md
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/minecraft-quest-tracker.git
   git push -u origin main
   ```

   **Or use GitHub Desktop:**
   - Open GitHub Desktop
   - File → Add Local Repository
   - Select your project folder
   - Commit changes
   - Publish to GitHub

3. **Enable GitHub Pages**
   - Go to your repository on GitHub
   - Click "Settings" tab
   - Click "Pages" in left sidebar
   - Under "Source", select "Deploy from a branch"
   - Branch: `main`, Folder: `/ (root)`
   - Click "Save"
   - Wait 1-2 minutes for deployment

4. **Get Your URL**
   - Your site will be at: `https://YOUR-USERNAME.github.io/minecraft-quest-tracker/`
   - Display: `https://YOUR-USERNAME.github.io/minecraft-quest-tracker/minecraft-quest-tracker.html`
   - Admin: `https://YOUR-USERNAME.github.io/minecraft-quest-tracker/minecraft-quest-tracker-admin.html`

5. **Configure DakBoard**
   - Open DakBoard settings
   - Add new "Custom URL" block
   - Enter URL: `https://YOUR-USERNAME.github.io/minecraft-quest-tracker/minecraft-quest-tracker.html`
   - Set refresh rate: 60 seconds
   - Position and size as desired
   - Save and preview

6. **Access Admin Panel**
   - Open admin URL in browser
   - Bookmark for easy access
   - Works from any device with internet

**Benefits:**
- ✅ Accessible from anywhere with internet
- ✅ No Raspberry Pi needed
- ✅ Free hosting
- ✅ Easy updates (just push to GitHub)
- ✅ Automatic HTTPS
- ✅ Works on any DakBoard device

---

#### **Option B: Raspberry Pi Local Files (Offline)**

**Best for:** Offline setup, local network only, more control

1. **Transfer Display File**
   ```bash
   # SSH into your Pi
   ssh pi@your-pi-address

   # Create directory
   mkdir -p /home/pi/minecraft-quests

   # Copy file to Pi (from your computer)
   scp minecraft-quest-tracker.html pi@your-pi-address:/home/pi/minecraft-quests/
   ```

2. **Add to DakBoard**
   - Open DakBoard settings
   - Add new "Custom URL" block
   - Enter URL: `file:///home/pi/minecraft-quests/minecraft-quest-tracker.html`
   - Set refresh rate: 60 seconds
   - Position and size as desired
   - Save and preview

3. **Access Admin Panel**
   - Upload `minecraft-quest-tracker-admin.html` to web hosting, OR
   - Save on your computer and open locally
   - Bookmark for easy access

**Benefits:**
- ✅ Works offline (if Firebase was cached)
- ✅ Local files, full control
- ✅ No public GitHub repository needed
- ❌ Requires Raspberry Pi
- ❌ Updates require manual file transfer

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

## 📱 Access Admin Panel Remotely

### Option 1: GitHub Pages (Best - If Using GitHub Deployment)
- Admin panel automatically hosted alongside display
- Access from anywhere: `https://YOUR-USERNAME.github.io/minecraft-quest-tracker/minecraft-quest-tracker-admin.html`
- Bookmark on phone/computer
- No additional setup needed
- Updates automatically when you push changes

### Option 2: Keep on Computer
- Save admin file in Documents
- Bookmark in browser
- Open when needed
- Works offline

### Option 3: Save to Phone
- Email file to yourself
- Save to phone
- Open in mobile browser
- Works offline

### Option 4: Other Web Hosting (Advanced)
- Upload to Netlify, Vercel, or other hosting service
- Access via URL from anywhere
- May require account/setup

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

### Display Won't Show on DakBoard

**Problem:** File path or permissions issue

**Solutions (Raspberry Pi):**
1. Verify file path: `file:///home/pi/minecraft-quests/minecraft-quest-tracker.html`
2. Check file permissions: `chmod 644 minecraft-quest-tracker.html`
3. Test by opening file directly in Pi's browser first
4. Check DakBoard refresh rate is set

**Solutions (GitHub Pages):**
1. Verify URL is correct: `https://YOUR-USERNAME.github.io/minecraft-quest-tracker/minecraft-quest-tracker.html`
2. Check GitHub Pages is enabled in repository settings
3. Wait 2-3 minutes after pushing changes (deployment delay)
4. Test URL in regular browser first
5. Check that repository is Public (required for free GitHub Pages)
6. Clear DakBoard cache and reload

### GitHub Pages Shows 404 Error

**Problem:** Page not found

**Solutions:**
1. Check repository name matches URL
2. Verify GitHub Pages is enabled (Settings → Pages)
3. Ensure branch is set to `main` and folder to `/ (root)`
4. File names are case-sensitive - use exact names
5. Wait 1-2 minutes after enabling GitHub Pages
6. Check repository is Public

### Changes Not Showing on GitHub Pages

**Problem:** Updated files but page shows old version

**Solutions:**
1. GitHub Pages has a cache delay (1-5 minutes)
2. Hard refresh in browser: Ctrl+Shift+R (Cmd+Shift+R on Mac)
3. Check your commit was pushed: `git log` or view on GitHub
4. Clear browser cache
5. Try incognito/private browsing mode
6. DakBoard may need cache clear + refresh

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

### Current Setup
- Database uses test mode rules (read/write allowed)
- Suitable for home use behind firewall
- No authentication required
- Firebase config is public (this is normal)

### For Production/Public Use
If you want to secure this for public internet:

1. **Add Authentication:**
   ```json
   {
     "rules": {
       ".read": "auth != null",
       ".write": "auth != null"
     }
   }
   ```

2. **Implement Firebase Auth:**
   - Add Firebase Authentication
   - Update HTML files to require login
   - Restrict database access to authenticated users

### Privacy
- No personal data is collected
- No analytics or tracking
- All data stays in your Firebase project
- You control all data

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

### v2.1 (Current)
- 🌐 Added GitHub Pages deployment option (recommended)
- 📝 Updated README with deployment choices
- 🔧 Fixed file name references in documentation
- 📚 Enhanced troubleshooting for web hosting
- 🔗 Live example: https://justinlammi.github.io/minecraft-quest-tracker/

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

*Last updated: January 2025*
