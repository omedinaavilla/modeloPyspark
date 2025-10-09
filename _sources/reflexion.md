# 4.Comparación de Resultados: PySpark vs Scikit-learn

## Tabla Comparativa de Métricas

| Métrica       | PySpark | Scikit-learn |
|---------------|---------|--------------|
| Accuracy      | 0.6203  | 0.6231       |
| Precision     | 0.7687  | 0.3029       |
| Recall        | 0.6203  | 0.6824       |
| F1-score      | 0.6585  | 0.4195       |
| ROC AUC       | 0.6994  | 0.7022       |

Aunque ambos modelos tienen valores similares en **accuracy** y **ROC AUC**, se observan diferencias importantes:  
- En **PySpark** la precisión global es más alta (0.76), pero a costa de un recall más bajo (0.62).  
- En **Scikit-learn** ocurre lo contrario: el recall es mayor (0.68), pero la precisión cae a 0.30.  

---

## Comparación de Tiempos de Cómputo

| Proceso        | PySpark          | Scikit-learn     |
|----------------|------------------|------------------|
| Entrenamiento  | **331.12 s**     | **329.71 s**     |
| Predicción     | **16.84 s**      | **3.86 s**     |

En general PySpark presenta una sobrecarga de cómputo al trabajar en un entorno distribuido, mientras que Scikit-learn es mucho más rápido en datasets medianos.  

---

## Gráficos
- **Curva ROC:**  
  - PySpark → AUC = 0.6994  
  - Scikit-learn → AUC = 0.7022  
  Ambas muestran un desempeño moderado, superior al azar.  

- **Matriz de Confusión:**  
  - PySpark privilegia la **precisión global** y reduce falsos positivos, pero deja escapar más casos de la clase 1.  
  - Scikit-learn logra un mejor **recall en la clase 1**, detectando más clientes de riesgo, aunque con mayor número de falsos positivos.  

---

##  Conclusión
  En este experimento se evidenció que scikit-learn obtuvo un desempeño ligeramente más rápido que PySpark, a pesar de que en teoría Spark está diseñado para optimizar procesos mediante paralelismo y cómputo distribuido. La explicación está en la forma en que se trabajó con cada entorno:

  Con scikit-learn se aplicaron múltiples etapas adicionales (preprocesamiento con imputación y escalado, codificación de variables categóricas, undersampling para balancear las clases y optimización de hiperparámetros con GridSearchCV y validación cruzada en paralelo).

  Con PySpark, en contraste, únicamente se corrió un modelo básico de RandomForest con un pipeline estándar, sin validación cruzada ni optimización de parámetros, y ejecutado en un entorno local sin clúster real.

  Bajo estas condiciones, y dado que el dataset (~1.3 millones de registros, 9 variables) aún es de un tamaño que cabe en memoria, scikit-learn aprovecha su implementación en C y la ausencia de overhead distribuido para responder más rápido. Spark, en cambio, incurre en costos adicionales de arranque, que no se compensan en este escenario al no contar con un clúster ni con un volumen de datos realmente masivo.

  En general, PySpark debería ser más eficiente en problemas a gran escala o cuando los datos no caben en memoria de una sola máquina, mientras que scikit-learn resulta más adecuado en contextos medianos o pequeños, donde la simplicidad y la velocidad local superan la sobrecarga del motor distribuido. 
