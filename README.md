# 📱 X - TRASUS | VORLEX EDITOR HD

## ⚡ Tentang Aplikasi

**X - TRASUS** adalah aplikasi mobile Android untuk mengedit foto dengan fitur lengkap:
- ✂️ Crop dengan berbagai ratio (1:1, 4:5, 16:9, bebas)
- 📝 Tambah teks dengan customisasi font, ukuran, warna
- ✨ HD Enhance & Upscale 2x
- 🎨 Filter cepat (B&W, Sepia, Negatif)
- ⚙️ Pengaturan kecerahan, kontras, saturasi, blur, ketajaman
- 🔄 Putar & balik gambar
- ⬇️ Download hasil editing dalam format HD

---

## 📋 Persyaratan Sistem untuk Build APK

### ✅ Software yang Diperlukan:
- **Node.js** v14+ (https://nodejs.org/)
- **Java Development Kit (JDK)** 11+ (https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- **Android SDK** (https://developer.android.com/studio)
- **Cordova CLI**

### ✅ Hardware Minimum:
- RAM: 4GB+
- Storage: 10GB+ (untuk Android SDK)
- Internet: Koneksi stabil

---

## 🚀 Panduan Build APK (Quick Start)

### Step 1: Install Dependencies
```bash
npm install -g cordova
```

### Step 2: Clone Repository
```bash
git clone https://github.com/agengganteng372-beep/vorlex-editor-hd.git
cd vorlex-editor-hd
```

### Step 3: Setup Cordova Project
```bash
cordova create vorlex-app com.trasus.vorlex "X - TRASUS"
cd vorlex-app
cordova platform add android
```

### Step 4: Copy Files
```bash
cp ../index.html www/
cp ../clock.html www/
cp ../config.xml .
```

### Step 5: Build APK
```bash
cordova build android
```

**Output:** `platforms/android/app/build/outputs/apk/debug/app-debug.apk`

---

## 🔑 Build Release APK (untuk Play Store)

### 1. Generate Keystore
```bash
keytool -genkey -v -keystore my-release-key.keystore \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias my-key-alias
```

### 2. Buat file `build.json`
```json
{
  "android": {
    "release": {
      "keystore": "my-release-key.keystore",
      "alias": "my-key-alias",
      "password": "YOUR_PASSWORD",
      "keystorePassword": "YOUR_KEYSTORE_PASSWORD"
    }
  }
}
```

### 3. Build Release APK
```bash
cordova build android --release
```

**Output:** `platforms/android/app/build/outputs/apk/release/app-release.apk`

---

## 📂 Struktur Project

```
vorlex-editor-hd/
├── index.html              # Main VORLEX Editor
├── clock.html              # Digital Clock (bonus)
├── config.xml              # Cordova Configuration
├── build.gradle            # Gradle Build Config
├── AndroidManifest.xml     # Android Manifest
├── README.md               # Dokumentasi
└── platforms/
    └── android/            # Generated Android Project
```

---

## 🎨 File yang Disediakan

| File | Deskripsi |
|------|-----------|
| `index.html` | VORLEX Editor - Edit foto, crop, teks |
| `clock.html` | Digital Clock - Multiple time zones |
| `config.xml` | Konfigurasi Cordova untuk Android |
| `build.gradle` | Build configuration untuk Gradle |
| `AndroidManifest.xml` | Manifest dengan permissions |

---

## 🔧 Environment Variables

### Windows:
```cmd
setx JAVA_HOME "C:\Program Files\Java\jdk-11"
setx ANDROID_HOME "C:\Users\YourUsername\AppData\Local\Android\Sdk"
setx PATH "%PATH%;%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools"
```

### Linux/Mac:
```bash
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```

---

## 🐛 Troubleshooting

| Error | Solusi |
|-------|--------|
| "Gradle not found" | `cordova platform remove android && cordova platform add android@latest` |
| "SDK not found" | Download Android SDK via Android Studio & set ANDROID_HOME |
| "JDK not found" | Install Java JDK 11+ & set JAVA_HOME |
| "Permission denied" | `chmod +x platforms/android/gradlew` (Linux/Mac) |
| "Build timeout" | Tambah `-Xmx2048m` di gradle.properties |

---

## 📱 Testing APK

### Install ke Device
```bash
adb install -r platforms/android/app/build/outputs/apk/debug/app-debug.apk
```

### Launch App
```bash
adb shell am start -n com.trasus.vorlex/.MainActivity
```

---

## 📤 Upload ke Play Store

1. Daftar Google Play Developer ($25)
2. Generate signed release APK
3. Upload ke Google Play Console
4. Isi metadata & deskripsi
5. Submit untuk review

---

## 🌟 Features Checklist

- ✅ Crop gambar (1:1, 4:5, 16:9, bebas)
- ✅ Tambah teks dengan font customizable
- ✅ HD Enhance & Upscale 2x
- ✅ Filter cepat (Grayscale, Sepia, Negatif)
- ✅ Pengaturan brightness, contrast, saturasi, blur
- ✅ Putar & balik gambar
- ✅ Download hasil HD
- ✅ LocalStorage untuk menyimpan preferensi
- ✅ Responsive design
- ✅ Touch-friendly UI

---

## 📞 Support & Resources

- **GitHub:** https://github.com/agengganteng372-beep/vorlex-editor-hd
- **Cordova Docs:** https://cordova.apache.org/docs/en/latest/
- **Android Studio:** https://developer.android.com/studio
- **Issues:** https://github.com/agengganteng372-beep/vorlex-editor-hd/issues

---

## 📄 License

MIT License - Bebas digunakan untuk keperluan pribadi maupun komersial

---

## 👨‍💻 Author

**TRASUS**  
Email: agengganteng372@gmail.com  
GitHub: https://github.com/agengganteng372-beep

---

**Version:** 1.0.0  
**App ID:** com.trasus.vorlex  
**Min API Level:** 21 (Android 5.0)  
**Target API Level:** 34 (Android 14)

Made with ❤️ by TRASUS
