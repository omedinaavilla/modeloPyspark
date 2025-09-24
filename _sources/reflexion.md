#  Comparación de Resultados: PySpark vs Scikit-learn

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

## 📌 Conclusión
- **PySpark:** más adecuado si se busca **minimizar falsos positivos** y trabajar con grandes volúmenes de datos, a costa de mayor tiempo de cómputo.  
- **Scikit-learn:** más eficiente en tiempo y con mejor **recall en la clase 1 (default)**, lo que lo hace útil en escenarios donde lo más importante es **no dejar escapar a clientes que no pagarán**.  
