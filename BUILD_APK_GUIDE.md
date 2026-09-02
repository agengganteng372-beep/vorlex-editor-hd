# 📱 PANDUAN BUILD APK X - TRASUS (DETAIL)

## ✅ Persiapan Awal

### 1. Download & Install Software Wajib

#### 🔹 Node.js (v14+)
- Download: https://nodejs.org/
- Pilih LTS version
- Install dengan default settings
- Verify: Buka CMD/Terminal, ketik:
```bash
node --version
npm --version
```

#### 🔹 Java JDK 11+
- Download: https://www.oracle.com/java/technologies/javase-jdk11-downloads.html
- Atau gunakan: https://adoptopenjdk.net/
- Install di: `C:\Program Files\Java\jdk-11` (Windows)
- Verify:
```bash
java -version
javac -version
```

#### 🔹 Android SDK
**PILIHAN 1: Via Android Studio (Rekomendasi)**
- Download: https://developer.android.com/studio
- Install & buka Android Studio
- Klik: SDK Manager → SDK Platforms
- Install: Android 12.0 (API 31) atau lebih baru
- Klik: SDK Manager → SDK Tools
- Install: Android SDK Build-Tools

**PILIHAN 2: Command Line Tools Saja**
- Download: https://developer.android.com/studio#command-tools
- Extract ke folder (misalnya: `C:\Android`)
- Buka Command Prompt di folder itu
- Jalankan:
```bash
bin\sdkmanager --sdk_root=%ANDROID_HOME% platform-tools "platforms;android-31" "build-tools;31.0.0"
```

---

## 🛠️ Setup Environment Variables

### WINDOWS:

1. Buka: **Start Menu** → ketik "Environment Variables"
2. Klik: "Edit the system environment variables"
3. Klik: "Environment Variables..." button
4. Klik: "New..." (System variables)

**Tambahkan 3 variables:**

| Nama Variable | Value |
|--------------|-------|
| `JAVA_HOME` | `C:\Program Files\Java\jdk-11` |
| `ANDROID_HOME` | `C:\Users\YourUsername\AppData\Local\Android\Sdk` |
| `PATH` | Tambahkan: `;%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools` |

5. Klik OK semua
6. Buka CMD baru, verify:
```bash
echo %JAVA_HOME%
echo %ANDROID_HOME%
```

---

### LINUX / MAC:

Buka terminal, edit `~/.bashrc` atau `~/.zshrc`:
```bash
nano ~/.bashrc
```

Tambahkan di akhir file:
```bash
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```

Simpan (Ctrl+X, Y, Enter), lalu:
```bash
source ~/.bashrc
```

---

## 🚀 BUILD APK STEP BY STEP

### STEP 1: Install Cordova CLI
Buka CMD/Terminal, jalankan:
```bash
npm install -g cordova
```

Verify:
```bash
cordova --version
```

---

### STEP 2: Clone Repository
```bash
git clone https://github.com/agengganteng372-beep/vorlex-editor-hd.git
cd vorlex-editor-hd
```

Jika tidak ada Git, download ZIP dari GitHub langsung.

---

### STEP 3: Buat Cordova Project
```bash
cordova create vorlex-app com.trasus.vorlex "X - TRASUS"
cd vorlex-app
```

Akan membuat folder struktur seperti ini:
```
vorlex-app/
├── www/                 (folder aplikasi)
│   ├── index.html
│   ├── css/
│   └── js/
├── platforms/          (akan dibuat nanti)
├── plugins/            (dependencies)
└── config.xml
```

---

### STEP 4: Tambahkan Android Platform
```bash
cordova platform add android
```

⏳ Ini akan download Android SDK tools (bisa 10-30 menit tergantung internet)

---

### STEP 5: Copy File HTML ke Project

Copy file dari repo asli:
```bash
# Dari folder vorlex-editor-hd ke vorlex-app/www/
copy ..\index.html www\index.html
copy ..\clock.html www\clock.html

# Linux/Mac:
cp ../index.html www/
cp ../clock.html www/
```

Jika ada index.html yang lama, delete dulu atau replace.

---

### STEP 6: Copy Config.xml
```bash
# Windows:
copy ..\config.xml config.xml

# Linux/Mac:
cp ../config.xml .
```

---

### STEP 7: BUILD APK (DEBUG)

```bash
cordova build android
```

⏳ Ini akan compile & build APK (5-15 menit untuk pertama kali)

**Output:**
```
🎉 APK berhasil dibuat di:
platforms/android/app/build/outputs/apk/debug/app-debug.apk
```

---

## 📲 TEST APK KE DEVICE

### Via USB Cable:

1. **Connect Android Phone ke PC via USB**
2. **Enable USB Debugging:**
   - Setting → Developer Options
   - Tap "USB Debugging" ON

3. **Install APK:**
```bash
adb install -r platforms/android/app/build/outputs/apk/debug/app-debug.apk
```

4. **Buka App di Phone** → Cari "X - TRASUS"

---

### Via Emulator:

```bash
# Lihat emulator yang aktif
adb devices

# Install
adb install -r platforms/android/app/build/outputs/apk/debug/app-debug.apk

# Launch app
adb shell am start -n com.trasus.vorlex/.MainActivity
```

---

## 🔑 BUILD RELEASE APK (Untuk Play Store)

### STEP 1: Generate Keystore
```bash
keytool -genkey -v -keystore my-release-key.keystore ^
  -keyalg RSA -keysize 2048 -validity 10000 ^
  -alias my-key-alias
```

**Jawab pertanyaan:**
```
Keystore password: ← INGAT PASSWORD INI
First and last name: Nama Anda
Organization: TRASUS
City/Locality: City Name
State/Province: State
Country code (XX): ID
Certificate password: ← Tekan Enter
```

File `my-release-key.keystore` akan dibuat.

---

### STEP 2: Buat build.json
Di folder `vorlex-app/`, buat file `build.json`:
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

**Ganti:**
- `YOUR_PASSWORD` = password dari step STEP 1
- `YOUR_KEYSTORE_PASSWORD` = keystore password dari STEP 1

---

### STEP 3: Build Release APK
```bash
cordova build android --release
```

**Output:**
```
✅ Signed Release APK di:
platforms/android/app/build/outputs/apk/release/app-release.apk
```

---

## 🐛 TROUBLESHOOTING

### ❌ Error: "Gradle not found"
**Solusi:**
```bash
cordova platform remove android
cordova platform add android@latest
```

---

### ❌ Error: "ANDROID_HOME not set"
**Solusi:** Setup environment variables (lihat di atas)

---

### ❌ Error: "JAVA_HOME not set"
**Solusi:** Setup environment variables dengan benar

---

### ❌ Error: "gradlew permission denied" (Linux/Mac)
```bash
chmod +x platforms/android/gradlew
cordova build android
```

---

### ❌ Build Timeout
Edit: `platforms/android/build.gradle`
Tambahkan:
```gradle
allprojects {
    gradle.projectsEvaluated {
        tasks.withType(JavaCompile) {
            options.compilerArgs.add('-Xmx2048m')
        }
    }
}
```

---

### ❌ APK berhasil tapi error saat dibuka
- Update semua plugin Cordova
- Bersihkan cache: `cordova clean android`
- Rebuild: `cordova build android`

---

## 📊 SIZE APK

Typical size untuk VORLEX Editor:
- **Debug APK:** 15-20 MB
- **Release APK:** 8-12 MB

Jika terlalu besar, gunakan ProGuard untuk minimize:
```gradle
android {
    buildTypes {
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt')
        }
    }
}
```

---

## 📤 UPLOAD KE PLAY STORE

1. **Daftar Google Play Developer**
   - Buka: https://play.google.com/console
   - Bayar: $25 (one-time)
   - Verifikasi email & payment method

2. **Create New App**
   - Klik "Create app"
   - Nama: "X - TRASUS"
   - Default language: English
   - App type: Application

3. **Upload Release APK**
   - Klik: Dashboard → Release
   - Klik: "Create new release"
   - Upload: `app-release.apk`

4. **Isi Metadata**
   - Title
   - Description
   - Screenshots (minimal 2)
   - Icon (512x512)
   - Feature image

5. **Submit untuk Review**
   - Klik: "Send for review"
   - Google akan review (24-48 jam)

---

## ✅ CHECKLIST BUILD APK

- [ ] Install Node.js v14+
- [ ] Install Java JDK 11+
- [ ] Install Android SDK
- [ ] Setup JAVA_HOME environment variable
- [ ] Setup ANDROID_HOME environment variable
- [ ] Install Cordova: `npm install -g cordova`
- [ ] Clone repository
- [ ] Buat Cordova project: `cordova create ...`
- [ ] Add Android platform: `cordova platform add android`
- [ ] Copy index.html ke www/
- [ ] Copy config.xml
- [ ] Build APK: `cordova build android`
- [ ] Test di device/emulator: `adb install ...`
- [ ] Generate keystore untuk release
- [ ] Build release APK: `cordova build android --release`

---

## 📞 BANTUAN LEBIH LANJUT

- **Cordova Docs:** https://cordova.apache.org/docs/en/latest/guide/cli/
- **Android Docs:** https://developer.android.com/docs
- **Stack Overflow:** https://stackoverflow.com/questions/tagged/cordova
- **GitHub Issues:** https://github.com/agengganteng372-beep/vorlex-editor-hd/issues

---

## 💡 TIPS

1. **First build paling lama** (15-30 menit) karena download dependencies
2. **Recompile lebih cepat** (3-5 menit) kalo hanya edit HTML/CSS
3. **Gunakan real device** untuk testing (lebih akurat daripada emulator)
4. **Test sebelum release** untuk cegah bugs
5. **Keep keystore file aman** - jangan share ke orang lain

---

**Made with ❤️ by TRASUS**  
Version 1.0.0 | 2026
