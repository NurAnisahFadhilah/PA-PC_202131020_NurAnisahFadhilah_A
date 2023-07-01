   # PROJECT UAS

        NAMA    : Nur Anisah Fadhilah
        NIM     : 202131020
        KELAS   : Pengolahan Citra - A

Project Uas kali ini saya membuat Deteksi Bentuk Gambar Menggunakan Countur.


## Teori Deteksi Bentuk Gambar Menggunakan Contours

^ Pengertian :
Deteksi bentuk gambar menggunakan contours adalah suatu teknik dalam pengolahan citra yang melibatkan ekstraksi kontur dari gambar dan menganalisis properti kontur tersebut untuk mengenali dan membedakan bentuk-bentuk objek yang ada dalam gambar.

Berikut adalah langkah-langkah umum dalam deteksi bentuk menggunakan contours:

- Pra-pemrosesan: Lakukan pra-pemrosesan pada gambar untuk mempersiapkannya sebelum deteksi contours. Ini mungkin melibatkan operasi seperti pengubahan skala keabuan (grayscale), filtering (misalnya dengan menggunakan Gaussian blur), atau pengubahan ambang (thresholding) untuk memisahkan objek dari latar belakang.

- Temukan Kontur: Gunakan algoritma seperti Canny edge detection atau fungsi contours pada OpenCV untuk menemukan kontur-kontur dalam gambar. Kontur adalah garis yang membentuk batas objek dalam gambar.

- Filter Kontur: Terapkan kriteria filtrasi untuk membuang kontur yang tidak diinginkan. Misalnya, Anda dapat membatasi ukuran kontur atau menerapkan batasan lain berdasarkan properti kontur seperti keliling (perimeter) atau luas area.

- Analisis Kontur: Lakukan analisis lebih lanjut pada kontur yang terdeteksi untuk mengidentifikasi bentuk-bentuk tertentu. Anda dapat menggunakan metode geometri seperti perbandingan aspek (aspect ratio), lingkaran terkecil (smallest enclosing circle), atau pendekatan bentuk lainnya.

- Ekstraksi Informasi: Setelah mendeteksi bentuk-bentuk, Anda dapat melakukan ekstraksi informasi tambahan seperti koordinat pusat (centroid), orientasi, atau atribut lainnya yang mungkin berguna dalam analisis lebih lanjut.

- Visualisasi dan Tindak Lanjut: Terakhir, Anda dapat memvisualisasikan hasil deteksi bentuk dengan menggambar kotak batas (bounding box) atau menandai objek yang terdeteksi pada gambar asli. Selanjutnya, Anda dapat melakukan tindakan lanjut seperti pengenalan objek atau penghitungan jumlah objek tertentu dalam gambar.

^ Tujuan:
deteksi bentuk gambar menggunakan contours bertujuan untuk mengidentifikasi dan membedakan objek-objek dengan bentuk tertentu dalam sebuah gambar. Dengan menganalisis kontur-kontur yang terdeteksi, kita dapat melakukan pengenalan dan ekstraksi informasi tentang bentuk-bentuk yang ada dalam gambar.

Berikut adalah beberapa tujuan umum dari deteksi bentuk gambar menggunakan contours:
- Segmentasi objek: Deteksi contours dapat digunakan untuk memisahkan objek dari latar belakang atau objek lain dalam gambar.

- Pengenalan bentuk: Dengan menganalisis properti kontur seperti jumlah sisi, perbandingan sisi, atau bentuk keseluruhan, kita dapat mengenali dan membedakan bentuk-bentuk spesifik seperti lingkaran, persegi, segitiga, atau bentuk-bentuk kompleks lainnya dalam gambar.

- Pemrosesan lanjutan: Deteksi contours dapat menjadi langkah awal untuk melakukan pemrosesan lanjutan pada objek-objek yang terdeteksi. 

^ Kelebihan :
Deteksi bentuk gambar menggunakan contours memiliki beberapa kelebihan yang membuatnya menjadi pendekatan yang populer dalam pengolahan citra dan visi komputer. Beberapa kelebihan tersebut antara lain:

- Sederhana dan efisien: Deteksi contours adalah pendekatan yang relatif sederhana dan efisien dalam mengidentifikasi bentuk-bentuk objek dalam gambar. 

- Robust terhadap variasi: Metode deteksi contours dapat mengatasi variasi dalam bentuk, ukuran, rotasi, dan posisi objek dalam gambar. 

- Toleran terhadap noise: Deteksi contours memiliki sifat yang toleran terhadap noise atau gangguan dalam gambar. 

^ Kekurangan :
Deteksi bentuk gambar menggunakan contours juga memiliki beberapa kekurangan yang perlu dipertimbangkan. Berikut adalah beberapa kekurangan yang mungkin terjadi:

- Sensitif terhadap kondisi pencahayaan: Deteksi contours dapat menjadi sensitif terhadap kondisi pencahayaan yang berbeda-beda dalam gambar. 

- Pengaruh noise: Meskipun contours memiliki toleransi terhadap noise dalam gambar, namun noise yang signifikan atau gangguan yang kuat dapat mempengaruhi hasil deteksi. 

- Terbatas pada objek dengan batas yang jelas: Deteksi contours cenderung bekerja lebih baik pada objek-objek dengan batas yang jelas dan tajam. 

## Penjelasan dari Program

Import Library 

```bash
  import cv2 ## Import Library opencv
  from matplotlib import pyplot as plt ## import Library matplotlib.pyplot dengan nama plt
  import numpy as np ##Import Library numpy dengan nama np

```

Show Image

```bash
  img = cv2.imread('dila1.jpeg') ## Membaca gambar dila1.jpeg dengan variabel img

  img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB) ## Mengubah gambar img menjadi warna gray
 
  plt.imshow(img) ## Menampilkan gambar
  plt.show() ## Menampilkan gambar
```

Contour Detection

```bash
  gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY) ## Mengubah gambar menjadi warna gray  

  thresh = cv2.adaptiveThreshold(
    gray, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY_INV, 21, 5) ## Terapkan ambang batas (threshold) untuk membuat citra biner 

  contours, _ = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE) ## Mencari Kontur dalam citra biner 

  detected_contours = img.copy() ## digunakan untuk membuat salinan (copy) dari citra asli (img) ke variabel detected_contours

  cv2.drawContours(detected_contours, contours, -500, (0, 255, 0), -500) ## Untuk menggambar kontur pada salinan citra asli
  
  plt.imshow(detected_contours)
  plt.title('Image With Contours') ## Menampilkan Keterangan pada gambar
  plt.show() ## Menampilkan gambar
```

Extracting Contours

```bash
  contours, _ = cv2.findContours(
    thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE) ## untuk menemukan kontur dalam citra biner (thresh) menggunakan fungsi "cv2.findContours" dari pustaka OpenCV.

  highlight = np.ones_like(img) ## untuk membuat sebuah array numpy dengan dimensi yang sama seperti citra img, yang diisi dengan nilai 1.

  cv2.drawContours(highlight, contours, -500, (255, 255, 255), -255) ## untuk menggambar kontur pada citra yang disimpan dalam variabel highlight menggunakan fungsi "cv2.drawContours" dari pustaka OpenCV.
 
  plt.imshow(highlight)
  plt.title('Highlight contour with color') ## Menampilkan Keterangan pada gambar
  plt.show() ## Menampilkan gambar 
```


```bash
  contours = {"Original Image": img, "Image with contours": detected_contours,
            "Color contours": highlight} ## untuk membuat sebuah kamus (dictionary) dengan tiga entri yang berisi citra-citra yang relevan dalam proses deteksi kontur.

  plt.subplots_adjust(wspace=.2, hspace=.2) ## untuk mengatur jarak antara subplot dalam sebuah plot menggunakan pustaka Matplotlib.
  plt.tight_layout() ## untuk secara otomatis mengatur tata letak subplot dan elemen-elemen dalam plot menggunakan pustaka Matplotlib.

  for i, (key, value) in enumerate(contours.items()): ## untuk melakukan iterasi melalui item-item dalam kamus contours menggunakan fungsi enumerate().
    plt.subplot(2, 2, i + 1) ## untuk membuat subplot dalam plot menggunakan pustaka Matplotlib.
    plt.tick_params(labelbottom=False) ## untuk mengatur parameter sumbu x pada plot menggunakan pustaka Matplotlib.
    plt.tick_params(labelleft=False) ## untuk mengatur parameter sumbu y pada plot menggunakan pustaka Matplotlib.
    plt.title("{}".format(key)) ## untuk mengatur judul pada plot menggunakan pustaka Matplotlib.
    plt.imshow(value) ## untuk menampilkan citra pada subplot menggunakan pustaka Matplotlib.

  plt.show() ## Menampilkan gambar 

```
Saya mengucapkan terima kasih kepada Ibu Dr. Dra. Dwina Kuswardani, M.Kom. selaku Dosen Mata Kuliah Pengolahan Citra dan Abang/Kakak Asisten Lab yang telah memberikan Project uas ini sehingga dapat menambah pengetahuan dan wawasan sesuai bidang studi yang saya tekuni.