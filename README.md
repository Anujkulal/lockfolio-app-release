# 🔐 Lockfolio

<div align="center">

![Lockfolio Version](https://img.shields.io/badge/version-5.0.4-blue.svg)
![React Native](https://img.shields.io/badge/React%20Native-0.81.5-61DAFB.svg)
![Expo SDK](https://img.shields.io/badge/Expo-~54.0-000020.svg)
![Platform](https://img.shields.io/badge/platform-Android-lightgrey.svg)

**A secure, offline-first document and credential manager**

</div>

---

## 📖 Overview

Lockfolio is a privacy-first Android app for storing sensitive documents and credentials on your device. Data stays local unless you choose to create a password-protected backup or share a file.

There is no account to create and no Lockfolio cloud backend. Everything is encrypted at rest: SQLCipher for the database, AES-256 for vault fields, and encrypted files for documents and note audio.

### 🎯 Key Highlights

- **🔒 Encryption at Rest**: SQLCipher database, AES-256 vault fields, and encrypted document and note-audio files
- **🔐 App Lock**: 6-digit PIN, optional biometrics, and a 12-word recovery key
- **📴 Offline-First**: Core features work on the device, with no cloud sync
- **🗂️ Documents**: Categories and slots, front and back files, search, and expiry tracking
- **🔑 Secure Vault**: Notes, bank accounts, Wi-Fi, email, licenses, device credentials, and web shortcuts
- **💾 Encrypted Backups**: Password-protected `.lockfolio` archives
- **🌗 Themes**: Light, dark, or system

---

## ✨ Features

### 🏠 Home

- Dashboard with expiry alerts, expiring documents, favorites, quick actions, recent files, and an overview
- In-app notification inbox for document expiry

### 📄 Documents

- **Categories**: Identity, Civil, Tax, Health, Education, Employment, Housing, Finance, Vehicle, Legal, Travel, Business & Corporate, and Warranties & Receipts
- **Slots**: Predefined document types in each category, plus a custom slot
- **Front and back**: A required front file and an optional back file. JPG, PNG, or PDF, up to **10 MB** each, from the gallery, camera, files, or the Android document scanner
- **Image edit**: Crop or rotate a photo before it is saved, preview a PDF in the picker, and swap front and back
- **Metadata**: Title, holder name, document number, category, slot, and expiry date
- **Search**: Find documents by title, holder, number, category, and slot, including voice search
- **Expiry**: Expiring Soon and Expired lists, optional calendar reminders, and optional local alerts at 30 days, 7 days, and on the expiry day
- **In-app viewer**: Pinch-zoom images or page through PDFs, and switch between front and back
- **Share**: Share files directly, or export a selection as a password-protected ZIP (share the password separately)
- **Statistics**: Counts by category, expiry status, and totals

### 🔐 Secure Vault

Typed templates:

- **Secure Note**: Private notes, voice dictation, and encrypted audio clips (up to 10)
- **Bank Account**: Bank name, account number, IFSC/SWIFT, and holder details
- **Wi-Fi**: Network name, password, and security type
- **Email**: Address, password, provider, and recovery info
- **Third-party Software**: Logins and license keys for apps and services
- **Device Credentials**: Phone, laptop, and other device account details
- **Software License**: License keys, expiry, and provider info
- **Web Shortcut**: App and site shortcuts

You can favorite items, filter by type, search, copy fields, and share item details. Vault contents can be exported to PDF after you unlock the app. That export leaves out web shortcuts.

### 🛡️ Security & Privacy

- **6-digit PIN**, with optional biometric unlock
- **12-word recovery key** to reset a forgotten PIN
- **Lock and blur**: Lock on launch, lock again after a background timeout, and blur the screen while the app is in the background
- **Failed-attempt lockout**: Temporary lock after repeated failed attempts
- **Action unlock**: Optional extra prompts before view, edit, delete, and share
- **On device**: Contents leave the phone only when you create a backup or share a file

The PIN and recovery key are stored as salted hashes. The PIN is not kept in plaintext.

### 💾 Backup & Restore

- Create a password-protected **`.lockfolio`** archive (password of at least 8 characters)
- Current backups use the **v4** format. Older backup versions are not restored
- The archive includes documents, vault items, front and back files, note audio, and the keys needed to reopen the vault
- The backup password is stretched with **PBKDF2-SHA256** (100,000 iterations) and the archive is checked for integrity
- Restore replaces the data already on the device after the archive is validated

### ⚙️ Settings

- Light, dark, or system theme
- App lock, biometrics, change PIN, and regenerate the recovery key
- Per-action unlock for view, edit, delete, and share
- Expiry alerts on or off
- Backup create and restore
- Document and vault item counts
- **Clear all data** after authentication and confirmation

---

## 🔒 Security

### Encryption

| Layer | What it protects |
| ----- | ---------------- |
| **SQLCipher** | The whole database at rest |
| **AES-256-CBC** | Sensitive vault fields |
| **AES-256-GCM** | Document files and secure-note audio |
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

---

<!-- ## 🖼️ Screenshots

<div align="center">

| Home Screen | Vault | Document Details | Settings |
|------------|-------|------------------|----------|
| *Document management* | *Secure credentials* | *Encrypted storage* | *Security settings* |

</div>

--- -->

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
4. Confirm. Existing documents, vault items, and files on the device are replaced

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

<!-- ### For Developers
- ✅ Never log sensitive data (even in development)
- ✅ Use `__DEV__` checks for debug logs
- ✅ Test encryption/decryption thoroughly
- ✅ Validate all user inputs
- ✅ Handle errors gracefully without exposing details
- ✅ Keep dependencies updated for security patches -->

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

<!-- ## 📧 Support

If you encounter any issues or have questions:
- Open an issue on [GitHub Issues](https://github.com/Anujkulal/lockfolio-app-release/issues)
- Check existing issues for solutions
- Provide detailed information (device, OS version, steps to reproduce)

--- -->

<div align="center">

**Made with ❤️ for privacy-conscious users**

⭐ **Star this repo if you find it helpful!** ⭐

</div>
