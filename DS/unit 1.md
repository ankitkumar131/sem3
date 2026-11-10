# DS — Unit 1 (Fundamentals of Data Science)

> Exam-prep notes: short definitions, key points, and diagrams.

**Contents**
1. [Importance of Data Science & Types of Data](#1-importance-of-data-science--types-of-data)
2. [Scales of Measurement & Data Formats](#2-scales-of-measurement--data-formats)
3. [Big Data vs Data Science & The Life Cycle](#3-big-data-vs-data-science--the-life-cycle)
4. [Process Models: CRISP-DM, TDSP, SEMMA](#4-process-models-crisp-dm-tdsp-semma)
5. [Applications, DS vs ML vs AI, Roles](#5-applications-ds-vs-ml-vs-ai-roles)
6. [Importance of Mathematical Statistics](#6-importance-of-mathematical-statistics)
7. [Quick Revision](#7-quick-revision)

---

## 1. Importance of Data Science & Types of Data

### 1.1 Importance of Data Science

- **Data Science** = interdisciplinary field that extracts **knowledge and insights** from data using statistics, ML, and domain knowledge.
- Why it matters today: massive data generation (2.5+ quintillion bytes/day) + cheap storage/compute + better algorithms → **data-driven decisions** beat intuition.
- Value: better decisions, prediction of trends, personalization, fraud detection, cost reduction, new products/services.

```mermaid
flowchart LR
    D["Raw DATA"] --> P["Processing &<br/>Analysis"] --> I["INSIGHTS<br/>(patterns, predictions)"] --> A["ACTIONS<br/>(decisions, products)"] --> V["BUSINESS VALUE"]
```

### 1.2 Types of Data (by structure)

| Type | Meaning | Examples |
|---|---|---|
| **Structured** | Fixed schema, rows & columns; easy to store/query | SQL tables, Excel sheets |
| **Semi-structured** | No rigid schema but has **tags/markers** | JSON, XML, HTML, emails, logs |
| **Unstructured** | No predefined format | Images, videos, audio, PDFs, social media text |

```mermaid
flowchart TD
    DATA["Types of Data"] --> S["STRUCTURED (~10%)<br/>relational tables, spreadsheets"]
    DATA --> SS["SEMI-STRUCTURED<br/>JSON, XML, CSV with headers, email"]
    DATA --> US["UNSTRUCTURED (~80-90%)<br/>images, video, audio, free text"]
```

- Also classified by **nature:** Quantitative (numerical: discrete/continuous) vs **Qualitative** (categorical: nominal/ordinal).

---

## 2. Scales of Measurement & Data Formats

### 2.1 Scales of Measurement (NOIR)

```mermaid
flowchart LR
    NO["NOMINAL<br/>labels, no order<br/>(gender, city, blood group)"] --> OR["ORDINAL<br/>+ order, gaps unknown<br/>(rank, satisfaction: low<med<high)"] --> IN["INTERVAL<br/>+ equal gaps, NO true zero<br/>(temperature °C, dates)"] --> RA["RATIO<br/>+ true zero → ratios valid<br/>(height, weight, salary, age)"]
```

| Scale | Order? | Equal intervals? | True zero? | Example | Allowed ops |
|---|---|---|---|---|---|
| **N**ominal | ✘ | ✘ | ✘ | Gender | Count, mode |
| **O**rdinal | ✔ | ✘ | ✘ | Class rank | + median |
| **I**nterval | ✔ | ✔ | ✘ | °C temperature | + mean, std (no ratios: 20°C ≠ 2×10°C) |
| **R**atio | ✔ | ✔ | ✔ | Weight, income | + ratios (80 kg = 2×40 kg) |

*Memory trick: **NOIR** — each level adds one more property.*

### 2.2 Data Formats

| Format | Nature | Example |
|---|---|---|
| **CSV** | Comma-Separated Values — plain text table, 1 row per line | `id,name,age`<br>`1,Amit,21` |
| **JSON** | JavaScript Object Notation — key-value pairs, arrays; lightweight, web APIs | `{"name": "Amit", "age": 21, "skills": ["Python","SQL"]}` |
| **XML** | eXtensible Markup Language — nested **tags**, schema (XSD), verbose | `<person><name>Amit</name><age>21</age></person>` |
| **SQL tables** | Structured relations in RDBMS — rows/columns, types, keys, SQL queries | `SELECT name FROM student WHERE age > 20;` |

- **JSON vs XML:** both semi-structured & human-readable; JSON is lighter & maps to objects directly; XML supports schemas/namespaces.

---

## 3. Big Data vs Data Science & The Life Cycle

### 3.1 Big Data vs Data Science

| Aspect | **Big Data** | **Data Science** |
|---|---|---|
| What | Huge **datasets** (too big for traditional tools) | The **field/methodology** to extract insights from data |
| Focus | Storage, processing, management | Analysis, modelling, prediction |
| Characterized by | **5 V's — Volume, Velocity, Variety, Veracity, Value** | Statistics + ML + domain expertise |
| Tools | Hadoop, Spark, NoSQL, Kafka | Python/R, SQL, ML libraries, visualization |
| Relation | Big Data is the **raw material** | Data Science is the **process** that refines it |

```mermaid
flowchart LR
    BD["BIG DATA<br/>(5 V's)"] -->|"input / raw material"| DS["DATA SCIENCE<br/>(analyse & model)"] -->|"produces"| K["Knowledge &<br/>predictions"]
```

### 3.2 Data Science Life Cycle (generic)

```mermaid
flowchart TD
    A["1. Problem / Business<br/>Understanding"] --> B["2. Data Collection<br/>(sources, formats)"]
    B --> C["3. Data Cleaning &<br/>Pre-processing"]
    C --> D["4. Exploratory Data<br/>Analysis (EDA)"]
    D --> E["5. Model Building<br/>(train ML models)"]
    E --> F["6. Evaluation<br/>(metrics, validation)"]
    F --> G["7. Deployment"]
    G --> H["8. Monitoring &<br/>Maintenance"]
    H -.feedback.-> A
```

---

## 4. Process Models: CRISP-DM, TDSP, SEMMA

### 4.1 CRISP-DM (Cross-Industry Standard Process for Data Mining)

The most widely used, **cyclic** model with 6 phases:

```mermaid
flowchart LR
    BU["1. Business<br/>Understanding"] --> DU["2. Data<br/>Understanding"]
    DU --> DP["3. Data<br/>Preparation"]
    DP --> M["4. Modeling"]
    M --> E["5. Evaluation"]
    E --> D["6. Deployment"]
    D -.new questions.-> BU
    M -.back.-> DP
```

- Key ideas: starts & ends with **business understanding**; data preparation is the most time-consuming phase (~60–70% effort); iterative, not one-way.
- **Why "cyclic"?** Deployment gives new insights → next iteration of the project.

### 4.2 TDSP (Team Data Science Process — Microsoft)

- An **agile, team-based** framework (extends CRISP-DM) with defined **roles** (manager, data scientist, engineer) and tools/infrastructure for collaboration.
- 5 lifecycle stages:

```mermaid
flowchart LR
    B["1. Business<br/>Understanding"] --> DA["2. Data Acquisition<br/>& Understanding"]
    DA --> MO["3. Modeling"]
    MO --> DE["4. Deployment"]
    DE --> CA["5. Customer<br/>Acceptance"]
    CA -.iterate.-> B
```

### 4.3 SEMMA (Sample, Explore, Modify, Model, Assess — SAS)

```mermaid
flowchart LR
    S["1. SAMPLE<br/>select data subset"] --> E["2. EXPLORE<br/>visualize, find patterns"]
    E --> MO["3. MODIFY<br/>clean, transform, select variables"]
    MO --> MD["4. MODEL<br/>apply techniques (regression, trees...)"]
    MD --> A["5. ASSESS<br/>evaluate model usefulness"]
```

| Model | Origin | Focus |
|---|---|---|
| CRISP-DM | Industry consortium | Business-goal driven, cyclic, most popular |
| TDSP | Microsoft | **Team collaboration**, agile, standardized tooling |
| SEMMA | SAS Institute | Data-mining **steps** in SAS EM tool (ignores business phase) |

---

## 5. Applications, DS vs ML vs AI, Roles

### 5.1 Applications of Data Science

- **Healthcare:** disease prediction, medical image analysis, drug discovery
- **Finance:** fraud detection, credit scoring, algorithmic trading
- **E-commerce / Retail:** recommendation systems, demand forecasting, price optimization
- **Transport:** route optimization, self-driving cars
- **Entertainment:** content recommendations (Netflix/Spotify)
- **Others:** spam filtering, weather forecasting, agriculture (crop prediction), sentiment analysis

### 5.2 Data Science vs Machine Learning vs AI

```mermaid
flowchart TD
    subgraph AI["ARTIFICIAL INTELLIGENCE - machines mimicking human intelligence"]
        subgraph ML["MACHINE LEARNING - learn from data, no explicit programming"]
            DL["Deep Learning<br/>(multi-layer neural networks)"]
        end
    end
    DS["DATA SCIENCE<br/>end-to-end insight extraction:<br/>statistics + ML + domain + visualization"] -.uses ML as one tool.-> ML
```

| | AI | ML | Data Science |
|---|---|---|---|
| Goal | Make machines **behave intelligently** | Machines **learn patterns** from data | Extract **insights/knowledge** from data |
| Scope | Broadest | Subset of AI | Interdisciplinary (stats + ML + business) |
| Output | Intelligent agents/systems | Trained models | Reports, predictions, decisions |
| Example | Chatbot, self-driving car | Spam classifier | Analysing sales data for strategy |

### 5.3 Roles in Data Science

| Role | Focus | Typical tasks & tools |
|---|---|---|
| **Data Analyst** | Descriptive: *what happened?* | Dashboards, reports, SQL, Excel, Power BI/Tableau |
| **Data Scientist** | Predictive: *what will happen & why?* | Modelling, statistics, experiments; Python/R, ML libraries |
| **Data Engineer** | Data **pipeline & infrastructure** | ETL, data lakes/warehouses, Spark, Airflow, SQL/NoSQL |
| **ML Engineer** | **Production-izing** models | Model deployment, monitoring, MLOps, Docker, APIs |

```mermaid
flowchart LR
    DE["Data Engineer<br/>(builds pipelines)"] -->|"clean, ready data"| DA["Data Analyst<br/>(reports)"] & SC["Data Scientist<br/>(models)"]
    SC -->|"trained model"| MLE["ML Engineer<br/>(deploys & scales)"] -->|"predictions"| U["Business / Users"]
```

---

## 6. Importance of Mathematical Statistics

- Statistics is the **foundation** of every DS phase — models are statistical in nature, and stats tells us whether a result is real or coincidence.
- Key contributions:

| Area | Use in Data Science |
|---|---|
| **Descriptive statistics** (mean, median, mode, variance, std) | Summarize & understand data (EDA) |
| **Probability & distributions** (Normal, Binomial, Poisson) | Basis of models & assumptions; uncertainty quantification |
| **Inferential statistics** — hypothesis testing, confidence intervals, p-values | Decide if a pattern is statistically significant (A/B testing) |
| **Sampling theory** | Draw valid conclusions from samples of big data |
| **Correlation & regression** | Relationships & prediction between variables |
| **Bayesian statistics** | Update beliefs with evidence (Naive Bayes, spam filters) |

- Without statistics a data scientist risks: wrong sampling → biased models; no significance testing → false discoveries; misinterpreting correlation as causation.

---

## 7. Quick Revision

| Item | One-liner |
|---|---|
| Data science | Extract insights from data (stats + ML + domain) |
| Data types | Structured (tables) · Semi-structured (JSON/XML) · Unstructured (media) |
| NOIR scales | Nominal → Ordinal → Interval → Ratio (each adds a property) |
| Interval vs Ratio | Interval: no true zero (°C); Ratio: true zero (weight) |
| Big Data 5 V's | Volume, Velocity, Variety, Veracity, Value |
| CRISP-DM | BU → DU → Prep → Model → Eval → Deploy (cyclic) |
| TDSP | Microsoft team-based agile version |
| SEMMA | Sample → Explore → Modify → Model → Assess |
| AI ⊃ ML ⊃ DL | DS overlaps and uses ML |
| Roles | Analyst (reports) · Scientist (models) · Engineer (pipelines) · MLE (deployment) |
| Why statistics | Sampling, significance, uncertainty — foundation of valid insights |
