# ¿Serás reemplazado por IA?

Análisis predictivo sobre el impacto de la IA en el destino de los puestos de trabajo.

## Resumen

Este proyecto analiza una base de datos de 2.000 empleados para determinar qué variables (personales, del puesto o de la empresa) explican realmente el riesgo de que un trabajador sea o bien reemplazado, modificado o mantenido en su puesto tras la adopción de IA en su empresa.

**Hallazgos principales:**

1. **Las variables personales del empleado (edad, experiencia, salario, educación, satisfacción) no predicen el reemplazo.**
2. **Dos variables estructurales concentran el 95% del poder predictivo:** el riesgo de automatización del puesto y el nivel de adopción de IA de la empresa.
3. **El efecto acumulado multiplica el riesgo por 26 veces** entre el escenario más favorable y el más expuesto.

## Contenido del repositorio

- `AI_Impact.ipynb` — Notebook con el análisis completo (EDA, modelado, interpretación, visualización).
- `ai_job_impact.csv` — Base de datos utilizada (2.000 observaciones, 17 variables).
- `README.md` — Este archivo.

## Metodología

El proyecto sigue el flujo típico de un problema de clasificación supervisada multiclase con clases desbalanceadas:

1. **EDA completo:** estadísticos descriptivos, distribuciones, análisis bivariado contra el target, relaciones multivariantes y detección formal de outliers.
2. **Feature engineering** aplicando el principio de parsimonia.
3. **Modelado con cinco tipos de algoritmos** (LogisticRegression, KNN, SVM, RandomForest, GradientBoosting) via GridSearchCV con validación cruzada.
4. **Análisis de estabilidad** por folds para evaluar la robustez de cada modelo.
5. **Selección del modelo final** mediante el principio de parsimonia (LogisticRegression con `C=0.01`).
6. **Interpretación de coeficientes** mediante odds ratios para traducir el modelo a lenguaje narrativo.

## Resultados del modelo final

| Métrica | Valor |
|---|---|
| Accuracy | 0.942 |
| Balanced accuracy | 0.951 |
| F1 macro | 0.856 |
| Recall de clase Replaced | 1.000 |

Gap train-test negativo en las tres métricas: sin evidencias de sobreajuste.

## Stack técnico

- Python 3.10+
- pandas, numpy
- scikit-learn (Pipelines, ColumnTransformer, GridSearchCV)
- matplotlib, seaborn

## Cómo reproducir el análisis

```bash
# Clonar el repositorio
git clone https://github.com/[tu-usuario]/[nombre-repo].git
cd [nombre-repo]

# Instalar dependencias
pip install pandas numpy scikit-learn matplotlib seaborn jupyter

# Abrir el notebook
jupyter notebook AI_Impact.ipynb
```

## Limitaciones reconocidas

- Dataset sintético: las conclusiones cuantitativas no deben extrapolarse a poblaciones reales sin validación adicional.
- La clase minoritaria `Replaced` cuenta con solo 106 casos, lo que aporta fragilidad estadística a las métricas sobre esa clase.
- Ausencia de dimensión temporal.
- Ambigüedad en la etiqueta `Replaced` (reemplazo efectivo vs reasignación funcional).

Estas limitaciones están detalladas en la sección I del notebook.

## Autor

**Yeray Benito Calviño**
Estudiante de 3º Data Science — Universidad Complutense de Madrid
[LinkedIn] · [GitHub]

## Licencia

Este proyecto se publica con fines meramente educativos y de portafolio. La base de datos utilizada es de dominio público (Kaggle).