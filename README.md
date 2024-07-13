Project ini melibatkan pengolahan citra digital untuk mendeteksi tepi dan kontur dalam gambar. Teori-teori yang mendukung proyek ini termasuk teori pemrosesan citra digital, deteksi tepi, dan deteksi kontur. Berikut peteori yang mendasari setiap tahap dalam proyek ini:

1. Pemrosesan Citra Digital
Pemrosesan citra digital adalah disiplin ilmu yang mencakup analisis dan manipulasi gambar menggunakan komputer. Gambar digital diwakili oleh matriks pixel, di mana setiap pixel memiliki nilai intensitas tertentu. Dalam konteks proyek ini, kita memulai dengan memuat gambar digital menggunakan pustaka OpenCV dan mengubahnya menjadi citra grayscale.

2. Konversi ke Citra Grayscale
Konversi citra berwarna ke citra grayscale mengurangi kompleksitas data, karena hanya ada satu kanal intensitas yang perlu diproses dibandingkan dengan tiga kanal warna (RGB). Ini dilakukan dengan menggunakan fungsi `cv2.cvtColor()` dari OpenCV:
```python
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
3. Deteksi Tepi Canny
Deteksi tepi adalah proses mendeteksi perbedaan intensitas yang signifikan di antara pixel yang berdekatan, yang seringkali menandakan adanya batas objek. Algoritma Canny adalah salah satu metode deteksi tepi yang paling populer dan efektif. Algoritma ini melibatkan beberapa langkah:
   - **Penghalusan (Smoothing)**: Mengurangi noise dalam citra menggunakan Gaussian filter.
   - **Penghitungan Gradien**: Menggunakan operator Sobel untuk menghitung gradien intensitas.
   - **Non-maximum Suppression**: Menekan semua gradien yang tidak maksimal untuk mempertajam tepi.
   - **Double Thresholding**: Menggunakan dua nilai ambang batas (threshold) untuk mengklasifikasikan tepi.
   - **Edge Tracking by Hysteresis**: Menghubungkan tepi yang terdeteksi berdasarkan konektivitas.

Implementasi deteksi tepi Canny:
```python
canny_edges = cv2.Canny(gray_image, 100, 200)
```

4. Deteksi Kontur
Deteksi kontur adalah teknik untuk menemukan dan mengekstrak batas objek dalam citra. Kontur adalah kurva yang menghubungkan semua titik kontinu dengan intensitas yang sama. OpenCV menyediakan fungsi `cv2.findContours()` untuk mendeteksi kontur dalam citra biner hasil dari deteksi tepi:
```python
contours, _ = cv2.findContours(canny_edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
```
5. Visualisasi
Tahap akhir adalah visualisasi hasil dari proses-proses di atas. Menggunakan pustaka Matplotlib, kita menampilkan citra asli, citra hasil deteksi tepi, dan citra dengan kontur yang telah digambar:
```python
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.title('Original Image')
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.axis('on')

plt.subplot(1, 3, 2)
plt.title('Canny Edge Detection')
plt.imshow(canny_edges, cmap='gray')
plt.axis('on')

plt.subplot(1, 3, 3)
plt.title('Contours Detection')
plt.imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB))
plt.axis('on')

plt.show()
```
Kesimpulan
Dengan memahami teori-teori di atas, kita dapat mengaplikasikan teknik-teknik pemrosesan citra digital untuk mendeteksi tepi dan kontur dalam gambar, yang dapat digunakan dalam berbagai aplikasi seperti pengenalan objek, analisis citra medis, dan robotika.
