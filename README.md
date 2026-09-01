# 🧬 Clasificación ATC de Medicamentos (ANMAT)

Dataset completo y estructurado de la **clasificación ATC (Anatomical Therapeutic Chemical)** de medicamentos, extraído de la página oficial de la **ANMAT (Administración Nacional de Medicamentos, Alimentos y Tecnología Médica de Argentina)**.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![CSV](https://img.shields.io/badge/format-CSV-blue)](codigos_atc_NUEVO_LIMPIO.csv)
[![JSON](https://img.shields.io/badge/format-JSON-blue)](codigos_atc.json)
[![Records](https://img.shields.io/badge/records-4,581-brightgreen)]()


---

## 📖 ¿Qué es la clasificación ATC?

La clasificación ATC es un sistema internacional de codificación de medicamentos, desarrollado por la **OMS (Organización Mundial de la Salud)**. Organiza los fármacos en **5 niveles jerárquicos** según el órgano o sistema sobre el que actúan, su efecto terapéutico, su estructura química y su principio activo.

| Nivel | Código | Descripción |
|-------|--------|-------------|
| **Nivel 1** | 1 letra | Grupo anatómico principal (ej. `A` = Tracto alimentario y metabolismo) |
| **Nivel 2** | 2 dígitos | Grupo terapéutico (ej. `A01` = Preparados estomatológicos) |
| **Nivel 3** | 1 letra + 2 dígitos | Subgrupo terapéutico/químico (ej. `A01A` = Preparados estomatológicos) |
| **Nivel 4** | 1 letra + 3 dígitos | Familia químico-terapéutica (ej. `A01AA` = Agentes para profilaxis de caries) |
| **Nivel 5** | 1 letra + 4 dígitos | Principio activo / Sustancia química (ej. `A01AA01` = fluoruro de sodio) |

Este recurso es ideal para:

- Sistemas de información farmacológica
- Buscadores de medicamentos
- Aplicaciones móviles y web de salud
- Análisis de datos y estudios epidemiológicos
- Proyectos de machine learning y minería de datos en salud

---

## 📂 Contenido del repositorio

| Archivo | Descripción |
|---------|-------------|
| `codigos_atc.csv` | Dataset en formato CSV (separador: punto y coma) |
| `codigos_atc.json` | Dataset en formato JSON (estructura jerárquica por registro) |

---

## 🧩 Estructura de los datos

El dataset contiene la clasificación ATC adaptada de ANMAT, estructurada en los siguientes campos y jerarquías con niveles unificados:

| Campo | Descripción | Ejemplo |
|-------|-------------|---------|
| `N1_COD` | Nivel 1: Grupo anatómico principal | `A` |
| `GRUPO ANATÓMICO PRINCIPAL` | Descripción del nivel 1 | `TRACTO ALIMENTARIO Y METABOLISMO` |
| `N23_COD` | **Niveles 2 y 3 fusionados (ANMAT):** Grupo y subgrupo terapéutico | `A01A` |
| `GRUPO/SUBGRUPO TERAPÉUTICO` | Descripción de los niveles 2 y 3 unificados | `PREPARADOS ESTOMATOLÓGICOS` |
| `N4_COD` | Nivel 4: Subgrupo químico-terapéutico | `A01AA` |
| `FAMILIA O SUBGRUPO QUÍMICO-TERAPÉUTICO` | Descripción del nivel 4 | `AGENTES PARA LA PROFILAXIS DE LAS CARIES` |
| `N5_COD` | Nivel 5: Código completo de la sustancia química | `A01AA01` |
| `PRINCIPIO ACTIVO / SUSTANCIA QUÍMICA` | Descripción del nivel 5 (Principio activo) | `FLUORURO DE SODIO` |


---

## 📊 Muestra de datos (JSON)

```json
[
  {
    "N1_Cod": "A",
    "Grupo Anatómico Principal": "TRACTO ALIMENTARIO Y METABOLISMO",
    "N2-3_Cod": "A01A",
    "Grupo/Subgrupo Terapéutico": "PREPARADOS ESTOMATOLÓGICOS",
    "N3_Cod": "A01AA",
    "Familia o Subgrupo Químico-Terapéutico": "Agentes para la profilaxis de las caries",
    "N4_Cod": "A01AA01",
    "Principio Activo / Sustancia Química": "fluoruro de sodio"
  },
  {
    "N1_Cod": "A",
    "Grupo Anatómico Principal": "TRACTO ALIMENTARIO Y METABOLISMO",
    "N2-3_Cod": "A01A",
    "Grupo/Subgrupo Terapéutico": "PREPARADOS ESTOMATOLÓGICOS",
    "N3_Cod": "A01AA",
    "Familia o Subgrupo Químico-Terapéutico": "Agentes para la profilaxis de las caries",
    "N4_Cod": "A01AA02",
    "Principio Activo / Sustancia Química": "monofluorfosfato de sodio"
  }
]
```

---

## 🚀 Uso

### CSV

```python
import csv

with open("codigos_atc.csv", "r", encoding="utf-8-sig") as f:
    reader = csv.DictReader(f, delimiter=";")
    for row in reader:
        print(row["N4_Cod"], row["Principio Activo / Sustancia Química"])
```

### JSON

```python
import json

with open("codigos_atc.json", "r", encoding="utf-8") as f:
    datos = json.load(f)
    for item in datos:
        print(item["N4_Cod"], item["Principio Activo / Sustancia Química"])
```

### JavaScript / Node.js

```javascript
const data = require("./codigos_atc.json");
data.forEach(item => {
    console.log(item["N4_Cod"], item["Principio Activo / Sustancia Química"]);
});
```

### SQL (ejemplo con SQLite)

```sql
CREATE TABLE atc (
    n1_cod TEXT,
    grupo_anatomico TEXT,
    n23_cod TEXT,
    grupo_terapeutico TEXT,
    n3_cod TEXT,
    familia_quimica TEXT,
    n4_cod TEXT PRIMARY KEY,
    principio_activo TEXT
);

-- Luego importar el CSV con la herramienta correspondiente
```

---

## 📌 Fuente de los datos

Los datos fueron extraídos de la página oficial de la **ANMAT**:

🔗 [https://www.anmat.gob.ar/atc/CodigosATC.asp](https://www.anmat.gob.ar/atc/CodigosATC.asp)

**Nota importante:** Este dataset es un trabajo de extracción, estructuración y normalización de información pública. La ANMAT no respalda ni está afiliada a este proyecto. Los datos se proporcionan "tal cual" y se recomienda validar con fuentes oficiales para usos críticos.

---

## 📜 Licencia

Este proyecto está bajo una **doble licencia**, según el tipo de contenido:

- **Los datos (`codigos_atc.csv` y `codigos_atc.json`)** → [CC0 1.0 Universal (Dominio Público)](https://creativecommons.org/publicdomain/zero/1.0/deed.es)  
  Puedes usarlos, modificarlos, compartirlos y comercializarlos sin restricciones.

- **El código (scripts de extracción)** → [MIT License](https://opensource.org/licenses/MIT)  
  Puedes usarlo, modificarlo y distribuirlo libremente, siempre que se incluya el aviso de copyright.

En resumen: **hacé lo que quieras con los datos y el código, no hay restricciones.**

---

## 🤝 Contribuciones

Si encontrás errores, datos faltantes o querés mejorar el dataset, podés:

- Abrir un **issue** en este repositorio
- Enviar un **pull request** con correcciones o mejoras
- Contactarme directamente

---

## 📬 Contacto

**Autor:** [Pablo Bella](https://github.com/psbella)  
**Repositorio:** [https://github.com/psbella/Codigos-ATC-ANMAT](https://github.com/psbella/Codigos-ATC-ANMAT)

---

## 🙏 Agradecimientos

- A la **ANMAT** por mantener pública la clasificación ATC.
- A la comunidad de **datos abiertos** y **salud digital** que impulsa proyectos colaborativos como este.

---

## ⭐ ¿Te resultó útil?

Si este dataset te ayudó en tu proyecto, considerá:

- Darle una **⭐ estrella** al repositorio
- **Compartirlo** con otras personas que puedan necesitarlo
- **Mencionarlo** en tus publicaciones o trabajos académicos

---

*Última actualización: 01/09/2026*
