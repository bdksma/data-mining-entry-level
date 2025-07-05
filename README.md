# data-mining
This is a repository for one of technical test for position data mining engineer internship and make me get the internship proved my skill in data mining using MySQL and PHP
```markdown
# 🧪 Data Mining Technical Test –  Portfolio

This repository contains the solution to a data mining technical test completed as part of a Data Mining Internship application. The project involves data preparation, cleaning, and solving business problems using SQL.

---

## 📁 Project Structure
data-mining-test/
├── data/
│   └── data\_cleaned.csv
├── notebooks/
│   └── data\_preparation\_colab.ipynb
├── result-query-desc/
│   └── fig1.png
│   └── technical test.pdf
├── README.md
---

🎯 Objective

To demonstrate proficiency in:
- Data cleaning and preparation
- SQL for business-oriented analysis
- Managing real-world retail transaction data

---

📊 Dataset Overview

- Rows: 75,970  
- Columns: 13  
- Original Format: Excel  
- Converted To: CSV for processing and MySQL import

Tools Used:
- Google Colab (Python, Pandas)
- MySQL (via XAMPP + PHPMyAdmin)
- Microsoft Excel (initial inspection)

---

⚙️ Data Preparation Summary

- Converted date strings to `datetime` format
- Cleaned percentage fields (`%gm`) and removed "%" symbol
- Ensured correct data types (e.g., `SKU` as `INT`, `members` as `BIGINT`)
- Handled missing values and duplicates
- Saved clean dataset to `data_cleaned.csv`

📎 [Google Colab Notebook](https://colab.research.google.com/drive/1kuDsMovKfawT14FODkt8t1j7JHUvMOvD?usp=sharing)  
📎 [Cleaned Dataset (CSV)](https://drive.google.com/file/d/1RUZrS0dvNvQ-iT9IEuZJvSuoAPiUMHLz/view?usp=sharing)

---

🧮 SQL Analysis & Insights

1. 🔍 Monthly Sales per Store (sorted by highest)

```sql
SELECT  
    kode_toko, 
    DATE_FORMAT(tgl_trs, '%Y-%m') AS bulan, 
    SUM(net_sales) AS total_sales
FROM  
    data_penjualan
GROUP BY  
    kode_toko, bulan
ORDER BY  
    total_sales DESC;
````

*Insight:*
Store `EU82` recorded the highest monthly sales in February 2024, totaling **Rp 196,726,064**.

---

2. 🏆 Top 20 Members by Average Gross Margin (%GM)

```sql
SELECT  
    members, 
    AVG(gm_percent) AS avg_gm
FROM  
    data_penjualan
GROUP BY  
    members
ORDER BY  
    avg_gm DESC
LIMIT 20;
```

*Insight:*
Members like `11003928059` and `11002214584` achieved the highest average gross margins.

---

3. 📦 Top Category per Tag (O, F, M, B, J) Based on Quantity

```sql
SELECT tag, kategori, total_qty
FROM (
    SELECT tag, kategori, SUM(qty) AS total_qty,
           ROW_NUMBER() OVER (PARTITION BY tag ORDER BY SUM(qty) DESC) AS rn
    FROM data_penjualan
    WHERE tag IN ('O', 'F', 'M', 'B', 'J')
    GROUP BY tag, kategori
) AS ranked
WHERE rn = 1;
```

Insight:
The category `1714 - STOCK SOUP` with tag `J` had the highest quantity at **243,023 units**.

---

4. 🚫 Sales from Non-"CIGARETTE & LIGHTER" Departments

```sql
SELECT  
    kode_toko, 
    SUM(net_sales) AS total_penjualan
FROM  
    data_penjualan
WHERE  
    departemen != '24 - CIGARETTE & LIGHTER'
GROUP BY  
    kode_toko
ORDER BY  
    total_penjualan DESC;
```

*Insight:*
Store `QC66` had the highest non-cigarette department sales: **Rp 102,800,014**.

---

👤 Author

**Yusuf Budi Kusuma**
📧 [yusufbudikusuma7@gmail.com](mailto:yusufbudikusuma7@gmail.com)
📱 +62 858-9475-3213

---

 💼 Summary

This project showcases end-to-end capabilities in:

* Data preprocessing and cleaning (Python)
* Query building and business analysis (MySQL)
* Analytical thinking based on real-world retail data

Great for roles in:

* Data Mining
* Business Intelligence
* Data Analyst / Junior Data Engineer
