# Prototipo de Validación Conceptual — Aprendizaje Federado para Ciberseguridad

Este repositorio contiene el notebook de demostración desarrollado como parte del Trabajo de Fin de Máster (TFM) **"Plataforma de Inteligencia Artificial para la Ciberseguridad en Infraestructuras Críticas frente a Amenazas de Día Cero"**, defendido en octubre de 2025 en la Universidad Internacional de Valencia (VIU), España — calificación 8,05/10.

---

## ¿Qué hace este notebook?

Implementa un ciclo completo de aprendizaje federado básico sobre el dataset NSL-KDD, con el propósito de demostrar que es posible entrenar un modelo de detección de intrusiones de forma distribuida sin que los datos de cada nodo abandonen su origen.

El ciclo cubre cuatro etapas:

1. **Preparación de datos** — carga del dataset NSL-KDD con balanceo estratificado (500 registros normales / 500 ataques).
2. **Entrenamiento local** — tres nodos simulados (energía, salud, transporte) entrenan modelos independientes sin compartir datos entre sí.
3. **Agregación FedAvg** — un servidor central promedia los pesos de los modelos locales para construir un modelo global. Ningún dato original es accesible en este paso.
4. **Evaluación y explicabilidad** — métricas del modelo global (F1-Score, precisión, recall) y análisis SHAP para identificar qué características del tráfico de red contribuyen más a la detección de ataques. Se incluye además una comparativa directa con un baseline centralizado.

---

## Resultados obtenidos

| Métrica | Modelo federado |
|---------|----------------|
| F1-Score (weighted) | 0,98 |
| Precisión — clase ataque | 0,99 |
| Recall — clase ataque | 0,97 |
| Accuracy global | 0,98 |

> Los resultados corresponden a una muestra balanceada de 1.000 eventos NSL-KDD distribuidos en tres nodos simulados. En el TFM completo, con Random Forest federado sobre el dataset completo, el F1-Score documentado es 0,891 con una mejora de +21,4% sobre el baseline centralizado.

---

## Limitaciones de esta implementación

Este prototipo es una demostración académica, no una implementación de producción. Las principales limitaciones son:

- La red neuronal utilizada (densa 64-32-1) es la más simple posible. El TFM trabajó con Random Forest federado.
- NSL-KDD data de 1998 y no representa tráfico industrial contemporáneo (OT/ICS).
- Los tres nodos se simulan en un solo entorno — no replica la heterogeneidad de una federación real.
- FedAvg se implementa como promedio simple de pesos. Una versión de producción requiere ponderación por volumen de datos y privacidad diferencial sobre los gradientes.

---

## Cómo ejecutarlo

El notebook está diseñado para correr en **Google Colab** sin configuración adicional.

1. Abrir [Google Colab](https://colab.research.google.com)
2. File → Open notebook → GitHub → pegar la URL de este repositorio
3. Runtime → Run all

El notebook descarga automáticamente el dataset NSL-KDD desde GitHub. Si la fuente no está disponible, genera un dataset sintético con la misma estructura para garantizar la ejecución completa.

---

## Stack técnico

- Python 3.12
- TensorFlow 2.19 / Keras
- scikit-learn 1.6
- SHAP (DeepExplainer)
- NumPy 2.0 / Pandas 2.2 / Matplotlib / Seaborn

---

## Contexto

Este prototipo corresponde al Anexo E del TFM y forma parte de una propuesta de investigación doctoral en aprendizaje profundo no supervisado aplicado a detección de anomalías en infraestructura crítica, en el marco de una cotutoría con la Universidad de Málaga (UMA).

---

**Autor:** Edgar O. Herrera Logroñ · M.Sc. Inteligencia Artificial — VIU España  
**Tutor TFM:** Dr. Jesús Gil Ruiz  
**Lugar:** Guayaquil, Ecuador
