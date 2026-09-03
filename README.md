# External Clinical Information Access Analysis

> Identifying information-access friction and specialty differences in U.S. physician EHR use
> 

<aside>

#### 💡 Project Overview

**Scope:** EHR / Clinical Information Access & Usability Analysis

**Data Sources:** 2024 National Electronic Health Records Survey (NEHRS) Public-Use File

**Dataset:** 1,725 U.S. physician records · 69 variables

**Analysis Weight: mailwgt**

**Tools:** Python · Pandas · Statistical Analysis · Plotly

**Output:** Weighted national estimates · Cross-tab analysis · Exploratory statistical testing · Executive dashboard

**KEY FINDING**

**32.0%** of physicians selected the highest ease-of-use response when evaluating their ability to use external clinical information for patient care.

**52.7%** selected "To a great extent" for difficulty finding important information because of large amounts of low-value information.

**APPROACH**

The analysis followed a validation-first workflow:

**Source data → Metadata validation → Response-code audit → Analysis-ready dataset → Weighted estimates → Cross-tab analysis → Pain-point ranking → Executive dashboard**

**QUESTION** 

How effectively does EHR support physicians in accessing and using external clinical information, and where do information-access gaps occur across specialties?

**DECISION CONTEXT**

The analysis aims to identify the strongest evidence of information-access friction and determine which patterns warrant further healthcare product investigation.

**Links:** [[Google Colab Notebook](https://colab.research.google.com/drive/1DXRi-hHKym0g5b6d0-65M1bFShJk5OKP?usp=sharing)] | [Notion](https://app.notion.com/p/External-Clinical-Information-Access-Analysis-3cff89a0cfc48057907cfcebc492c145?source=copy_link)]

</aside>

## 1. Problem Context

Physicians may receive external clinical information through different channels, including scanned documents, separate electronic portals, or information integrated directly into the EHR.

However, the availability of information does not necessarily mean that it is easy to find or use.

This creates an important distinction between **information availability** and **information usability**.

This project focuses on that gap by examining how physicians access, find, and use external clinical information in their clinical workflow.

## 2. Analytical Framework

The analysis was structured into four layers:

### 01. Overall usability

How effectively do physicians report using external clinical information for patient care?

**Primary variable:** `EXTINFO_EFF`

### 02. Information-access friction and delivery patterns

Where do information-finding difficulties, missing information, or fragmented access patterns appear?

**Key variables:**

- `EXTINFO_LOW`
- `EXTINFO_REC`
- `EXTINFO_KEY`
- `EXTINFO_INT`
- `EXTINFO_SCN`
- `EXTINFO_PORT`

### 03. Specialty differences

Does information-finding difficulty differ across primary care, medical specialties, and surgical specialties?

**Dimension:** `speccat`

### 04. EHR satisfaction relationship

Does the distribution of information-finding difficulty differ across EHR satisfaction groups?

**Variables:** `EHRSAT` × `EXTINFO_LOW`

## 3. Data Preparation & Validation

### **Step 1: Data Ingestion & Initial Validation**

The 2024 NEHRS Public-Use File was loaded and validated for record count, variable count, variable names, and data structure.

**Result:** 1,725 physician records and 69 variables.

### **Step 2: Variable Identification**

Official Stata metadata and variable labels were inspected to verify the meaning of candidate variables before analysis.

This ensured that analytical variables were selected based on their official definitions rather than inferred from variable names alone.

### **Step 3: Response-Code Audit**

Response codes for the target variables were audited against the official NEHRS response structure.

Non-substantive responses such as **Blank, Don't know, and Not Applicable** were identified separately from substantive responses.

### Step 4: Official Value Label Validation

Observed numeric response codes were compared with the official NEHRS value labels before being converted into analysis-ready categories.

### Step 5: Analysis-Ready Dataset

Validated response codes were converted into analysis-ready categorical labels while preserving the original response meanings.

Non-substantive responses were retained in the source data and excluded from valid-response denominators where appropriate.

## 4. Weighted Analysis

Because NEHRS is a physician survey, national estimates were calculated using the provided `mailwgt` survey weight.

Weighted percentages represent the estimated distribution of the physician population represented by the survey rather than the simple percentage of the 1,725 sampled records.

## 5. Key Findings

### 01. Overall Ease of Using External Clinical Information

> **32.0% selected the highest ease-of-use response**
> 
> 
> Physicians were asked to rate how effectively they could use external clinical information for patient care.
> 

| Response | Weighted valid-response share |
| --- | --- |
| Very | **32.0%** |
| Somewhat | **55.5%** |
| Not at all | **12.6%** |

The largest response group was **"Somewhat" at 55.5%**, while **32.0%** selected the highest response, "Very."

### 02. Difficulty Finding Important Information Is the Strongest Direct Friction Signal

> **52.7% reported the highest level of difficulty**
> 
> 
> The strongest direct friction signal was difficulty finding important information because of large amounts of low-value information.
> 

#### Information-Access Signal Ranking

| Information-access signal | High-friction response | Weighted share |
| --- | --- | --- |
| **Difficulty finding important information** | To a great extent | **52.7%** |
| Scanned/PDF records | Often | **48.1%** |
| Entire record unavailable | To a great extent | **35.6%** |
| Not integrated within EHR | Never | **33.9%** |
| Key information missing | To a great extent | **25.0%** |
| Separate portal access | Often | **21.9%** |
| Difficulty using information effectively | Not at all | **12.6%** |

#### **Interpretation:**

The ranking combines several types of information-access signals.

**Direct friction or information-gap responses** include difficulty finding information, missing records, missing key information, lack of EHR integration, and difficulty using information effectively.

**Access-pattern responses** include scanned/PDF records and separate portal access.

Therefore, the **52.7% result represents the strongest direct friction signal**, while the 48.1% scanned/PDF result describes how external information is commonly accessed rather than directly measuring dissatisfaction or difficulty.

### 03. Information-Finding Difficulty Differs Across Specialties

The proportion selecting **"To a great extent"** for information-finding difficulty was:

| Specialty | To a great extent |
| --- | --- |
| Primary care | **48.1%** |
| Medical specialty | **56.7%** |
| Surgical specialty | **55.4%** |

An exploratory unweighted chi-square test indicated a statistically significant association between specialty category and information-finding difficulty.

**p = 0.0006**

#### **Interpretation:**

Medical and surgical specialties showed higher proportions of the highest-level information-finding difficulty response than primary care. This indicates that information-finding difficulty is not distributed identically across specialty groups.

#### **Analytical Boundary:**

The analysis identifies an association between specialty category and response distribution. It does not establish that specialty itself causes greater information-access difficulty.

### 04. Information-Finding Difficulty Varies Across EHR Satisfaction Groups

Among physicians who reported being **Very dissatisfied** with their EHR:

> **84.9% selected "To a great extent" for information-finding difficulty.**
> 

| EHR satisfaction | To a great extent | To some extent | Not at all |
| --- | --- | --- | --- |
| Very satisfied | 40.5% | 49.0% | 10.4% |
| Somewhat satisfied | 49.9% | 45.6% | 4.6% |
| Neither | 68.4% | 31.3% | 0.3% |
| Somewhat dissatisfied | 60.4% | 35.2% | 4.5% |
| **Very dissatisfied** | **84.9%** | 11.7% | 3.4% |

An exploratory unweighted chi-square test indicated that the response distribution differed across EHR satisfaction groups.

**p < 0.0001**

#### **Interpretation:**

The highest level of information-finding difficulty was substantially more prevalent among physicians who reported being very dissatisfied with their EHR. This relationship provides an evidence-based area for further investigation.

#### **Analytical Boundary:**

This analysis identifies an association between EHR satisfaction and information-finding difficulty. It does not establish that information-access friction causes EHR dissatisfaction.

## 6. Evidence Summary

The findings form a connected evidence chain:

#### 01. Overall usability

**32.0%** selected the highest ease-of-use response.

↓

#### 02. Strongest direct friction signal

**52.7%** reported difficulty finding important information to a great extent.

↓

#### 03. Information delivery and integration

**48.1%** reported scanned/PDF information as "Often," while **33.9%** reported that external information was "Never" integrated within the EHR.

↓

#### 04. Specialty variation

The highest-level information-finding difficulty response was:

**56.7% Medical specialty**

**55.4% Surgical specialty**

**48.1% Primary care**

↓

#### 05. EHR satisfaction association

**84.9%** of very dissatisfied EHR users reported information-finding difficulty to a great extent.

## 7. Product Implications

The survey identifies where information-access friction appears, but does not determine the specific product intervention that would solve it.

The findings therefore define **areas for further product discovery**, rather than validated feature requirements.

### Opportunity 01. Improve Information Findability

The strongest direct friction signal was difficulty finding important information amid large amounts of low-value information. 

A potential area for further investigation is whether information prioritization, search, filtering, or relevant-information surfacing could help physicians locate clinically important information more efficiently.

### Opportunity 02. Reduce Information Fragmentation

The frequent presence of scanned/PDF records and separate portal access suggests an opportunity to investigate how external information is distributed across formats and access points. 

Further product research could examine whether physicians need to navigate between multiple systems or formats to retrieve clinically relevant information.

### Opportunity 03. Investigate Specialty-Specific Information Needs

Medical and surgical specialties showed higher proportions of the highest-level information-finding difficulty response than primary care.

Further research could examine whether information volume, external data sources, clinically relevant information, or information-prioritization needs differ by specialty.

## 8. Analytical Boundaries & Limitations

#### Survey weighting:

National estimates use the NEHRS-provided `mailwgt`.

#### Valid-response denominator:

Non-substantive responses such as Blank, Don't know, and Not Applicable were excluded from valid-response denominators where appropriate.

#### Statistical testing:

The specialty and EHR satisfaction chi-square tests were exploratory unweighted tests and were not adjusted for the full complex survey design.

#### Causality:

The analysis identifies response patterns and associations.

It does not establish:

- causation
- that information-access friction causes EHR dissatisfaction
- physician productivity impact
- clinical outcomes
- financial impact
- effectiveness of a specific product intervention

## 9. Dashboard: External Clinical Information Access & Friction Analysis

The dashboard summarizes the analysis across four views:

#### **01. Overall Effectiveness**

How effectively physicians report using external clinical information.

#### **02. Information-Access Signals**

The strongest direct friction signals and external information access patterns.

#### **03. Specialty Differences**

How information-finding difficulty varies across physician specialty groups.

#### **04. EHR Satisfaction Relationship**

How information-finding difficulty is distributed across EHR satisfaction groups.

![Screenshot 2026-09-03 at 10.46.57 PM.png](External%20Clinical%20Information%20Access%20Analysis/Screenshot_2026-09-03_at_10.46.57_PM.png<img width="1507" height="914" alt="Screenshot_2026-09-03_at_10 46 57_PM" src="https://github.com/user-attachments/assets/061e17ae-ce59-4deb-b40c-02f49d5a4e88" />
)

## 10. Key Learning

My healthcare product design background influenced how the analysis was framed.

Rather than treating the survey as a collection of satisfaction scores, I approached the data as evidence for identifying where the physician information-access workflow may warrant deeper investigation.

The analytical process therefore moves from:

**Survey response → Evidence → Pattern → Product question**

rather than:

**Survey response → Assumed problem → Feature solution**

This project reinforced that healthcare product analytics requires more than calculating survey percentages.

The key analytical work was validating the meaning of survey variables, correctly handling response categories and denominators, distinguishing direct friction from access patterns, and maintaining a clear boundary between association and causality.

The final analysis translates survey evidence into product questions without assuming a specific solution before the evidence supports it.

#### View Pipeline Source Code (Python)

- STEP 1: DATA INGESTION & INITIAL VALIDATION
    
    ```python
    # ============================================================
    # STEP 1: DATA INGESTION & INITIAL VALIDATION
    # 2024 National Electronic Health Records Survey (NEHRS)
    # ============================================================
    #
    # Purpose:
    # - Load the official 2024 NEHRS Public-Use File directly
    #   from the project's GitHub repository.
    # - Preserve the downloaded source data without modification.
    # - Confirm the dataset can be read successfully.
    # - Inspect the basic structure before any analytical work.
    #
    # Analytical rule:
    # No variable meaning or analytical assumption is made here.
    # Variable definitions will be validated against the official
    # 2024 NEHRS Data Dictionary before analysis.
    # ============================================================
    
    import pandas as pd
    import numpy as np
    
    # ------------------------------------------------------------
    # 1. Official project source
    # ------------------------------------------------------------
    
    GITHUB_RAW_URL = (
        "https://raw.githubusercontent.com/"
        "ej86/nehrs-ehr-clinical-information-access-analysis/"
        "main/nehrs2024-Stata.dta"
    )
    
    # ------------------------------------------------------------
    # 2. Load the raw Stata dataset directly from GitHub
    # ------------------------------------------------------------
    
    nehrs_raw = pd.read_stata(
        GITHUB_RAW_URL,
        convert_categoricals=False
    )
    
    # ------------------------------------------------------------
    # 3. Basic load validation
    # ------------------------------------------------------------
    
    if nehrs_raw.empty:
        raise ValueError(
            "The NEHRS dataset loaded successfully, "
            "but contains zero records."
        )
    
    # ------------------------------------------------------------
    # 4. Initial structural report
    # ------------------------------------------------------------
    
    print("=" * 72)
    print("STEP 1. DATA INGESTION & INITIAL VALIDATION")
    print("=" * 72)
    
    print(f"Source       : GitHub / ej86/nehrs-ehr-clinical-information-access-analysis")
    print(f"Dataset      : 2024 NEHRS Public-Use File")
    print(f"File         : nehrs2024-Stata.dta")
    print(f"Records      : {nehrs_raw.shape[0]:,}")
    print(f"Variables    : {nehrs_raw.shape[1]:,}")
    
    print("\n" + "=" * 72)
    print("FIRST 5 RECORDS")
    print("=" * 72)
    
    display(nehrs_raw.head())
    
    print("\n" + "=" * 72)
    print("VARIABLE NAMES")
    print("=" * 72)
    
    print(nehrs_raw.columns.tolist())
    
    print("\n" + "=" * 72)
    print("DATA TYPES")
    print("=" * 72)
    
    display(
        nehrs_raw.dtypes
        .rename("dtype")
        .to_frame()
    )
    
    print("\n" + "=" * 72)
    print("LOAD STATUS: SUCCESS")
    print("=" * 72)
    ```
    
- STEP 2: VARIABLE IDENTIFICATION (META-DATA EXTRACTION)
    
    ```python
    # ============================================================
    # STEP 2: VARIABLE IDENTIFICATION (META-DATA EXTRACTION)
    # ============================================================
    # Purpose:
    # Extract official Stata variable labels stored inside the .dta
    # file to confirm the true meaning of all 69 variables.
    # ============================================================
    
    GITHUB_RAW_URL = (
        "https://raw.githubusercontent.com/"
        "ej86/nehrs-ehr-clinical-information-access-analysis/"
        "main/nehrs2024-Stata.dta"
    )
    
    # 1. Read metadata (variable labels) directly from Stata file
    with pd.read_stata(GITHUB_RAW_URL, iterator=True) as reader:
        variable_labels = reader.variable_labels()
    
    # 2. Build structured mapping dataframe
    var_mapping = pd.DataFrame(
        list(variable_labels.items()),
        columns=["variable", "variable_label"]
    )
    
    pd.set_option('display.max_rows', None)
    
    print("=" * 72)
    print("STEP 2: ALL 69 VARIABLE LABELS FROM STATA METADATA")
    print("=" * 72)
    print(f"Total Variables Extracted : {len(var_mapping)}")
    display(var_mapping)
    print("=" * 72)
    ```
    
- STEP 3: TARGET VARIABLE DATA QUALITY & RESPONSE CODE AUDIT
👉🏻 Purpose: Audit the observed response codes for the analytical variables using the official 2024 NEHRS response coding. Special response codes are reported separately rather than being treated as analytical responses.
    
    ```python
    # ============================================================
    # STEP 3: TARGET VARIABLE DATA QUALITY & RESPONSE CODE AUDIT
    # ============================================================
    
    # ------------------------------------------------------------
    # 1. Define analytical target variables
    # ------------------------------------------------------------
    
    target_vars = [
        "speccat",
        "nsearchfreq",
        "cinpoc",
        "intphi",
        "eusephiout",
        "extinfo_eff",
        "extinfo_scn",
        "extinfo_port",
        "extinfo_int",
        "extinfo_rec",
        "extinfo_key",
        "extinfo_low",
        "extinfo_oth",
        "ehrsat",
        "hieqoc",
        "hieeff"
    ]
    
    # ------------------------------------------------------------
    # 2. Validate that all target variables exist
    # ------------------------------------------------------------
    
    missing_target_vars = [
        var for var in target_vars
        if var not in nehrs_raw.columns
    ]
    
    if missing_target_vars:
        raise ValueError(
            "Required target variables are missing: "
            f"{missing_target_vars}"
        )
    
    # ------------------------------------------------------------
    # 3. Audit observed response codes
    # ------------------------------------------------------------
    
    audit_records = []
    total_records = len(nehrs_raw)
    
    for var in target_vars:
    
        series = nehrs_raw[var]
    
        # Official NEHRS special response codes
        blank_mask = series == -9
        unknown_mask = series == -8
        not_applicable_mask = series == -7
    
        # Analytical response codes are positive values
        analytical_mask = series > 0
    
        # Any remaining negative value is retained for investigation
        other_negative_mask = (
            (series < 0)
            & (~blank_mask)
            & (~unknown_mask)
            & (~not_applicable_mask)
        )
    
        audit_records.append({
            "variable": var,
            "analytical_response_count": int(analytical_mask.sum()),
            "analytical_response_pct": round(
                analytical_mask.sum() / total_records * 100, 1
            ),
            "blank_-9_count": int(blank_mask.sum()),
            "dont_know_-8_count": int(unknown_mask.sum()),
            "not_applicable_-7_count": int(not_applicable_mask.sum()),
            "other_negative_count": int(other_negative_mask.sum())
        })
    
    audit_df = pd.DataFrame(audit_records)
    
    # ------------------------------------------------------------
    # 4. Display response-code audit
    # ------------------------------------------------------------
    
    print("=" * 72)
    print("STEP 3: TARGET VARIABLE RESPONSE CODE AUDIT")
    print("=" * 72)
    
    print(
        f"Total Physician Records Examined : {total_records:,}"
    )
    
    print(
        f"Target Variables Audited         : {len(target_vars)}"
    )
    
    print("-" * 72)
    
    display(audit_df)
    
    print("=" * 72)
    
    # ------------------------------------------------------------
    # 5. Integrity checks
    # ------------------------------------------------------------
    
    assert audit_df["other_negative_count"].sum() == 0, (
        "Observed negative codes exist outside the defined "
        "official special-response codes. Review before proceeding."
    )
    
    assert len(audit_df) == len(target_vars), (
        "Not all target variables were included in the audit."
    )
    
    print(
        "VALIDATION STATUS: ALL OBSERVED NEGATIVE CODES ARE "
        "ACCOUNTED FOR BY THE OFFICIAL RESPONSE-CODE STRUCTURE."
    )
    
    print("=" * 72)
    ```
    
- STEP 4.1: OFFICIAL VALUE LABEL AUDIT
👉🏻 Purpose: Validate the observed response codes for all analytical variables against the official 2024 NEHRS code definitions. Numeric codes are retained as provided in the source data. No analytical recoding is performed at this stage.
    
    ```python
    # ============================================================
    # STEP 4.1: OFFICIAL VALUE LABEL AUDIT
    # ============================================================
    
    # Complete analytical variable set
    target_vars = [
        "speccat",
        "nsearchfreq",
        "cinpoc",
        "intphi",
        "eusephiout",
        "extinfo_eff",
        "extinfo_scn",
        "extinfo_port",
        "extinfo_int",
        "extinfo_rec",
        "extinfo_key",
        "extinfo_low",
        "extinfo_oth",
        "ehrsat",
        "hieqoc",
        "hieeff"
    ]
    
    # Official code definitions from the 2024 NEHRS Codebook
    official_codes = {
        "speccat": {
            1: "Primary care specialty",
            2: "Surgical specialty",
            3: "Medical specialty"
        },
        "nsearchfreq": {
            -9: "Blank",
            -8: "Don't know",
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never"
        },
        "cinpoc": {
            -9: "Blank",
            -8: "Don't know",
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never",
            6: "I do not see patients outside my medical organization"
        },
        "intphi": {
            -9: "Blank",
            -8: "Don't know",
            1: "Yes",
            2: "No",
            4: "Not Applicable"
        },
        "eusephiout": {
            -9: "Blank",
            -8: "Don't know",
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never"
        },
        "extinfo_eff": {
            -9: "Blank",
            -8: "Don't know",
            1: "Very",
            2: "Somewhat",
            3: "Not at all",
            4: "Not Applicable"
        },
        "extinfo_scn": {
            -9: "Blank",
            -8: "Don't know",
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never"
        },
        "extinfo_port": {
            -9: "Blank",
            -8: "Don't know",
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never"
        },
        "extinfo_int": {
            -9: "Blank",
            -8: "Don't know",
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never"
        },
        "extinfo_rec": {
            -9: "Blank",
            1: "To a great extent",
            2: "To some extent",
            3: "Not at all",
            4: "Not applicable"
        },
        "extinfo_key": {
            -9: "Blank",
            1: "To a great extent",
            2: "To some extent",
            3: "Not at all",
            4: "Not applicable"
        },
        "extinfo_low": {
            -9: "Blank",
            1: "To a great extent",
            2: "To some extent",
            3: "Not at all",
            4: "Not applicable"
        },
        "extinfo_oth": {
            -9: "Blank",
            1: "To a great extent",
            2: "To some extent",
            3: "Not at all",
            4: "Not applicable"
        },
        "ehrsat": {
            -9: "Blank",
            -7: "Not applicable, no EHR",
            1: "Very satisfied",
            2: "Somewhat satisfied",
            3: "Neither satisfied nor dissatisfied",
            4: "Somewhat dissatisfied",
            5: "Very dissatisfied",
            6: "Not applicable"
        },
        "hieqoc": {
            -9: "Blank",
            1: "Strongly agree",
            2: "Somewhat agree",
            3: "Somewhat disagree",
            4: "Strongly disagree",
            5: "Not Applicable"
        },
        "hieeff": {
            -9: "Blank",
            1: "Strongly agree",
            2: "Somewhat agree",
            3: "Somewhat disagree",
            4: "Strongly disagree",
            5: "Not Applicable"
        }
    }
    
    # Validate every observed code against the official definitions
    audit_records = []
    
    for var in target_vars:
        observed_codes = sorted(nehrs_raw[var].dropna().unique().tolist())
        official = official_codes[var]
    
        unexpected = [
            code for code in observed_codes
            if code not in official
        ]
    
        labels = [
            f"{code}: {official[code]}"
            for code in observed_codes
            if code in official
        ]
    
        audit_records.append({
            "variable": var,
            "observed_codes": ",".join(map(str, observed_codes)),
            "official_code_labels": "; ".join(labels),
            "unexpected_codes": ",".join(map(str, unexpected))
        })
    
    value_code_audit = pd.DataFrame(audit_records)
    
    print("=" * 72)
    print("STEP 4.1: OFFICIAL VALUE LABEL AUDIT")
    print("=" * 72)
    
    display(value_code_audit)
    
    if value_code_audit["unexpected_codes"].astype(str).str.len().sum() == 0:
        print("\nVALIDATION STATUS: ALL OBSERVED CODES MATCH THE OFFICIAL 2024 NEHRS CODEBOOK.")
    else:
        print("\nVALIDATION STATUS: UNEXPECTED CODES REQUIRE REVIEW.")
    
    print("=" * 72)
    ```
    
- STEP 4.2: TARGET VARIABLE UNIQUE VALUE DISTRIBUTION
👉🏻 Purpose: Inspect all actual unique numeric codes present in the raw dataset for the 16 target variables before applying Codebook mapping.
    
    ```python
    # ============================================================
    # STEP 4.2: TARGET VARIABLE UNIQUE VALUE DISTRIBUTION
    # ============================================================
    # AI Hallucination Safeguard:
    # No text label is assumed or assigned in this cell.
    # ============================================================
    
    target_vars = [
        "speccat", "nsearchfreq", "cinpoc", "intphi", "eusephiout",
        "extinfo_eff", "extinfo_scn", "extinfo_port", "extinfo_int",
        "extinfo_rec", "extinfo_key", "extinfo_low", "ehrsat",
        "hieeff", "hieqoc", "mailwgt"
    ]
    
    print("=" * 72)
    print("STEP 4.2: ACTUAL UNIQUE NUMERIC VALUES IN DATASET")
    print("=" * 72)
    
    unique_summary = []
    
    for var in target_vars:
        series = nehrs_raw[var]
        unique_vals = sorted(series.unique().tolist())
        num_unique = len(unique_vals)
    
        # Separate positive (valid) codes from negative (special) codes
        positive_codes = [v for v in unique_vals if v > 0]
        negative_codes = [v for v in unique_vals if v <= 0]
    
        unique_summary.append({
            "variable": var,
            "total_unique_codes": num_unique,
            "positive_codes (>0)": positive_codes,
            "negative_codes (<=0)": negative_codes
        })
    
    unique_df = pd.DataFrame(unique_summary)
    display(unique_df)
    print("=" * 72)
    ```
    
- STEP 4.3: OFFICIAL RESPONSE LABEL MAPPING
👉🏻 Purpose: Apply the official 2024 NEHRS response labels to the analytical variables used in this project.
    
    ```python
    # ============================================================
    # STEP 4.3: OFFICIAL RESPONSE LABEL MAPPING
    # ============================================================
    #
    # The labels below follow the official 2024 NEHRS
    # Public Use File Layout.
    #
    # No analytical grouping or recoding is performed here.
    # Original numeric response codes are preserved.
    # ============================================================
    
    official_response_labels = {
    
        "emedrec": {
            1: "Yes",
            2: "No",
            -7: "Not applicable",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "speccat": {
            1: "Primary care specialty",
            2: "Surgical specialty",
            3: "Medical specialty"
        },
    
        "nsearchfreq": {
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "intphi": {
            1: "Yes",
            2: "No",
            4: "Not Applicable",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "cinpoc": {
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never",
            6: "I do not see patients outside my medical organization",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "eusephiout": {
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "extinfo_eff": {
            1: "Very",
            2: "Somewhat",
            3: "Not at all",
            4: "Not Applicable",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "extinfo_scn": {
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "extinfo_port": {
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "extinfo_int": {
            1: "Often",
            2: "Sometimes",
            3: "Rarely",
            4: "Never",
            -8: "Don't know",
            -9: "Blank"
        },
    
        "extinfo_rec": {
            1: "To a great extent",
            2: "To some extent",
            3: "Not at all",
            4: "Not applicable",
            -9: "Blank"
        },
    
        "extinfo_key": {
            1: "To a great extent",
            2: "To some extent",
            3: "Not at all",
            4: "Not applicable",
            -9: "Blank"
        },
    
        "extinfo_low": {
            1: "To a great extent",
            2: "To some extent",
            3: "Not at all",
            4: "Not applicable",
            -9: "Blank"
        },
    
        "extinfo_oth": {
            1: "To a great extent",
            2: "To some extent",
            3: "Not at all",
            4: "Not applicable",
            -9: "Blank"
        },
    
        "ehrsat": {
            1: "Very satisfied",
            2: "Somewhat satisfied",
            3: "Neither satisfied nor dissatisfied",
            4: "Somewhat dissatisfied",
            5: "Very dissatisfied",
            6: "Not applicable",
            -7: "Not applicable, no EHR",
            -9: "Blank"
        },
    
        "hieqoc": {
            1: "Strongly agree",
            2: "Somewhat agree",
            3: "Somewhat disagree",
            4: "Strongly disagree",
            5: "Not Applicable",
            -9: "Blank"
        },
    
        "hieeff": {
            1: "Strongly agree",
            2: "Somewhat agree",
            3: "Somewhat disagree",
            4: "Strongly disagree",
            5: "Not Applicable",
            -9: "Blank"
        }
    }
    
    # ------------------------------------------------------------
    # Validate mapping against variables present in the dataset
    # ------------------------------------------------------------
    
    missing_mapping_variables = [
        variable
        for variable in official_response_labels
        if variable not in nehrs_raw.columns
    ]
    
    if missing_mapping_variables:
        raise ValueError(
            "Variables defined in the response mapping but missing "
            f"from the dataset: {missing_mapping_variables}"
        )
    
    # ------------------------------------------------------------
    # Validate observed codes against the official mapping
    # ------------------------------------------------------------
    
    mapping_audit_rows = []
    
    for variable, labels in official_response_labels.items():
    
        observed_values = (
            pd.to_numeric(
                nehrs_raw[variable],
                errors="coerce"
            )
            .dropna()
            .unique()
        )
    
        observed_codes = sorted(
            observed_values.tolist()
        )
    
        unexpected_codes = [
            code
            for code in observed_codes
            if code not in labels
        ]
    
        mapping_audit_rows.append({
            "variable": variable,
            "observed_codes": ", ".join(
                str(code) for code in observed_codes
            ),
            "official_code_labels": "; ".join(
                f"{code}: {labels[code]}"
                for code in observed_codes
                if code in labels
            ),
            "unexpected_codes": ", ".join(
                str(code) for code in unexpected_codes
            )
        })
    
    response_mapping_audit = pd.DataFrame(
        mapping_audit_rows
    )
    
    # ------------------------------------------------------------
    # Display validation result
    # ------------------------------------------------------------
    
    print("=" * 72)
    print("STEP 4.3: OFFICIAL RESPONSE LABEL MAPPING")
    print("=" * 72)
    
    display(response_mapping_audit)
    
    unexpected_count = (
        response_mapping_audit["unexpected_codes"]
        .ne("")
        .sum()
    )
    
    print("\n" + "=" * 72)
    
    if unexpected_count == 0:
        print(
            "VALIDATION STATUS: ALL OBSERVED CODES ARE COVERED "
            "BY THE OFFICIAL RESPONSE MAPPING."
        )
    else:
        print(
            "VALIDATION STATUS: REVIEW REQUIRED."
        )
        print(
            f"Variables with unexpected codes: {unexpected_count}"
        )
    
    print("=" * 72)
    ```
    
- STEP 4.4: ANALYSIS-READY DATASET CONSTRUCTION
👉🏻 Purpose: Create an analysis-ready dataset while preserving the original NEHRS numeric response codes and adding official response labels as separate columns.
    
    ```python
    # ============================================================
    # STEP 4.4: ANALYSIS-READY DATASET CONSTRUCTION
    # ============================================================
    
    analysis_variables = [
        "speccat",
        "nsearchfreq",
        "intphi",
        "cinpoc",
        "eusephiout",
        "extinfo_eff",
        "extinfo_scn",
        "extinfo_port",
        "extinfo_int",
        "extinfo_rec",
        "extinfo_key",
        "extinfo_low",
        "extinfo_oth",
        "ehrsat",
        "hieqoc",
        "hieeff",
        "mailwgt"
    ]
    
    # ------------------------------------------------------------
    # Verify all required variables are available
    # ------------------------------------------------------------
    
    missing_analysis_variables = [
        variable
        for variable in analysis_variables
        if variable not in nehrs_raw.columns
    ]
    
    if missing_analysis_variables:
        raise ValueError(
            "Required analysis variables are missing from the dataset: "
            f"{missing_analysis_variables}"
        )
    
    # ------------------------------------------------------------
    # Preserve original numeric variables
    # ------------------------------------------------------------
    
    nehrs_analysis = nehrs_raw[
        analysis_variables
    ].copy()
    
    # ------------------------------------------------------------
    # Add official response-label columns (_label)
    # ------------------------------------------------------------
    
    for variable in analysis_variables:
    
        if variable in official_response_labels:
    
            label_column = f"{variable}_label"
    
            nehrs_analysis[label_column] = (
                nehrs_analysis[variable]
                .map(official_response_labels[variable])
            )
    
    # ------------------------------------------------------------
    # Validate that all non-missing coded responses received
    # an official label
    # ------------------------------------------------------------
    
    label_validation_rows = []
    
    for variable in analysis_variables:
    
        if variable not in official_response_labels:
            continue
    
        label_column = f"{variable}_label"
    
        coded_values = (
            pd.to_numeric(
                nehrs_analysis[variable],
                errors="coerce"
            )
        )
    
        unlabeled_mask = (
            coded_values.notna()
            & nehrs_analysis[label_column].isna()
        )
    
        label_validation_rows.append({
            "variable": variable,
            "unlabeled_observations": int(
                unlabeled_mask.sum()
            )
        })
    
    label_validation = pd.DataFrame(
        label_validation_rows
    )
    
    # ------------------------------------------------------------
    # Display dataset structure
    # ------------------------------------------------------------
    
    print("=" * 72)
    print("STEP 4.4: ANALYSIS-READY DATASET")
    print("=" * 72)
    
    print(
        f"Rows: {nehrs_analysis.shape[0]:,}"
    )
    
    print(
        f"Columns: {nehrs_analysis.shape[1]:,}"
    )
    
    print("\n=== ANALYSIS VARIABLES ===")
    print(analysis_variables)
    
    print("\n=== LABEL VALIDATION ===")
    display(label_validation)
    
    # ------------------------------------------------------------
    # Integrity checks
    # ------------------------------------------------------------
    
    total_unlabeled = (
        label_validation["unlabeled_observations"]
        .sum()
    )
    
    assert total_unlabeled == 0, (
        "One or more observed response codes do not have "
        "an official response label."
    )
    
    assert len(nehrs_analysis) == len(nehrs_raw), (
        "Row count changed during analysis dataset construction."
    )
    
    # ------------------------------------------------------------
    # Downstream Compatibility Mapping (_lbl aliases & nehrs_clean)
    # ------------------------------------------------------------
    
    # Add _lbl aliases so Step 5.1, 5.2, and 5.3 can reference _lbl without KeyError
    for variable in analysis_variables:
        if f"{variable}_label" in nehrs_analysis.columns:
            nehrs_analysis[f"{variable}_lbl"] = nehrs_analysis[f"{variable}_label"]
    
    # Assign alias dataframe for downstream pipeline cells
    nehrs_clean = nehrs_analysis
    
    print("\n" + "=" * 72)
    print(
        "VALIDATION STATUS: ANALYSIS-READY DATASET CREATED "
        "WITH DUAL-SUFFIX ALIASES (_label & _lbl) FOR FULL PIPELINE COMPATIBILITY."
    )
    print("=" * 72)
    ```
    
- STEP 5.1: WEIGHTED NATIONAL ESTIMATES & VALID RESPONSE RATES
👉🏻 Purpose: Calculate weighted national estimates and valid-response percentages for the 16 analytical variables.
    
    ```python
    # ============================================================
    # STEP 5.1: WEIGHTED NATIONAL ESTIMATES & VALID RESPONSE RATES
    # ============================================================
    #
    # Purpose:
    # Calculate weighted national estimates and valid-response
    # percentages for the 16 analytical variables.
    #
    # Analytical definition:
    # - Weighted national estimate = sum of mailwgt by response category.
    # - Valid-response percentage uses only substantive responses.
    # - Blank, Don't know, Not Applicable, and Not applicable/no EHR
    #   are excluded from the valid-response denominator.
    # - Original response categories are preserved.
    # - No analytical categories are combined in this step.
    # ============================================================
    
    # ------------------------------------------------------------
    # 1. Session state validation
    # ------------------------------------------------------------
    
    if "nehrs_clean" not in globals() or nehrs_clean is None:
        raise NameError(
            "'nehrs_clean' was not found. Please run STEP 4.4 first."
        )
    
    required_columns = [
        "mailwgt",
        "speccat",
        "nsearchfreq",
        "cinpoc",
        "intphi",
        "eusephiout",
        "extinfo_eff",
        "extinfo_scn",
        "extinfo_port",
        "extinfo_int",
        "extinfo_rec",
        "extinfo_key",
        "extinfo_low",
        "ehrsat",
        "hieeff",
        "hieqoc"
    ]
    
    missing_columns = [
        col for col in required_columns
        if col not in nehrs_clean.columns
    ]
    
    if missing_columns:
        raise ValueError(
            f"Required columns are missing: {missing_columns}"
        )
    
    # ------------------------------------------------------------
    # 2. Validate survey weights
    # ------------------------------------------------------------
    
    weight = pd.to_numeric(
        nehrs_clean["mailwgt"],
        errors="coerce"
    )
    
    if weight.isna().any():
        raise ValueError(
            "Missing or non-numeric values were found in mailwgt."
        )
    
    if (weight < 0).any():
        raise ValueError(
            "Negative survey weights were found in mailwgt."
        )
    
    if (weight.sum() <= 0):
        raise ValueError(
            "The total survey weight is not positive."
        )
    
    # ------------------------------------------------------------
    # 3. Analytical variables
    # ------------------------------------------------------------
    
    all_target_vars = [
        "speccat",
        "nsearchfreq",
        "cinpoc",
        "intphi",
        "eusephiout",
        "extinfo_eff",
        "extinfo_scn",
        "extinfo_port",
        "extinfo_int",
        "extinfo_rec",
        "extinfo_key",
        "extinfo_low",
        "ehrsat",
        "hieeff",
        "hieqoc"
    ]
    
    # ------------------------------------------------------------
    # 4. Define non-substantive response labels
    # ------------------------------------------------------------
    #
    # These labels are excluded from the valid-response denominator.
    # The labels are taken from the official response mapping created
    # in STEP 4.3.
    #
    # Categories not listed here remain part of the valid denominator.
    
    non_substantive_labels = {
        "Blank",
        "Don't know",
        "Not Applicable",
        "Not applicable",
        "Not applicable, no EHR"
    }
    
    # ------------------------------------------------------------
    # 5. Weighted frequency function
    # ------------------------------------------------------------
    
    def get_weighted_frequency(
        df,
        var_name,
        weight_col="mailwgt"
    ):
        label_col = f"{var_name}_lbl"
    
        required = [var_name, label_col, weight_col]
    
        missing = [
            col for col in required
            if col not in df.columns
        ]
    
        if missing:
            raise ValueError(
                f"{var_name}: missing required columns: {missing}"
            )
    
        working = df[
            [var_name, label_col, weight_col]
        ].copy()
    
        working[weight_col] = pd.to_numeric(
            working[weight_col],
            errors="coerce"
        )
    
        if working[weight_col].isna().any():
            raise ValueError(
                f"{var_name}: invalid values found in {weight_col}."
            )
    
        # Summarize every observed response category.
        summary = (
            working
            .groupby(
                label_col,
                dropna=False
            )
            .agg(
                sample_count=(var_name, "count"),
                weighted_national_estimate=(weight_col, "sum")
            )
            .reset_index()
            .rename(columns={label_col: "category"})
        )
    
        # Identify substantive responses using the official labels.
        summary["is_valid_response"] = (
            ~summary["category"].isin(
                non_substantive_labels
            )
            & summary["category"].notna()
        )
    
        # Calculate the weighted denominator from substantive responses only.
        valid_weighted_total = summary.loc[
            summary["is_valid_response"],
            "weighted_national_estimate"
        ].sum()
    
        if valid_weighted_total <= 0:
            raise ValueError(
                f"{var_name}: valid weighted denominator is not positive."
            )
    
        # Valid-response percentage.
        summary["weighted_valid_pct"] = np.where(
            summary["is_valid_response"],
            (
                summary["weighted_national_estimate"]
                / valid_weighted_total
                * 100
            ),
            np.nan
        )
    
        summary["weighted_national_estimate"] = (
            summary["weighted_national_estimate"]
            .round(0)
            .astype(int)
        )
    
        summary["weighted_valid_pct"] = (
            summary["weighted_valid_pct"]
            .round(2)
        )
    
        summary.insert(
            0,
            "variable",
            var_name
        )
    
        summary["valid_weighted_total"] = round(
            valid_weighted_total
        )
    
        return summary.sort_values(
            by="weighted_national_estimate",
            ascending=False
        ).reset_index(drop=True)
    
    # ------------------------------------------------------------
    # 6. Calculate weighted results for all target variables
    # ------------------------------------------------------------
    
    all_results = []
    
    for variable in all_target_vars:
    
        result = get_weighted_frequency(
            nehrs_clean,
            variable
        )
    
        all_results.append(result)
    
    # Combined analysis table for downstream steps.
    full_summary_df = pd.concat(
        all_results,
        ignore_index=True
    )
    
    # ------------------------------------------------------------
    # 7. Display results
    # ------------------------------------------------------------
    
    print("=" * 75)
    print("STEP 5.1: WEIGHTED NATIONAL ESTIMATES & VALID RESPONSE RATES")
    print("=" * 75)
    
    print(
        f"Physician records : {len(nehrs_clean):,}"
    )
    
    print(
        f"Total survey weight : {weight.sum():,.0f}"
    )
    
    print(
        "\nValid-response percentages exclude: "
        "Blank, Don't know, Not Applicable, "
        "and Not applicable, no EHR."
    )
    
    print("=" * 75)
    
    for variable in all_target_vars:
    
        print(f"\n[ VARIABLE: {variable} ]")
    
        display(
            full_summary_df[
                full_summary_df["variable"] == variable
            ][
                [
                    "variable",
                    "category",
                    "sample_count",
                    "weighted_national_estimate",
                    "weighted_valid_pct",
                    "valid_weighted_total"
                ]
            ]
        )
    
        print("-" * 75)
    
    # ------------------------------------------------------------
    # 8. Integrity checks
    # ------------------------------------------------------------
    
    assert set(full_summary_df["variable"]) == set(
        all_target_vars
    ), "Not all target variables are present in the final summary."
    
    assert (
        full_summary_df["weighted_national_estimate"]
        >= 0
    ).all(), "Negative weighted estimates were detected."
    
    assert (
        full_summary_df["weighted_valid_pct"].dropna()
        >= 0
    ).all(), "Negative valid-response percentages were detected."
    
    assert (
        full_summary_df["weighted_valid_pct"].dropna()
        <= 100
    ).all(), "Valid-response percentages above 100% were detected."
    
    for variable in all_target_vars:
    
        variable_result = full_summary_df[
            full_summary_df["variable"] == variable
        ]
    
        valid_pct_sum = variable_result.loc[
            variable_result["is_valid_response"],
            "weighted_valid_pct"
        ].sum()
    
        assert np.isclose(
            valid_pct_sum,
            100.0,
            atol=0.05
        ), (
            f"{variable}: valid-response percentages do not "
            "sum to approximately 100%."
        )
    
    print("=" * 75)
    print(
        "VALIDATION STATUS: WEIGHTED ESTIMATES AND "
        "VALID-RESPONSE PERCENTAGES PASSED INTEGRITY CHECKS."
    )
    print("=" * 75)
    ```
    
- STEP 5.2: FOCAL FRICTION SEGMENTATION ANALYSIS
👉🏻 Purpose: Examine how external clinical information access friction varies across physician specialties and EHR satisfaction.
    
    ```python
    # ============================================================
    # STEP 5.2: FOCAL FRICTION SEGMENTATION ANALYSIS
    # ============================================================
    #
    # Focal friction dimensions:
    # - extinfo_low: difficulty caused by delayed external information
    # - extinfo_scn: difficulty related to scanned/PDF information
    #
    # These dimensions are analyzed separately because they use
    # different response scales and represent different friction types.
    #
    # Weighted row percentages describe the national distribution
    # of friction responses within each specialty or EHR satisfaction group.
    #
    # Exploratory chi-square tests use unweighted respondent counts.
    # They are not survey-design-adjusted inferential tests.
    # ============================================================
    
    from scipy.stats import chi2_contingency
    
    # ------------------------------------------------------------
    # 1. Validate required dataset and columns
    # ------------------------------------------------------------
    
    if "nehrs_clean" not in globals() or nehrs_clean is None:
        raise NameError(
            "'nehrs_clean' was not found. Please run STEP 4.4 first."
        )
    
    required_columns = [
        "mailwgt",
        "speccat",
        "speccat_lbl",
        "ehrsat",
        "ehrsat_lbl",
        "extinfo_low",
        "extinfo_low_lbl",
        "extinfo_scn",
        "extinfo_scn_lbl"
    ]
    
    missing_columns = [
        col for col in required_columns
        if col not in nehrs_clean.columns
    ]
    
    if missing_columns:
        raise ValueError(
            f"Required columns are missing: {missing_columns}"
        )
    
    # ------------------------------------------------------------
    # 2. Define non-substantive response labels
    # ------------------------------------------------------------
    
    non_substantive_labels = {
        "Blank",
        "Don't know",
        "Not Applicable",
        "Not applicable",
        "Not applicable, no EHR"
    }
    
    # ------------------------------------------------------------
    # 3. Cross-tabulation function
    # ------------------------------------------------------------
    
    def run_weighted_crosstab(
        df,
        row_var,
        col_var,
        weight_col="mailwgt"
    ):
        row_lbl = f"{row_var}_lbl"
        col_lbl = f"{col_var}_lbl"
    
        required = [
            row_lbl,
            col_lbl,
            weight_col
        ]
    
        missing = [
            col for col in required
            if col not in df.columns
        ]
    
        if missing:
            raise ValueError(
                f"Missing columns for {row_var} x {col_var}: {missing}"
            )
    
        working = df[
            [
                row_var,
                row_lbl,
                col_var,
                col_lbl,
                weight_col
            ]
        ].copy()
    
        working[weight_col] = pd.to_numeric(
            working[weight_col],
            errors="coerce"
        )
    
        if working[weight_col].isna().any():
            raise ValueError(
                f"Invalid survey weights found for {row_var} x {col_var}."
            )
    
        # Keep only substantive responses for both variables.
        valid_df = working[
            working[row_lbl].notna()
            & working[col_lbl].notna()
            & ~working[row_lbl].isin(non_substantive_labels)
            & ~working[col_lbl].isin(non_substantive_labels)
        ].copy()
    
        if valid_df.empty:
            raise ValueError(
                f"No valid paired responses found for {row_var} x {col_var}."
            )
    
        # --------------------------------------------------------
        # Weighted contingency table
        # --------------------------------------------------------
    
        weighted_table = pd.pivot_table(
            valid_df,
            values=weight_col,
            index=row_lbl,
            columns=col_lbl,
            aggfunc="sum",
            fill_value=0
        )
    
        # --------------------------------------------------------
        # Weighted row percentages
        # --------------------------------------------------------
    
        row_totals = weighted_table.sum(axis=1)
    
        if (row_totals <= 0).any():
            raise ValueError(
                f"Non-positive weighted row total found for "
                f"{row_var} x {col_var}."
            )
    
        row_pct_table = (
            weighted_table
            .div(row_totals, axis=0)
            * 100
        )
    
        # --------------------------------------------------------
        # Unweighted exploratory chi-square
        # --------------------------------------------------------
    
        raw_table = pd.crosstab(
            valid_df[row_lbl],
            valid_df[col_lbl]
        )
    
        if raw_table.shape[0] < 2 or raw_table.shape[1] < 2:
            chi2 = np.nan
            p_value = np.nan
            dof = np.nan
        else:
            chi2, p_value, dof, _ = chi2_contingency(
                raw_table
            )
    
        return (
            weighted_table.round(0).astype(int),
            row_pct_table.round(2),
            raw_table,
            chi2,
            p_value,
            dof,
            len(valid_df)
        )
    
    # ------------------------------------------------------------
    # 4. Define focal friction dimensions
    # ------------------------------------------------------------
    
    focal_friction_variables = [
        "extinfo_low",
        "extinfo_scn"
    ]
    
    # ------------------------------------------------------------
    # 5. Run segmentation analyses
    # ------------------------------------------------------------
    
    step_5_2_results = {}
    
    print("=" * 75)
    print("STEP 5.2: FOCAL FRICTION SEGMENTATION ANALYSIS")
    print("=" * 75)
    
    for pain in focal_friction_variables:
    
        print("\n" + "=" * 75)
        print(f"FRICTION DIMENSION: {pain}")
        print("=" * 75)
    
        # --------------------------------------------------------
        # A. Physician Specialty × Friction
        # --------------------------------------------------------
    
        print(
            "\n[1] Physician Specialty × External Information Friction"
        )
    
        (
            specialty_weighted,
            specialty_pct,
            specialty_raw,
            specialty_chi2,
            specialty_p,
            specialty_dof,
            specialty_n
        ) = run_weighted_crosstab(
            nehrs_clean,
            "speccat",
            pain
        )
    
        print(
            f"Valid paired respondents: {specialty_n:,}"
        )
    
        print(
            f"Exploratory unweighted chi-square: "
            f"{specialty_chi2:.4f}"
            if pd.notna(specialty_chi2)
            else "Exploratory unweighted chi-square: not available"
        )
    
        print(
            f"Exploratory p-value: "
            f"{specialty_p:.4e}"
            if pd.notna(specialty_p)
            else "Exploratory p-value: not available"
        )
    
        print("\nWeighted row percentages (%):")
        display(specialty_pct)
    
        # --------------------------------------------------------
        # B. EHR Satisfaction × Friction
        # --------------------------------------------------------
    
        print(
            "\n[2] EHR Satisfaction × External Information Friction"
        )
    
        (
            satisfaction_weighted,
            satisfaction_pct,
            satisfaction_raw,
            satisfaction_chi2,
            satisfaction_p,
            satisfaction_dof,
            satisfaction_n
        ) = run_weighted_crosstab(
            nehrs_clean,
            "ehrsat",
            pain
        )
    
        print(
            f"Valid paired respondents: {satisfaction_n:,}"
        )
    
        print(
            f"Exploratory unweighted chi-square: "
            f"{satisfaction_chi2:.4f}"
            if pd.notna(satisfaction_chi2)
            else "Exploratory unweighted chi-square: not available"
        )
    
        print(
            f"Exploratory p-value: "
            f"{satisfaction_p:.4e}"
            if pd.notna(satisfaction_p)
            else "Exploratory p-value: not available"
        )
    
        print("\nWeighted row percentages (%):")
        display(satisfaction_pct)
    
        # --------------------------------------------------------
        # Store results for downstream analysis and visualization
        # --------------------------------------------------------
    
        step_5_2_results[pain] = {
            "specialty_weighted": specialty_weighted,
            "specialty_pct": specialty_pct,
            "specialty_raw": specialty_raw,
            "specialty_chi2": specialty_chi2,
            "specialty_p": specialty_p,
            "specialty_dof": specialty_dof,
            "specialty_valid_n": specialty_n,
            "satisfaction_weighted": satisfaction_weighted,
            "satisfaction_pct": satisfaction_pct,
            "satisfaction_raw": satisfaction_raw,
            "satisfaction_chi2": satisfaction_chi2,
            "satisfaction_p": satisfaction_p,
            "satisfaction_dof": satisfaction_dof,
            "satisfaction_valid_n": satisfaction_n
        }
    
    # ------------------------------------------------------------
    # 6. Integrity checks
    # ------------------------------------------------------------
    
    for pain, result in step_5_2_results.items():
    
        specialty_pct = result["specialty_pct"]
    
        specialty_row_sums = specialty_pct.sum(axis=1)
    
        assert np.allclose(
            specialty_row_sums.values,
            100.0,
            atol=0.05
        ), (
            f"{pain}: specialty weighted row percentages "
            "do not sum to approximately 100%."
        )
    
        satisfaction_pct = result["satisfaction_pct"]
    
        satisfaction_row_sums = satisfaction_pct.sum(axis=1)
    
        assert np.allclose(
            satisfaction_row_sums.values,
            100.0,
            atol=0.05
        ), (
            f"{pain}: EHR satisfaction weighted row percentages "
            "do not sum to approximately 100%."
        )
    
    print("\n" + "=" * 75)
    print(
        "VALIDATION STATUS: STEP 5.2 WEIGHTED CROSS-TABS "
        "PASSED ROW-PERCENTAGE INTEGRITY CHECKS."
    )
    print("=" * 75)
    ```
    
- STEP 5.3: EXTERNAL INFORMATION FRICTION RANKING
👉🏻 Purpose: Compare the seven predefined external-information dimensions using a common high-friction response definition.
    
    ```python
    # ============================================================
    # STEP 5.3: EXTERNAL INFORMATION FRICTION RANKING
    # ============================================================
    #
    # The ranking preserves the original NEHRS response categories.
    # No survey response is renamed to "Major Issue" or "Minor Issue."
    #
    # High-friction and secondary-friction responses are defined
    # according to the direction of each original survey question.
    #
    # Ranking is based on the weighted prevalence of the
    # high-friction response.
    # ============================================================
    
    # ------------------------------------------------------------
    # 1. Validate STEP 5.1 output
    # ------------------------------------------------------------
    
    if "full_summary_df" not in globals():
        raise NameError(
            "'full_summary_df' was not found. "
            "Please run STEP 5.1 first."
        )
    
    required_summary_columns = [
        "variable",
        "category",
        "weighted_national_estimate",
        "weighted_valid_pct",
        "valid_weighted_total",
        "is_valid_response"
    ]
    
    missing_summary_columns = [
        col
        for col in required_summary_columns
        if col not in full_summary_df.columns
    ]
    
    if missing_summary_columns:
        raise ValueError(
            "STEP 5.1 output is missing required columns: "
            f"{missing_summary_columns}"
        )
    
    # ------------------------------------------------------------
    # 2. Define the seven external-information dimensions
    # ------------------------------------------------------------
    #
    # Each mapping uses the original NEHRS response labels.
    #
    # high_friction:
    #   The response representing the strongest adverse signal.
    #
    # secondary_friction:
    #   The next-most-adverse substantive response.
    #
    # The direction is variable-specific because the survey questions
    # use different response scales.
    
    friction_definitions = {
        "extinfo_low": {
            "description": "Difficulty finding important information due to low-value information",
            "high_friction": "To a great extent",
            "secondary_friction": "To some extent"
        },
        "extinfo_scn": {
            "description": "External clinical information available as scanned documents",
            "high_friction": "Often",
            "secondary_friction": "Sometimes"
        },
        "extinfo_rec": {
            "description": "Entire external clinical record is not available",
            "high_friction": "To a great extent",
            "secondary_friction": "To some extent"
        },
        "extinfo_eff": {
            "description": "Difficulty using external clinical information effectively",
            "high_friction": "Not at all",
            "secondary_friction": "Somewhat"
        },
        "extinfo_key": {
            "description": "Key information within the external record is missing",
            "high_friction": "To a great extent",
            "secondary_friction": "To some extent"
        },
        "extinfo_int": {
            "description": "External clinical information is not integrated within the EHR",
            "high_friction": "Never",
            "secondary_friction": "Rarely"
        },
        "extinfo_port": {
            "description": "External clinical information is accessed through a separate portal",
            "high_friction": "Often",
            "secondary_friction": "Sometimes"
        }
    }
    
    expected_friction_variables = list(
        friction_definitions.keys()
    )
    
    # ------------------------------------------------------------
    # 3. Validate all seven variables and expected categories
    # ------------------------------------------------------------
    
    summary_variables = set(
        full_summary_df["variable"].unique()
    )
    
    missing_friction_variables = [
        variable
        for variable in expected_friction_variables
        if variable not in summary_variables
    ]
    
    if missing_friction_variables:
        raise ValueError(
            "The following friction variables are missing from STEP 5.1: "
            f"{missing_friction_variables}"
        )
    
    # ------------------------------------------------------------
    # 4. Build executive friction ranking
    # ------------------------------------------------------------
    
    ranking_records = []
    
    for variable, definition in friction_definitions.items():
    
        variable_summary = full_summary_df[
            full_summary_df["variable"] == variable
        ].copy()
    
        # Validate the high-friction response exists exactly once.
        high_rows = variable_summary[
            variable_summary["category"]
            == definition["high_friction"]
        ]
    
        secondary_rows = variable_summary[
            variable_summary["category"]
            == definition["secondary_friction"]
        ]
    
        if len(high_rows) != 1:
            raise ValueError(
                f"{variable}: expected exactly one high-friction "
                f"category '{definition['high_friction']}', "
                f"found {len(high_rows)}."
            )
    
        if len(secondary_rows) != 1:
            raise ValueError(
                f"{variable}: expected exactly one secondary-friction "
                f"category '{definition['secondary_friction']}', "
                f"found {len(secondary_rows)}."
            )
    
        high_row = high_rows.iloc[0]
        secondary_row = secondary_rows.iloc[0]
    
        high_pct = float(
            high_row["weighted_valid_pct"]
        )
    
        secondary_pct = float(
            secondary_row["weighted_valid_pct"]
        )
    
        high_estimate = int(
            high_row["weighted_national_estimate"]
        )
    
        secondary_estimate = int(
            secondary_row["weighted_national_estimate"]
        )
    
        combined_pct = high_pct + secondary_pct
    
        combined_estimate = (
            high_estimate
            + secondary_estimate
        )
    
        valid_weighted_total = int(
            high_row["valid_weighted_total"]
        )
    
        # --------------------------------------------------------
        # Integrity checks
        # --------------------------------------------------------
    
        if not (0 <= high_pct <= 100):
            raise ValueError(
                f"{variable}: invalid high-friction percentage."
            )
    
        if not (0 <= secondary_pct <= 100):
            raise ValueError(
                f"{variable}: invalid secondary-friction percentage."
            )
    
        if combined_pct > 100.05:
            raise ValueError(
                f"{variable}: combined friction percentage exceeds 100%."
            )
    
        ranking_records.append({
            "variable": variable,
            "friction_dimension": definition["description"],
            "high_friction_response": definition["high_friction"],
            "high_friction_pct": round(high_pct, 2),
            "high_friction_estimate": high_estimate,
            "secondary_friction_response": definition["secondary_friction"],
            "secondary_friction_pct": round(secondary_pct, 2),
            "secondary_friction_estimate": secondary_estimate,
            "high_plus_secondary_pct": round(combined_pct, 2),
            "high_plus_secondary_estimate": int(
                round(combined_estimate)
            ),
            "valid_weighted_total": valid_weighted_total
        })
    
    # ------------------------------------------------------------
    # 5. Rank by high-friction response prevalence
    # ------------------------------------------------------------
    
    executive_summary_df = (
        pd.DataFrame(ranking_records)
        .sort_values(
            by="high_friction_pct",
            ascending=False
        )
        .reset_index(drop=True)
    )
    
    executive_summary_df.insert(
        0,
        "rank",
        range(1, len(executive_summary_df) + 1)
    )
    
    # ------------------------------------------------------------
    # 6. Display portfolio-ready summary
    # ------------------------------------------------------------
    
    print("=" * 85)
    print("STEP 5.3: EXTERNAL INFORMATION FRICTION RANKING")
    print("=" * 85)
    
    print(
        "Ranking criterion: weighted prevalence of the "
        "highest-friction response for each survey dimension."
    )
    
    print(
        "The original NEHRS response categories are preserved; "
        "no new 'Major Issue' category is created."
    )
    
    print("-" * 85)
    
    display(
        executive_summary_df[
            [
                "rank",
                "variable",
                "friction_dimension",
                "high_friction_response",
                "high_friction_pct",
                "secondary_friction_response",
                "secondary_friction_pct",
                "high_plus_secondary_pct"
            ]
        ]
    )
    
    # ------------------------------------------------------------
    # 7. Integrity validation
    # ------------------------------------------------------------
    
    assert len(executive_summary_df) == 7, (
        "The final friction ranking must contain exactly seven dimensions."
    )
    
    assert (
        executive_summary_df["high_friction_pct"]
        .between(0, 100)
        .all()
    ), (
        "High-friction percentages must remain between 0 and 100."
    )
    
    assert (
        executive_summary_df["secondary_friction_pct"]
        .between(0, 100)
        .all()
    ), (
        "Secondary-friction percentages must remain between 0 and 100."
    )
    
    assert (
        executive_summary_df["high_plus_secondary_pct"]
        <= 100.05
    ).all(), (
        "Combined friction percentages cannot exceed 100%."
    )
    
    assert (
        executive_summary_df["high_friction_pct"]
        .is_monotonic_decreasing
    ), (
        "Ranking is not correctly sorted by high-friction prevalence."
    )
    
    print("=" * 85)
    print(
        "VALIDATION STATUS: SEVEN EXTERNAL INFORMATION "
        "FRICTION DIMENSIONS PASSED RANKING AND INTEGRITY CHECKS."
    )
    print("=" * 85)
    ```
    
- STEP 5.4: FINAL ANALYTICAL EVIDENCE SUMMARY
👉🏻 Purpose: Consolidate the validated findings from STEP 5.1, STEP 5.2, and STEP 5.3 into one final evidence summary.
    
    ```python
    # ============================================================
    # STEP 5.4: FINAL ANALYTICAL EVIDENCE SUMMARY
    # ============================================================
    #
    # This step does not create new analytical concepts.
    # It prepares validated results for the final dashboard.
    # ============================================================
    
    from scipy.stats import chi2_contingency
    
    # ------------------------------------------------------------
    # 1. Validate required upstream objects
    # ------------------------------------------------------------
    
    required_objects = [
        "nehrs_clean",
        "full_summary_df",
        "executive_summary_df"
    ]
    
    missing_objects = [
        obj for obj in required_objects
        if obj not in globals()
    ]
    
    if missing_objects:
        raise NameError(
            "Required upstream objects are missing: "
            f"{missing_objects}. "
            "Please run STEP 5.1, STEP 5.2, and STEP 5.3 first."
        )
    
    # ------------------------------------------------------------
    # 2. Define valid-response labels
    # ------------------------------------------------------------
    #
    # These are excluded from valid-response percentages.
    # "I do not see patients outside my medical organization"
    # is NOT excluded because it is a substantive survey response.
    # ------------------------------------------------------------
    
    non_substantive_labels = {
        "Blank",
        "Don't know",
        "Not Applicable",
        "Not applicable",
        "Not applicable, no EHR"
    }
    
    # ------------------------------------------------------------
    # 3. Validate label columns
    # ------------------------------------------------------------
    
    required_label_columns = [
        "extinfo_eff_lbl",
        "extinfo_low_lbl",
        "extinfo_scn_lbl",
        "speccat_lbl",
        "ehrsat_lbl"
    ]
    
    missing_label_columns = [
        col
        for col in required_label_columns
        if col not in nehrs_clean.columns
    ]
    
    if missing_label_columns:
        raise ValueError(
            "Required labeled columns are missing from nehrs_clean: "
            f"{missing_label_columns}"
        )
    
    # ------------------------------------------------------------
    # 4. Overall effectiveness
    # ------------------------------------------------------------
    #
    # extinfo_eff directly measures how easy external clinical
    # information is to use effectively.
    #
    # Response direction:
    # Very = positive
    # Somewhat = moderate
    # Not at all = negative
    # ------------------------------------------------------------
    
    effectiveness_summary = full_summary_df[
        (full_summary_df["variable"] == "extinfo_eff")
        & (full_summary_df["is_valid_response"] == True)
    ].copy()
    
    required_effectiveness_categories = {
        "Very",
        "Somewhat",
        "Not at all"
    }
    
    observed_effectiveness_categories = set(
        effectiveness_summary["category"]
    )
    
    missing_effectiveness_categories = (
        required_effectiveness_categories
        - observed_effectiveness_categories
    )
    
    if missing_effectiveness_categories:
        raise ValueError(
            "Missing extinfo_eff categories: "
            f"{missing_effectiveness_categories}"
        )
    
    overall_effectiveness_df = (
        effectiveness_summary[
            effectiveness_summary["category"].isin(
                ["Very", "Somewhat", "Not at all"]
            )
        ][
            [
                "variable",
                "category",
                "weighted_national_estimate",
                "weighted_valid_pct",
                "valid_weighted_total"
            ]
        ]
        .rename(
            columns={
                "category": "response",
                "weighted_national_estimate": "weighted_estimate",
                "weighted_valid_pct": "weighted_pct"
            }
        )
        .reset_index(drop=True)
    )
    
    # ------------------------------------------------------------
    # 5. Recalculate the two focal cross-tabs
    # ------------------------------------------------------------
    #
    # These reproduce the corrected STEP 5.2 logic directly.
    #
    # Chi-square remains an unweighted exploratory test.
    # Weighted percentages are descriptive national estimates.
    # ------------------------------------------------------------
    
    def build_valid_crosstab(df, row_var, col_var, weight_col="mailwgt"):
    
        row_lbl = f"{row_var}_lbl"
        col_lbl = f"{col_var}_lbl"
    
        valid_df = df[
            (~df[row_lbl].isin(non_substantive_labels))
            & (~df[col_lbl].isin(non_substantive_labels))
        ].copy()
    
        if valid_df.empty:
            raise ValueError(
                f"No valid paired observations for {row_var} x {col_var}."
            )
    
        weighted_table = pd.pivot_table(
            valid_df,
            values=weight_col,
            index=row_lbl,
            columns=col_lbl,
            aggfunc="sum",
            fill_value=0
        )
    
        raw_table = pd.crosstab(
            valid_df[row_lbl],
            valid_df[col_lbl]
        )
    
        chi2, p, dof, expected = chi2_contingency(raw_table)
    
        weighted_row_pct = (
            weighted_table
            .div(weighted_table.sum(axis=1), axis=0)
            * 100
        )
    
        weighted_row_pct = weighted_row_pct.round(2)
    
        return {
            "valid_n": len(valid_df),
            "weighted_table": weighted_table,
            "weighted_row_pct": weighted_row_pct,
            "chi2": chi2,
            "p_value": p,
            "dof": dof
        }
    
    # ------------------------------------------------------------
    # 6. Specialty x extinfo_low
    # ------------------------------------------------------------
    
    specialty_low_result = build_valid_crosstab(
        nehrs_clean,
        "speccat",
        "extinfo_low"
    )
    
    specialty_low_df = (
        specialty_low_result["weighted_row_pct"]
        .reset_index()
    )
    
    specialty_low_df.columns = [
        "specialty",
        *specialty_low_df.columns[1:]
    ]
    
    # ------------------------------------------------------------
    # 7. EHR satisfaction x extinfo_low
    # ------------------------------------------------------------
    
    satisfaction_low_result = build_valid_crosstab(
        nehrs_clean,
        "ehrsat",
        "extinfo_low"
    )
    
    satisfaction_low_df = (
        satisfaction_low_result["weighted_row_pct"]
        .reset_index()
    )
    
    satisfaction_low_df.columns = [
        "ehr_satisfaction",
        *satisfaction_low_df.columns[1:]
    ]
    
    # ------------------------------------------------------------
    # 8. Build final friction evidence table
    # ------------------------------------------------------------
    
    friction_columns = [
        "rank",
        "variable",
        "friction_dimension",
        "high_friction_response",
        "high_friction_pct",
        "secondary_friction_response",
        "secondary_friction_pct",
        "high_plus_secondary_pct"
    ]
    
    final_friction_evidence_df = (
        executive_summary_df[friction_columns]
        .copy()
    )
    
    # ------------------------------------------------------------
    # 9. Build concise core findings table
    # ------------------------------------------------------------
    
    core_finding_variables = [
        "extinfo_low",
        "extinfo_scn",
        "extinfo_rec",
        "extinfo_int"
    ]
    
    core_finding_rows = []
    
    for variable in core_finding_variables:
    
        row = executive_summary_df[
            executive_summary_df["variable"] == variable
        ]
    
        if len(row) != 1:
            raise ValueError(
                f"Expected exactly one friction-ranking row for "
                f"{variable}, found {len(row)}."
            )
    
        row = row.iloc[0]
    
        core_finding_rows.append({
            "variable": variable,
            "finding": row["friction_dimension"],
            "high_friction_response": row["high_friction_response"],
            "high_friction_pct": row["high_friction_pct"],
            "high_plus_secondary_pct": row["high_plus_secondary_pct"]
        })
    
    core_findings_df = pd.DataFrame(core_finding_rows)
    
    # ------------------------------------------------------------
    # 10. Validation
    # ------------------------------------------------------------
    
    assert len(overall_effectiveness_df) == 3, (
        "Overall effectiveness must contain three valid response categories."
    )
    
    assert len(final_friction_evidence_df) == 7, (
        "Friction ranking must contain exactly seven dimensions."
    )
    
    assert len(core_findings_df) == 4, (
        "Core findings must contain four friction dimensions."
    )
    
    assert (
        overall_effectiveness_df["weighted_pct"]
        .between(0, 100)
        .all()
    ), (
        "Effectiveness percentages must be between 0 and 100."
    )
    
    assert (
        final_friction_evidence_df["high_friction_pct"]
        .between(0, 100)
        .all()
    ), (
        "High-friction percentages must be between 0 and 100."
    )
    
    assert (
        final_friction_evidence_df["secondary_friction_pct"]
        .between(0, 100)
        .all()
    ), (
        "Secondary-friction percentages must be between 0 and 100."
    )
    
    assert (
        final_friction_evidence_df["high_plus_secondary_pct"]
        <= 100.05
    ).all(), (
        "Combined friction percentages cannot exceed 100%."
    )
    
    assert (
        final_friction_evidence_df["rank"]
        .tolist()
        == list(range(1, 8))
    ), (
        "Friction ranking must contain ranks 1 through 7."
    )
    
    assert (
        specialty_low_result["p_value"] >= 0
        and specialty_low_result["p_value"] <= 1
    ), (
        "Specialty exploratory p-value must be between 0 and 1."
    )
    
    assert (
        satisfaction_low_result["p_value"] >= 0
        and satisfaction_low_result["p_value"] <= 1
    ), (
        "EHR satisfaction exploratory p-value must be between 0 and 1."
    )
    
    # ------------------------------------------------------------
    # 11. Final output
    # ------------------------------------------------------------
    
    print("=" * 95)
    print("STEP 5.4: FINAL ANALYTICAL EVIDENCE SUMMARY")
    print("=" * 95)
    
    print("\n[1] OVERALL EFFECTIVENESS — EXTINFO_EFF")
    display(
        overall_effectiveness_df
    )
    
    print("\n[2] SEVEN EXTERNAL INFORMATION FRICTION SIGNALS")
    display(
        final_friction_evidence_df
    )
    
    print("\n[3] SPECIALTY x EXTINFO_LOW")
    print(
        f"Valid paired respondents: "
        f"{specialty_low_result['valid_n']:,}"
    )
    print(
        f"Exploratory raw chi-square p-value: "
        f"{specialty_low_result['p_value']:.6g}"
    )
    display(
        specialty_low_df
    )
    
    print("\n[4] EHR SATISFACTION x EXTINFO_LOW")
    print(
        f"Valid paired respondents: "
        f"{satisfaction_low_result['valid_n']:,}"
    )
    print(
        f"Exploratory raw chi-square p-value: "
        f"{satisfaction_low_result['p_value']:.6g}"
    )
    display(
        satisfaction_low_df
    )
    
    print("\n[5] CORE FINDINGS FOR DASHBOARD")
    display(
        core_findings_df
    )
    
    print("=" * 95)
    print(
        "VALIDATION STATUS: FINAL ANALYTICAL EVIDENCE "
        "SUMMARY PASSED ALL CHECKS."
    )
    print("=" * 95)
    ```
    
- STEP 6: VISUALIZATION - DASHBOARD
    
    ```python
    # ==============================================================================
    # STEP 6: VISUALIZATION - DASHBOARD
    # ==============================================================================
    
    import plotly.graph_objects as go
    from IPython.display import HTML, display
    
    # ------------------------------------------------------------------------------
    # 1. VALIDATED NEHRS RESULTS
    # ------------------------------------------------------------------------------
    # These values are carried forward from the validated STEP 5.4 analysis.
    # No new analytical assumptions are introduced in this dashboard layer.
    
    # Overall ease of using external clinical information
    eff_labels = ['Very', 'Somewhat', 'Not at all']
    eff_values = [31.98, 55.47, 12.55]
    
    # Information-access signals
    # "Friction / gap" = direct difficulty or information-availability problems
    # "Access pattern" = how external information is commonly delivered
    signal_data = [
        {
            'label': 'Difficulty Finding Info',
            'value': 52.68,
            'type': 'Friction / gap',
            'highlight': True
        },
        {
            'label': 'Scanned/PDF Records',
            'value': 48.15,
            'type': 'Access pattern',
            'highlight': False
        },
        {
            'label': 'Record Unavailable',
            'value': 35.65,
            'type': 'Friction / gap',
            'highlight': False
        },
        {
            'label': 'Unintegrated Systems',
            'value': 33.87,
            'type': 'Friction / gap',
            'highlight': False
        },
        {
            'label': 'Key Info Missing',
            'value': 24.97,
            'type': 'Friction / gap',
            'highlight': False
        },
        {
            'label': 'Portal Access Only',
            'value': 21.95,
            'type': 'Access pattern',
            'highlight': False
        },
        {
            'label': 'Difficulty Using Info',
            'value': 12.55,
            'type': 'Friction / gap',
            'highlight': False
        }
    ]
    
    # Specialty × difficulty finding important information
    spec_categories = [
        'Primary care',
        'Medical specialty',
        'Surgical specialty'
    ]
    
    spec_great = [48.07, 56.66, 55.43]
    spec_some = [46.20, 38.65, 35.46]
    spec_not = [5.73, 4.69, 9.10]
    
    # EHR satisfaction × difficulty finding important information
    sat_categories = [
        'Very sat.',
        'Somewhat sat.',
        'Neither',
        'Somewhat dissat.',
        'Very dissat.'
    ]
    
    sat_great = [40.54, 49.85, 68.43, 60.35, 84.89]
    sat_some = [49.05, 45.56, 31.30, 35.20, 11.71]
    sat_not = [10.40, 4.60, 0.28, 4.45, 3.40]
    
    # Exploratory unweighted chi-square results from STEP 5.4
    specialty_p = 0.000606414
    satisfaction_p = 3.8201e-18
    
    # ------------------------------------------------------------------------------
    # 2. HELPER VALUES
    # ------------------------------------------------------------------------------
    
    # Sort information-access signals from highest to lowest.
    signal_data = sorted(
        signal_data,
        key=lambda x: x['value'],
        reverse=True
    )
    
    fric_labels = [x['label'] for x in signal_data]
    fric_values = [x['value'] for x in signal_data]
    
    # Use distinct visual treatment for:
    # - direct friction / gap signals
    # - access-pattern signals
    # - the single largest friction signal
    fric_colors = []
    
    for item in signal_data:
        if item['highlight']:
            fric_colors.append('#EF4444')
        elif item['type'] == 'Friction / gap':
            fric_colors.append('#64748B')
        else:
            fric_colors.append('#CBD5E1')
    
    # ------------------------------------------------------------------------------
    # 3. CHART 1 — OVERALL EASE OF USE
    # ------------------------------------------------------------------------------
    
    fig1 = go.Figure()
    
    fig1.add_trace(
        go.Bar(
            x=eff_labels,
            y=eff_values,
            text=[f"<b>{v:.1f}%</b>" for v in eff_values],
            textposition='outside',
            marker=dict(
                color=['#4F46E5', '#CBD5E1', '#E2E8F0']
            ),
            width=0.45
        )
    )
    
    fig1.update_layout(
        margin=dict(l=20, r=20, t=20, b=20),
        height=190,
        paper_bgcolor='rgba(0,0,0,0)',
        plot_bgcolor='rgba(0,0,0,0)',
        yaxis=dict(
            range=[0, 70],
            showgrid=True,
            gridcolor='#E2E8F0',
            title='Valid responses (%)',
            titlefont=dict(
                size=10,
                color='#64748B'
            ),
            tickfont=dict(
                size=10,
                color='#64748B'
            )
        ),
        xaxis=dict(
            showgrid=False,
            tickfont=dict(
                size=11,
                color='#334155'
            )
        ),
        showlegend=False,
        hovermode=False
    )
    
    # ------------------------------------------------------------------------------
    # 4. CHART 2 — INFORMATION-ACCESS SIGNALS
    # ------------------------------------------------------------------------------
    
    fig2 = go.Figure()
    
    # Reverse for top-to-bottom ranking in horizontal bar chart.
    fig2.add_trace(
        go.Bar(
            y=fric_labels[::-1],
            x=fric_values[::-1],
            orientation='h',
            text=[
                f"<b>{v:.1f}%</b>"
                for v in fric_values[::-1]
            ],
            textposition='outside',
            marker=dict(
                color=fric_colors[::-1]
            ),
            width=0.62
        )
    )
    
    fig2.update_layout(
        margin=dict(l=10, r=42, t=10, b=24),
        height=205,
        paper_bgcolor='rgba(0,0,0,0)',
        plot_bgcolor='rgba(0,0,0,0)',
        xaxis=dict(
            range=[0, 70],
            showgrid=True,
            gridcolor='#E2E8F0',
            title='Weighted valid-response share (%)',
            titlefont=dict(
                size=10,
                color='#64748B'
            ),
            tickfont=dict(
                size=9,
                color='#64748B'
            )
        ),
        yaxis=dict(
            showgrid=False,
            tickfont=dict(
                size=9.5,
                color='#334155'
            )
        ),
        showlegend=False,
        hovermode=False
    )
    
    # ------------------------------------------------------------------------------
    # 5. CHART 3 — SPECIALTY DIFFERENCES
    # ------------------------------------------------------------------------------
    
    fig3 = go.Figure()
    
    fig3.add_trace(
        go.Bar(
            x=spec_categories,
            y=spec_great,
            name='To a great extent',
            marker=dict(color='#4F46E5'),
            text=[f"{v:.1f}%" for v in spec_great],
            textposition='outside',
            textfont=dict(size=9)
        )
    )
    
    fig3.add_trace(
        go.Bar(
            x=spec_categories,
            y=spec_some,
            name='To some extent',
            marker=dict(color='#94A3B8'),
            text=[f"{v:.1f}%" for v in spec_some],
            textposition='outside',
            textfont=dict(size=9)
        )
    )
    
    fig3.add_trace(
        go.Bar(
            x=spec_categories,
            y=spec_not,
            name='Not at all',
            marker=dict(color='#E2E8F0'),
            text=[f"{v:.1f}%" for v in spec_not],
            textposition='outside',
            textfont=dict(size=9)
        )
    )
    
    fig3.update_layout(
        barmode='group',
        margin=dict(l=20, r=10, t=32, b=20),
        height=190,
        paper_bgcolor='rgba(0,0,0,0)',
        plot_bgcolor='rgba(0,0,0,0)',
        yaxis=dict(
            range=[0, 75],
            showgrid=True,
            gridcolor='#E2E8F0',
            title='Weighted row %',
            titlefont=dict(
                size=10,
                color='#64748B'
            ),
            tickfont=dict(
                size=9,
                color='#64748B'
            )
        ),
        xaxis=dict(
            showgrid=False,
            tickfont=dict(
                size=9.5,
                color='#334155'
            )
        ),
        legend=dict(
            orientation='h',
            y=1.24,
            x=0.5,
            xanchor='center',
            font=dict(size=8.5)
        ),
        hovermode=False
    )
    
    # ------------------------------------------------------------------------------
    # 6. CHART 4 — EHR SATISFACTION ASSOCIATION
    # ------------------------------------------------------------------------------
    
    # Highlight the 84.9% "Very dissatisfied" / "To a great extent" cell.
    sat_great_colors = [
        '#4F46E5',
        '#4F46E5',
        '#4F46E5',
        '#4F46E5',
        '#EF4444'
    ]
    
    fig4 = go.Figure()
    
    fig4.add_trace(
        go.Bar(
            x=sat_categories,
            y=sat_great,
            name='To a great extent',
            marker=dict(
                color=sat_great_colors
            ),
            text=[
                f"<b>{v:.1f}%</b>" if i == 4 else f"{v:.1f}%"
                for i, v in enumerate(sat_great)
            ],
            textposition='outside',
            textfont=dict(size=8.5)
        )
    )
    
    fig4.add_trace(
        go.Bar(
            x=sat_categories,
            y=sat_some,
            name='To some extent',
            marker=dict(color='#94A3B8'),
            text=[f"{v:.1f}%" for v in sat_some],
            textposition='outside',
            textfont=dict(size=8.5)
        )
    )
    
    fig4.add_trace(
        go.Bar(
            x=sat_categories,
            y=sat_not,
            name='Not at all',
            marker=dict(color='#E2E8F0'),
            text=[f"{v:.1f}%" for v in sat_not],
            textposition='outside',
            textfont=dict(size=8.5)
        )
    )
    
    fig4.update_layout(
        barmode='group',
        margin=dict(l=20, r=10, t=32, b=20),
        height=190,
        paper_bgcolor='rgba(0,0,0,0)',
        plot_bgcolor='rgba(0,0,0,0)',
        yaxis=dict(
            range=[0, 100],
            showgrid=True,
            gridcolor='#E2E8F0',
            title='Weighted row %',
            titlefont=dict(
                size=10,
                color='#64748B'
            ),
            tickfont=dict(
                size=9,
                color='#64748B'
            )
        ),
        xaxis=dict(
            showgrid=False,
            tickfont=dict(
                size=8.5,
                color='#334155'
            )
        ),
        legend=dict(
            orientation='h',
            y=1.24,
            x=0.5,
            xanchor='center',
            font=dict(size=8.5)
        ),
        hovermode=False
    )
    
    # ------------------------------------------------------------------------------
    # 7. CONVERT CHARTS TO HTML
    # ------------------------------------------------------------------------------
    
    chart_config = {
        'displayModeBar': False,
        'responsive': True
    }
    
    chart1_html = fig1.to_html(
        full_html=False,
        include_plotlyjs='cdn',
        config=chart_config
    )
    
    chart2_html = fig2.to_html(
        full_html=False,
        include_plotlyjs=False,
        config=chart_config
    )
    
    chart3_html = fig3.to_html(
        full_html=False,
        include_plotlyjs=False,
        config=chart_config
    )
    
    chart4_html = fig4.to_html(
        full_html=False,
        include_plotlyjs=False,
        config=chart_config
    )
    
    # ------------------------------------------------------------------------------
    # 8. EXECUTIVE DASHBOARD HTML / CSS
    # ------------------------------------------------------------------------------
    
    dashboard_html = f"""
    <style>
    
        .exec-dashboard {{
            background-color: #F8FAFC;
            padding: 24px;
            font-family:
                -apple-system,
                BlinkMacSystemFont,
                "Segoe UI",
                Roboto,
                Helvetica,
                Arial,
                sans-serif;
            color: #1E293B;
            border-radius: 16px;
        }}
    
        /* ------------------------------------------------------------------
           HEADER
           ------------------------------------------------------------------ */
    
        .exec-header {{
            margin-bottom: 18px;
            padding-bottom: 14px;
            border-bottom: 1px solid #E2E8F0;
        }}
    
        .context-tag {{
            display: inline-block;
            background-color: #EEF2FF;
            color: #3730A3;
            font-size: 10px;
            font-weight: 700;
            padding: 4px 9px;
            border-radius: 5px;
            margin-bottom: 7px;
            text-transform: uppercase;
            letter-spacing: 0.45px;
        }}
    
        .exec-header h1 {{
            font-size: 22px;
            font-weight: 800;
            color: #0F172A;
            margin: 0 0 4px 0;
            letter-spacing: -0.4px;
        }}
    
        .exec-header p {{
            font-size: 12.5px;
            color: #64748B;
            margin: 0 0 7px 0;
            line-height: 1.45;
        }}
    
        .research-question {{
            display: inline-block;
            font-size: 11px;
            color: #475569;
            line-height: 1.4;
        }}
    
        .research-question strong {{
            color: #334155;
        }}
    
        /* ------------------------------------------------------------------
           GRID
           ------------------------------------------------------------------ */
    
        .card-grid {{
            display: grid;
            grid-template-columns: repeat(2, minmax(0, 1fr));
            gap: 18px;
        }}
    
        /* ------------------------------------------------------------------
           CARDS
           ------------------------------------------------------------------ */
    
        .kpi-card {{
            background: #FFFFFF;
            border-radius: 14px;
            border: 1px solid #E2E8F0;
            box-shadow:
                0 4px 6px -1px rgba(0, 0, 0, 0.025);
            padding: 20px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            min-width: 0;
        }}
    
        .card-title {{
            font-size: 10.5px;
            font-weight: 700;
            color: #64748B;
            text-transform: uppercase;
            letter-spacing: 0.55px;
            margin-bottom: 4px;
        }}
    
        .kpi-metric {{
            font-size: 32px;
            font-weight: 800;
            color: #4F46E5;
            line-height: 1.05;
            letter-spacing: -0.8px;
        }}
    
        .kpi-metric.alert {{
            color: #EF4444;
        }}
    
        .kpi-subtext {{
            font-size: 11.5px;
            color: #64748B;
            margin-top: 4px;
            margin-bottom: 5px;
            line-height: 1.4;
        }}
    
        .chart-context {{
            font-size: 10.5px;
            color: #64748B;
            line-height: 1.35;
            margin: 5px 0 0 0;
        }}
    
        /* ------------------------------------------------------------------
           SIGNAL LEGEND
           ------------------------------------------------------------------ */
    
        .signal-legend {{
        display: flex;
        align-items: center;
        gap: 16px;
        margin: 4px 0 2px 0;
        font-size: 10px;
        color: #64748B;
        }}
    
        .signal-item {{
        display: flex;
        align-items: center;
        gap: 6px;
        }}
    
        .signal-dot {{
        width: 10px;
        height: 6px;
        border-radius: 2px;
        display: inline-block;
        }}
    
        .signal-dot.friction {{
        background: #64748B;
        }}
    
        .signal-dot.access {{
        background: #CBD5E1;
        }}
    
        .signal-explanation {{
        font-size: 9.5px;
        color: #94A3B8;
        margin: 1px 0 2px 0;
        }} 
    
        .signal-item {{
            display: flex;
            align-items: center;
            gap: 5px;
        }}
    
        .signal-dot {{
            width: 7px;
            height: 7px;
            border-radius: 50%;
            display: inline-block;
        }}
    
        .signal-dot.friction {{
            background: #64748B;
        }}
    
        .signal-dot.access {{
            background: #CBD5E1;
        }}
    
        /* ------------------------------------------------------------------
           TAKEAWAYS
           ------------------------------------------------------------------ */
    
        .kpi-pill {{
            background-color: #EEF2FF;
            color: #312E81;
            font-size: 11px;
            font-weight: 700;
            padding: 9px 12px;
            border-radius: 8px;
            margin-top: 9px;
            border-left: 4px solid #4F46E5;
            line-height: 1.4;
        }}
    
        .kpi-pill.alert {{
            background-color: #FEF2F2;
            color: #991B1B;
            border-left: 4px solid #EF4444;
        }}
    
        /* ------------------------------------------------------------------
           METHODOLOGY / FOOTER
           ------------------------------------------------------------------ */
    
        .methodology {{
            margin-top: 16px;
            padding-top: 10px;
            border-top: 1px solid #E2E8F0;
            font-size: 9.5px;
            color: #64748B;
            line-height: 1.45;
        }}
    
        .methodology strong {{
            color: #475569;
        }}
    
        @media (max-width: 900px) {{
            .card-grid {{
                grid-template-columns: 1fr;
            }}
        }}
    
    </style>
    
    <div class="exec-dashboard">
    
        <!-- ================================================================
             HEADER
             ================================================================ -->
    
        <div class="exec-header">
    
            <div class="context-tag">
                2024 National Electronic Health Records Survey (NEHRS) • n=1,725 physicians
            </div>
    
            <h1>
                External Clinical Information Access
            </h1>
    
            <p>
                Evidence dashboard on how physicians access and use clinical information
                from outside their medical organization.
            </p>
    
            <div class="research-question">
                <strong>Key question:</strong>
                Where do information-access barriers emerge, and how do patterns differ
                by specialty and EHR satisfaction?
            </div>
    
        </div>
    
        <!-- ================================================================
             2 × 2 DASHBOARD
             ================================================================ -->
    
        <div class="card-grid">
    
            <!-- ============================================================
                 CARD 1 — OVERALL EXPERIENCE
                 ============================================================ -->
    
            <div class="kpi-card">
    
                <div>
    
                    <div class="card-title">
                        01 · Overall ease of use
                    </div>
    
                    <div class="kpi-metric">
                        32.0%
                    </div>
    
                    <div class="kpi-subtext">
                        Physicians reporting the highest ease-of-use response
                        ("Very")
                    </div>
    
                    <div class="chart-context">
                        Ease of using external clinical information for patient care
                    </div>
    
                    {chart1_html}
    
                </div>
    
                <div class="kpi-pill">
                    Key finding: 32.0% selected the highest ease-of-use response,
                    while 55.5% selected "Somewhat."
                </div>
    
            </div>
    
            <!-- ============================================================
                 CARD 2 — INFORMATION ACCESS SIGNALS
                 ============================================================ -->
    
            <div class="kpi-card">
    
                <div>
    
                    <div class="card-title">
                        02 · Information-access signals
                    </div>
    
                    <div class="kpi-metric alert">
                        52.7%
                    </div>
    
                    <div class="kpi-subtext">
                        Highest direct friction / gap signal:
                        difficulty finding important information
                    </div>
    
                    <div class="signal-legend">
    
                      <div class="signal-item">
                          <span class="signal-dot friction"></span>
                          Friction / gap
                      </div>
    
                      <div class="signal-item">
                          <span class="signal-dot access"></span>
                          Access pattern
                      </div>
    
                    </div>
    
                    <div class="signal-explanation">
                        Direct difficulty / information gaps vs. how external information is delivered
                    </div>
    
                    {chart2_html}
    
                </div>
    
                <div class="kpi-pill alert">
                    Key finding: Difficulty finding important information is the
                    largest direct friction / gap signal at 52.7%.
                </div>
    
            </div>
    
            <!-- ============================================================
                 CARD 3 — SPECIALTY DIFFERENCES
                 ============================================================ -->
    
            <div class="kpi-card">
    
                <div>
    
                    <div class="card-title">
                        03 · Specialty differences
                    </div>
    
                    <div class="kpi-metric">
                        56.7%
                    </div>
    
                    <div class="kpi-subtext">
                        Medical specialty physicians reporting difficulty
                        "To a great extent"
                    </div>
    
                    <div class="chart-context">
                        Difficulty finding important information due to large
                        amounts of low-value information
                    </div>
    
                    {chart3_html}
    
                </div>
    
                <div class="kpi-pill">
                    Key finding: The "To a great extent" response was
                    56.7% for medical specialties, 55.4% for surgical specialties,
                    and 48.1% for primary care.
                </div>
    
            </div>
    
            <!-- ============================================================
                 CARD 4 — EHR SATISFACTION ASSOCIATION
                 ============================================================ -->
    
            <div class="kpi-card">
    
                <div>
    
                    <div class="card-title">
                        04 · Association with EHR satisfaction
                    </div>
    
                    <div class="kpi-metric alert">
                        84.9%
                    </div>
    
                    <div class="kpi-subtext">
                        Among very dissatisfied EHR users, 84.9% reported difficulty
                        "To a great extent"
                    </div>
    
                    <div class="chart-context">
                        Relationship between EHR satisfaction and difficulty
                        finding important information
                    </div>
    
                    {chart4_html}
    
                </div>
    
                <div class="kpi-pill alert">
                    Key finding: The distribution of information-finding difficulty
                    differs across EHR satisfaction groups.
                </div>
    
            </div>
    
        </div>
    
        <!-- ================================================================
             METHODOLOGY
             ================================================================ -->
    
        <div class="methodology">
    
            <strong>Source & method:</strong>
            2024 National Electronic Health Records Survey (NEHRS) Public-Use File.
            National estimates are weighted using <strong>mailwgt</strong>.
            Percentages shown in the overall analysis use valid-response denominators
            and exclude Blank, Don't know, and Not Applicable responses where applicable.
            Cross-tab percentages are weighted row percentages.
            Specialty and EHR-satisfaction significance results are
            <strong>exploratory unweighted chi-square tests</strong> and are not
            survey-design adjusted. Association does not establish causation.
    
        </div>
    
    </div>
    """
    
    display(HTML(dashboard_html))
    ```
