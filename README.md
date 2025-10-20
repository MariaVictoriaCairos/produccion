# 📘 Proceso ETL – Objetivos de Vendedores (Power BI / Power Query)

## 🔹 1. Objetivo  
Consolidar, limpiar y transformar múltiples archivos Excel de objetivos de ventas por año, generando una tabla analítica lista para su modelado en Power BI.  

El flujo permite:
- Integrar varios ficheros con la misma estructura.
- Unificar datos de distintos años.
- Clasificar vendedores por antigüedad.
- Crear un campo de fecha válido para análisis temporal.

---

## 🔹 2. Fuente de datos  

**Origen:** Carpeta local sincronizada (iCloud / Power BI / Producción).  
**Estructura de archivos:**
Cada archivo contiene datos de **Región**, **ID de Vendedor** y objetivos mensuales en formato matricial (una columna por mes).

```
.
├── data
│   ├── 1 - Ventas.xlsx
│   ├── 2 - Productos.xlsx
│   ├── 2 - Vendedores
│   │   ├── 2 - Vendedores 2017.xlsx
│   │   ├── 2 - Vendedores 2018.xlsx
│   │   ├── 2 - Vendedores 2019.xlsx
│   │   └── 2 - Vendedores 2020.xlsx
│   └── 4 - Objetivos.xlsx
├── ProduccionVentas.pbix
└── README.md

3 directories, 9 files
```
---

## 🔹 3. Conexión y carga en Power BI  

1. En Power BI Desktop → **Obtener datos → Carpeta**.  
2. Se seleccionó el directorio con los ficheros.  
3. En el **Editor de Power Query**, se filtraron únicamente los archivos `.xlsx` para evitar errores con archivos del sistema (`.DS_Store`):

   ```powerquery
   Table.SelectRows(#"Origen", each [Extension] = ".xlsx")````
## 🔹 Flujo del proceso

### 1️⃣ Conexión y carga
- Fuente: Carpeta con ficheros `2 - Vendedores ####.xlsx`.
- Se conectó mediante **Obtener datos > Carpeta**.
- Se filtraron solo archivos `.xlsx`, excluyendo `.DS_Store`.
- Se usó **Combinar archivos** para integrar las hojas.

### 2️⃣ Limpieza y transformación
- **Promocionar encabezados**: primera fila como encabezado.
- **Eliminar totales** (“Total Región”, “Total general”).
- **Anular dinamización** para convertir columnas mensuales en filas.

Resultado base:
| Región | ID Vendedor | Mes-año | Objetivo |

---

## 🔹 Campos creados

    🧠 Antigüedad (por año del archivo) en la table Vendedores
    🗓️ Fecha (primer día del mes) en la tabla objetivo


Autor: María Victoria Cairós González
Proyecto: ProducciónVentas
Fecha: Octubre 2025