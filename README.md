# 🛡️ Detección de Tráfico Benigno y Ataques DoS (GoldenEye y HULK)

Este proyecto implementa un sistema de clasificación de tráfico de red para diferenciar entre **tráfico benigno** y ataques de denegación de servicio (DoS) de tipo **GoldenEye** y **HULK**.  
Se emplearon enfoques de **aprendizaje supervisado** y **aprendizaje profundo**, con diferentes representaciones de características: **features simples** y **windowing**.  

---

## 📂 Dataset  

Se trabajó con dos representaciones de los datos:  

### 1️⃣ Características simples por flujo  

| flow                               | packet_count | total_bytes | avg_packet_len | small_packet_count | label |
|-----------------------------------|--------------|------------|----------------|------------------|-------|
| 192.168.1.11:32768-192.168.1.10:80 | 9            | 3600.0     | 400.0          | 0.0              | 2     |
| 192.168.1.11:32768-192.168.1.12:80 | 18           | 5605.0     | 311.4          | 6.0              | 2     |
| 192.168.1.11:32770-192.168.1.10:80 | 18           | 4764.0     | 264.7          | 8.0              | 2     |
| 192.168.1.11:32770-192.168.1.12:80 | 13           | 3623.0     | 278.7          | 5.0              | 2     |
| 192.168.1.11:32772-192.168.1.10:80 | 10           | 4139.0     | 413.9          | 0.0              | 2     |

### 2️⃣ Características por ventanas de tiempo (windowing)  

| window_id | total_packets | total_bytes | avg_packet_size | avg_payload_size | packet_rate | small_packet_ratio | syn_count | ack_count | fin_count | label |
|-----------|---------------|------------|----------------|----------------|------------|------------------|----------|-----------|-----------|-------|
| 0         | 2756          | 502668     | 182.39         | 114.12         | 5512.0     | 0.730            | 749      | 2007      | 0         | 1     |
| 1         | 2221          | 430794     | 193.96         | 125.64         | 4442.0     | 0.705            | 640      | 1581      | 0         | 1     |
| 2         | 4925          | 820389     | 166.58         | 98.70          | 9850.0     | 0.767            | 1150     | 3775      | 0         | 1     |
| 3         | 3727          | 626560     | 168.11         | 100.20         | 7454.0     | 0.764            | 881      | 2846      | 0         | 1     |
| 4         | 2945          | 516173     | 175.27         | 107.22         | 5890.0     | 0.750            | 735      | 2210      | 0         | 1     |

---

## ⚙️ Metodología  

- **Preprocesamiento de datos**: limpieza, normalización y codificación de etiquetas.  
- **Modelos utilizados**:  
  - Aprendizaje Superficial (Random Forest, Árboles de decisión, Regresión logística).  
  - Redes Neuronales (aprendizaje profundo con múltiples capas).  
- **Validación**: validación cruzada (CV) y partición de datos en entrenamiento y validación.  

---

## 📊 Resultados  

### 🔹 Aprendizaje Superficial

**Con características simples por flujo**  

| Clase | Precision | Recall | F1-score | Support |
|-------|-----------|--------|----------|---------|
| 0     | 0.98      | 1.00   | 0.99     | 298     |
| 1     | 1.00      | 1.00   | 1.00     | 1785    |
| 2     | 1.00      | 1.00   | 1.00     | 5646    |

<img width="915" height="398" alt="image" src="https://github.com/user-attachments/assets/6904556f-5594-4d7d-900a-89213b2138b0" />

| Métrica            | Valor  |
|-------------------|--------|
| Accuracy           | 0.999  |
| F1-score (macro)   | 0.997  |
| F1-score (weighted)| 0.999  |
| Accuracy CV        | 0.999 ± 0.000 |

**Con windowing**  

| Clase | Precision | Recall | F1-score | Support |
|-------|-----------|--------|----------|---------|
| 0     | 1.00      | 1.00   | 1.00     | 165     |
| 1     | 1.00      | 1.00   | 1.00     | 43      |
| 2     | 1.00      | 1.00   | 1.00     | 109     |

<img width="813" height="375" alt="image" src="https://github.com/user-attachments/assets/a804bc3d-ef46-42c2-ba88-4f107ef14350" />

| Métrica            | Valor  |
|-------------------|--------|
| Accuracy           | 1.000  |
| F1-score (macro)   | 1.000  |
| F1-score (weighted)| 1.000  |
| Accuracy CV        | 0.999 ± 0.001 |

---

### 🔹 Aprendizaje Profundo

**Con características simples por flujo**  

| Clase | Precision | Recall | F1-score | Support |
|-------|-----------|--------|----------|---------|
| 0     | 0.98      | 1.00   | 0.99     | 298     |
| 1     | 1.00      | 1.00   | 1.00     | 1785    |
| 2     | 1.00      | 1.00   | 1.00     | 5646    |

<img width="823" height="374" alt="image" src="https://github.com/user-attachments/assets/61a6dd1c-9f2f-4fee-87e3-53ff3358415a" />


| Métrica            | Valor  |
|-------------------|--------|
| Accuracy           | 0.999  |
| F1-score (macro)   | 0.996  |
| F1-score (weighted)| 0.999  |

**Con windowing**  

| Clase | Precision | Recall | F1-score | Support |
|-------|-----------|--------|----------|---------|
| 0     | 1.00      | 1.00   | 1.00     | 165     |
| 1     | 1.00      | 1.00   | 1.00     | 43      |
| 2     | 1.00      | 1.00   | 1.00     | 109     |

<img width="901" height="390" alt="image" src="https://github.com/user-attachments/assets/e7cac6ba-b47b-4fdc-9622-b8c86a990b27" />


| Métrica            | Valor  |
|-------------------|--------|
| Accuracy           | 1.000  |
| F1-score (macro)   | 1.000  |
| F1-score (weighted)| 1.000  |

---

## ✅ Conclusiones  

- Tanto el aprendizaje superficial como el profundo logran una **detección casi perfecta** de tráfico benigno y ataques DoS GoldenEye y HULK.  
- La representación mediante **ventanas (windowing)** mejora la robustez del modelo.  
- Los modelos alcanzan métricas cercanas al **100% de precisión, recall y F1-score**, indicando una clasificación confiable.  

---

## 🖥️ Instalación y Uso  

Clona este repositorio:  

```bash
git clone https://github.com/Wilmer3198/WProyecto.git
cd WProyecto
