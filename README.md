# Certificate Data Cleaning and Transformation Project

This project aims to consolidate, clean, and transform data from multiple certificate Excel files to generate a unified and standardized dataset ready for analysis.

## Project Structure

The workflow is divided into two main notebooks:

### 1. Cleaning and Joining (`data_cleaning_and_joining.ipynb`)

This notebook handles the initial ingestion and consolidation of raw files.

**Steps performed:**
*   **File Reading:** Scanning the `lista_certificados` folder to identify all `.xlsx` files.
*   **Structure Validation:** Verifying that each file contains a single data sheet.
*   **Metadata Removal:** Cleaning unnecessary rows (headers) and columns (indices) at the beginning of each sheet.
*   **Column Selection:** Removing columns with sensitive or irrelevant information (`CÓDIGO`, `DNI`, `APELLIDOS Y NOMBRES`, `N° CELULAR`, `EMAIL`), preserving only academic interest data.
*   **Consolidation:** Merging (concatenating) all individual files into a single master file (`consolidado.xlsx`).

### 2. Exploration and Transformation (`data_explore_and_transformation.ipynb`)

This notebook takes the consolidated file and applies deep transformations to ensure data quality.

**Transformations by Column:**

*   **`COORDINADORA`:**
    *   Standardization to uppercase.
    *   Removal of whitespace.
    *   Typo correction and name unification (e.g., 'ELIZABET F' -> 'ELIZABETH F').

*   **`CURSO` (Course):**
    *   Analysis of frequencies and unique values.
    *   Creation of the new **`AREA`** column via keyword-based classification (e.g., 'PYTHON' -> 'PROGRAMACIÓN Y DESARROLLO').

*   **`NOTA` (Grade):**
    *   Rounding decimal grades to the nearest integer.
    *   Data type conversion to integer (`int`).

*   **`NOTA TXT` (Grade in Text):**
    *   Standardization to uppercase and accent removal for uniformity (e.g., 'DIECISÉIS' -> 'DIECISEIS').

*   **`PERIODO` (Period):**
    *   Extraction and structuring of dates using regular expressions.
    *   Creation of three new columns: **`FECHA_INICIO`** (Start Date), **`FECHA_FIN`** (End Date), and **`AÑO`** (Year).
    *   Conversion to `datetime` objects and handling years as integers (`Int64`).

*   **`HORAS` (Hours):**
    *   Format standardization (uppercase and spaces).

*   **`CIUDAD` (City):**
    *   Massive correction of city and department names (e.g., 'JUNIN' -> 'JUNÍN').
    *   Geographic standardization (mapping cities to their corresponding regions, e.g., 'CHIMBOTE' -> 'ÁNCASH').
    *   Grouping foreign countries under the 'OTRO PAÍS' (Other Country) category.

**Final Cleanup:**
*   Exhaustive verification of null values.
*   Removal of rows with incomplete data.
*   DataFrame index reset.
*   Export of the final clean dataset to `lista_certificados/data_transformation/consolidado_clean.xlsx`.

## Final Result

The resulting file `consolidado_clean.xlsx` contains a structured dataset, free of implicit duplicates due to typos, with processable dates and a new categorization by thematic areas, ready to be connected to visualization tools (Dashboards).
