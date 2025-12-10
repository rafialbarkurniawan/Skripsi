Deskripsi Singkat Tiap Komponen
1. Data Mentah

Berisi hasil scraping ulasan Google Play Store dengan kolom:

user name

date

rating

content (dipakai sebagai sumber utama pemodelan topik)

2. Preprocessing (preprocessing/)

Tahapan pembersihan data mengikuti pipeline penelitian:

case folding

pembersihan teks menggunakan regex

normalisasi kata berbasis kamus

tokenisasi

stopword removal

stemming

filtering dokumen kosong

menyimpan hasil preprocessing

Output utama:

hasil_preprocessing.csv

3. Model IndoBERT Lokal (model/)

Folder opsional untuk menjalankan pipeline tanpa koneksi internet.

Jika tidak tersedia, model otomatis diunduh dari HuggingFace.

4. Embedding Cache (emb_cache/)

Pipeline menyimpan file embedding IndoBERT agar perhitungan tidak perlu diulang.

Format file:

embeddings_18377.npy

5. Pipeline Pemodelan (pipeline/)
a. Process_full.ipynb (Pipeline Utama)

Mencakup langkah:

load data hasil preprocessing

generate embedding IndoBERT

reduksi dimensi UMAP

clustering HDBSCAN

pemodelan topik dengan BERTopic

menghitung koherensi (c_v)

menghasilkan c-TF-IDF

visualisasi (wordcloud, barchart, intertopic map)

ekspor CSV hasil pemodelan

Pipeline ini menghasilkan 38 topik dengan mean coherence ~0.665 dan outlier ~68%.

b. bertopic_indobert_honkai_dummy.ipynb

Eksperimen dataset dummy 5%, 10%, 25% untuk mempelajari pengaruh ukuran dataset
c. tuning_experiments.ipynb

Eksperimen parameter UMAP–HDBSCAN

Diputuskan menggunakan baseline karena memberikan:

topik stabil,

struktur semantik jelas,

koherensi paling tinggi.

Folder Hasil (hasil/)

Folder ini memuat seluruh keluaran pipeline:

1. CSV Hasil Pemodelan

topic_info.csv → ringkasan topik (jumlah dokumen, label otomatis)

representasi_ctfidf.csv → bobot kata tiap topik

docs_with_topic.csv → dokumen + prediksi topik

topic_assignments.csv → label topik final

evaluasi_per_topik_c_v.csv → skor koherensi tiap topik

2. Visualisasi

intertopic_map.html

barchart_topics.html

wordcloud_global.png

Semua visualisasi bebas dibuka menggunakan browser atau aplikasi gambar.

Cara Menjalankan Pipeline
1. Install dependensi
Jalankan pipeline installer.ipynb atau copy paste baris kode installer dan jalankan di terminal


Atau secara manual:

pip install bertopic sentence-transformers hdbscan umap-learn gensim wordcloud
pip install plotly kaleido   # opsional untuk ekspor PNG

2. Jalankan preprocessing dan pemodelan topik
jupyter notebook pipeline/Process_full.ipynb

🔍 Reproduksibilitas Penelitian

Repositori ini mencakup:

seluruh kode yang digunakan,

dataset hasil preprocessing,

parameter eksak untuk setiap model,

output pemodelan lengkap,

dan visualisasi interaktif.

Seluruh proses dapat direplikasi ulang 100% tanpa modifikasi, sesuai dengan prinsip transparansi penelitian ilmiah.
