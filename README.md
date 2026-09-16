# Evaluación comparativa de modelos de Machine Learning (XGBoost) y Deep Learning (LSTM) para el forecasting de demanda eléctrica a corto plazo en Ecuador

## Descripción del proyecto

Este proyecto corresponde a un Trabajo de Fin de Máster orientado a la predicción de la demanda eléctrica horaria, con un horizonte de una semana, para un alimentador del Sistema Nacional Interconectado ecuatoriano (alimentador Sur, subestación Quito, período agosto 2021 - noviembre 2022).

Se comparan tres enfoques de forecasting bajo condiciones metodológicas equivalentes:
- **Baseline** de semana equivalente
- **XGBoost** con estrategia recursiva
- **LSTM** con estrategia multi-output

El desarrollo sigue la metodología **CRISP-DM** y utiliza la librería **skforecast** para asegurar que los tres modelos se evalúen con el mismo esquema de backtesting, las mismas variables exógenas (temperatura y calendario con codificación cíclica) y las mismas métricas de error (MAE, RMSE, MAPE).

El estudio evita generalizar los hallazgos como una superioridad definitiva de una familia de modelos sobre otra, situándolos dentro de sus límites metodológicos, temporales y de alcance del alimentador estudiado. Adicionalmente, se documentan las implicaciones de costo computacional de cada alternativa (un aspecto poco abordado en la literatura ecuatoriana revisada), así como consideraciones de privacidad de datos y líneas de trabajo futuro.

## Instrucciones de instalación

### Requisitos previos
- Python 3.13.5
- pip (gestor de paquetes de Python)
- Jupyter Notebook o Google Colab

### Pasos de instalación

1. Clona este repositorio:
```bash
   git clone https://github.com/davids01pg/tfm_comparativa_forecasting.git
```

2. Ingresa al directorio del proyecto:
```bash
   cd tfm_comparativa_forecasting
```

3. (Opcional) Crea y activa un entorno virtual:
```bash
   python -m venv venv
   source venv/bin/activate   # En Windows: venv\Scripts\activate
```

4. Instala las dependencias necesarias:
```bash
   pip install -r requirements.txt
```

5. Inicia Jupyter Notebook:
```bash
   jupyter notebook
```

## Guía de uso de los cuadernos

El proyecto contiene los siguientes cuadernos (notebooks), ubicados en la carpeta `/notebooks`:

- **KagglePrepareData.ipynb**: Este notebook realiza el preprocesamiento completo del conjunto de datos de demanda eléctrica, desde la lectura del archivo fuente hasta la generación del dataset final listo para modelado.

  **Fuente de datos:** Kaggle — Electrical Power Data: Equatorial Regions (Ecuador)
  🔗 https://www.kaggle.com/datasets/erikfmndez/electrical-power-data-equatorial-regions-ecuador

  El archivo fuente `Data_All2.csv` contiene 23 columnas y 882.570 filas con registros de demanda energética de Ecuador entre 2018 y 2022.

  **Alcance de este notebook:**
  - Filtrar el período agosto 2021 — noviembre 2022
  - Seleccionar únicamente el alimentador Sur de Quito (subestación Quito, alimentador Sur)
  - Convertir unidades de kW a MW
  - Completar la serie temporal horaria con interpolación
  - Incorporar temperatura horaria desde Open-Meteo (San Rafael, Valle de los Chillos)
  - Agregar variables de calendario
  - Exportar el dataset final a CSV

- **CompareXGBoostLSTM.ipynb**: Este notebook implementa y compara tres modelos de predicción de demanda eléctrica horaria del Sistema Nacional Interconectado (SNI) de Ecuador:
  - **Baseline**: modelo de referencia basado en semanas equivalentes anteriores
  - **XGBoost**: modelo de Machine Learning con estrategia recursiva
  - **LSTM**: red neuronal recurrente con estrategia multi-output

  **Caso de uso:** forecasting univariante multi-step con variables exógenas.
  **Horizonte:** 168 horas (7 días). Activación: cada domingo a las 23:00.
  **Período de datos:** agosto 2021 — noviembre 2022.

### Orden de ejecución recomendado

Para reproducir los resultados correctamente, se recomienda ejecutar los cuadernos en el siguiente orden:

1. Abre el cuaderno correspondiente desde la interfaz de Jupyter.
2. Ejecuta las celdas en orden secuencial (Shift + Enter).
3. Asegúrate de que los archivos de datos necesarios estén ubicados en la carpeta `/data` antes de ejecutar.
4. Los resultados y gráficos generados se guardarán en la carpeta `/outputs` (si aplica).

## Estructura del proyecto

```
nombre-repositorio/
├── data/                          # Datos utilizados en el proyecto
│   └── data_2021_2022_interpolado.csv
├── notebooks/                     # Cuadernos de Jupyter
│   ├── KagglePrepareData.ipynb
│   └── CompareXGBoostLSTM.ipynb
├── outputs/                       # Resultados generados
├── requirements.txt               # Dependencias del proyecto
└── README.md                      # Este archivo
```

## Autor

Geovanna Gallegos, David Paredes

## Licencia

Este proyecto está bajo la licencia CC0: Public Domain en la plataforma Kaggle.
