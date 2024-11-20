# Sistem Kontrol LED Multi-Thread dengan FreeRTOS

## Tentang Proyek
Repository ini mengimplementasikan RTOS pada STM32F103C8T6 dengan tiga task: defaultTask, greenLedTask, dan redLedTask untuk mengontrol LED. Menggunakan CMSIS-OS untuk manajemen task dan STM32 HAL untuk konfigurasi clock serta GPIO, program ini mengelola inisialisasi perangkat keras serta kontrol LED secara periodik melalui masing-masing task.

## Diagram Alur Kerja
<!-- Tambahkan diagram alur kerja jika diperlukan -->

## Struktur Task

### 1. Default Task
- **Prioritas:** Normal (`osPriorityNormal`)
- **Stack Size:** 128 bytes
- **Fungsi:** Task ini berjalan dalam loop kosong dengan delay minimal, berfungsi sebagai task idle untuk sistem.

### 2. Green LED Task (GreenLEDTask)
- **Prioritas:** Idle (`osPriorityIdle`)
- **Stack Size:** 128 bytes
- **Fungsi:** 
  - Mengontrol LED hijau dengan pola kedipan spesifik.
  - Menyalakan indikator task LED hijau.
  - Mengedipkan LED hijau setiap 0.5 detik.
  - Mengakses data bersama dan menunjukkan interferensi jika ada konflik akses dengan LED biru.

### 3. Red LED Task (RedLEDTask)
- **Prioritas:** Normal (`osPriorityNormal`)
- **Stack Size:** 128 bytes
- **Fungsi:** 
  - Mengontrol LED merah(pada video demo saya menggunakan led kuning) dengan pola kedipan yang lebih cepat.
  - Menyalakan indikator task LED merah.
  - Mengedipkan LED kuning setiap 0.1 detik.
  - Mengakses data bersama dan menunjukkan interferensi jika ada konflik akses dengan LED biru.

### Interaksi Antar Task
- Ketiga task berjalan secara independen tanpa saling mempengaruhi.
- `RedLEDTask` memiliki prioritas yang lebih tinggi dibandingkan task lainnya.
- Setiap task memiliki LED indikator terpisah untuk menunjukkan status aktif.
- `DefaultTask` berjalan di background sebagai idle task.

### Pengelolaan Data Bersama
Fungsi `accessSharedData` digunakan untuk mengelola akses ke data bersama antara task `GreenLEDTask` dan `RedLEDTask`. 

Jika `startFlag` bernilai `1`, task diperbolehkan mengakses data dan flag diubah menjadi `0`. Jika task lain mencoba mengakses data saat `startFlag` bernilai `0`, LED merah akan menyala sebagai indikasi adanya konflik akses (interferensi). Setelah akses selesai, `startFlag` diatur kembali menjadi `1` dan LED biru dimatikan.

## Konfigurasi Hardware
- Menggunakan GPIO Port A untuk semua LED.
- Konfigurasi pin sebagai output push-pull.
- Tidak menggunakan pull-up/pull-down resistor.
- Kecepatan clock diatur ke frekuensi rendah untuk efisiensi daya.

## Persyaratan Sistem
- **Hardware:** STM32 Microcontroller
- **Software:**
  - FreeRTOS
  - STM32CubeIDE atau lingkungan pengembangan serupa
  - HAL Driver STM32

## Cara Penggunaan
1. Clone repository ini.
2. Buka proyek menggunakan STM32CubeIDE.
3. Build proyek.
4. Flash ke board STM32.
5. LED akan mulai berkedip sesuai pola yang telah diprogram.

## Catatan Pengembangan
- Program menggunakan HSI (High Speed Internal) clock.
- Tidak menggunakan PLL untuk simplisitas.
- Menggunakan HAL library untuk abstraksi hardware.




https://github.com/user-attachments/assets/19ef2b5e-cb03-4c06-a7c4-ab76eca92209


