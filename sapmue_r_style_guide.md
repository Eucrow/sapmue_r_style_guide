# **Sampling Data Quality Assurance Team - R Style Guide**

Version 1.0

This style guide documents the coding conventions used by the Sampling Data Quality Assurance Team for the SAP project (Spanish Institute of Oceanography). Following these guidelines ensures consistency and maintainability across the codebase.

Idioma: English | [Español](./sapmue_r_style_guide_sp.md)

---

## **Table of Contents**

- [**Sampling Data Quality Assurance Team - R Style Guide**](#sampling-data-quality-assurance-team---r-style-guide)
  - [**Table of Contents**](#table-of-contents)
  - [**1. Language Use Guidelines**](#1-language-use-guidelines)
  - [**2. File Organization**](#2-file-organization)
    - [**2.1 Project Structure**](#21-project-structure)
    - [**2.2 Repository Naming**](#22-repository-naming)
  - [**3. Code Structure**](#3-code-structure)
    - [**3.1 Script Organization**](#31-script-organization)
    - [**3.2 Section Headers**](#32-section-headers)
  - [**4. Naming Conventions**](#4-naming-conventions)
    - [**4.1 Variables**](#41-variables)
    - [**4.2 Functions**](#42-functions)
    - [**4.3 Data Frame Columns**](#43-data-frame-columns)
  - [**5. Function Documentation**](#5-function-documentation)
    - [**5.1 Roxygen2 Documentation**](#51-roxygen2-documentation)
    - [**5.2 Documentation Sections Order**](#52-documentation-sections-order)
  - [**6. Code Formatting**](#6-code-formatting)
    - [**6.1 Spacing**](#61-spacing)
    - [**6.2 Line Length**](#62-line-length)
    - [**6.3 Indentation**](#63-indentation)
  - [**7. Control Structures**](#7-control-structures)
    - [**7.1 General Rules**](#71-general-rules)
    - [**7.2 Return Statements**](#72-return-statements)
  - [**8. Comments**](#8-comments)
    - [**8.1 Comment Style**](#81-comment-style)
    - [**8.2 Commented Code**](#82-commented-code)
  - [**9. Error Messages in Error Detection Scripts**](#9-error-messages-in-error-detection-scripts)
    - [**9.1 Error Message Format**](#91-error-message-format)
    - [**9.2 Error Types**](#92-error-types)
  - [**10. Package Loading**](#10-package-loading)
    - [**10.1 Package Order**](#101-package-order)
    - [**10.2 Package Installation Comments**](#102-package-installation-comments)
  - [**11. File Paths**](#11-file-paths)
    - [**11.1 Path Construction**](#111-path-construction)
    - [**11.2 Path Variables**](#112-path-variables)
  - [**12. Anti-Patterns (What to Avoid)**](#12-anti-patterns-what-to-avoid)
    - [**12.1 Don't Mix Naming Conventions**](#121-dont-mix-naming-conventions)
    - [**12.2 Don't Modify Global Variables Inside Functions**](#122-dont-modify-global-variables-inside-functions)
    - [**12.3 Don't Use Hardcoded Paths**](#123-dont-use-hardcoded-paths)

---

## **1. Language Use Guidelines**

- **Variable names, function names, and comments:** Use English for all code elements and comments to maximize readability and maintain consistency with R community standards.
- **Error and warning messages:** In error-detection scripts, use Spanish in generated files.
- **Data frame columns:** Use English; Spanish is allowed when the original imported reports use Spanish column names.

---

## **2. File Organization**

### **2.1 Project Structure**
It is highly recommended to use this structure when possible:
```
project_name/
├── R/                    # R functions and scripts
├── data/                 # Generated/processed data
├── data-raw/             # Reference data (CSV, Excel files...)
├── private/              # Sensitive information (credentials, contacts)
└── main_script.R         # Main execution script(s) - one or more
```

**Description of structure:**
- **project_name/** - Contains one or more main execution scripts (e.g., `project_name.R`, `analysis.R`). These are the entry points that orchestrate the workflow
- **R/** - Contains all R functions and scripts
  - Use subfolders to organize functions by category (e.g., `errors_functions/`, `helpers/`)
- **data/** - Stores generated or processed data organized by year/month or analysis. **Important:** Add `data/` to `.gitignore` if it contains large files or sensitive information
- **data-raw/** - Read-only reference data (species lists, lookup tables, etc.)
  - Add to `.gitignore` if files are large or contain sensitive information
- **private/** - Sensitive information that should NOT be committed to version control. **Important:** Always add `private/` to `.gitignore`

---
 

### **2.2 Repository Naming**

- Prefer underscores (`_`) for all repository names (e.g., `sapmue_r_guide`) to maintain consistency across the organization.

---

## **3. Code Structure**

### **3.1 Script Organization**
Use the following section order whenever feasible:

```r
# Title and purpose comment

# INSTRUCTIONS ----------------------------------------------------------------

# PACKAGES --------------------------------------------------------------------

# FUNCTIONS -------------------------------------------------------------------

# GLOBAL VARIABLES ------------------------------------------------------------

# IMPORT DATA -----------------------------------------------------------------

# OTHER SECTION NAME IN CAPS WITH DASHES --------------------------------------

# EXPORT DATA -----------------------------------------------------------------
```

### **3.2 Section Headers**
- Use uppercase for section names
- Add dashes to reach column 80
- Add a space between the last character and the first dash
- One blank line before section, no blank line after

```r
# CORRECT ✓
# IMPORT DATA -----------------------------------------------------------------

# INCORRECT ✗
# Import Data
# import data -----------------------------------------------------------------
#IMPORT DATA
```

---

## **4. Naming Conventions**

**General Principles:**
- **Use descriptive names** that clearly indicate the variable's purpose or content
- Avoid abbreviations unless they are widely understood (e.g., `ID`, `URL`)
- Prefer longer, clear names over short, cryptic ones
- Names should be self-documenting - a reader should understand what the variable contains without additional comments
- Avoid special characters (except underscores)

```r
# ✓ Good - descriptive names
historical_species_sampled
accessory_email_info

# ✗ Bad - unclear abbreviations
hist_sp_samp
acc_em_inf
```

### **4.1 Variables**

**Constants (Global Configuration):**
```r
# All uppercase with underscores
MONTH <- c(5)
YEAR <- 2025
DATA_FOLDER_NAME <- "input"
PATH_INPUT_FILES <- file.path(PATH_FILES, DATA_FOLDER_NAME)
BASE_FIELDS <- c("COD_ID", "COD_PUERTO", "PUERTO")
```

**Regular Variables:**
```r
# Lowercase with underscores (snake_case)
mixed_species <- especies_mezcla
errors_filename <- paste0("errors", "_", IDENTIFIER)
working_folders <- list(backup = PATH_BACKUP, errors = PATH_ERRORS)
```

### **4.2 Functions**
```r
# Lowercase with underscores (snake_case)
create_month_as_character <- function(month, suffix) { }
add_type_of_error <- function(errors, type, code, description) { }
export_errors_list <- function(errors_list, filename) { }
```

### **4.3 Data Frame Columns**
```r
# Uppercase with underscores
COD_ID
COD_PUERTO
FECHA_MUE
ESTRATO_RIM
COD_TIPO_MUE
```

---

## **5. Function Documentation**

### **5.1 Roxygen2 Documentation**
All functions must include complete roxygen2 documentation:

```r
#' Brief one-line description
#'
#' @description
#' Detailed description of what the function does.
#'
#' @param param_name Data type. Description of the parameter.
#' @param another_param Data type. Description.
#'
#' @return Description of what is returned. Specify NULL if nothing is returned.
#'
#' @details
#' Additional implementation details or usage notes.
#'
#' @note Any other important notes
#'
function_name <- function(param_name, another_param) {
  # Implementation
}
```

**Example:**
```r
#' Detect false MT1 sampling type
#'
#' @description
#' Identifies catch records incorrectly marked as MT1 sampling type when they
#' should be MT2 or MT2B based on species and RIM strata criteria.
#'
#' @param catches Data frame. The catches data returned by importRIMFiles().
#'
#' @return Data frame with detected errors, or NULL if no errors found.
#'
#' @details
#' MT1 is only valid for specific species in certain RIM strata. This function
#' validates that MT1 assignments follow these business rules.
#'
#' @note Check code: 1016
#'
detect_false_mt1 <- function(catches) {
  # Implementation
}
```

### **5.2 Documentation Sections Order**
1. `@description`
2. `@param` (all parameters in order)
3. `@return`
4. `@details` (if applicable)
5. `@note` (check code first, then other notes; if applicable)
6. `@examples`

---

## **6. Code Formatting**

### **6.1 Spacing**

**Assignment Operators:**
```r
# Use spaces around <- and =
x <- 5          # ✓
x<-5            # ✗

list(a = 1, b = 2)    # ✓
list(a=1,b=2)         # ✗
```

**Function Calls:**
```r
# Space after comma, no space before
function(arg1, arg2, arg3)     # ✓
function(arg1,arg2,arg3)       # ✗
function(arg1 , arg2 , arg3)   # ✗
```

**Operators:**
```r
# Space around operators
x + y           # ✓
x+y             # ✗

x == y          # ✓
x==y            # ✗
```

### **6.2 Line Length**
- Target 80 characters maximum
- Break long lines logically

```r
# ✓ Good
errors <- add_type_of_error(
  errors = errors,
  type = "ERROR",
  code = "1016",
  description = "ERROR 1016: MT1 falso"
)

# ✗ Avoid
errors <- add_type_of_error(errors = errors, type = "ERROR", code = "1016", description = "ERROR 1016: MT1 falso")
```

### **6.3 Indentation**
- Use 2 spaces (not tabs)
- Align function arguments vertically when breaking lines

```r
# ✓ Good
result <- long_function_name(
  first_argument = value1,
  second_argument = value2,
  third_argument = value3
)

# ✗ Avoid
result <- long_function_name(first_argument = value1,
                            second_argument = value2,
                            third_argument = value3)
```

---

## **7. Control Structures**

### **7.1 General Rules**

**Single line - use without braces:**
```r
if (condition) return(NULL)
```

**Multi-line - always use braces:**
```r
# If statements
if (nrow(errors) > 0) {
  errors <- add_type_of_error(errors, "ERROR", "1016", "MT1 falso")
  return(errors)
}

# For loops
for (i in 1:10) {
  print(i)
}

# While loops
while (condition) {
  # Do something
}

# Apply family functions - use braces for multi-line
lapply(list, function(x) {
  result <- process(x)
  return(result)
})
```

**Multiple conditions - one per line:**
```r
if (condition1 &&
    condition2 &&
    condition3) {
  # Do something
}
```

### **7.2 Return Statements**
```r
# Explicit returns for consistency, including NULL
if (nrow(errors) > 0) {
  return(errors)
}
return(NULL)  # ✓ Explicit

# ✗ Avoid implicit returns
if (nrow(errors) > 0) {
  return(errors)
}
# Missing explicit return
```

---

## **8. Comments**

### **8.1 Comment Style**

**Section Comments:**
```r
# SECTION NAME -----------------------------------------------------------------
```

**Inline Comments:**
- Single space after hash
```r
# ✓ Good
x <- 5  # Brief explanation

# ✗ Avoid
x <- 5 #no space before
```

**TODO Comments:**
- Space after the hash
- Text “TODO:”
- Space after the colon
- Sentence that describes the task
```r
# TODO: Create a coherence check for rim_stratum-origin
# TODO: Find a better way to handle this case

# ✗ Avoid
# TODO: ALL CAPS TASK
# todo: lowercase start
```

### **8.2 Commented Code**
- Keep alternatives commented with explanation
- Remove unexplaunexplained commented code or useless or dedundant commented code
```r
# ✓ Good
# errors <- rim_check_annual(muestreos_up)  # Annual check alternative
# errors <- oab_check(muestreos_up)         # OAB check alternative

# ✗ Avoid unexplained commented code
# errors <- rim_check_annual(muestreos_up)
# errors <- oab_check(muestreos_up)
```

---

## **9. Error Messages in Error Detection Scripts**

### **9.1 Error Message Format**
- Language: **Spanish**
- Format: `ERROR {code}: {description}`
- Code: 4 digits (e.g., 1016, 1051)

```r
# ✓ Correct
"ERROR 1016: MT1 falso"
"ERROR 1021: Número de barcos es 0 o NA."
"WARNING 1087: Número de barcos es mayor que 2."

# ✗ Incorrect
"Error 1016: False MT1"           # English
"ERROR 16: MT1 falso"             # Wrong code format
"error 1016: mt1 falso"           # Wrong capitalization
```

### **9.2 Error Types**
- `ERROR` - Data quality issue that must be fixed
- `WARNING` - Potential issue requiring review

---

## **10. Package Loading**

### **10.1 Package Order**
Load packages at the beginning in logical groups if needed:

```r
# PACKAGES ---------------------------------------------------------------------
# Data manipulation
library(dplyr)

# File I/O
library(openxlsx)

# Email functionality
library(blastula)

# Project-specific
library(sapmuebase)
```

### **10.2 Package Installation Comments**
When a package is not available on CRAN:
- Keep installation instructions or installation code commented
```r
# Install sapmuebase from GitHub
# install_github("eucrow/sapmuebase")
```

---

## **11. File Paths**

### **11.1 Path Construction**
- Always use file.path() for cross-platform compatibility
- Avoid string concatenation
```r
# ✓ Good
PATH_FILES <- file.path(getwd(), "data", YEAR, IDENTIFIER)
PATH_ERRORS <- file.path(PATH_FILES, ERRORS_FOLDER_NAME)

# ✗ Bad
PATH_FILES <- paste0(getwd(), "/data/", YEAR, "/", IDENTIFIER)
```

### **11.2 Path Variables**
```r
# Use descriptive uppercase names for path constants
PATH_INPUT_FILES <- file.path(PATH_FILES, DATA_FOLDER_NAME)
PATH_PRIVATE_FILES <- file.path(getwd(), PRIVATE_FOLDER_NAME)
PATH_DATA_RAW <- file.path(getwd(), DATA_RAW_FOLDER_NAME)
```

---

## **12. Anti-Patterns (What to Avoid)**

### **12.1 Don't Mix Naming Conventions**
```r
# ✗ Bad
myVariable <- 5
another_variable <- 10
YetAnotherVariable <- 15

# ✓ Good
my_variable <- 5
another_variable <- 10
yet_another_variable <- 15
```

### **12.2 Don't Modify Global Variables Inside Functions**
```r
# ✗ Bad
check_function <- function(data) {
  BASE_FIELDS <- c(BASE_FIELDS, "NEW_FIELD")  # Modifies global!
  # ...
}

# ✓ Good
check_function <- function(data) {
  required_fields <- c(BASE_FIELDS, "NEW_FIELD")  # Local variable
  # ...
}
```

### **12.3 Don't Use Hardcoded Paths**
```r
# ✗ Bad
data <- read.csv("C:/Users/Marco/data/file.csv")

# ✓ Good
data <- read.csv(file.path(PATH_DATA_RAW, "file.csv"))
```

---
