# PA-PC_202231036_MUHAMMAD-RAFI_A

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt
```
Codingan tersebut mengimpor pustaka yang diperlukan untuk pemrosesan gambar dan visualisasi: cv2 dari OpenCV untuk pemrosesan gambar, numpy sebagai np untuk komputasi numerik dan manipulasi array, serta pyplot dari Matplotlib sebagai plt untuk membuat visualisasi data.

```python
img = cv2.imread('rafi.jpeg')
```
Codingan tersebut untuk membaca image yang user inginkan dengan nama image nya rafi.jpeg

```python
img.shape
[baris, kolom] = img.shape[:2]
```
Codingan img.shape mengambil dimensi gambar dalam bentuk (height = 1600, width = 1200, channels = 3), dan [baris, kolom] = img.shape[:2] mengekstrak jumlah baris (height) dan kolom (width), menyimpannya ke dalam variabel baris dan kolom.

```python
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
Codingan ini mengonversi gambar img dari format warna BGR (Blue, Green, Red) yang digunakan oleh OpenCV ke format warna RGB (Red, Green, Blue) yang lebih umum digunakan dalam visualisasi gambar.

```python
img_median = img.copy()
img_median_after = cv2.medianBlur(img_median, 11)

fig, axis = plt.subplots(1, 2, figsize = (15, 15))
ax = axis.ravel()

ax[0].imshow(img, cmap='gray')
ax[0].set_title('Original Citra')

ax[1].imshow(img_median_after, cmap='gray')
ax[1].set_title('After Citra Filter Median')
plt.show()
```
img_median = img.copy(): Membuat salinan dari gambar img dan menyimpannya dalam variabel img_median. Hal ini dilakukan untuk memastikan bahwa gambar asli tidak diubah. img_median_after = cv2.medianBlur(img_median, 11): Menerapkan filter median dengan ukuran kernel 11x11 pada img_median dan menyimpan hasilnya dalam variabel img_median_after. Filter median berguna untuk mengurangi noise dalam gambar. setelah itu fig, axis = plt.subplots(1, 2, figsize = (15, 15)): Membuat subplots dengan 1 baris dan 2 kolom untuk menampilkan dua gambar berdampingan, dengan ukuran figur 15x15 inci. ax = axis.ravel(): Mengubah array axis menjadi array satu dimensi untuk memudahkan akses ke subplot. ax[0].imshow(img, cmap='gray'): Menampilkan gambar asli img pada subplot pertama dengan colormap gray. ax[0].set_title('Original Citra'): Menetapkan judul "Original Citra" untuk subplot pertama. ax[1].imshow(img_median_after, cmap='gray'): Menampilkan gambar yang telah difilter median img_median_after pada subplot kedua dengan colormap gray. ax[1].set_title('After Citra Filter Median'): Menetapkan judul "After Citra Filter Median" untuk subplot kedua. plt.show(): Menampilkan semua plot yang telah didefinisikan. intinya Codingan ini menunjukkan perbandingan antara gambar asli dan gambar setelah diterapkan filter median.

```python
img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```
Codingan img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY) mengonversi gambar img dari format warna BGR (Blue, Green, Red) ke format grayscale (abu-abu), di mana setiap piksel hanya memiliki satu nilai intensitas cahaya, sehingga menghilangkan informasi warna dan menyimpan hasilnya dalam variabel img_gray.

```python
plt.imshow(img_gray, cmap='gray')
```
Codingan ini menampilkan gambar img_gray dalam format grayscale menggunakan Matplotlib. Parameter cmap=gray memastikan bahwa gambar ditampilkan dalam skala abu-abu.

```python
copyCitra1 = img_gray.copy().astype(float)

m1, n1 = copyCitra1.shape
output1 = np.empty([m1, n1])

print("shape copy citra 1 : ", copyCitra1.shape)
print("shape output citra 1 : ", output1.shape)

print("m1 : ", m1)
print("n1 : ", n1)
print()
```
Codingan copyCitra1 = img_gray.copy().astype(float): Membuat salinan dari gambar grayscale img_gray dan mengonversinya menjadi tipe data float. Operasi .copy() digunakan untuk memastikan bahwa kita membuat salinan yang independen dari img_gray, dan .astype(float) mengubah tipe data piksel menjadi float untuk persiapan operasi matematis selanjutnya. m1, n1 = copyCitra1.shape: Mengambil dimensi dari copyCitra1, yaitu jumlah baris disimpan di m1 dan jumlah kolom disimpan di n1. output1 = np.empty([m1, n1]): Membuat array kosong output1 dengan ukuran yang sama dengan copyCitra1. Array ini akan digunakan untuk menyimpan hasil operasi yang akan dilakukan pada copyCitra1. Print statements (print("shape copy citra 1 : ", copyCitra1.shape), print("shape output citra 1 : ", output1.shape), print("m1 : ", m1), print("n1 : ", n1)) digunakan untuk mencetak dimensi copyCitra1, output1, m1, dan n1 ke dalam output konsol. Secara Keseluruhan nya codingan ini menginisialisasi salinan gambar grayscale dalam tipe data float, membuat array kosong untuk menyimpan hasil operasi, dan mencetak informasi mengenai dimensi dan bentuk dari gambar serta array yang telah dibuat. dengan shape copy citra 1 (1600, 1200), shape output citra 1 (1600, 1200) dan m1 1600, n1 1200

```python
for baris in range (0, m1-1) :
    for kolom in range (0, n1-1) :
        a1 = baris
        b1 = kolom
        jumlah = copyCitra1[a1-1, b1-1] + copyCitra1[a1-1, b1] + copyCitra1[a1-1, b1+1] +\
            copyCitra1[a1, b1-1] + copyCitra1[a1, b1] + copyCitra1[a1, b1+1] +\
            copyCitra1[a1+1, b1-1] + copyCitra1[a1+1, b1] + copyCitra1[a1+1, b1+1]
        output1[a1, b1] = 1/9 * jumlah
```
Codingan for baris in range(0, m1-1):: Melakukan iterasi untuk setiap baris dalam rentang 0 sampai m1-1 (baris terakhir tidak termasuk). m1 adalah jumlah baris dalam gambar copyCitra1. for kolom in range(0, n1-1):: Di dalam setiap iterasi baris, melakukan iterasi untuk setiap kolom dalam rentang 0 sampai n1-1 (kolom terakhir tidak termasuk). n1 adalah jumlah kolom dalam gambar copyCitra1. a1 = baris dan b1 = kolom: Menyimpan nilai indeks baris dan kolom saat ini ke dalam variabel a1 dan b1. jumlah = copyCitra1[a1-1, b1-1] + ... + copyCitra1[a1+1, b1+1]: Menghitung jumlah nilai piksel di sekitar piksel saat ini (a1, b1) menggunakan jendela 3x3. Ini termasuk nilai piksel di sekeliling piksel saat ini (atas-kiri, atas, atas-kanan, kiri, tengah, kanan, bawah-kiri, bawah, bawah-kanan). output1[a1, b1] = 1/9 * jumlah: Menghitung nilai rata-rata dari total nilai piksel di sekitar piksel saat ini (9 nilai total) dan menyimpannya di lokasi yang sesuai dalam array output1. Ini menerapkan operasi mean filtering untuk menghasilkan gambar yang lebih halus.

```python
fig, axis = plt.subplots(1, 2, figsize = (10, 10))
ax = axis.ravel()

ax[0].imshow(img_gray, cmap='gray')
ax[0].set_title('Original Image')

ax[1].imshow(output1, cmap='gray')
ax[1].set_title('Mean Filtered Image')
plt.show()
```
Codingan ini menggunakan Matplotlib untuk menampilkan dua gambar berdampingan: gambar asli dalam format grayscale (img_gray) dan gambar yang telah mengalami proses mean filtering (output1), dengan masing - masing ukuran (10,10.  

# Teori Mendukung
1. Filtering Median
Filtering median adalah salah satu teknik yang paling umum digunakan dalam pengolahan citra untuk mengurangi noise atau gangguan yang ada dalam gambar. Noise dapat berasal dari berbagai sumber, seperti sensor kamera yang kurang sensitif atau kondisi pencahayaan yang tidak ideal. Teknik ini bertujuan untuk menghaluskan gambar tanpa mengorbankan detail yang penting. Prosesnya melibatkan pengambilan nilai median dari nilai-nilai piksel di sekitar piksel yang sedang diproses, dengan menggunakan jendela atau kernel berukuran tertentu. Median dipilih karena lebih tahan terhadap outlier daripada mean (rata-rata), sehingga cocok untuk mengurangi jenis noise yang disebut salt-and-pepper noise, di mana ada piksel yang secara acak menjadi sangat terang atau sangat gelap.
2. Filtering Rata-Rata (Mean Filtering)
Mean filtering, atau yang dikenal juga sebagai smoothing filter, adalah teknik lain dalam pengolahan citra yang digunakan untuk mengurangi noise dan halus. Teknik ini bekerja dengan mengganti nilai piksel dengan nilai rata-rata dari nilai-nilai piksel di sekitarnya, menggunakan jendela atau kernel yang sama seperti pada filtering median. Meskipun efektif dalam mengurangi noise berfrekuensi rendah, mean filtering cenderung memperhalus tepi dan detail halus dalam gambar, yang bisa menjadi kelemahan jika detail tersebut penting untuk analisis lebih lanjut.
3. Library
-OpenCV (cv2)
OpenCV (Open Source Computer Vision Library) adalah sebuah library open-source yang menyediakan berbagai fungsi untuk pengolahan citra dan visi komputer. Beberapa fungsi utama dari OpenCV yang digunakan dalam codingan ini adalah:
cv2.imread('rafi.jpeg'): Fungsi ini digunakan untuk membaca sebuah gambar dari file dengan nama 'rafi.jpeg' dan menyimpannya dalam bentuk array Numpy yang dapat diolah lebih lanjut.
cv2.cvtColor(img, cv2.COLOR_BGR2RGB): Fungsi ini digunakan untuk mengubah format warna gambar dari BGR (Blue, Green, Red) yang digunakan oleh OpenCV menjadi RGB (Red, Green, Blue) yang lebih umum digunakan untuk tampilan dan visualisasi.
cv2.medianBlur(img_median, 11): Fungsi ini menerapkan filter median ke gambar img_median dengan kernel berukuran 11x11. Filter median digunakan untuk mengurangi noise dalam gambar dengan cara menggantikan nilai piksel dengan nilai median dari nilai-nilai piksel di sekitarnya.
cv2.cvtColor(img, cv2.COLOR_BGR2GRAY): Fungsi ini mengonversi gambar img dari format warna BGR ke format grayscale (abu-abu), di mana setiap piksel hanya memiliki satu nilai intensitas cahaya.
-NumPy('numpy')
NumPy adalah library fundamental untuk komputasi numerik dalam Python. Beberapa fungsi NumPy yang relevan dalam kode Anda adalah:
np.empty([m1, n1]): Fungsi ini digunakan untuk membuat array Numpy kosong dengan dimensi [m1, n1], yang nantinya akan digunakan untuk menyimpan hasil operasi dalam pemrosesan gambar.
astype(float): Metode ini digunakan pada array Numpy (copyCitra1.astype(float)) untuk mengubah tipe data dari integer ke float. Ini berguna untuk mempersiapkan gambar dalam format yang tepat untuk operasi matematis yang memerlukan presisi floating-point.
-Matplotlib (matplotlib.pyplot as plt)
Matplotlib adalah library untuk visualisasi data dalam Python. Beberapa fungsi utama yang digunakan dalam codingan ini untuk menampilkan gambar adalah:
plt.subplots(1, 2, figsize=(15, 15)): Fungsi ini digunakan untuk membuat sebuah figur yang terdiri dari 1 baris dan 2 kolom subplot dengan ukuran figur 15x15 inci.
ax.imshow(img, cmap='gray'): Metode ini digunakan untuk menampilkan gambar img dalam subplot dengan colormap 'gray', yang menghasilkan tampilan gambar dalam skala abu-abu.
ax.set_title('Original Image'): Metode ini digunakan untuk menetapkan judul 'Original Image' pada subplot yang sesuai.

Jurnal:
https://jurnal.umk.ac.id/index.php/simet/article/viewFile/3283/1874
https://www.bing.com/search?pglt=41&q=jurnal+fitering+median+dan+filtering+rata-rata&cvid=23c71eaee11640c986678759bc65fbd0&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIICAEQ6QcY_FXSAQkzMzg2MWowajGoAgCwAgA&FORM=ANNAB1&PC=ASTS
