# 🌪️ Multiplayer AR Spinning Top Battle

> **Proyek Pengembangan Game Augmented Reality & Network Programming**
>
> *Rasakan sensasi pertarungan gasing (Beyblade) di dunia nyata bersama teman melalui teknologi AR dan Multiplayer Online.*



https://github.com/user-attachments/assets/cefe97bc-469c-4878-9dae-767f361d34da



---

## 📖 Deskripsi Proyek
**Multiplayer AR Spinning Top** adalah game mobile berbasis **Augmented Reality (AR)** yang memungkinkan pemain untuk memunculkan arena pertarungan di lantai dunia nyata dan bertarung melawan pemain lain secara *real-time* melalui internet.

Game ini menggabungkan fisika momentum, sinkronisasi jaringan tingkat lanjut, dan deteksi lingkungan AR untuk menciptakan pengalaman bermain yang imersif.

---

## 🛠️ Tech Stack (Teknologi)
Proyek ini dibangun menggunakan teknologi standar industri:

*   **Engine:** Unity 6.2
*   **Language:** C#
*   **Network:** Photon PUN 2 (Photon Unity Networking)
*   **AR Framework:** AR Foundation (ARCore & ARKit)
*   **Pattern:** Singleton, Observer, Object Pooling
*   **Platform:** Android 

---

## ✨ Fitur Unggulan

### 1. 🌐 Real-time Multiplayer
*   **Lobby System:** Login dengan Nickname, Create/Join Room otomatis.
*   **Matchmaking:** Mencari lawan secara acak atau membuat ruang sendiri jika server kosong.

### 2. 📱 Augmented Reality (AR) Implementation
*   **Plane Detection:** Mendeteksi permukaan lantai untuk menaruh Arena.
*   **World Scaling:** Fitur slider untuk membesarkan/mengecilkan ukuran dunia AR (`XROrigin`) agar pas di ruangan sempit maupun luas.
*   **Relative Positioning:** Sistem koordinat khusus agar posisi pemain tetap sinkron meskipun titik nol (0,0,0) AR di HP setiap pemain berbeda.

### 3. ⚔️ Gameplay & Fisika
*   **Physics-Based Combat:** Damage dihitung berdasarkan **Kecepatan Linear** dan **Massa**. Gasing yang lebih cepat akan memberikan damage lebih besar saat tabrakan.
*   **Class System:** 
    *   🔴 **Attacker:** Damage besar, tapi pertahanan lemah.
    *   🟢 **Defender:** Damage kecil, tapi pertahanan (Defense) sangat kuat.
*   **Spin Speed as Health:** Nyawa adalah kecepatan putar. Jika berhenti berputar, pemain mati.

---

## 📂 Struktur Kode & Arsitektur (Code Architecture)

Proyek ini terdiri dari **15 Script Utama** yang saling bekerja sama, dibagi menjadi 4 modul utama:

### 🔹 Modul 1: Network & Game Flow
*   `Singleton.cs` & `SceneLoader.cs`: Mengatur manajemen scene dan loading screen agar transisi mulus tanpa menghancurkan objek penting (*DontDestroyOnLoad*).
*   `LobbyManager.cs`: Menangani koneksi ke Photon Master Server dan login UI.
*   `SpinningTopsGameManager.cs`: Logika Matchmaking (Join Random Room / Create Room) dan penanganan pemain keluar/masuk.
*   `MultiplayerARSpinnerTopGame.cs`: Konstanta global untuk mencegah *Hardcoded Strings* (Typo).

### 🔹 Modul 2: AR Management
*   `ARPlacementManager.cs`: Menggunakan **Raycasting** untuk menempatkan Arena mengikuti posisi kamera.
*   `ARPlacementAndPlaneDetectionController.cs`: Mengelola fase "Placing" (Menaruh Arena) dan fase "Battle" (Mengunci posisi Arena dan mematikan deteksi lantai).
*   `ScaleController.cs`: Mengatur skala `XROrigin` menggunakan UI Slider.

### 🔹 Modul 3: Player Spawning & Sync (Tantangan Terberat)
*   `SpawnManager.cs`:
    *   Menggunakan **Manual Instantiation** (bukan `PhotonNetwork.Instantiate`).
    *   Mengirim data posisi via **`RaiseEvent`** dengan kalkulasi **Posisi Relatif terhadap Arena** untuk mengatasi perbedaan koordinat dunia AR antar-pemain.
*   `MySynchronizationScript.cs`: Implementasi `IPunObservable` manual untuk sinkronisasi posisi dengan **Lag Compensation** (prediksi gerakan) agar tidak patah-patah.
*   `PlayerSetup.cs`: Memastikan Input Joystick hanya aktif di karakter milik sendiri (`IsMine`).

### 🔹 Modul 4: Battle Mechanics
*   `MovementController.cs`: Menggerakkan gasing menggunakan `Rigidbody.AddForce` dan efek kemiringan (Tilt).
*   `Spinner.cs`: Menangani visual rotasi gasing yang terpisah dari fisika utamanya.
*   `BattleScript.cs`: Otak gameplay. Menghitung kalkulasi tabrakan, pengurangan Spin Speed (HP), RPC untuk sinkronisasi damage, dan Object Pooling untuk efek partikel.
*   `PlayerSelectionManager.cs`: Menyimpan pilihan model karakter ke `CustomProperties` jaringan.


---

## 🚀 Cara Instalasi & Menjalankan
1.  Clone repository ini.
2.  Buka project menggunakan **Unity 2023.x**.
3.  Pastikan settings **Photon AppID** sudah terpasang di `PhotonServerSettings`.
4.  Build ke device **Android** (pastikan support ARCore) atau **iOS**.
5.  Mainkan dengan minimal 2 device untuk mencoba fitur multiplayer.

---

## 👤 Author
**Kelompok MarinirX**
*   Mahasiswa Rekayasa Kecerdasan Artificial
*   Institut Teknologi Sepuluh Nopember
*   Alif As'ad Ramadhan      : 5054231007
*   Danial Rajiv Syahidan    : 5054231004
*   Gandrung Ghafar H.A.     : 5054231008
*   Jeremiah Alexander Kevin : 5054231028
*   M. Naufal Arifin         : 5054231006

---
*Terima kasih telah meninjau proyek ini!*
