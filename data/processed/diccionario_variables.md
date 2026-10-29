# Diccionario de Datos: Base Integrada ENAHO - ESCALE 2025

Este dataset es el resultado de la fusión del Módulo 100, 200, 300 y Sumaria de la ENAHO 2025, junto con el padrón espacial de instituciones educativas ESCALE (MINEDU). Solo incluye a la población en edad escolar (6 a 17 años).

## 1. Llaves Primarias y Geográficas (Preservadas como texto)
*   **CONGLOME:** Número del conglomerado (4 dígitos).
*   **VIVIENDA:** Número de selección de la vivienda (3 dígitos).
*   **HOGAR:** Número secuencial del hogar (2 dígitos).
*   **CODPERSO:** Número de orden de la persona en el hogar (2 dígitos).
*   **UBIGEO:** Código de ubicación geográfica del distrito (6 dígitos).

## 2. Variables Socioeconómicas y Demográficas (ENAHO)
*   **ESTRATO:** Dominio geográfico (1 al 5 = Urbano; 6 al 8 = Rural).
*   **P208A:** Edad en años cumplidos (filtrado de 6 a 17 años).
*   **P300A:** Lengua materna de la persona encuestada.
*   **P314A:** ¿Utilizó internet en los últimos 3 meses? (1 = Sí, 2 = No).
*   **INGHOG2D:** Ingreso neto total del hogar (Soles anuales).
*   **GASHOG2D:** Gasto neto total del hogar (Soles anuales).

## 3. Variables de Ingeniería Creadas (Nuevas)
*   **RATIO_ALUMNO_DOCENTE (Float):** Variable de contexto ESCALE. Calcula la proporción de alumnos por cada docente a nivel distrital. Creada dividiendo `TOTAL_ALUMNOS` entre `TOTAL_DOCENTES` para el distrito del hogar.
*   **LENGUA_ORIGINARIA (Binaria 0/1):** Creada a partir de `P300A`. 
    *   `1` = Si la lengua materna es Quechua, Aymara u otra lengua nativa (códigos 4, 5, 6).
    *   `0` = Si la lengua materna es Castellano.
*   **TARGET_EXCLUSION (Binaria 0/1):** Variable objetivo para el modelo de Clasificación Supervisada, derivada de `P314A`.
    *   `1` = Estudiante excluido digitalmente (No usó internet).
    *   `0` = Estudiante conectado (Sí usó internet).
*   **CLUSTER (Categórica 0, 1, 2):** Etiqueta asignada por el modelo de aprendizaje no supervisado K-Means.
    *   `0` = Vulnerabilidad y ruralidad profunda.
    *   `1` = Privilegio y altos ingresos.
    *   `2` = Clase media urbana masificada.