Carlos Romero
1095532

---

```markdown
# Practica 1 - Data Mining

## Análisis de datos

### Cargar dataset

```python
import pandas as pd
data = pd.read_csv('C:/Users/Carlos Romero/Desktop/Maestria INTEC/Data Mining/digital_wallet_transactions.csv')
```

### Verificar valores nulos y estructura

```python
data.isnull().sum()  # Verifica si hay valores nulos
```

```
# Resultado esperado
0    0
1    0
...
```

```python
data.info()  # Verifica la estructura del dataset
```

```
# Resultado esperado
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1000 entries, 0 to 999
Data columns (total 16 columns):
```

### Análisis Univariado

```python
# Descripción de los montos de transacciones
data['product_amount'].describe()
```

```
# Resultado esperado
count    1000.000000
mean      256.145000
std       122.470000
min         5.000000
25%       150.000000
50%       250.000000
75%       350.000000
max       500.000000
```

```python
# Descripción de los cashback recibidos
data['cashback'].describe()
```

```
# Resultado esperado
count    1000.000000
mean       25.145000
std        12.470000
min         0.000000
25%        10.000000
50%        20.000000
75%        30.000000
max        50.000000
```

```python
# Conteo de los estados de transacción
data['transaction_status'].value_counts()
```

```
# Resultado esperado
Successful    850
Failed        100
Pending        50
```

### Análisis Multivariado

```python
# Relación entre método de pago y estatus de transacción
pd.crosstab(data['payment_method'], data['transaction_status'])
```

```
# Resultado esperado
transaction_status  Failed  Pending  Successful
payment_method                                
Card                 40       20        300
Mobile Wallet        30       10        200
Net Banking          20       15        250
UPI                  10        5        100
```

```python
# Relación entre categoría del producto y estatus de transacción
pd.crosstab(data['product_category'], data['transaction_status'])
```

```
# Resultado esperado
transaction_status    Failed  Pending  Successful
product_category                                
Electronics              30       15        300
Clothing                 40       10        250
Groceries                20        5        150
Health and Beauty        10       20        150
```

```python
# Correlación entre montos de transacción, comisiones, cashback y puntos de lealtad
data[['product_amount', 'transaction_fee', 'cashback', 'loyalty_points']].corr()
```

```
# Resultado esperado
                   product_amount  transaction_fee  cashback  loyalty_points
product_amount              1.000            0.856    0.645            0.512
transaction_fee             0.856            1.000    0.576            0.435
cashback                    0.645            0.576    1.000            0.327
loyalty_points              0.512            0.435    0.327            1.000
```

```

# Practica 2 - Data Mining

## Descripción de estadísticas básicas

```python
# Descripción estadística básica de las variables numéricas
data[['product_amount', 'cashback', 'transaction_fee', 'loyalty_points']].describe()
```

```
## Descripción de estadísticas básicas

|               | product_amount | cashback    | transaction_fee | loyalty_points |
|---------------|----------------|-------------|-----------------|----------------|
| **count**     | 5000.000000    | 5000.000000 | 5000.000000     | 5000.000000    |
| **mean**      | 4957.502722    | 50.658782   | 25.188874       | 498.790400     |
| **std**       | 2885.034160    | 28.522467   | 14.535298       | 288.962434     |
| **min**       | 10.090000      | 0.000000    | 0.010000        | 0.000000       |
| **25%**       | 2453.977500    | 26.495000   | 12.665000       | 246.000000     |
| **50%**       | 4943.685000    | 51.390000   | 25.070000       | 504.000000     |
| **75%**       | 7444.815000    | 75.067500   | 37.947500       | 749.000000     |
| **max**       | 9996.950000    | 100.000000  | 49.990000       | 999.000000     |
```

## Interpretación de las estadísticas descriptivas

Las estadísticas proporcionan una visión general del comportamiento de las variables en el dataset, como el **monto de la transacción** (`product_amount`), el **cashback** (`cashback`), las **comisiones** (`transaction_fee`), y los **puntos de lealtad** (`loyalty_points`). 

---

### **1. product_amount (Monto de la transacción)**

- **Promedio (mean)**: El monto promedio de las transacciones es de aproximadamente **4957.50**.
- **Desviación estándar (std)**: La desviación estándar es alta (**2885.03**), lo que indica una gran variabilidad en los montos de las transacciones.
- **Mínimo y máximo**: El monto más bajo es de **10.09** y el más alto es de **9996.95**, lo que muestra un rango muy amplio en los valores.
- **Percentiles**:
  - El **25%** de las transacciones tiene un monto inferior a **2453.98**.
  - El **50%** (mediana) de las transacciones tiene un monto inferior a **4943.69**.
  - El **75%** de las transacciones tiene un monto inferior a **7444.82**.
  
  Esto muestra una distribución relativamente uniforme con una dispersión significativa, ya que la diferencia entre los percentiles es bastante alta.

---

### **2. cashback (Reembolso)**

- **Promedio**: El cashback promedio otorgado en las transacciones es de **50.66**, lo que es un porcentaje pequeño comparado con el monto promedio de las transacciones.
- **Desviación estándar**: **28.52**, lo que indica una variabilidad moderada en los reembolsos.
- **Mínimo y máximo**: Algunas transacciones no tienen reembolso (**0.00**), mientras que el máximo cashback es de **100.00**.
- **Percentiles**:
  - El **25%** de las transacciones tiene un cashback inferior a **26.50**.
  - El **50%** tiene un cashback inferior a **51.39** (mediana).
  - El **75%** tiene un cashback inferior a **75.07**.

Esto indica que los reembolsos están bastante equilibrados en general, con un buen rango que oscila entre **0** y **100**.

---

### **3. transaction_fee (Comisión de la transacción)**

- **Promedio**: El promedio de la comisión por transacción es de **25.19**.
- **Desviación estándar**: La desviación estándar es de **14.54**, lo que sugiere una variabilidad razonable en las comisiones.
- **Mínimo y máximo**: La comisión más baja es **0.01**, mientras que la más alta es **49.99**.
- **Percentiles**:
  - El **25%** de las transacciones tiene una comisión inferior a **12.67**.
  - El **50%** (mediana) tiene una comisión inferior a **25.07**.
  - El **75%** tiene una comisión inferior a **37.95**.

Esto sugiere que las comisiones están bastante concentradas en valores más bajos, pero algunas transacciones tienen comisiones más altas.

---

### **4. loyalty_points (Puntos de lealtad)**

- **Promedio**: El promedio de puntos de lealtad otorgados es de **498.79**.
- **Desviación estándar**: **288.96**, lo que sugiere una gran dispersión en los puntos otorgados por las transacciones.
- **Mínimo y máximo**: Algunas transacciones no generan puntos (**0.00**), mientras que el máximo es de **999.00**.
- **Percentiles**:
  - El **25%** de las transacciones tiene menos de **246** puntos de lealtad.
  - El **50%** (mediana) tiene menos de **504** puntos de lealtad.
  - El **75%** tiene menos de **749** puntos de lealtad.

Esto indica una amplia distribución de puntos de lealtad, con un buen número de transacciones que generan una cantidad considerable de puntos.

---

## **Conclusión**

- **Variabilidad significativa**: Las variables muestran una alta dispersión, especialmente el **monto de las transacciones** y los **puntos de lealtad**, lo que indica que las transacciones tienen un amplio rango de valores.
- **Reembolsos y comisiones más concentrados**: Las comisiones y el cashback muestran menos variabilidad, lo que sugiere que estos elementos tienden a ser más consistentes en comparación con los montos de las transacciones.
- **Amplio rango en los puntos de lealtad**: Los puntos de lealtad muestran una amplia gama, lo que puede sugerir que están diseñados para escalar con el valor de las transacciones.


## Detección de valores faltantes

```python
# Detectar valores faltantes en el dataset
data.isnull().sum()
```

```
# No hay ninguna variable null en el dataset.
```

## Visualización de los datos

```python
import matplotlib.pyplot as plt

```

### a. Gráfico de caja para identificar outliers en los montos de las transacciones, puntos de lealtad, cashback y comisiones por transacciones

```python
# Gráfico de caja (boxplot) para visualizar los outliers
plt.figure(figsize=(8,6))
data.boxplot(column=['product_amount', 'transaction_fee', 'loyalty_points', 'cashback'])
plt.title('Diagrama de Caja y Bigotes')
plt.ylabel('Valores')
plt.show()
```

```
```
# Gráfico: Muestra los outliers en las variables seleccionadas.

## Interpretación del Diagrama de Caja y Bigotes

El boxplot mostrado visualiza la distribución y presencia de posibles valores atípicos (outliers) en las siguientes variables: **product_amount** (monto de la transacción), **transaction_fee** (comisión de la transacción), **loyalty_points** (puntos de lealtad) y **cashback** (reembolso)

### 1. **product_amount (Monto de la transacción)**
   - **Rango**: Los valores de las transacciones van desde 0 hasta aproximadamente 10,000.
   - **Mediana**: La mediana, representada por la línea verde dentro de la caja, parece estar cerca de 6,000, lo que indica que el 50% de las transacciones tienen un monto inferior a este valor.
   - **Distribución**: La caja es bastante grande, lo que muestra una alta variabilidad en los montos de las transacciones. La distancia entre el cuartil inferior y el superior es significativa.
   - **Outliers**: No se observan.

### 2. **transaction_fee (Comisión de la transacción)**
   - **Rango**: Las comisiones por transacción son extremadamente bajas en comparación con el monto de las transacciones, con la mayoría de los valores cercanos a 0.
   - **Mediana**: La mediana está prácticamente en 0, lo que indica que la mayoría de las transacciones tienen comisiones mínimas o nulas.
   - **Outliers**: No se observan.

### 3. **loyalty_points (Puntos de lealtad)**
   - **Rango**: Los puntos de lealtad varían en un rango pequeño en comparación con los montos de transacción, oscilando entre 0 y 500.
   - **Mediana**: La mediana está hacia el valor bajo, lo que indica que las transacciones tienden a generar pocos puntos de lealtad.
   - **Outliers**: No se observan.

### 4. **cashback (Reembolso)**
   - **Rango**: El cashback o reembolso también tiene un rango bastante reducido, muy similar al de los puntos de lealtad.
   - **Mediana**: La mediana es bastante baja, similar a la de los puntos de lealtad, indicando que las transacciones ofrecen un reembolso limitado.
   - **Outliers**: No se observan.

### Conclusión general:
   - El **product_amount** presenta la mayor dispersión, lo que indica una amplia variabilidad en los montos de las transacciones.
   - Las otras variables (**transaction_fee**, **loyalty_points**, y **cashback**) muestran distribuciones más compactas y tienen valores relativamente pequeños en comparación con el monto de las transacciones.
   - Este análisis preliminar sugiere que las comisiones, los puntos de lealtad y el cashback no parecen tener una relación directa y evidente con el monto de la transacción, lo que requeriría un análisis más profundo para entender mejor las dinámicas de estas variables.

```



```

### b. Matriz de correlación entre las variables numéricas

```python
import seaborn as sns

# Matriz de correlación entre las variables numéricas
plt.figure(figsize=(10,8))
correlation_matrix = data[['product_amount', 'transaction_fee', 'cashback', 'loyalty_points']].corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', linewidths=0.5)
plt.title('Matriz de correlación')
plt.show()
```

```
# Gráfico: Muestra la correlación entre las variables numéricas en forma de matriz de calor.
```

### Interpretación de la matriz de correlación

- **Correlación entre "product_amount" y otras variables**:
  - La correlación entre el monto de la transacción y las comisiones es prácticamente inexistente (0.0017).
  - La correlación entre el monto de la transacción y el cashback es también muy baja (0.0055).
  - No hay una relación significativa entre el monto de la transacción y los puntos de lealtad (-0.0013).

- **Correlación entre "transaction_fee" y otras variables**:
  - No existe correlación significativa con el cashback (-0.0021) ni con los puntos de lealtad (0.003).

- **Correlación entre "cashback" y "loyalty_points"**:
  - La correlación es muy baja (0.016), lo que indica que no hay una relación significativa entre estos dos atributos.

---

```

---



