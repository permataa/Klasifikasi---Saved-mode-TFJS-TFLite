# 🌄 CNN Image Classification — 6 Kelas Pemandangan Alam

Proyek ini membangun model Convolutional Neural Network (CNN) menggunakan TensorFlow/Keras untuk mengklasifikasikan gambar pemandangan alam ke dalam 6 kelas: **bangunan, hutan, gletser, gunung, laut, jalan**. Dataset berisi ±25.000 gambar berukuran 150×150 px dan telah dipisahkan menjadi train, test, dan prediction set. Proyek ini dibuat untuk memenuhi seluruh kriteria tugas model CNN.

## 📁 Dataset
- Total gambar: ±25.000  
- Train: ±14.000  
- Test: ±3.000  
- Prediction: ±7.000  
- Kelas:
  - 0: bangunan  
  - 1: hutan  
  - 2: gletser  
  - 3: gunung  
  - 4: laut  
  - 5: jalan  

Dataset berasal dari kompetisi Intel (Analytics Vidhya).

## 🎯 Tujuan Proyek
- Menggunakan model **Sequential**, **Conv2D**, **MaxPooling2D**.  
- Membagi dataset menjadi **Train, Validation, Test**.  
- Mencapai **≥85% akurasi**.  
- Membuat grafik akurasi & loss.  
- Menyimpan model dalam:
  - **SavedModel**
  - **TF Lite (.tflite)**
  - **TensorFlow.js**

## 🛠 Arsitektur CNN
```
Sequential([
  Conv2D(32, (3,3), activation='relu', input_shape=(150,150,3)),
  MaxPooling2D(2,2),
  Conv2D(64, (3,3), activation='relu'),
  MaxPooling2D(2,2),
  Conv2D(128, (3,3), activation='relu'),
  MaxPooling2D(2,2),
  Flatten(),
  Dense(128, activation='relu'),
  Dropout(0.5),
  Dense(6, activation='softmax')
])
```

## 📊 Hasil Training & Testing

### Training Results
```
66/66 ━━━━━━━━━━━━━━━━━━━━ 5s 76ms/step
accuracy: 0.8920 
loss: 0.2879 
precision: 0.9035 
recall: 0.8836
```

### Testing Results
| Metric | Value |
|--------|--------|
| Accuracy | **0.8835** |
| Precision | **0.8947** |
| Recall | **0.8769** |

## 💾 Export Model

### SavedModel
```
model.save("models/saved_model/")
```

### TensorFlow Lite
```
converter = tf.lite.TFLiteConverter.from_saved_model("models/saved_model/")
tflite_model = converter.convert()
open("models/model.tflite", "wb").write(tflite_model)
```

### TensorFlow.js
```
tensorflowjs_converter   --input_format=tf_saved_model   models/saved_model   models/tfjs_model/
```

## ▶️ Cara Menjalankan
```
git clone <repo-url>
pip install -r requirements.txt
jupyter notebook
```

## 📝 Kesimpulan
Model CNN berhasil dilatih menggunakan dataset besar dan mencapai akurasi di atas 85%. Model telah diekspor ke format SavedModel, TFLite, dan TFJS sehingga dapat digunakan pada aplikasi server, mobile, maupun web. Proyek ini memenuhi seluruh kriteria tugas CNN.
