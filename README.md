# Proyecto 1 — Obtención y Limpieza de Datos (P1-DS)

**Autores:** Gabriel Paz | Andy Fuentes | Davis Roldan  
**Curso:** Data Science 
**Entorno sugerido:** Google Colab o Python 3.11+ con `venv`  
**Estado:** Entrega de la parte 1 del proyecto)

---

## ✨ Objetivo

Dejar un **conjunto de datos listo para análisis** a partir de `dataset_institutions.csv`, documentando cada transformación realizada (reproducible, sin eliminar columnas ni hacer análisis).  
La limpieza sigue los pasos solicitados en la guía del proyecto.

---

## 📁 Estructura del repositorio

```
P1-DS/
├─ dataset_institutions.csv   # Datos crudos (entrada)
├─ LibroDeCodigos.pdf         # Diccionario / libro de códigos del dataset
├─ P1_DS.ipynb                # Notebook con los puntos 1–5 implementados
├─ P1_DS_limpio.csv           # Salida con establecimientos consolidados (punto 5)
└─ README.md                  # Este documento
```

---

## 🧭 Contenido del notebook (`P1_DS.ipynb`)

1. **Descripción del dataset (shape y vista previa)**  
   - Filas/columnas, `head()`, comentarios sobre tipos y formatos.
2. **Variables que más limpieza requieren**  
   - Conteo de **nulos** por variable y **valores únicos**.
3. **Estrategia de limpieza (plan)**  
   - Pasos propuestos por columna clave (`ESTABLECIMIENTO`, `DIRECCION`, `TELEFONO`, `DIRECTOR`, `SECTOR`, `PLAN`).
4. **Procesos de limpieza (ejecución reproducible)**  
   - Normalización de texto (lower/upper, `strip`, regex).  
   - Homologación de abreviaturas en direcciones.  
   - Depuración de teléfonos (solo dígitos, longitud validada, inválidos → `NaN`).  
   - Formateo de nombres propios (`title`, espacios).  
   - Unificación de categorías (`SECTOR`, `PLAN`).  
   - **Sin eliminar columnas ni hacer análisis**. Duplicados exactos pueden marcarse o removerse según nota metodológica.
5. **Consistencia y deduplicación de establecimientos**  
   - *Matching difuso* de `ESTABLECIMIENTO_clean` con `rapidfuzz` (umbral configurable).  
   - Generación de **nombre representante** por cluster (`ESTABLECIMIENTO_final`).  
   - Consolidación por **modo** de `DIRECCION` y `TELEFONO` dentro de cada cluster.  
   - Agregación de **JORNADA** a `HORARIOS` (lista `;`-separada).  
   - Exportación a `P1_DS_limpio.csv`.

> **Nota:** No se realiza análisis estadístico; el objetivo es dejar los datos coherentes y listos.

---

## 🚀 Cómo ejecutar

### Opción A) Google Colab (recomendado)
1. Abre Colab y crea un cuaderno nuevo.  
2. Sube `dataset_institutions.csv` (o monta Drive).  
3. Abre/copia el contenido de `P1_DS.ipynb` y **Ejecutar todo**.  
4. Descarga `P1_DS_limpio.csv` desde la carpeta de trabajo.

### Opción B) Local con `venv`
```bash
# Crear y activar entorno
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
# source .venv/bin/activate

# Paquetes mínimos
pip install -U pip pandas rapidfuzz jupyterlab

# Iniciar Jupyter
jupyter lab
```
Abre `P1_DS.ipynb` y ejecuta las celdas en orden.

---

## 📤 Salidas principales

- **`P1_DS_limpio.csv`**  
  Contiene una fila por **establecimiento único** (tras clustering difuso), con columnas representativas:

| Columna                  | Descripción                                                   |
|--------------------------|---------------------------------------------------------------|
| `ESTABLECIMIENTO_final`  | Nombre consolidado (representante del cluster)                |
| `DIRECCION_final`        | Dirección más frecuente dentro del cluster                    |
| `TELEFONO_final`         | Teléfono validado (8 dígitos) o `NaN` si no hay válido       |
| `HORARIOS`               | Jornadas únicas agregadas por establecimiento, separadas por `;` |


---

## 🧪 Notas metodológicas (decisiones de limpieza)

- **Normalización de texto**: uso de `str.lower()/upper()`, `strip()`, colapso de espacios, mapeos puntuales.  
- **Direcciones**: homologación de abreviaturas comunes (`av.`→`avenida`, `km`→`kilómetro`), limpieza de símbolos.  
- **Teléfonos**: eliminación de no-dígitos; validación de longitud (8). Inválidos → `NaN` (no se imputan).  
- **Categorías**: unificación de `SECTOR` y `PLAN` a conjuntos conocidos.  
- **Duplicados**:  
  - *Exactos*: pueden eliminarse con `drop_duplicates` (documentado).  
  - *Semánticos*: se agrupan por **matching difuso** en el paso 5 para evitar múltiples variantes del mismo establecimiento.  
- **Sin análisis**: no se incluyen estadísticas inferenciales ni gráficos analíticos en esta etapa.  
- **Reproducibilidad**: todas las transformaciones están en celdas de código con comentarios de “rationale”.

---

## 📚 Recursos

- `LibroDeCodigos.pdf`: glosario de variables del dataset para interpretar nombres y categorías.  
- `dataset_institutions.csv`: fuente cruda.
- `P1_DS_limpio.csv`: dataset con datos limpios.

---

## ✅ Checklist de entrega

- [x] Python Notebook completo.  
- [x] Transformaciones reproducibles sin análisis.  
- [x] Exportación de `P1_DS_limpio.csv`.  
- [x] `LibroDeCodigos.pdf` completo y bien formateado.  
- [x] Este `README.md` con instrucciones y notas.

---

