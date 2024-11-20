# STM32 FreeRTOS LED Control with Shared Data Simulation  
Proyek ini mendemonstrasikan penggunaan FreeRTOS pada mikrokontroler STM32 untuk mengontrol beberapa LED menggunakan task dan mensimulasikan akses data bersama.  
## Features  
- **Task-based LED Control**  
  - Green LED berkedip dengan delay 500 ms.  
  - Red LED berkedip dengan delay 100 ms.  
- **Shared Data Access Simulation**  
  - Task berbagi flag(`startFlag`) untuk mensimulasikan sumber daya bersama.  
  - Jika terjadi konflik(akses bersamaan), Blue LED menyala sebagai indikator interferensi.  
- **FreeRTOS Integration**  
  - Menunjukan penggunaan multithreading dan penjadwalan task berbasis prioritas.  
## Components Used  
- **Hardware**  
  - STM32 Microcontroller (dikonfigurasi dengan sumber clock HSI).  
  - Tiga LEDs terhubung ke pin GPIO :  
    - Green LED: `GPIO_PIN_0`.  
    - Red LED: `GPIO_PIN_1`.  
    - Blue LED: `GPIO_PIN_2`.  
- **Software**  
  - STM32CubeIDE untuk pengembangan dan debugging.  
  - FreeRTOS untuk pengelolaan task real-time.  
## How It Works  
1. **Task Descriptions**  
- GreenLEDTask: Mengontrol LED Hijau, menyala-mati setiap 500 ms.
- RedLEDTask: Mengontrol LED Merah, menyala-mati setiap 100 ms.
- Kedua task memanggil accessSharedData() untuk mensimulasikan akses sumber daya bersama..  
2. **Shared Data Handling**  
- Variabel global startFlag digunakan untuk melacak akses data.
- Jika sebuah task mencoba mengakses data ketika task lain sedang menggunakannya, LED Biru akan 
  menyala untuk menunjukkan interferensi.  
## Usage
- Jalankan program pada papan STM32 Anda.
- Amati perilaku LED:
    - LED Hijau menyala-mati setiap 500 ms.
    - LED Merah menyala-mati setiap 100 ms.
    - LED Biru menyala jika terjadi konflik selama akses data bersama
## Noted 
- Program ini mendemonstrasikan multithreading dasar. Untuk aplikasi tingkat produksi, 
  implementasikan mekanisme sinkronisasi seperti mutex atau semaphore untuk mengelola sumber 
  daya bersama dengan aman.
- Konfigurasi clock diatur untuk sumber HSI. Sesuaikan jika diperlukan untuk perangkat keras 
  Anda.
## Demo
 

https://github.com/user-attachments/assets/162988e6-ae6e-4bca-9021-3e8d7a89e014


