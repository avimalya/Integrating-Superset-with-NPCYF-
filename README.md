
# Integrating Superset with NPCYF

A project report submitted for **Data Science Internship at ISI, Kolkata**

**Author:** Avimalya Dey
**Date:** October 31, 2024
**Institute:** IDEAS – Institute of Data Engineering, Analytics and Science Foundation (Technology Innovation Hub @ Indian Statistical Institute, Kolkata)

---

## 📌 Project Overview

The objective of this project is to build a **comprehensive dashboard for crop production data in India** using **Apache Superset** integrated with a MySQL backend.

* Provides insights into crop production trends (2013–2024)
* Enables stakeholders to make **data-driven decisions**
* Covers **installation, database integration, dashboard creation, and embedding**
* Supports interactive analysis through **filters and role-based access**

---

## 📊 Dataset Overview

* **Source:** Ministry of Agriculture & Farmers Welfare (DA\&FW)
* **Time Period:** 2013–2024
* **Seasons Covered:** Kharif, Rabi, Summer
* **Units:** Lakh tonnes (converted for some crops like jute, mesta, and cotton)
* **Preprocessing Steps:**

  * Removed redundant records (e.g., *Total Pulses*, *Cereals*)
  * Imputed or excluded missing data (`@`, `$`, `#`)
  * Converted units for uniformity
  * Standardized crop names
  * Replaced missing seasonal values with `0`

---

## ⚙️ Installation

### 1. Install Docker

```bash
# Verify installation
docker --version
```

### 2. Run Apache Superset in Docker

```bash
docker run -d -p 8080:8088 -e "SUPERSET_SECRET_KEY=mysuperset" --name superset apache/superset:27ff8f2-dev
```

### 3. Create Admin User

```bash
docker exec -it superset superset fab create-admin \
  --username admin \
  --firstname Superset \
  --lastname Admin \
  --email admin@superset.com \
  --password admin
```

### 4. Initialize Superset

```bash
docker exec -it superset superset db upgrade
docker exec -it superset superset load_examples
```

Access Superset at: **[http://localhost:8080](http://localhost:8080)**

---

## 📈 Dashboard Design

### **1. Overall Crop Production View**

* Bar chart: Total crop production over years
* Stacked bar: Seasonal breakdown (Kharif, Rabi, Summer)
* Pie chart: Crop distribution
* Line chart: Decadal trend (2013–2024)
* Heatmap: Seasonal intensity of crops

📷 **Screenshot:**
![Overall View Dashboard](images/overall_view.png)

---

### **2. Specific Crop View**

* Multi-series bar chart: Best & worst production years
* Heatmap: Crop performance across seasons
* Table: Seasonal production metrics and percentages

📷 **Screenshot:**
![Specific View Dashboard](images/specific_view.png)

---

### **3. Interactive Filters**

* Season (Kharif, Rabi, Summer)
* Year (2013–14 → 2023–24)
* Crop Type

📷 **Screenshot:**
![Filters](images/filters.png)

---

## 🔐 Role-Based Access

Configured roles for secure dashboard usage:

* **Admin** – Full access
* **Gamma/Alpha/SQL Lab** – Limited technical access
* **Public (Custom)** – Restricted to crop dashboards

---

## 🌐 Embedding Dashboards

Enabled embedding via `superset_config.py`:

```python
FEATURE_FLAGS = {"EMBEDDED_SUPERSET": True}
ENABLE_PROXY_FIX = True
SESSION_COOKIE_SAMESITE = None
PUBLIC_ROLE_LIKE_GAMMA = True
AUTH_ROLE_PUBLIC = 'Gamma'
WTF_CSRF_ENABLED = False
TALISMAN_ENABLED = False
```

Example HTML embed:

```html
<iframe src="http://localhost:8080/superset/dashboard/p/PxlMk67LoWR/" width="1600" height="1500" frameborder="0"></iframe>
```

---

## ✅ Conclusion & Future Scope

This project demonstrates the **successful integration of Apache Superset** with MySQL to deliver **interactive, role-secured, and embeddable dashboards** for agricultural insights.

**Future Enhancements:**

* Expand data sources (weather, price indices, trade data)
* Enable advanced analytics (forecasting, predictive modeling)
* Improve user experience with **custom filters & visualization options**

---

## 📂 Repository

[GitHub Link](https://github.com/avimalya/Integrating-Superset-with-NPCYF-)

---

