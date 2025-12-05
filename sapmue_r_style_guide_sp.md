# **Equipo de Aseguramiento de la Calidad de Muestreo - Guía de Estilo en R**

Versión 1.0

Esta guía de estilo documenta las convenciones de codificación utilizadas por el Equipo de Control de Calidad del equipo Muestreos del proyecto SAP (Instituto Español de Oceanografía). Seguir estas directrices garantiza la consistencia y el mantenimiento del código.

Idioma: [English](./sapmue_r_style_guide.md) | Español

---

## **Tabla de Contenidos**

- [**Equipo de Aseguramiento de la Calidad de Muestreo - Guía de Estilo en R**](#equipo-de-aseguramiento-de-la-calidad-de-muestreo---guía-de-estilo-en-r)
  - [**Tabla de Contenidos**](#tabla-de-contenidos)
  - [**1. Directrices sobre el uso del idioma**](#1-directrices-sobre-el-uso-del-idioma)
  - [**2. Organización de archivos**](#2-organización-de-archivos)
    - [**2.1 Estructura del proyecto**](#21-estructura-del-proyecto)
    - [**2.2 Nomenclatura del repositorio**](#22-nomenclatura-del-repositorio)
  - [**3. Estructura del código**](#3-estructura-del-código)
    - [**3.1 Organización de scripts**](#31-organización-de-scripts)
    - [**3.2 Encabezados de sección**](#32-encabezados-de-sección)
  - [**4. Convenciones de nombres**](#4-convenciones-de-nombres)
    - [**4.1 Variables**](#41-variables)
    - [**4.2 Funciones**](#42-funciones)
    - [**4.3 Columnas de data frame**](#43-columnas-de-data-frame)
  - [**5. Documentación de funciones**](#5-documentación-de-funciones)
    - [**5.1 Documentación con Roxygen2**](#51-documentación-con-roxygen2)
    - [**5.2 Orden de secciones de documentación**](#52-orden-de-secciones-de-documentación)
  - [**6. Formato de código**](#6-formato-de-código)
    - [**6.1 Espaciado**](#61-espaciado)
    - [**6.2 Longitud de línea**](#62-longitud-de-línea)
    - [**6.3 Sangría**](#63-sangría)
  - [**7. Estructuras de control**](#7-estructuras-de-control)
    - [**7.1 Reglas generales**](#71-reglas-generales)
    - [**7.2 Sentencias return**](#72-sentencias-return)
  - [**8. Comentarios**](#8-comentarios)
    - [**8.1 Estilo de comentarios**](#81-estilo-de-comentarios)
    - [**8.2 Código comentado**](#82-código-comentado)
  - [**9. Mensajes de error en scripts de detección de errores**](#9-mensajes-de-error-en-scripts-de-detección-de-errores)
    - [**9.1 Formato del mensaje de error**](#91-formato-del-mensaje-de-error)
    - [**9.2 Tipos de mensajes de error**](#92-tipos-de-mensajes-de-error)
  - [**10. Carga de paquetes**](#10-carga-de-paquetes)
    - [**10.1 Orden de paquetes**](#101-orden-de-paquetes)
    - [**10.2 Comentarios de instalación de paquetes**](#102-comentarios-de-instalación-de-paquetes)
  - [**11. Rutas de archivos**](#11-rutas-de-archivos)
    - [**11.1 Construcción de rutas**](#111-construcción-de-rutas)
    - [**11.2 Variables de ruta**](#112-variables-de-ruta)
  - [**12. Antipatrones (Qué evitar)**](#12-antipatrones-qué-evitar)
    - [**12.1 No mezclar convenciones de nombres**](#121-no-mezclar-convenciones-de-nombres)
    - [**12.2 No modificar variables globales dentro de funciones**](#122-no-modificar-variables-globales-dentro-de-funciones)
    - [**12.3 No usar rutas codificadas**](#123-no-usar-rutas-codificadas)

---

## **1. Directrices sobre el uso del idioma**

- **Nombres de variables, funciones y comentarios:** Usar el inglés para todos los elementos del código y los comentarios para maximizar la legibilidad y mantener la consistencia con los estándares de la comunidad de R.
- **Mensajes de error y advertencia:** En los scripts de detección de errores, usar el español en los archivos generados.
- **Columnas de data frame:** Usar el inglés; permitir el español cuando los informes importados originales usan nombres de columnas en español.

---

## **2. Organización de archivos**

### **2.1 Estructura del proyecto**
Usar la siguiente estructura cuando sea posible:
```
project_name/
├── R/                    # Funciones y scripts en R
├── data/                 # Datos resultantes/procesados
├── data-raw/             # Datos de referencia (CSV, archivos Excel...)
├── private/              # Información sensible (credenciales, contactos)
└── main_script.R         # Scripts principales - uno o varios
```

**Descripción de la estructura:**
- **project_name/** - Contiene uno o más scripts principales (p. ej., `nombre_proyecto.R`, `analisis.R`). Estos son los puntos de entrada que orquestan el flujo de trabajo
- **R/** - Contiene todas las funciones y scripts de R
  - Usar subcarpetas para organizar funciones por categoría (p. ej., `errors_functions/`, `helpers/`)
- **data/** - Almacena datos generados o procesados, organizados por año/mes o por análisis. **Importante:** Añadir `data/` a `.gitignore` si contiene archivos grandes o información sensible
- **data-raw/** - Datos de referencia de solo lectura (listados de especies, tablas de búsqueda, etc.)
  - Añadir a `.gitignore` si los archivos son grandes o contienen información sensible
- **private/** - Información sensible que NO debe enviarse al control de versiones. **Importante:** Añadir siempre `private/` a `.gitignore`

---
 

### **2.2 Nomenclatura del repositorio**

- Se prefiere guiones bajos (`_`) para todos los nombres de repositorio (p. ej., `sapmue_r_style_guide`) para mantener la consistencia en la organización.

---

## **3. Estructura del código**

### **3.1 Organización de scripts**
Usar el siguiente orden de secciones cuando sea posible:

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

### **3.2 Encabezados de sección**
- Usar mayúsculas para los nombres de sección
- Añadir guiones hasta alcanzar la columna 80
- Añadir un espacio entre el último carácter y el primer guion
- Una línea en blanco antes de la sección, ninguna después

```r
# CORRECT ✓
# IMPORT DATA -----------------------------------------------------------------

# INCORRECT ✗
# Import Data
# import data -----------------------------------------------------------------
#IMPORT DATA
```

---

## **4. Convenciones de nombres**

**Principios generales:**
- **Usar nombres descriptivos** que indiquen claramente el propósito o contenido de la variable
- Evitar abreviaturas a menos que sean fácilmente comprensibles (p. ej., `ID`, `URL`)
- Preferir nombres largos y claros sobre nombres cortos y crípticos
- Los nombres deben ser autoexplicativos: el lector debe entender qué contiene la variable sin comentarios adicionales
- Evitar caracteres especiales (excepto el guión bajo)

```r
# ✓ Bien - nombres descriptivos
historical_species_sampled
accessory_email_info

# ✗ Mal - abreviaturas no claras
hist_sp_samp
acc_em_inf
```

### **4.1 Variables**

**Constantes (configuración global):**
```r
# En mayúsculas y con guiones bajos
MONTH <- c(5)
YEAR <- 2025
DATA_FOLDER_NAME <- "input"
PATH_INPUT_FILES <- file.path(PATH_FILES, DATA_FOLDER_NAME)
BASE_FIELDS <- c("COD_ID", "COD_PUERTO", "PUERTO")
```

**Variables regulares:**
```r
# En minúsculas y con guiones bajos (snake_case)
mixed_species <- especies_mezcla
errors_filename <- paste0("errors", "_", IDENTIFIER)
working_folders <- list(backup = PATH_BACKUP, errors = PATH_ERRORS)
```

### **4.2 Funciones**
```r
# En minúsculas y con guiones bajos (snake_case)
create_month_as_character <- function(month, suffix) { }
add_type_of_error <- function(errors, type, code, description) { }
export_errors_list <- function(errors_list, filename) { }
```

### **4.3 Columnas de data frame**
```r
# En mayúsculas y con guiones bajos
COD_ID
COD_PUERTO
FECHA_MUE
ESTRATO_RIM
COD_TIPO_MUE
```

---

## **5. Documentación de funciones**

### **5.1 Documentación con Roxygen2**
Todas las funciones deben incluir documentación completa con roxygen2:

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
  # Implementación
}
```

**Ejemplo:**
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
  # Implementación
}
```

### **5.2 Orden de secciones de documentación**
1. `@description`
2. `@param` (todos los parámetros en orden)
3. `@return`
4. `@details` (si es aplicable)
5. `@note` (código de verificación primero; luego otras notas, si es aplicable)
6. `@examples`

---

## **6. Formato de código**

### **6.1 Espaciado**

**Operadores de asignación:**
```r
# Espacios alrededor de <- y =
x <- 5          # ✓
x<-5            # ✗

list(a = 1, b = 2)    # ✓
list(a=1,b=2)         # ✗
```

**Llamadas a funciones:**
```r
# Espacio despues de la coma, sin espacio antes
function(arg1, arg2, arg3)     # ✓
function(arg1,arg2,arg3)       # ✗
function(arg1 , arg2 , arg3)   # ✗
```

**Operadores:**
```r
# Espacio alrededor de operadores
x + y           # ✓
x+y             # ✗

x == y          # ✓
x==y            # ✗
```

### **6.2 Longitud de línea**
- Objetivo: máximo 80 caracteres
- Dividir líneas largas de forma lógica

```r
# ✓ Bien
errors <- add_type_of_error(
  errors = errors,
  type = "ERROR",
  code = "1016",
  description = "ERROR 1016: MT1 falso"
)

# ✗ Evitar
errors <- add_type_of_error(errors = errors, type = "ERROR", code = "1016", description = "ERROR 1016: MT1 falso")
```

### **6.3 Sangría**
- Usar 2 espacios (no tabs)
- Alinear los argumentos de función verticalmente al dividir líneas

```r
# ✓ Bien
result <- long_function_name(
  first_argument = value1,
  second_argument = value2,
  third_argument = value3
)

# ✗ Evitar
result <- long_function_name(first_argument = value1,
                            second_argument = value2,
                            third_argument = value3)
```

---

## **7. Estructuras de control**

### **7.1 Reglas generales**

**Una sola línea: no usar llaves:**
```r
if (condition) return(NULL)
```

**Multilínea: usar siempre llaves:**
```r
# Condicionales If
if (nrow(errors) > 0) {
  errors <- add_type_of_error(errors, "ERROR", "1016", "MT1 falso")
  return(errors)
}

# Bucles for
for (i in 1:10) {
  print(i)
}

# Bucles while
while (condition) {
  # Do something
}

# Funciones familia apply - usar llaves para múltiples líneas
lapply(list, function(x) {
  result <- process(x)
  return(result)
})
```

**Múltiples condiciones: una por línea:**
```r
if (condition1 &&
    condition2 &&
    condition3) {
  # Do something
}
```

### **7.2 Sentencias return**
```r
# Devolver explícitamente el resultado, incluso los NULL
if (nrow(errors) > 0) {
  return(errors)
}
return(NULL)  # ✓ Explícito

# ✗ Evitar devolver implícitamente el resultado
if (nrow(errors) > 0) {
  return(errors)
}
# Falta el return del null explícito
```

---

## **8. Comentarios**

### **8.1 Estilo de comentarios**

**Comentarios de sección:**
```r
# SECTION NAME -----------------------------------------------------------------
```

**Comentarios en línea:**
- Espacio en blanco después de la almohadilla
```r
# ✓ Bien
x <- 5  # Brief explanation

# ✗ Evitar
x <- 5 #no space before
```

**Comentarios TODO:**
- Espacio después de la almohadilla
- texto "TODO:"
- Espacio después de los :
- Frase que describa la tarea
```r
# TODO: Create a coherence check for rim_stratum-origin
# TODO: Find a better way to handle this case

# ✗ Evitar
# TODO: TAREA EN MAYÚSCULA
# todo: todo en minúsculas
```

### **8.2 Código comentado**
- Mantener las alternativas explicadas con comentarios
- Evitar código comentado sin expliación o código comentado innecesario o redundante
```r
# ✓ Bien
# errors <- rim_check_annual(muestreos_up)  # Annual check alternative
# errors <- oab_check(muestreos_up)         # OAB check alternative

# ✗ Mal - Evitar código comentado sin explicación
# errors <- rim_check_annual(muestreos_up)
# errors <- oab_check(muestreos_up)
```

---

## **9. Mensajes de error en scripts de detección de errores**

### **9.1 Formato del mensaje de error**
- Idioma: **Español**
- Formato: `ERROR {código}: {descripción}`
- Código: 4 dígitos (p. ej., 1016, 1051)

```r
# ✓ Bien
"ERROR 1016: MT1 falso"
"ERROR 1021: Número de barcos es 0 o NA."
"WARNING 1087: Número de barcos es mayor que 2."

# ✗ Mal
"Error 1016: False MT1"           # En inglés
"ERROR 16: MT1 falso"             # Formato de código equivocado
"error 1016: mt1 falso"           # Mayúsculas incorrectas
```

### **9.2 Tipos de mensajes de error**
- `ERROR` - Problema de calidad de datos que debe corregirse
- `WARNING` - Posible problema que requiere revisión

---

## **10. Carga de paquetes**

### **10.1 Orden de paquetes**
Cargar los paquetes al inicio, en grupos lógicos si es necesario:

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

### **10.2 Comentarios de instalación de paquetes**
Cuando un paquete no está disponible en CRAN:
- Mantener comentadas las intrucciones o el código para su instalación
```r
# Install sapmuebase from GitHub
# install_github("eucrow/sapmuebase")
```

---

## **11. Rutas de archivos**

### **11.1 Construcción de rutas**
- Usar siempre file.path() para compatibilidad multiplataforma
- Evitar concatenación de caracteres
```r
# ✓ Bien
PATH_FILES <- file.path(getwd(), "data", YEAR, IDENTIFIER)
PATH_ERRORS <- file.path(PATH_FILES, ERRORS_FOLDER_NAME)

# ✗ Mal
PATH_FILES <- paste0(getwd(), "/data/", YEAR, "/", IDENTIFIER)
```

### **11.2 Variables de ruta**
```r
# Usar nombres descriptivos en mayúsculas para constantes de rutas
PATH_INPUT_FILES <- file.path(PATH_FILES, DATA_FOLDER_NAME)
PATH_PRIVATE_FILES <- file.path(getwd(), PRIVATE_FOLDER_NAME)
PATH_DATA_RAW <- file.path(getwd(), DATA_RAW_FOLDER_NAME)
```

---

## **12. Antipatrones (Qué evitar)**

### **12.1 No mezclar convenciones de nombres**
```r
# ✗ Mal
myVariable <- 5
another_variable <- 10
YetAnotherVariable <- 15

# ✓ Bien
my_variable <- 5
another_variable <- 10
yet_another_variable <- 15
```

### **12.2 No modificar variables globales dentro de funciones**
```r
# ✗ Mal
check_function <- function(data) {
  BASE_FIELDS <- c(BASE_FIELDS, "NEW_FIELD")  # Modifica la variable global
  # ...
}

# ✓ Good
check_function <- function(data) {
  required_fields <- c(BASE_FIELDS, "NEW_FIELD")  # Crea una variable local
  # ...
}
```

### **12.3 No usar rutas codificadas**
```r
# ✗ Bad
data <- read.csv("C:/Users/Marco/data/file.csv")

# ✓ Good
data <- read.csv(file.path(PATH_DATA_RAW, "file.csv"))
```

---
