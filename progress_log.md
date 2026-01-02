# Film Data Analytics Project – Task Checklist

## 1. Project Structure
- [x] Create folders `/data`, `/notebooks`, `/models`, `/viz`, `/docs`
- [x] Write `README.md` summarizing purpose, data, and goals

## 2. Dataset Definition
- [x] Define all tables and relationships
- [x] Create ER diagram (`docs/er_diagram.md`)
- [x] Write data dictionary (`docs/data_dictionary.md`)

## 3. Exploratory Data Analysis (EDA)
- [ ] Distribution analysis
    rating, year, budget, box_office için histogram veya KDE çiz.
    Kategorik değişkenler için countplot.
    İlk gözlem: veri normal mi, sağa/sola çarpık mı, log dönüşüm gerekir mi?

- [ ] Missing value analysis
    df.isna().sum() ile yüzdeleri bul.
    Hangi değişkenlerde eksik çoksa, bu değişkenlerin analizlerde kullanımı veya imputasyonu planlanır.

- [ ] Outlier analysis
    Boxplot veya IQR yöntemiyle tespit et.
    Özellikle budget ve box_office log ölçeğe ihtiyaç duyar.

- [ ] Correlation analysis
    Sayısal değişkenlerde df.corr() + heatmap.
    Hedef değişken (ör. rating veya box_office) ile anlamlı ilişkileri değerlendir.

- [ ] Sonuç olarak:
    EDA bitince model hedefini tanımla (ör. “box_office tahmini” mi, “rating tahmini” mi?).
    Bu hedefe göre hangi değişkenlerin etkili olduğuna karar ver.

## 4. Feature Engineering
- [ ] Encode categorical variables (genre, country)
- [ ] Create new features: ROI, age_since_release, num_awards, is_franchise
- [ ] (Optional) Generate NLP embeddings from text fields

## 5. Modeling
- [ ] Regression: predict box office or rating
- [ ] Clustering: group films by genre or audience profile
- [ ] Classification: label “successful” films (IMDb>7.5 or ROI>2)

## 6. Visualization (Tableau)
- [ ] Dashboard 1 – Key statistics
- [ ] Dashboard 2 – Correlations and trends
- [ ] Dashboard 3 – Model results and prediction comparisons

## 7. Reporting & Presentation
- [ ] Write final report (`report.docx` / `report.pdf`)
- [ ] Prepare Tableau Story presentation

## 8. Progress Tracking
- [x] Initialize `progress_log.md`
- [ ] Log each milestone with date, summary, and % completion

---

### Example Log Entries
- 2025-10-19 — EDA completed. Missing values <2%.
- 2025-10-22 — ROI feature engineered, preliminary model accuracy 0.81 R².
