# Makine Öğrenmesi ile Ağ Anomali Tespiti

Bu proje, **CSE-CIC-IDS2018** veri seti üzerinde makine öğrenmesi yöntemleri kullanılarak ağ trafiğinin **normal** veya **saldırı** olarak sınıflandırılmasını amaçlamaktadır. Projede ağ anomali tespiti problemi, gözetimli öğrenme yaklaşımıyla ele alınmış ve iki farklı topluluk öğrenme algoritması karşılaştırılmıştır:

* Random Forest
* XGBoost

Proje, Eskişehir Osmangazi Üniversitesi Makine Öğrenmesi dersi kapsamında hazırlanmıştır.

---

## Proje Ekibi

Bu proje 2 kişilik grup çalışması olarak hazırlanmıştır.

| Öğrenci        | Numara       |
| -------------- | ------------ |
| Çağrı Elagöz   | 152120211097 |
| Yusuf Özgöçmen | 152120221093 |

---

## Projenin Amacı

Geleneksel imza tabanlı saldırı tespit sistemleri, yalnızca daha önce tanımlanmış saldırı kalıplarını yakalayabilir. Ancak günümüz ağ ortamlarında sıfırıncı gün saldırıları, polimorfik tehditler, DDoS saldırıları, brute force denemeleri ve botnet tabanlı aktiviteler gibi çok daha değişken ve karmaşık tehditler bulunmaktadır.

Bu proje kapsamında amaç, ağ trafiğinden elde edilen akış tabanlı öznitelikleri kullanarak trafiğin normal mi yoksa saldırı mı olduğunu makine öğrenmesi modelleriyle tahmin etmektir.

Projenin temel hedefleri şunlardır:

* CSE-CIC-IDS2018 veri setini makine öğrenmesi için uygun hale getirmek
* Veri temizleme ve ön işleme adımlarını uygulamak
* Sınıf dengesizliği problemini dikkate almak
* En anlamlı öznitelikleri seçmek
* Random Forest ve XGBoost algoritmalarını eğitmek
* Modelleri accuracy, precision, recall, F1-score, ROC-AUC ve PR-AUC metrikleriyle karşılaştırmak
* Elde edilen sonuçları bilimsel rapor formatında yorumlamak

---

## Kullanılan Veri Seti

Bu projede **CSE-CIC-IDS2018** veri seti kullanılmıştır.

CSE-CIC-IDS2018, Canadian Institute for Cybersecurity tarafından yayımlanmış modern bir saldırı tespit veri setidir. Veri seti, AWS ortamında simüle edilmiş kurumsal ağ trafiğinden oluşur. Ağ trafiği kayıtları CICFlowMeter aracı ile işlenmiş ve makine öğrenmesi çalışmalarında kullanılabilecek akış tabanlı CSV dosyalarına dönüştürülmüştür.

Bu projede kullanılan CSV dosyaları Kaggle üzerinde paylaşılan **CSE-CIC-IDS2018 CICFlowMeter** sürümünden indirilmiştir. Veri setinin orijinal kaynağı ise University of New Brunswick / Canadian Institute for Cybersecurity tarafından yayımlanan CSE-CIC-IDS2018 veri setidir.

Veri seti genel olarak şu saldırı türlerini içerir:

* Brute-force
* Heartbleed
* Botnet
* DoS
* DDoS
* Web saldırıları
* İç ağ sızması / infiltration

Veri setinde ağ trafiğinden çıkarılmış 80 civarında akış tabanlı öznitelik bulunmaktadır. Bu öznitelikler paket sayısı, paket uzunluğu, akış süresi, bayrak bilgileri, saniyedeki paket oranları ve ileri/geri yönlü trafik istatistikleri gibi değerleri içerir.

---

## Veri Seti Kaynakları

Veri seti dosyaları büyük boyutlu olduğu için bu GitHub reposuna yüklenmemiştir. Projeyi çalıştırmak isteyen kullanıcıların veri setini aşağıdaki kaynaklardan indirip proje klasörüne yerleştirmesi gerekir.

* Resmi veri seti sayfası:
  https://www.unb.ca/cic/datasets/ids-2018.html

* Kaggle CSV sürümü:
  https://www.kaggle.com/datasets/masjohncook/cse-cic-ids2018-cicflowmeter

CSV dosyaları indirildikten sonra aşağıdaki klasöre yerleştirilmelidir:

```text
data/MachineLearningCSV/
```

Beklenen veri seti yapısı:

```text
data/MachineLearningCSV/
├── 02-14-2018.csv
├── 02-15-2018.csv
├── 02-16-2018.csv
├── 02-20-2018.csv
├── 02-21-2018.csv
├── 02-22-2018.csv
├── 02-23-2018.csv
├── 02-28-2018.csv
├── 03-01-2018.csv
└── 03-02-2018.csv
```

---

## Repository Yapısı

```text
Network-Anomaly-Detection-IDS2018/
│
├── ag_anomali_tespiti_final_teslim.ipynb
├── README.md
├── .gitignore
│
├── data/
│   └── MachineLearningCSV/
│       └── .gitkeep
│
├── files/
│   ├── ESOGUmmfSABLON.docx.pdf
│   ├── Literatur_Cizelge.xlsx
│   ├── Rapor_1.pdf
│   ├── Rapor_2.pdf
│   ├── Sunum_1.pdf
│   └── Sunum_2.pdf
│
└── outputs/
```

Açıklamalar:

* `ag_anomali_tespiti_final_teslim.ipynb`: Projenin ana makine öğrenmesi notebook dosyasıdır.
* `data/MachineLearningCSV/`: Veri seti CSV dosyalarının yerleştirileceği klasördür.
* `files/`: Proje raporları, sunum dosyaları, literatür çizelgesi ve makale şablonu bu klasörde tutulur.
* `outputs/`: Notebook çalıştırıldığında üretilen grafikler, metrik tabloları ve çıktı dosyaları bu klasöre kaydedilir.
* `.gitignore`: Büyük veri seti dosyalarının ve çıktı dosyalarının GitHub’a yüklenmesini engeller.

---

## Kullanılan Yöntemler

Projede uygulanan makine öğrenmesi süreci aşağıdaki adımlardan oluşmaktadır:

1. Veri setindeki CSV dosyalarının okunması
2. Tekrarlı başlık satırlarının temizlenmesi
3. Duplicate kayıtların kaldırılması
4. Sonsuz ve eksik değerlerin işlenmesi
5. Modelin ezberleme yapmasına neden olabilecek tanımlayıcı sütunların çıkarılması
6. Etiketlerin binary sınıflandırmaya dönüştürülmesi
7. Eğitim ve test veri setlerinin ayrılması
8. Min-Max ölçeklendirme uygulanması
9. Mutual Information ile öznitelik seçimi yapılması
10. Random Forest modelinin eğitilmesi
11. XGBoost modelinin eğitilmesi
12. Modellerin performans metrikleriyle karşılaştırılması
13. Confusion matrix, ROC eğrisi, Precision-Recall eğrisi ve feature importance grafiklerinin üretilmesi

---

## Veri Ön İşleme

Veri ön işleme aşamasında aşağıdaki işlemler uygulanmıştır:

### 1. Gereksiz Sütunların Çıkarılması

Modelin veri setine özgü bilgileri ezberlemesini önlemek için aşağıdaki türde sütunlar model girdisinden çıkarılmıştır:

* Flow ID
* Source IP
* Destination IP
* Timestamp
* Source file bilgisi

Bu sütunlar ağ trafiğinin davranışsal yapısından çok veri kaynağına özgü kimlik bilgileri içerdiği için modelin genellenebilirliğini olumsuz etkileyebilir.

### 2. Eksik ve Sonsuz Değerlerin İşlenmesi

CSE-CIC-IDS2018 veri setinde bazı akış istatistikleri `NaN`, `Inf` veya `-Inf` değerler içerebilir. Bu değerler model eğitiminden önce temizlenmiş ve sayısal sütunlardaki eksik değerler medyan ile doldurulmuştur.

### 3. Binary Etiket Dönüşümü

Orijinal veri setindeki tüm saldırı türleri tek bir saldırı sınıfına dönüştürülmüştür.

| Orijinal Etiket           | Yeni Etiket |
| ------------------------- | ----------- |
| BENIGN                    | 0           |
| Diğer tüm saldırı türleri | 1           |

Bu dönüşüm sonucunda problem şu hale getirilmiştir:

| Sınıf  | Açıklama        |
| ------ | --------------- |
| BENIGN | Normal trafik   |
| ATTACK | Saldırı trafiği |

---

## Öznitelik Seçimi

Veri setinde çok sayıda akış tabanlı özellik bulunduğu için, modelin daha verimli çalışması amacıyla öznitelik seçimi yapılmıştır. Bu projede **Mutual Information** yöntemi kullanılarak hedef değişkenle en ilişkili öznitelikler seçilmiştir.

Seçilen önemli özniteliklerden bazıları şunlardır:

* Dst Port
* Init Fwd Win Byts
* Fwd Pkts/s
* Flow Pkts/s
* Fwd Pkt Len Mean
* Fwd Seg Size Avg
* Bwd Seg Size Avg
* Pkt Len Mean
* Pkt Len Std
* Pkt Len Var

Bu öznitelikler, ağ trafiğinin zamanlama, hacim, paket uzunluğu ve port davranışı gibi yönlerini temsil eder.

---

## Kullanılan Modeller

### Random Forest

Random Forest, birden fazla karar ağacının birlikte kullanıldığı bagging tabanlı bir topluluk öğrenme algoritmasıdır. Her ağaç farklı örnekler ve farklı öznitelik alt kümeleriyle eğitilir. Son karar çoğunluk oylaması ile verilir.

Bu projede Random Forest şu nedenlerle tercih edilmiştir:

* Gürültülü verilerde kararlı çalışabilir.
* Tabular veri setlerinde güçlü sonuçlar verir.
* Overfitting riskini tek karar ağacına göre azaltır.
* Feature importance değeri üreterek yorumlanabilirlik sağlar.
* Ağ trafiği gibi çok öznitelikli veri setlerinde iyi performans gösterebilir.

### XGBoost

XGBoost, boosting tabanlı güçlü bir topluluk öğrenme algoritmasıdır. Model, önceki ağaçların hatalarını azaltacak şekilde ardışık karar ağaçları oluşturur.

Bu projede XGBoost şu nedenlerle tercih edilmiştir:

* Büyük veri setlerinde etkili çalışabilir.
* Sınıf dengesizliğine karşı `scale_pos_weight` parametresi kullanılabilir.
* Regularization desteği sayesinde aşırı öğrenme riski azaltılabilir.
* Doğrusal olmayan karmaşık saldırı örüntülerini öğrenebilir.
* ROC-AUC ve PR-AUC gibi ayırt edicilik metriklerinde güçlü sonuçlar verebilir.

---

## Değerlendirme Metrikleri

Ağ anomali tespitinde yalnızca accuracy metriğine bakmak yeterli değildir. Çünkü veri setinde normal trafik saldırı trafiğine göre daha fazla olabilir. Bu durumda model sürekli normal tahmin yaparak yüksek accuracy elde edebilir, fakat saldırıları kaçırabilir.

Bu nedenle projede aşağıdaki metrikler birlikte değerlendirilmiştir:

| Metrik    | Açıklama                                                             |
| --------- | -------------------------------------------------------------------- |
| Accuracy  | Tüm doğru tahminlerin toplam örnek sayısına oranı                    |
| Precision | Saldırı olarak tahmin edilen kayıtların gerçekten saldırı olma oranı |
| Recall    | Gerçek saldırıların ne kadarının doğru tespit edildiği               |
| F1-score  | Precision ve recall değerlerinin harmonik ortalaması                 |
| ROC-AUC   | Modelin sınıfları ayırt etme başarısı                                |
| PR-AUC    | Dengesiz veri setlerinde precision-recall başarısını gösteren alan   |

Ağ güvenliği açısından özellikle `Recall` kritik öneme sahiptir. Çünkü düşük recall, gerçek saldırıların bir kısmının normal trafik olarak sınıflandırılması anlamına gelir. Bu da güvenlik riski oluşturur.

---

## Deneysel Sonuçlar

Bu projede CSE-CIC-IDS2018 veri setinden örneklenmiş CSV kayıtları kullanılarak Random Forest ve XGBoost modelleri karşılaştırılmıştır.

Elde edilen genel sonuçlar:

| Model         | Accuracy | Precision | Recall | F1-score | ROC-AUC | PR-AUC |
| ------------- | -------: | --------: | -----: | -------: | ------: | -----: |
| Random Forest |   0.9541 |    0.9159 | 0.8833 |   0.8993 |  0.9793 | 0.9605 |
| XGBoost       |   0.9479 |    0.8783 | 0.9000 |   0.8890 |  0.9875 | 0.9699 |

### Sonuçların Yorumu

Random Forest modeli accuracy, precision ve F1-score açısından daha dengeli sonuç vermiştir. Bu durum, Random Forest modelinin daha az yanlış alarm ürettiğini ve saldırı olarak işaretlediği kayıtların daha yüksek oranda gerçekten saldırı olduğunu göstermektedir.

XGBoost modeli ise recall, ROC-AUC ve PR-AUC metriklerinde daha başarılı sonuç vermiştir. Bu durum, XGBoost modelinin gerçek saldırıları yakalama konusunda daha güçlü olduğunu göstermektedir. Ancak XGBoost daha fazla saldırı yakalarken daha fazla yanlış alarm üretme eğilimi göstermiştir.

Bu nedenle model seçimi sistemin önceliğine göre yapılmalıdır:

* Yanlış alarm sayısını azaltmak önemliyse Random Forest tercih edilebilir.
* Saldırı kaçırmamak daha önemliyse XGBoost tercih edilebilir.

---

## Kurulum

Projeyi yerel bilgisayara indirmek için:

```bash
git clone https://github.com/cagrielagozz/Network-Anomaly-Detection-IDS2018.git
cd Network-Anomaly-Detection-IDS2018
```

Sanal ortam oluşturmak için:

```bash
python -m venv .venv
```

Windows PowerShell için sanal ortamı aktif etme:

```powershell
.\\.venv\\Scripts\\Activate.ps1
```

CMD için:

```cmd
.venv\\Scripts\\activate
```

Linux/macOS için:

```bash
source .venv/bin/activate
```

Gerekli kütüphaneleri yüklemek için:

```bash
pip install numpy pandas matplotlib scikit-learn xgboost jupyter
```

---

## Kullanım

1. Veri setini Kaggle veya resmi CSE-CIC-IDS2018 kaynağından indirin.
2. CSV dosyalarını aşağıdaki klasöre yerleştirin:

```text
data/MachineLearningCSV/
```

3. Jupyter Notebook’u başlatın:

```bash
jupyter notebook
```

4. Aşağıdaki notebook dosyasını açıp hücreleri sırayla çalıştırın:

```text
ag_anomali_tespiti_final_teslim.ipynb
```

Notebook çalıştırıldığında çıktı dosyaları `outputs/` klasöründe oluşturulur.

---

## Oluşturulan Çıktılar

Notebook çalıştırıldıktan sonra aşağıdaki türde çıktı dosyaları üretilir:

```text
outputs/
├── raw_label_distribution.csv
├── raw_label_distribution.png
├── binary_label_distribution.csv
├── binary_label_distribution.png
├── missing_values_summary.csv
├── feature_selection_scores.csv
├── selected_features.csv
├── selected_features_mutual_information.png
├── random_forest_confusion_matrix.csv
├── random_forest_confusion_matrix.png
├── random_forest_roc_curve.png
├── random_forest_precision_recall_curve.png
├── random_forest_feature_importance.csv
├── random_forest_feature_importance.png
├── xgboost_confusion_matrix.csv
├── xgboost_confusion_matrix.png
├── xgboost_roc_curve.png
├── xgboost_precision_recall_curve.png
├── xgboost_feature_importance.csv
├── xgboost_feature_importance.png
└── model_comparison_results.csv
```

Bu çıktılar proje raporu ve sunumunda kullanılabilecek deneysel bulguları içerir.

---

## Notlar

* CSV veri seti dosyaları büyük boyutlu olduğu için repoya dahil edilmemiştir.
* `data/MachineLearningCSV/` klasörü `.gitkeep` dosyası ile repoda tutulmuştur.
* Notebook göreli dosya yolları ile çalışır; bilgisayara özel dosya yolu kullanılmaz.
* Varsayılan olarak her CSV dosyasından örnekleme yapılır.
* Tüm veri setiyle çalışmak istenirse notebook içindeki okuma modu değiştirilebilir.
* Test verisine SMOTE veya benzeri dengeleme uygulanmamıştır.
* Sınıf dengesizliği model seviyesinde `class_weight` ve `scale_pos_weight` ile ele alınmıştır.

---

## Gelecek Çalışmalar

Bu proje ilerleyen aşamalarda şu yönlerde geliştirilebilir:

* Çok sınıflı saldırı türü sınıflandırması yapılabilir.
* GridSearchCV veya RandomizedSearchCV ile hiperparametre optimizasyonu uygulanabilir.
* SMOTE, undersampling ve class weighting yöntemleri karşılaştırılabilir.
* LSTM veya GRU ile zamansal ağ trafiği analizi yapılabilir.
* SHAP veya LIME ile açıklanabilir yapay zeka desteği eklenebilir.
* Gerçek zamanlı ağ anomali tespit sistemi geliştirilebilir.
* Model bir API servisi olarak dağıtılabilir.

---

## Akademik Bağlam

Bu çalışma, Makine Öğrenmesi dersi kapsamında hazırlanmış bir proje çalışmasıdır. Proje kapsamında literatür taraması, veri seti seçimi, veri ön işleme, modelleme, deneysel değerlendirme ve sonuç yorumlama adımları gerçekleştirilmiştir.

---

## Lisans ve Kullanım

Bu repository akademik ve eğitim amaçlı hazırlanmıştır. CSE-CIC-IDS2018 veri setinin kullanım şartları ve atıf gereklilikleri orijinal veri seti sağlayıcılarına aittir.

Veri seti kullanılırken orijinal CSE-CIC-IDS2018 kaynağına ve veri seti sağlayıcılarına uygun şekilde atıf yapılmalıdır.
