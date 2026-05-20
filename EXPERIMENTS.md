# Experiment Log

Catat setiap percobaan hyperparameter di sini. **Minimal 5 eksperimen.**

> Tips: ubah **satu hyperparameter pada satu waktu** agar bisa mengisolasi efeknya. Setelah memahami efek tiap variabel, baru gabungkan untuk hasil terbaik.

---

## 📋 Tabel Ringkasan

Isi tabel ini setelah selesai semua eksperimen.

| # | Hidden | Neurons | Activation | Optimizer | LR     | Batch | Epochs | Dropout | Test Acc | Train Time |
|---|--------|---------|------------|-----------|--------|-------|--------|---------|----------|------------|
| 0 | 1      | 64      | relu       | sgd       | 0.01   | 32    | 10     | 0.0     | ~85%     | ~30s       |
| 1 | 2      | 128     | relu       | adam      | 0.001  | 64    | 20     | 0.0     | 87%      | ~90s       |
| 2 | 2      | 128     | relu       | adam      | 0.001  | 64    | 20     | 0.3     | 88.12%   | ~90s       |
| 3 | 3      | 256     | relu       | adamax    | 0.001  | 128   | 25     | 0.2     | 89.29%   | ~154s      |
| 4 | 1      | 256     | tanh       | sgd       | 0.1    | 32    | 15     | 0.0     | 87.67%   | ~102s      |
| 5 | 4      | 512     | relu       | adam      | 0.001  | 64    | 50     | 0.5     | 86.88%   | ~1358s     |

> **Eksperimen #0** = baseline (jangan ubah, ini patokan kalian).

---

## 🧪 Detail Setiap Eksperimen

Gunakan template di bawah untuk SETIAP eksperimen.

---

### Eksperimen #1

**Apa yang diubah:**
# --- Arsitektur Model ---
HIDDEN_LAYERS     = 2           
NEURONS_PER_LAYER = 128        
ACTIVATION        = 'relu'       
DROPOUT_RATE      = 0.0         

# --- Optimizer & Pelatihan ---
OPTIMIZER     = 'adam'            
LEARNING_RATE = 0.001             
BATCH_SIZE    = 64               
EPOCHS        = 20   

**Hipotesis:**
Peningkatan HIDDEN_LAYERS (2), NEURONS_PER_LAYER (128), Adam optimizer, LEARNING_RATE lebih rendah (0.001), dan EPOCHS lebih banyak (20) diharapkan meningkatkan akurasi model karena kapasitas pembelajaran yang lebih besar. Namun, ada potensi risiko overfitting.

**Hasil:**
- Test accuracy: 87.00%
- Train accuracy: 94.06%
- Validation accuracy: 88.20%
- Train time: 90.4 detik
- Apakah overfit/underfit? Overfit (gap train vs val = 5.9%)

**Observasi:**
1. Akurasi Training Tinggi: 94.06%, menunjukkan pembelajaran yang baik pada data latih.
2. Gap Train vs Val: Terdapat gap 5.9% antara akurasi train (94.06%) dan validasi (88.20%), serta test (87.00%), yang mengindikasikan overfitting.
3. Saran Sistem: Kurangi neuron, tambah dropout, atau kurangi epoch untuk mengatasi overfitting.
4. Durasi Training: 90.4 detik.

---

### Eksperimen #2

**Apa yang diubah:**
# --- Arsitektur Model ---
HIDDEN_LAYERS     = 2           
NEURONS_PER_LAYER = 128        
ACTIVATION        = 'relu'       
DROPOUT_RATE      = 0.3         

# --- Optimizer & Pelatihan ---
OPTIMIZER     = 'adam'            
LEARNING_RATE = 0.001             
BATCH_SIZE    = 64               
EPOCHS        = 20   

**Hipotesis:**
Menambahkan DROPOUT_RATE 0.3 diharapkan mengurangi overfitting yang terlihat di Eksperimen 1, sehingga memperkecil gap antara akurasi training dan validasi, serta meningkatkan generalisasi model ke data test.

**Hasil:**
- Test accuracy: 88.12%
- Train accuracy: 89.24%
- Validation accuracy: 88.83%
- Train time: 93.4 detik
- Apakah overfit/underfit? Tidak overfit / underfit (Train-val gap sehat)

**Observasi:**
1. Overfitting Berkurang Signifikan: Gap antara akurasi training dan validasi sangat kecil (0.4%), menunjukkan bahwa Dropout 0.3 berhasil mengatasi overfitting. Sistem juga melaporkan Train-val gap sehat.
2. Akurasi Test Meningkat: Akurasi test naik menjadi 88.12% (dari 87.00% di Eksperimen 1), menunjukkan model lebih baik dalam menggeneralisasi.
3. Akurasi Training Turun: Akurasi training sedikit menurun (89.24% dari 94.06%), yang wajar karena dropout bertindak sebagai regularisasi.
4. Waktu Training Konsisten: Durasi training tetap sekitar 93.4 detik.

---

### Eksperimen #3

**Apa yang diubah:**
# --- Arsitektur Model ---
HIDDEN_LAYERS     = 1          
NEURONS_PER_LAYER = 64           
ACTIVATION        = 'relu'      
DROPOUT_RATE      = 0.0          

# --- Optimizer & Pelatihan ---
OPTIMIZER     = 'sgd'            
LEARNING_RATE = 0.01             
BATCH_SIZE    = 32              
EPOCHS        = 10   

**Hipotesis:**
Dengan meningkatkan HIDDEN_LAYERS menjadi 3, NEURONS_PER_LAYER menjadi 256, mengubah optimizer menjadi Adamax, BATCH_SIZE menjadi 128, dan EPOCHS menjadi 25, model diharapkan dapat menangkap pola yang lebih kompleks dan meningkatkan akurasi secara keseluruhan, sambil mempertahankan Train-val gap sehat dengan DROPOUT_RATE 0.2.

**Hasil:**
- Test accuracy: 89.29%
- Train accuracy: 92.18%
- Validation accuracy: 89.45%
- Train time: 154.5 detik
- Apakah overfit/underfit? Tidak overfit / underfit (Train-val gap sehat)

**Observasi:**
1. Peningkatan Akurasi: Akurasi test, train, dan validasi semuanya meningkat dibandingkan Eksperimen 2 (Test: 89.29% vs 88.12%).
2. Gap Sehat Terpelihara: Meskipun model lebih dalam dan lebar, gap antara akurasi train dan validasi tetap sehat (2.73%), menunjukkan kombinasi dropout dan optimizer Adamax bekerja dengan baik dalam mengelola kompleksitas model.
3. Waktu Training Meningkat: Durasi training bertambah menjadi 154.5 detik, yang wajar mengingat peningkatan jumlah layer, neuron, dan epoch.

---

### Eksperimen #4

**Apa yang diubah:**
# --- Arsitektur Model ---
HIDDEN_LAYERS     = 1            
NEURONS_PER_LAYER = 256        
ACTIVATION        = 'tanh'       
DROPOUT_RATE      = 0.0          

# --- Optimizer & Pelatihan ---
OPTIMIZER     = 'sgd'          
LEARNING_RATE = 0.1          
BATCH_SIZE    = 32             
EPOCHS        = 15              

**Hipotesis:**
Dengan arsitektur yang lebih sederhana (1 hidden layer, 256 neuron), aktivasi tanh, optimizer SGD dengan LEARNING_RATE lebih tinggi (0.1), dan tanpa dropout, diharapkan model dapat belajar dengan cepat namun mungkin memiliki batas pada kompleksitas pola yang bisa dipelajari. Performa kemungkinan akan sedikit lebih rendah dari model yang lebih kompleks (Eksperimen 3), tetapi mungkin lebih cepat dalam training dan mempertahankan gap train-val yang sehat.

**Hasil:**
- Test accuracy: 87.67%
- Train accuracy: 91.02%
- Validation accuracy: 88.58%
- Train time: 102.9 detik
- Apakah overfit/underfit? Tidak overfit / underfit (Train-val gap sehat)

**Observasi:**
1. Akurasi Menurun Sedikit: Akurasi test (87.67%) sedikit lebih rendah dibandingkan Eksperimen 3 (89.29%), yang wajar mengingat arsitektur model yang lebih sederhana (1 layer vs 3 layer) dan tanpa dropout.
2. Gap Sehat Terpelihara: Train-val gap tetap sehat (2.44%), menunjukkan model tidak mengalami overfitting, kemungkinan karena arsitektur yang lebih sederhana dan penggunaan tanh.
3. Waktu Training Lebih Cepat: Waktu training (102.9 detik) lebih cepat dibandingkan Eksperimen 3 (154.5 detik), yang diharapkan dari model yang kurang kompleks.
4. Performa Relatif terhadap Baseline: Meskipun lebih sederhana, akurasi test Eksperimen 4 (87.67%) masih lebih baik dari baseline (yang ~87% di Eksperimen 1), menunjukkan tanh dan SGD dengan LR=0.1 pada 1 layer 256 neuron bisa menjadi alternatif yang efisien.

---

### Eksperimen #5

**Apa yang diubah:**
# --- Arsitektur Model ---
HIDDEN_LAYERS     = 1          
NEURONS_PER_LAYER = 64          
ACTIVATION        = 'relu'    
DROPOUT_RATE      = 0.0       

# --- Optimizer & Pelatihan ---
OPTIMIZER     = 'sgd'          
LEARNING_RATE = 0.01            
BATCH_SIZE    = 32            
EPOCHS        = 10               

**Hipotesis:**
Dengan model yang jauh lebih kompleks (4 hidden layers, 512 neuron per layer) dan EPOCHS yang tinggi (50), diharapkan model dapat menangkap pola yang sangat detail. DROPOUT_RATE yang tinggi (0.5) dipasang untuk mengontrol overfitting yang mungkin terjadi akibat kompleksitas model ini, serta Adam optimizer dengan LEARNING_RATE rendah (0.001) untuk konvergensi yang stabil. Potensi untuk akurasi tertinggi, namun juga waktu training yang sangat panjang.

**Hasil:**
- Test accuracy: 86.88%
- Train accuracy: 87.24%
- Validation accuracy: 87.80%
- Train time: 1358.6 detik
- Apakah overfit/underfit? Tidak overfit / underfit (Train-val gap sehat)

**Observasi:**
1.  **Akurasi Menurun:** Akurasi test (86.88%) sedikit lebih rendah dari Eksperimen 3 (89.29%) dan bahkan Eksperimen 4 (87.67%). Ini mungkin mengindikasikan bahwa `DROPOUT_RATE` yang terlalu tinggi (0.5) pada `EPOCHS` yang banyak atau kompleksitas model yang berlebihan tidak selalu menghasilkan performa terbaik.
2.  **Gap Sehat Terpelihara:** Gap antara akurasi train (87.24%) dan validasi (87.80%) sangat sehat, dengan validasi bahkan sedikit lebih tinggi dari train di akhir, mengindikasikan dropout sangat efektif mencegah overfitting. Sistem juga melaporkan `Train-val gap sehat`.
3.  **Waktu Training Sangat Lama:** Durasi training sangat signifikan meningkat menjadi 1358.6 detik (sekitar 22.6 menit), yang sesuai dengan peningkatan `HIDDEN_LAYERS`, `NEURONS_PER_LAYER`, dan terutama `EPOCHS` yang sangat tinggi (50).
4.  **Trade-off Akurasi vs. Kompleksitas/Waktu:** Eksperimen ini menunjukkan bahwa model yang lebih besar dan lebih lama dilatih tidak selalu menghasilkan akurasi yang lebih tinggi jika hyperparameter seperti dropout rate tidak di-tune dengan tepat. Akurasi stagnan atau bahkan sedikit menurun meskipun training memakan waktu jauh lebih lama.
---

## 🏆 Konfigurasi Terbaik

Setelah semua eksperimen, salin konfigurasi terbaik kalian ke sini:

HIDDEN_LAYERS     = 3
NEURONS_PER_LAYER = 256
ACTIVATION        = 'relu'
DROPOUT_RATE      = 0.2
OPTIMIZER         = 'adamax'
LEARNING_RATE     = 0.001
BATCH_SIZE        = 128
EPOCHS            = 25

Test accuracy final: 89.29%
