# 🧱 Handling Categorical Missing Values — Mode & “Missing” Imputation  
**🧠 AI-Generated README**

---

## 📌 Overview  
This project demonstrates how to **handle categorical missing values** using the **Housing dataset**.  
We focus on two columns:
- `GarageQual`
- `FireplaceQu`

The goal is to handle missing values using:
- **Mode imputation** (most frequent category)
- **“Missing” label imputation** (adding a new category)

---

## 🧰 Libraries Used  
- pandas  
- matplotlib  
- seaborn  
- scikit-learn  

---

## 📂 Dataset Information  
Dataset available in the repo.  
Contains the following columns for this task:
- `GarageQual` → 81 missing values  
- `FireplaceQu` → 690 missing values  
- `SalePrice` → target column for visual comparison  

---

## ⚙️ Step-by-Step Workflow  

### 1️⃣ GarageQual Exploration
- **Bar Plot (<img width="580" height="438" alt="cat1" src="https://github.com/user-attachments/assets/6d7b3dad-3d9b-47f2-98cd-f7d7cc448dd3" />
)** → Shows **TA (Typical/Average)** as the most frequent category, making it the **mode**.  
- **KDE Plot (<img width="567" height="453" alt="cat2" src="https://github.com/user-attachments/assets/8fff72a6-e453-4191-8f18-264cd711f77d" />
)** → Compared `SalePrice` distributions for TA vs missing; they differ slightly.  
- **Imputation:** Missing `GarageQual` values were filled with **TA**.  
- **Bar Plot (<img width="560" height="438" alt="cat3" src="https://github.com/user-attachments/assets/48d0f949-86a2-4a59-a402-7e3c928be3e8" />
)** → TA count increased, nulls removed.  
- **KDE Plot (<img width="554" height="453" alt="cat4" src="https://github.com/user-attachments/assets/5e41cf70-bba4-469e-adcd-28574be7a8cd" />
)** → Before vs after imputation distributions are nearly identical — minimal effect on data.

---

### 2️⃣ FireplaceQu Exploration
- **Bar Plot (<img width="552" height="438" alt="cat5" src="https://github.com/user-attachments/assets/f172e0ff-d676-4c21-bf3f-8ceff185c9dd" />
)** → **GD (Good)** is most frequent, hence the **mode**.  
- **KDE Plot (<img width="567" height="435" alt="cat6" src="https://github.com/user-attachments/assets/bc84ec0c-4e93-4744-b44a-c6260cd3b205" />
)** → Big difference between GD and null distributions.  
- Imputed missing `FireplaceQu` values with **GD**.  
- **Bar Plot (<img width="560" height="438" alt="cat7" src="https://github.com/user-attachments/assets/d8abec9d-49a5-4665-b275-5bc6893d1355" />
)** → GD count increased significantly after imputation.  
- **KDE Plot (<img width="554" height="435" alt="cat8" src="https://github.com/user-attachments/assets/973eeafd-4d13-4310-9ed7-22ee932cebe6" />
)** → Distribution changed — noticeable difference, indicating mode imputation slightly distorted feature behavior.

---

### 3️⃣ Using Scikit-learn for Mode Imputation  
- Applied **`SimpleImputer(strategy='most_frequent')`** to automate mode imputation.  
- Used `ColumnTransformer` to apply on selected categorical columns.  
- Results were identical to manual mode filling — simpler and reproducible.

---

### 4️⃣ Adding a “Missing” Category  
Instead of filling with mode, another method is to **create a new category** for missing values.  
This helps models recognize missing data as a separate class.  
Used:
```python
df['GarageQual'].fillna('Missing', inplace=True)
df['FireplaceQu'].fillna('Missing', inplace=True)
```

Bar Plot (<img width="560" height="470" alt="cat9" src="https://github.com/user-attachments/assets/16dff69a-8f7c-46de-9206-86e3389ec1cb" />
) → New bar “Missing” visible showing replaced nulls.

Adds interpretability — model can learn if missingness has meaning.

### 📊 Comparison Table
Method	Distribution Change	Model Awareness	Best Used When
Mode Imputation	Low	Neutral	Few nulls, random missingness
SimpleImputer	Low	Neutral	Automated preprocessing
“Missing” Label	None (adds class)	High	Missingness might carry meaning
### 🧩 Observations

GarageQual imputation with TA caused minimal distortion.

FireplaceQu imputation changed distribution significantly due to many nulls.

“Missing” category provides better model interpretability.

SimpleImputer simplifies the process in production pipelines.

### 🖼️ Attached Images

Bar plot of GarageQual before imputation

KDE plot TA vs null (GarageQual)

Bar plot after imputation (GarageQual)

KDE before/after GarageQual imputation

Bar plot FireplaceQu before

KDE FireplaceQu before imputation

Bar plot after FireplaceQu imputation

KDE before/after FireplaceQu imputation

Bar plot with “Missing” category added

📄 Note: This README was AI-generated for documentation and educational purposes.
