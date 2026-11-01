# Lockfolio

![Lockfolio Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![React Native](https://img.shields.io/badge/React%20Native-0.81.5-61DAFB.svg)
![Expo SDK](https://img.shields.io/badge/Expo-~54.0-000020.svg)
![Platform](https://img.shields.io/badge/platform-Android-lightgrey.svg)

**A secure, offline-first document and credential manager**

---

## 📖 Overview

Lockfolio is a privacy-first Android app for storing sensitive documents and credentials on your device. Data stays local unless you choose to create a password-protected backup or share a file. Built by [Anuj Kulal](https://lockfolio.netlify.app).

There is no account to create and no Lockfolio cloud backend. Everything is encrypted at rest: SQLCipher for the database, AES-256 for vault fields, and Android Jetpack `EncryptedFile` for document and note-audio binaries.

Lockfolio combines four surfaces in one app:

1. **Home** — Dashboard for expiry alerts, expiring documents, favorites, quick actions, recent files, and an overview
2. **Documents** — Organize ID cards, certificates, vehicle papers, and other files by category and slot, with encrypted storage, expiry tracking, search, and in-app viewing
3. **Vault** — Store notes, bank accounts, Wi-Fi passwords, email logins, software licenses, device credentials, and web shortcuts behind the app lock
4. **Settings** — PIN and biometric lock, password-protected backup/restore, recycle bin, expiry alerts, and clear-all data

|             |                                                        |
| ----------- | ------------------------------------------------------ |
| **Version** | 1.0.0                                                  |
| **Package** | `com.anujkulal.lockfolio`                              |
| **Site**    | [lockfolio.netlify.app](https://lockfolio.netlify.app) |

### 🎯 Key Highlights

- **🔒 Encryption at Rest**: SQLCipher database, AES-256 vault fields, and encrypted document and note-audio files
- **🔐 App Lock**: 6-digit PIN, optional biometrics, and a 12-word recovery key
- **📴 Offline-First**: Core features work on the device, with no cloud sync
- **🗂️ Documents**: Categories and slots, front and back files, search, expiry tracking, and recycle bin
- **🔑 Secure Vault**: Notes, bank accounts, Wi-Fi, email, licenses, device credentials, and web shortcuts
- **💾 Encrypted Backups**: Password-protected `.lockfolio` archives
- **🗑️ Recycle Bin**: Deleted documents and vault items stay for 30 days before automatic removal
- **🌗 Themes**: Light, dark, or system

---

## ✨ Features

### 🏠 Home

- Greeting dashboard with expiry alerts, expiring documents, favorites, quick actions, recent files, and an overview
- In-app notification inbox for document expiry

### 📄 Documents

- **Categories**: Identity, Civil, Tax, Health, Education, Employment, Housing, Finance, Vehicle, Legal, Travel, Business & Corporate, and Warranties & Receipts
- **Slots**: Predefined document types in each category, plus a custom slot
- **Views**: Category grid/list, all-documents list, and category detail (card stack or list)
- **CRUD**: Create, edit, view, delete, and share documents. Delete moves a document to the recycle bin; it is not erased immediately
- **Front and back**: A required front file and an optional back file. JPG, PNG, or PDF, up to **15 MB** each, from the gallery, camera, files, or the Android document scanner
- **Image edit**: Crop or rotate a photo before it is saved, preview a PDF in the picker, and swap front and back
- **Metadata**: Title, holder name, document number, category, slot (or custom slot label), and expiry date
- **Search**: Find documents by title, holder, number, category, and slot, including voice search
- **Expiry**: Expiring Soon and Expired lists, optional calendar reminders, and optional local alerts at 30 days, 7 days, and on the expiry day
- **In-app viewer**: Pinch-zoom images or page through PDFs, and switch between front and back
- **Export from the viewer**:
  - Share the current side
  - Open a PDF in another app
  - Save an image to the gallery
  - Save image sides as a PDF (front, back, or both) into a folder you choose
  - Save the current file to a folder
  - Add the expiry date to the calendar
- **Share**: Share files directly, or export a selection as a password-protected ZIP (both sides included; share the password separately)
- **Statistics**: Counts by category, expiry status, and totals

### 🔐 Secure Vault

Typed templates:

| Type                     | Purpose                                               |
| ------------------------ | ----------------------------------------------------- |
| **Web Shortcut**         | App / site shortcuts (icon grid)                      |
| **Secure Note**          | Private notes, voice dictation, and encrypted audio   |
| **Bank Account**         | Bank name, account number, IFSC/SWIFT, holder details |
| **Wi-Fi**                | Network name, password, security type                 |
| **Email**                | Address, password, provider, recovery info            |
| **Third-party Software** | Logins and license keys for apps/services             |
| **Device Credentials**   | Phone / laptop / device account details               |
| **Software License**     | License keys, expiry, provider info                   |

Vault capabilities:

- Create, view, edit, and delete. Delete moves an item to the recycle bin; it is not erased immediately
- Favorites and type filter chips
- Search across vault items
- Copy fields to clipboard
- Share item details
- **Secure Note audio** — record (pause/resume/stop/preview) or upload clips (up to 10); encrypted on disk like documents
- **Voice dictation** — speech-to-text in the note editor
- **PDF export** of vault contents (auth-gated; excludes web shortcuts)
- Vault statistics

### 🛡️ Security & Privacy

- **6-digit PIN**, with optional biometric unlock
- **12-word recovery key** to reset a forgotten PIN
- **Lock and blur**: Lock on launch, lock again after a background timeout, and blur the screen while the app is in the background
- **Failed-attempt lockout**: Temporary lock after repeated failed attempts
- **Action unlock**: Optional extra prompts before view, edit, delete, and share
- **Toggleable security**: Enable or disable App Lock and biometrics in Settings
- **On device**: Contents leave the phone only when you create a backup or share a file

The PIN and recovery key are stored as salted hashes. The PIN is not kept in plaintext.

### 💾 Backup & Restore

- Create a password-protected `.lockfolio` archive (password of at least 8 characters)
- Current backups use the **v1** format. Older backup versions are not restored
- The archive includes documents, vault items, recycle-bin items (with the date they were deleted), front and back files, note audio, and the keys needed to reopen the vault
- The backup password is stretched with **PBKDF2-SHA256** (100,000 iterations) and the archive is checked for integrity
- Restore replaces the data already on the device after the archive is validated
- Restore puts recycle-bin items back in the bin. Items already older than 30 days are permanently removed in batches after the restore finishes
- Progress UI during create and restore

### ⚙️ Settings

- About / version / author link
- Light, dark, or system theme
- App lock, biometrics, change PIN, and regenerate the recovery key
- Per-action unlock for view, edit, delete, and share
- Expiry alerts on or off
- Backup create and restore
- **Recycle bin** — deleted documents and vault items stay for 30 days. Restore them, delete one forever, or empty the bin. Items older than 30 days are removed automatically when the app is open
- Document and vault item counts
- **Clear all data** after authentication and confirmation

---

## 🔒 Security

### Encryption

| Layer | What it protects |
| ----- | ---------------- |
| **SQLCipher** | The whole database at rest |
| **AES-256-CBC** | Sensitive vault fields |
| **AES-256-GCM** (EncryptedFile) | Document files and secure-note audio |
| **PBKDF2-SHA256 + AES-CBC** | The portable `.lockfolio` backup |
| **Salted hash** | The app PIN and the recovery key |

Master keys stay in device secure storage. They are not the same thing as your PIN.

### Authentication

- A 6-digit PIN you choose inside the app
- Optional fingerprint or face unlock
- A 12-word recovery phrase if you forget the PIN
- A temporary lock after repeated failed attempts
- Lock on launch and again after the app has been in the background

### Privacy

- **Local-first**: Primary data lives on the device
- **No account**: No sign-in and no Lockfolio cloud for core features
- **You choose the export**: Backups and shares happen only when you create them
- **Document scanning**: Optional Android scans use Google ML Kit on the device. Document contents are not uploaded to Google. ML Kit may still send diagnostic or usage metrics to Google
- **Voice input**: Speech recognition may use an on-device model or a network connection, depending on the phone
- **Auth-gated destructive actions**: Clear data, exports, and sensitive views can ask for the PIN or biometrics when those locks are enabled

---

## 🚀 Getting Started (User Guide)

### First Launch

1. Complete the short onboarding
2. Set a **6-digit PIN** and store the **12-word recovery key** somewhere you can find later
3. Turn on biometric unlock if you want it
4. Allow camera, photos, microphone, notifications, or calendar access only for the features you use

### Adding Documents

1. Open **Documents** and add a document
2. Choose a category and a slot (or a custom slot)
3. Add a front file, and a back file if the document has one
4. Enter the title, holder, number, and expiry date
5. Save. The file is encrypted on the device

### Using Secure Vault

1. Open the **Vault** tab
2. Create an item and choose a template (note, bank account, Wi-Fi, email, and so on)
3. Enter the details
4. Save. Vault fields are encrypted before they are stored

### Creating Backups

1. Go to **Settings** and open backup
2. Create a backup
3. Enter a backup password of at least 8 characters
4. Choose where to save the file
5. Keep the `.lockfolio` file and its password. The app cannot recover a forgotten backup password

### Restoring Backups

1. Go to **Settings** and open restore
2. Select a `.lockfolio` file from the current backup format
3. Enter the backup password
4. Confirm. Existing documents, vault items, recycle-bin items, and files on the device are replaced

### Recycle Bin

1. Go to **Settings** and open the recycle bin
2. Restore an item, delete it forever, or empty the bin
3. Items older than 30 days are removed automatically when the app is open

---

## 📱 Permissions (Android)

- **Camera** — capture document photos
- **Photos / media** — pick and save document images
- **Storage** — document picker and backup file access
- **Microphone** — voice search, note dictation, and secure-note audio
- **Notifications** — local expiry reminders
- **Biometrics** — optional app unlock and gated actions
- **Calendar** — optional expiry reminder events

---

## 🔐 Security Best Practices

### For Users

- ✅ Write down the 12-word recovery key and keep it offline
- ✅ Turn on biometrics if this phone supports them
- ✅ Use a backup password that is different from the app PIN
- ✅ Store backup files somewhere you control
- ✅ Share a ZIP password separately from the ZIP itself
- ✅ Lock the app before handing the phone to someone else
- ❌ Never share your backup password or recovery key

---

## 👨‍💻 Author

**Anuj Kulal**

- GitHub: [@Anujkulal](https://github.com/Anujkulal)
- Website: [lockfolio.netlify.app](https://lockfolio.netlify.app)
- Package: `com.anujkulal.lockfolio`

---

## ⚠️ Disclaimer

Lockfolio is designed for personal use to store sensitive information on your own device. The app encrypts data at rest and password-protects backups. You are responsible for:

- Keeping the app PIN, recovery key, and backup password
- Securing the phone itself
- Storing backup files safely
- Understanding the risks of keeping digital copies of sensitive documents

**The developer is not responsible for any data loss, security breaches, or misuse of the application.**

---

**Made with ❤️ for privacy-conscious users**
