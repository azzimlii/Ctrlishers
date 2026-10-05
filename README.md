# Ctrlishers
Binary Classification 
# Ctrl is Hers Final — Binary Classification (Kaggle)

Kaggle müsabiqəsi **ctrl-is-hers-final** üçün ikili (binary) təsnifat layihəsi. Məqsəd: hər sətir (məqalə) üçün `target` (0/1) ehtimalını proqnozlaşdırmaq və `submission.csv` hazırlamaqdır.

## Data

| Fayl | Təsvir |
|---|---|
| `train.csv` | 31 715 sətir, 49 sütun (`target` daxil) |
| `test.csv` | `target` olmayan data |
| `sample_submission.csv` | Submission formatı |

- `publish_date`, `weekday`, `channel` — tarix və kateqorial dəyişənlər

Train datasında boş dəyər və dublikat yoxdur. Target balanslıdır (1: 17 357, 0: 14 358).

## Addımlar

1. **Data hazırlığı**
   - `publish_date` → `year`, `month`, `day`
   - `weekday` və `channel` → one-hot encoding (`drop_first=True`)
   - `id` modelə verilmir, çünki identifikatordur
2. **Baseline** — `LogisticRegression` (scale olmadan)
3. **Scaling** — `StandardScaler` + `LogisticRegression`
4. **Test proqnozu** — test datasına train ilə eyni addımlar tətbiq olunur, sonra `submission.csv` yazılır

Train/validation bölgüsü: 80/20, `stratify=y`, `random_state=42`.

## Nəticələr (validation)

 Model ROC-AUC 
 
Logistic Regression (scale olmadan) ROC-AUC 0.61

Logistic Regression + StandardScaler ROC-AUC 0.70
