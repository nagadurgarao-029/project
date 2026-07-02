# A Comprehensive Measure of Well-Being

An end-to-end framework and data architecture designed to quantify, analyze, and track multi-dimensional human well-being. This project establishes a composite index by gathering demographic-linked survey insights and mapping them against structural quality-of-life indicators.

## 📌 Project Overview

Traditional metrics like GDP often fail to capture true human prosperity. This project builds a data model to evaluate well-being holistically across several life dimensions (e.g., mental health, financial resilience, and social connectivity). By combining structured surveys with an algorithmic weighting system, the platform generates a dynamic **Well-Being Index** score for individuals and populations.

---

## 📊 Data Architecture (ERD)
<img width="875" height="483" alt="image" src="https://github.com/user-attachments/assets/3bee22f0-0eff-4e69-a7f0-355037f4a671" />



The repository utilizes an Entity-Relationship model designed for relational databases (PostgreSQL/MySQL) to capture framework structures, survey items, user metrics, and final scoring benchmarks.

```mermaid
erDiagram
    INDIVIDUAL ||--o{ SURVEY_RESPONSE : completes
    INDIVIDUAL ||--o{ BENCHMARK_RESULT : achieves
    DIMENSION ||--|{ INDICATOR : contains
    INDICATOR ||--o{ SURVEY_QUESTION : measures
    SURVEY_QUESTION ||--o{ SURVEY_RESPONSE : collects
    WELL_BEING_INDEX ||--|{ DIMENSION : aggregates
    WELL_BEING_INDEX ||--o{ BENCHMARK_RESULT : evaluates

    INDIVIDUAL {
        int individual_id PK
        string age_group
        string gender
        string region
        string employment_status
    }

    WELL_BEING_INDEX {
        int index_id PK
        string index_name
        string framework_version
        date creation_date
    }

    DIMENSION {
        int dimension_id PK
        int index_id FK
        string dimension_name
        float weight_percentage
    }

    INDICATOR {
        int indicator_id PK
        int dimension_id FK
        string indicator_name
        string data_type
    }

    SURVEY_QUESTION {
        int question_id PK
        int indicator_id FK
        string question_text
        string scale_type
    }

    SURVEY_RESPONSE {
        int response_id PK
        int individual_id FK
        int question_id FK
        int selected_value
        datetime submitted_at
    }

    BENCHMARK_RESULT {
        int benchmark_id PK
        int individual_id FK
        int index_id FK
        float calculated_score
        string well_being_tier
        date evaluation_date
    }
```

---

## 🔑 Key Entity Descriptions

*   **`INDIVIDUAL`**: Stores anonymized demographic metadata used to segment and analyze well-being trends across different regions and backgrounds.
*   **`WELL_BEING_INDEX`**: Holds version control configurations for the overarching math framework.
*   **`DIMENSION`**: Categorizes broad sectors of life quality (e.g., Physical Health, Financial Stability, Social Connection) and assigns thematic weights.
*   **`INDICATOR`**: Breaks down dimensions into specific measurable metrics (e.g., Stress Levels, Disposable Income).
*   **`SURVEY_QUESTION`**: Houses individual Likert-scale questions utilized to harvest empirical data.
*   **`SURVEY_RESPONSE`**: Captures raw user-submitted responses linkable back to user demographic brackets.
*   **`BENCHMARK_RESULT`**: Computes, updates, and indexes the individual's definitive well-being score alongside descriptive classifications (e.g., *Thriving*, *Struggling*).

---

## 🚀 Getting Started

### Prerequisites
*   A relational database manager (e.g., **PostgreSQL 15+** or **MySQL 8.0+**).
*   A data visualization tool or notebook backend (e.g., **Python 3.10+**, **Tableau**, or **PowerBI**) to consume the computed scores.

### Installation & Initialization
1. Clone this repository:
   ```bash
   git clone https://github.com
   cd well-being-measure
   ```
2. Set up the schema inside your database target:
   ```bash
   # Example if using PostgreSQL CLI
   psql -u your_user -d well_being_db -f src/db/schema.sql
   ```

---

