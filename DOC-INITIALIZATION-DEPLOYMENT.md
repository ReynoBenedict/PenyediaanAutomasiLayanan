# Dokumentasi Percobaan Deployment Aplikasi di Kubernetes

**Referensi:**

- [README.md - Kubernetes Installation](https://github.com/Widhi-yahya/kubernetes_installation_docker/blob/master/README.md)

- [DEPLOYMENT.md - Web App Deployment](https://github.com/Widhi-yahya/kubernetes_installation_docker/blob/master/DEPLOYMENT.md)

---

## 1. Konfigurasi Kubernetes Dashboard

Langkah pertama yang dilakukan adalah menerapkan konfigurasi untuk Kubernetes Dashboard, mengekspos layanan tersebut menggunakan tipe `NodePort`, dan membuat token otentikasi agar dashboard dapat diakses dengan hak akses admin.

![Kubernetes Configuration](screenshots/Picture1.jpg)

## 2. Deployment Database (MySQL)

Langkah berikutnya adalah memastikan ketersediaan layanan _backend_ dengan melakukan deployment database MySQL. Kita perlu menunggu hingga kondisi pod MySQL sepenuhnya `Ready` sebelum mengaktifkan layanan web.

![Deployment Database](screenshots/Picture2.png)

## 3. Apply Web Application Configurations (Login App)

Setelah database siap, dilanjutkan dengan mengaplikasikan manifest untuk aplikasi web.

Pertama, mengaplikasikan konfigurasi deployment aplikasi:
![Apply Web Application Configurations (1)](screenshots/Picture3.png)

Kedua, mengaplikasikan konfigurasi service agar aplikasi web dapat diakses:
![Apply Web Application Configurations (2)](screenshots/Picture4.png)

Ketiga, memverifikasi status pod untuk memastikan _login-app_ sudah berjalan di dalam cluster. Pada tahap ini, terdapat 2 replika pod yang sedang berjalan.
![Apply Web Application Configurations (3)](screenshots/Picture5.png)

## 4. Uji Coba Akses Aplikasi (Browser)

Mengakses halaman antarmuka aplikasi melalui browser web pada port `30080` (NodePort). Koneksi dilakukan dengan bantuan akses jaringan kampus (eduVPN UB) untuk menjangkau IP Node server. Halaman pertama yang diuji adalah halaman **Login**.

![Testing app access](screenshots/Picture6.png)

Selanjutnya, menguji fungsionalitas aplikasi dengan mencoba mendaftarkan pengguna baru pada halaman **Register** (menggunakan kredensial _admin_).

![Testing register functionality](screenshots/Picture7.png)

## 5. Verifikasi Integritas Database

Untuk memastikan sistem terhubung dengan benar, dilakukan verifikasi langsung ke dalam pod MySQL menggunakan perintah `kubectl exec`. Pemeriksaan pada tabel `users` membuktikan bahwa data registrasi _admin_ berhasil tersimpan di database.

![Database Integrity Verification](screenshots/Picture8.png)

## 6. Scaling Deployment Aplikasi

Untuk menguji skalabilitas cluster, dilakukan proses _scaling up_ pada deployment `login-app` sehingga jumlah replika bertambah menjadi 3 pod (`--replicas=3`).

![Scaling Deployment](screenshots/Picture9.png)

## 7. Hasil Akhir & Image Upload Dashboard

Verifikasi akhir menunjukkan pengguna berhasil masuk (login) dan diarahkan ke halaman **Image Upload Dashboard**. Bersamaan dengan itu, pemantauan melalui terminal mengonfirmasi bahwa ketiga replika pod _login-app_ kini berjalan dengan stabil, beserta informasi IP dan Port dari masing-masing service yang aktif.

![User already login](screenshots/Picture10.png)

Dokumentasi_Deployment_K8s.md
Menampilkan Dokumentasi_Deployment_K8s.md.
