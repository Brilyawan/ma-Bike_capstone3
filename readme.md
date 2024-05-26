# <h1 style='text-align:left; color: yellow'><b>Capstone Project Module 3 - Ma-Bike: Pendekatan Prediktif untuk Menyeimbangkan Sistem Penyewaan Sepeda</b></h1>
**Created by: Kristian Brilyawan**

<p align="center">
  <img src="./docs/header.png" alt="Header" width="800" height="400">
</p>

## Context

Dalam beberapa dekade terakhir, kepadatan lalu lintas dan isu lingkungan di area perkotaan telah mendorong pencarian alternatif transportasi ramah lingkungan. Sistem penyewaan sepeda muncul sebagai solusi menjanjikan karena mampu mengurangi emisi gas buang dan meningkatkan kesehatan fisik pengguna. Sistem ini memungkinkan pengguna menyewa sepeda dari stasiun otomatis untuk perjalanan jarak pendek dan mengembalikannya di stasiun lain.

Saat ini, lebih dari 500 program penyewaan sepeda beroperasi di seluruh dunia, menyediakan lebih dari 500.000 sepeda. Inovasi ini mengotomatisasi proses pendaftaran, penyewaan, dan pengembalian sepeda, sehingga mempermudah akses pengguna.

Meskipun menawarkan banyak manfaat, seperti pengurangan emisi karbon, kemacetan lalu lintas, dan biaya transportasi, operator sistem ini menghadapi tantangan dalam memprediksi permintaan secara akurat. Ketidakakuratan prediksi menyebabkan distribusi sepeda yang tidak merata, meningkatkan biaya pemeliharaan, dan mengurangi kepuasan pelanggan.

Selain manfaat langsung bagi masyarakat, data yang dihasilkan dari sistem penyewaan sepeda juga memiliki nilai penelitian yang tinggi. Data ini mencatat durasi perjalanan, posisi keberangkatan, dan kedatangan secara rinci, menjadikan sistem penyewaan sepeda sebagai jaringan sensor virtual untuk memantau mobilitas perkotaan.

## Problem Statement

Penyedia penyewaan sepeda menghadapi kesulitan dalam memprediksi permintaan dengan akurat, mengakibatkan distribusi sepeda yang tidak merata. Hal ini menyebabkan peningkatan biaya operasional dan pemeliharaan, serta mengurangi kepuasan pelanggan karena sering kali tidak menemukan sepeda yang tersedia. Kekurangan sepeda di area dengan permintaan tinggi juga menyebabkan kehilangan pendapatan potensial karena pelanggan beralih ke moda transportasi lain.

Mengatasi masalah ini penting untuk mengoptimalkan distribusi sepeda, mengurangi biaya operasional, meningkatkan kepuasan pelanggan, dan memaksimalkan pendapatan. Untuk menangani masalah tersebut, dua pertanyaan inti yang perlu dijawab adalah:

- Bagaimana kita dapat memprediksi permintaan penyewaan sepeda di berbagai lokasi dan waktu dengan akurasi tinggi, dengan mempertimbangkan variabel-variabel seperti cuaca, waktu, peristiwa khusus, dan tren historis?

## Goals

Berdasarkan permasalahan di atas, tujuan utamanya adalah untuk membangun model prediktif yang mampu memprediksi kuantitas permintaan sewa dengan mempertimbangkan faktor-faktor yang ada dengan kesalahan sekecil mungkin. Berikut adalah target yang spesifik dan terukur:

- Mengembangkan model prediktif yang dapat memprediksi jumlah penyewaan sepeda dengan tingkat akurasi 90%.
- Menggunakan prediksi ini untuk mengoptimalkan distribusi sepeda secara efektif, memastikan ketersediaan sepeda yang memadai di semua lokasi tanpa kelebihan atau kekurangan yang signifikan.

## Analytic Approach

Pendekatan analitis yang diusulkan menggunakan metode supervised machine learning, dengan model regresi. Model ini akan dilatih dengan data historis untuk menghasilkan prediksi yang lebih akurat. Solusi ini dirancang untuk menjadi alat bantu penting dalam operasional harian dan perencanaan strategis sistem penyewaan sepeda, menyediakan data yang diperlukan untuk pengambilan keputusan yang tepat dan responsif terhadap dinamika permintaan sepeda urban.

## Metric Evaluation

Miss-prediction terjadi ketika model gagal memprediksi jumlah penyewaan sepeda dengan akurat. Hal ini bisa bermanifestasi sebagai over-prediction, di mana model memprediksi permintaan yang lebih tinggi dari yang sebenarnya, atau under-prediction, di mana model memprediksi permintaan yang lebih rendah dari yang sebenarnya.

| Metric | Penjelasan |
|--------|-------------|
| **MAE (Mean Absolute Error)** | MAE mengukur rata-rata dari nilai absolut kesalahan antara prediksi dan nilai sebenarnya. Ini memberikan pemahaman langsung tentang kesalahan rata-rata yang diharapkan dalam prediksi jumlah sepeda. MAE sangat berguna untuk menilai dampak rata-rata dari miss-predictions dan membantu dalam optimasi persediaan karena tidak memberikan hukuman berlebihan untuk outlier. |
| **MAPE (Mean Absolute Percentage Error)** | MAPE sangat berguna karena mengukur kesalahan sebagai persentase dari nilai sebenarnya, yang sangat relevan dalam kasus di mana fluktuasi permintaan memiliki skala yang luas sepanjang tahun (berdasarkan musim atau kondisi cuaca). Ini memberikan perspektif tentang seberapa besar kesalahan prediksi relatif terhadap jumlah sepeda yang sebenarnya disewakan. |
| **R² (Coefficient of Determination)** | R² bisa menunjukkan seberapa baik model dapat menjelaskan variabilitas permintaan sepeda. Nilai yang tinggi menunjukkan bahwa model dengan akurat menjelaskan perubahan dalam jumlah penyewaan sepeda dan berpotensi dapat dipercaya dalam setting operasional untuk prediksi permintaan. |

## Asumsi

Asumsi yang digunakan dalam pengembangan model ini termasuk:

- Permintaan penyewaan sepeda dipengaruhi oleh variabel seperti cuaca, hari dalam minggu, dan musim, yang semua tersedia dalam data.
- Data historis yang digunakan untuk pelatihan model cukup bersih dan representatif untuk kondisi operasional saat ini dan masa depan.
- Hubungan antara faktor-faktor tersebut dan permintaan penyewaan dipercaya cukup konsisten sepanjang waktu untuk membenarkan penggunaan model prediktif.

## Proses Pemodelan

- Berdasarkan dua eksperimen yang dilakukan (tanpa transformasi target dan dengan transformasi target), empat model terbaik dipilih untuk tuning, yaitu Catboost Regressor, XGBoost Regressor, Support Vector Regressor, dan Random Forest Regressor.
- Catboost Regressor tetap menjadi model terbaik setelah tuning dan digunakan sebagai model akhir. Dengan parameter tuning terbaik yaitu 'iterations': 1800, 'learning_rate': 0.07, 'depth': 8, diperoleh hasil kinerja rata-rata dengan MAE: 34.03, R2: 90.07%, dan MAPE: 28.55%.
- Saat memprediksi data pengujian (df_unseen), hasil kinerja menjadi lebih baik dengan MAE: 30.54, R2: 92.26%, dan MAPE: 26.89%. Ini menunjukkan bahwa model akhir andal untuk memprediksi data yang belum terlihat atau data serupa lainnya.

## Keterbatasan Model

1. **Ketersediaan Data**:
   - Proyek ini terbatas pada data yang sudah tersedia yang mencakup tanggal, waktu, cuaca, dan jumlah penyewaan sepeda. Keterbatasan data seperti ketidaktersediaan informasi spesifik lokasi atau data perilaku pengguna dapat membatasi akurasi dan aplikabilitas model dalam memprediksi permintaan di lokasi spesifik atau untuk segmentasi pengguna tertentu.
2. **Kualitas Data**:
   - Data yang digunakan diharapkan bersih dan telah melalui proses pembersihan awal; namun, kemungkinan masih adanya noise atau outliers yang tidak terdeteksi. Hal ini dapat menyebabkan model prediktif mengalami bias atau overfitting, yang mengurangi kemampuan generalisasi model pada data baru atau dalam kondisi operasional yang berbeda.
3. **Kompleksitas Model**:
   - Model yang dipilih harus seimbang antara akurasi prediksi dan kompleksitas komputasi. Model yang terlalu kompleks mungkin memerlukan sumber daya komputasi yang signifikan, yang bisa tidak praktis untuk implementasi operasional real-time.
4. **Variabilitas Kondisi Eksternal**:
   - Model akan menggunakan data historis cuaca, namun perubahan iklim dan variabilitas cuaca tahunan mungkin tidak sepenuhnya terprediksi. Ini bisa mengakibatkan model kurang akurat dalam merespons kondisi cuaca yang tidak terduga atau perubahan pola cuaca jangka panjang.
5. **Kesalahan Prediksi pada Nilai Kecil**:
   - Model akhir masih memiliki kesalahan yang cukup besar berdasarkan MAPE sekitar 28%. Hal ini disebabkan oleh rentang prediksi yang luas dari 1 hingga 970, sehingga kesalahan prediksi pada nilai kecil cukup tinggi. Namun, model ini lebih akurat untuk memprediksi jumlah pelanggan yang besar.
6. **Rentang Nilai Kecil (0-50)**:
   - Kurang dapat diandalkan dengan MAPE sekitar 48.27%. Meskipun demikian, MAE dalam rentang ini adalah sekitar 7 poin, menunjukkan bahwa model kurang akurat untuk permintaan kecil tetapi lebih dapat diandalkan untuk permintaan yang lebih besar.
7. **Rentang Nilai 51-100**:
   - Memiliki MAPE yang cukup tinggi sekitar 33.19%, meskipun lebih rendah dibandingkan rentang nilai kecil. Model ini menunjukkan kinerja yang lebih baik pada rentang ini namun masih memerlukan perbaikan.
8. **Rentang Nilai yang Lebih Besar (101-200 dan di atasnya)**:
   - Menunjukkan bahwa model lebih akurat dengan MAPE yang lebih rendah dan MAE yang lebih kecil. Misalnya, pada rentang 101-200, MAPE sekitar 24.68% dan MAE sekitar 36 poin, dengan biaya overpredict dan underpredict lebih terkontrol.
9. **Pengguna Kasual (Casual)**:
   - Model ini kurang dapat diandalkan untuk memprediksi pengguna kasual karena MAPE yang cukup besar yaitu 45.90%, meskipun memiliki MAE yang relatif kecil, yaitu sekitar 8. Sebaliknya, untuk memprediksi pengguna terdaftar (registered), model cukup andal dengan MAPE sekitar 29.43% dan MAE sekitar 26.

## Dampak Bisnis

- Dengan prediksi permintaan yang akurat, perusahaan dapat mengoptimalkan alokasi sumber daya seperti sepeda pada waktu dan kondisi yang tepat, mencegah ketidakseimbangan antara ketersediaan sepeda dan permintaan pengguna yang dapat menyebabkan implikasi finansial.
- Misalnya, jika perusahaan biasanya menyiapkan alokasi sepeda yang sama setiap hari dalam berbagai kondisi, hal ini dapat menyebabkan kerugian karena permintaan lebih rendah dari alokasi yang disediakan (overprediction), mengakibatkan biaya operasional yang lebih besar daripada keuntungan yang diperoleh, atau hilangnya potensi keuntungan karena permintaan lebih tinggi dari yang diprediksi (underprediction) akibat kondisi tertentu, yang mengakibatkan hilangnya potensi pendapatan.
- Informasi dari prediksi permintaan dapat digunakan untuk merancang kampanye pemasaran yang lebih terarah. Perusahaan dapat menargetkan promosi atau penawaran khusus pada kondisi atau periode tertentu, misalnya dengan mempertimbangkan jam sebagai acuan strategi karena jam merupakan fitur yang paling berpengaruh pada prediksi penyewaan.

## Rekomendasi

1. **Fine-Tuning untuk Rentang Permintaan Rendah (1-50) dan Tinggi (>600)**:
   - Lakukan fine-tuning model secara khusus untuk rentang permintaan rendah (1-50) dan sangat tinggi (>600). Ini dapat melibatkan rekayasa fitur tambahan, penyesuaian hyperparameter, atau penggunaan pendekatan pemodelan yang lebih sensitif terhadap variasi kecil.
2. **Penyesuaian Metrik Evaluasi**:
   - Tinjau metrik evaluasi model dan pastikan metrik yang digunakan sesuai dengan tujuan bisnis dan karakteristik permintaan sepeda. Gunakan MAPE (Mean Absolute Percentage Error) untuk memprediksi rentang nilai yang besar (lebih dari 100) dan MAE (Mean Absolute Error) untuk memprediksi rentang nilai kecil (1-50). Ini akan memberikan gambaran yang lebih jelas tentang kinerja model pada berbagai skala permintaan.
3. **Analisis Mendalam terhadap Prediksi**:
   - Lakukan analisis mendalam untuk memahami penyebab perkiraan yang terlalu rendah atau terlalu tinggi. Identifikasi faktor eksternal yang tidak dimasukkan dalam model, perubahan perilaku pengguna, atau perubahan kebijakan yang dapat mempengaruhi pola permintaan. Analisis pola musiman atau tren yang mungkin mempengaruhi permintaan sepeda.
4. **Penambahan Fitur yang Relevan**:
   - Tambahkan fitur yang lebih berkorelasi terhadap target, seperti lokasi stasiun sepeda, jarak stasiun sepeda dengan perkantoran, sekolah, ruang publik, dan data acara lokal. Fitur-fitur ini dapat membantu model untuk lebih memahami faktor-faktor yang mempengaruhi permintaan sepeda dan meningkatkan akurasi prediksi.
5. **Perluasan Dataset**:
   - Dataset yang digunakan saat ini hanya mencakup rentang 2 tahun (2011 dan 2012). Memperluas dataset dengan menambahkan data dari tahun-tahun berikutnya akan memberikan lebih banyak informasi kepada model, membantu menangkap tren jangka panjang dan variasi musiman yang dapat meningkatkan akurasi prediksi.
6. **Pengembangan Model Tambahan**:
   - Model yang sudah dibuat ini dapat digunakan sebagai dasar untuk mengembangkan model lain, seperti model yang memprediksi total unit sepeda yang disewa pada lokasi tertentu. Informasi ini dapat digunakan untuk analisa lebih lanjut dalam perencanaan penambahan stasiun sepeda di lokasi-lokasi strategis.
7. **Optimasi Alokasi Sumber Daya**:
   - Gunakan hasil prediksi untuk mengoptimalkan alokasi sumber daya, seperti jumlah sepeda yang ditempatkan di berbagai stasiun. Ini akan membantu mengurangi biaya operasional dengan memastikan bahwa jumlah sepeda yang disediakan sesuai dengan permintaan.
8. **Pemantauan dan Pembaruan Model Secara Berkala**:
   - Lakukan pemantauan kinerja model secara berkala dan perbarui model sesuai dengan perubahan data atau pola permintaan. Ini memastikan bahwa model tetap relevan dan akurat dalam kondisi yang berubah.

Dengan menerapkan rekomendasi ini, perusahaan dapat lebih efektif dalam mengelola operasi sepeda dan meningkatkan pengalaman pengguna, sambil meminimalkan biaya operasional dan memaksimalkan keuntungan.