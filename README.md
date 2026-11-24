# Regímenes de riesgo en mercados bursátiles

**Evaluación de modelos de aprendizaje automático no supervisado para la identificación de regímenes de riesgo en mercados bursátiles: un estudio de generalización entre empresas cotizadas**

Trabajo Final de Máster · Máster en Ciencia de Datos e Inteligencia Artificial · EBIS Business Techschool

Autor: Nicolás García Escobar · Noviembre de 2026

**Cuadro de mando interactivo:** https://nicolasgarciaescobar.github.io/tfm-regimenes-riesgo-bursatil/

Versión sin conexión: [`respaldo_cuadro_de_mando.pdf`](respaldo_cuadro_de_mando.pdf)

## Pregunta de investigación

> ¿En qué medida los modelos de aprendizaje automático no supervisado permiten identificar regímenes de mercado diferenciados por sus características de rentabilidad y riesgo, y hasta qué punto estos patrones se generalizan a empresas cotizadas y periodos temporales no utilizados durante el entrenamiento?

## Resumen

A partir de precios diarios de Yahoo Finance se construyó una muestra de 1591 empresas estadounidenses entre noviembre de 2019 y agosto de 2026. Para cada acción y cada día se calcularon cinco variables de riesgo (volatilidad, cambio de volatilidad, rendimiento del último mes, caída desde el máximo y volumen negociado frente al habitual), y K-Means agrupó los 2.426.275 días resultantes en tres regímenes:

| Régimen | Qué lo caracteriza |
|---|---|
| Calma | Volatilidad baja y descendente, sin tendencia, cerca del máximo y con poca negociación |
| Impulso | Volatilidad media y en aumento, precio subiendo y negociación muy alta |
| Estrés | Volatilidad muy alta, pérdidas fuertes en el mes y caída profunda desde el máximo |

Para medir la generalización, las empresas se dividieron en un grupo de entrenamiento (70 %) y un grupo reservado (30 %), y el tiempo en tres bloques: entrenamiento (2020–2022), validación (2023–2024) y prueba (2025–2026).

- **Entre empresas**, los regímenes se reproducen casi igual: la coincidencia (ARI) con empresas no vistas es 0,94, frente a 0,98 de referencia.
- **Entre periodos**, la coincidencia baja a 0,66–0,80: los regímenes conservan su significado, pero la definición del Estrés depende del periodo de entrenamiento.
- **Los dos grupos de empresas se mueven a la vez**: la correlación diaria del porcentaje de acciones en cada régimen está entre 0,94 y 0,99.
- **Gaussian Mixture**, usada como comparación, coincide con K-Means solo en el 56–59 % de las observaciones y no distingue entre subidas y caídas fuertes.

## Contenido del repositorio

| Carpeta o archivo | Contenido |
|---|---|
| `docs/` | Cuadro de mando publicado con GitHub Pages (`index.html`), sus tablas de datos (`docs/datos/`) y la librería D3.js (`docs/lib/`) |
| `resultados/figuras/` | Las seis figuras del documento |
| `respaldo_cuadro_de_mando.pdf` | Vista inicial del cuadro de mando en PDF |
| `cuadernos/` | Cuadernos de Google Colab de las 23 actividades, con sus resultados |

## Cuadernos

El trabajo se desarrolló en 23 actividades. Las actividades 1 a 7 están en un mismo cuaderno; cada una de las demás tiene el suyo.

| Actividad | Cuaderno | Contenido |
|---|---|---|
| 1–7 | `01_inventario_repositorio` | Inventario y versión del repositorio, calidad, calendario, directorio de Nasdaq y prueba con la SEC |
| 8 | `08_consulta_sec` | Régimen de información de cada empresa en la SEC |
| 9 | `09_clasificacion_final` | Clasificación definitiva de los instrumentos |
| 10 | `10_consolidacion` | Descarga del universo y consolidación |
| 11 | `11_metricas_seleccion` | Validez de los datos y métricas de selección |
| 12 | `12_filtros_saltos` | Criterio de liquidez y saltos extremos |
| 13 | `13_detalle_saltos` | Revisión detallada de los saltos |
| 14 | `14_muestra_separacion` | Muestra definitiva y separación de empresas |
| 15 | `15_variables` | Cálculo de las variables de riesgo |
| 16 | `16_preprocesamiento` | Recorte de extremos y escalado |
| 17 | `17_eleccion_k` | Métricas para elegir el número de regímenes |
| 18 | `18_perfiles_candidatos` | Perfiles con tres y seis grupos |
| 19 | `19_modelo_definitivo` | Modelo definitivo |
| 20 | `20_metricas_generalizacion` | Métricas de generalización |
| 21 | `21_gaussian_mixture` | Mezcla de gaussianas |
| 22 | `22_diagnostico_gmm` | Diagnóstico de las diferencias entre algoritmos |
| 23 | `23_figuras_tablas` | Figuras y tablas de resultados |

Los cuadernos conservan las salidas de su ejecución. Antes de publicarlos se retiraron el correo de contacto usado con la SEC y una vista de ejemplo con precios originales.

## Datos

- **Fuente de precios:** repositorio [AmirTrader/YahooFinance](https://huggingface.co/datasets/AmirTrader/YahooFinance) en Hugging Face, carpeta `data/daily`, versión fijada `4c921233b7cc7b36c56891d21bed8c4f5010d7be` (4 de noviembre de 2026).
- **Clasificación de los instrumentos:** directorio de símbolos de Nasdaq Trader y datos públicos de EDGAR (SEC).
- **Qué se publica:** solo resultados derivados (porcentajes por régimen, perfiles, métricas). No se publican los precios originales de Yahoo Finance ni el directorio de Nasdaq, cuyas condiciones no permiten redistribuirlo. Para reproducir el trabajo, los cuadernos descargan los datos de sus fuentes originales.

## Cómo reproducir el trabajo

1. Abrir los cuadernos de `cuadernos/` en Google Colab, en orden.
2. Guardar un token de lectura de Hugging Face en los Secretos de Colab con el nombre `HF_TOKEN` y activar su acceso en cada cuaderno.
3. La consulta a la SEC (actividad 8) exige identificarse con un correo de contacto propio en el User-Agent.
4. Los parámetros completos (semillas, periodos, umbrales) figuran en el anexo C del documento.

## Herramientas

Python, Google Colab, pandas, NumPy, scikit-learn, Matplotlib, huggingface_hub, exchange_calendars y D3.js para el cuadro de mando.
