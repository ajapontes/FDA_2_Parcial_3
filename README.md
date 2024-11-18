# FDA_2_Parcial_3
Universidad ICESI.  
Maestría en Ciencia de Datos.  
Asignatura de Fundamentos de Analítica II.  
Parcial 3: CNN clasificación y localización.  
Integrantes: Alfredo Guevara | Álvaro Rodríguez.
# Descripción
Se requiere desarrollar un modelo predictivo para determinar la clasificación y localización de Pinguinos o Tortugas que aparecen en una imagen. Se le proporciona un conjunto de datos que contiene imágenes y sus anotaciones correspondientes. Su modelo debe detectar qué animal es y la ubicación en la foto.  Las métricas de evaluación para esta competencia es el IOU para la tarea de regresión de cuadro delimitador y accuracy para la tarea de clasificación de objetos.
# Citation
Daniel Osorio and JavierDiaz. AF II 2024-II: object localization. https://kaggle.com/competitions/af-ii-2024-ii-object-localization, 2024. Kaggle.
# Evaluation
Para facilidad de análisis del presente repositorio, lo dividiremos en 3 grandes rubros:
1.	Aumento de datos (Data Augmentation):
Uso de diferentes técnicas de aumento de datos para ver su impacto en el desempeño de ambas tareas (clasificación y localización).
2.	CNN personalizado:
Modelo de red neuronal convolucional personalizado como backbone (features extractor) y entrénelo desde cero.
3.	CNN con transferencia de aprendizaje (Transfer learning):
Usar dos modelos preentrenados como backbones y conectar los creados previamente cabezas de clasificación y regresión para recibir entradas de ellas.
# 1.	Data Augmentation.
El primer paso para construir el CNN personalizado y el CNN con transfer learning, es construir un nuevo dataset de train local, que contenga mayor cantidad de imágenes usando la técnica de data augmentation.  La información fuente para este proceso que incluye notebook, el nuevo archivo train.csv y las 2.860 imágenes generadas, se pueden encontrar en la carpeta pública de Kaggle https://www.kaggle.com/datasets/alvarorodriguez87/dataalvaro?select=data_augmentation
Sin embargo, por temas de compatibilidad con el notebook original y el aplicativo Kaggle, este nuevo dataset genera inconvenientes al correr la red neuronal en el paso de entrenamiento del modelo.  Esta situación se dejó en evidencia en la clase del 13 de noviembre de 2024 con el profesor Daniel Osorio.
De tal manera, se ha decidido conversar la metodología inicial de data augmenation, es decir, que dicho proceso se genere en línea a través del aplicativo Kaggle con el dataset original de Daniel.
# 2.	CNN Personalizado.
## 2.1  CNN Personalizado.
•	Ver carpeta [02_01_20241117_0612_CNN_personalizado](/02_01_20241117_0612_CNN_personalizado/).  
# 3.	CNN con transferencia de aprendizaje.
## 3.1.	VGG16 original con 5 épocas
•	Ver carpeta [03_01_20241113_1150_VGG16_original_5_epocas](/03_01_20241113_1150_VGG16_original_5_epocas/).  
•	Se ajustó el modelo original de Daniel, incorporando 5 épocas en el entrenamiento y un learning rate de 0,004.  Los resultados generan mejoría, llegando a un nivel IOU de validación de 0.419 y de accuracy de 0.85.  El accuracy en Kaggle es del 0.7510.  
# 3.2.	VGG16_2_epocas
•	Ver carpeta [03_02_20241114_0122_VGG16_2_epocas](/03_02_20241114_0122_VGG16_2_epocas/).  
•	En este modelo se realizó un modelo VGG16 ajustando capas tanto en el backbone como en las cabezas del modelo.  
•	En el backbone se modificaron las capas convolucionales y se agregaron capas de batch normalization y de activación relu.  
•	En las cabezas de clasificación y de regresión se modificaron las capas lineales y de activación relu.  
•	Learning rate: 0.001.  
•	Épocas: 2.  
•	Se llegó a un IOU de validación de 0.2827, accuracy de validación de de 1.0 y accuracy de Kaggle del 0.7510.  
•	Debido a la gran mejoría en el accuracy de validación, se conservará el learning rate para el resto de experimentos de transfer learning.  
## 3.3.	VGG16_12_epocas
•	Ver carpeta [03_03_20241114_0654_VGG16_12_epocas](/03_03_20241114_0654_VGG16_12_epocas/).  
•	En este modelo se realizó un moldeo VGG16 ajustando capas tanto en el backbone como en las cabezas del modelo.  Los cambios mencionados son respecto al modelo original, pero frente al modelo anterior no se modifica ni el backbone ni las cabezas, debido a la mejoría presentada.  
•	Learning rate: 0.001.  
•	Épocas: 12.  
•	Resultados: IOU validación: 0.3654, Accuracy validación: 1.0, Acurracy Kaggle: 0.7510.  
## 3.4.	03_04_20241114_1230_Resnet50_2_epocas
•	Ver carpeta [03_04_20241114_1230_Resnet50_2_epocas](/03_04_20241114_1230_Resnet50_2_epocas/).  
•	Modificamos el backbone por un resnet50.  
•	Las cabezas las conservamos respecto al modelo anterior.  
•	Learning rate: 0.001.  
•	Debido a que lo resultado del modelo anterior con 2 épocas fueron aceptables, conservaremos ese valor.  
•	Resultados: IOU validación: 0.4345, acurracy validación: 0.8571, Accuracy Kaggle: 0.73469.  
•	Vemos que el accuracy de Kaggle empieza a decaer.  
##  3.5.	Efficientnet b0 10 épocas
•	Ver carpeta [03_05_20241114_1307_efficientnet_b0_10_epocas](/03_05_20241114_1307_efficientnet_b0_10_epocas/).  
•	Modificamos el backbone por un Efficientnet b0.  
•	Las cabezas las conservamos respecto al modelo anterior.  
•	Learning rate: 0.001.  
•	Épocas:10.  
•	Resultados: IOU validación: 0.3688, acurracy validación: 0.4286, Accuracy Kaggle: 0.5102.  
## 3.6.	Mobilenet 10 épocas
•	Ver carpeta [03_06_20241114_1332_mobilenet_V2_10_epocas](/03_06_20241114_1332_mobilenet_V2_10_epocas/).  
•	Modificamos el backbone por un mobilenet_v2.  
•	Las cabezas las conservamos respecto al modelo anterior.  
•	Learning rate: 0.001.  
•	Épocas:10.  
•	Resultados: IOU validación: 0.3387, acurracy validación: 0.7142, Accuracy Kaggle: 0.48979.  
# 3.7.	Swin transformer 3 épocas
•	Ver carpeta [03_07_20241114_1403_Swin_transformer_3_epocas](/03_07_20241114_1403_Swin_transformer_3_epocas/).  
•	Modificamos el backbone por un Swin transformer.  
•	Las cabezas las conservamos respecto al modelo anterior.  
•	Learning rate: 0.001.  
•	Épocas: 3.  
•	Resultados: IOU validación: 0.3119, acurracy validación: 0.7142, Accuracy Kaggle: 0.48979.  
# 3.8.	VGG16 early stopping
•	Ver carpeta [03_08_20241117_1711_VGG16__early_stopping](/03_08_20241117_1711_VGG16__early_stopping_/).  
•	Usamos el backbone de VGG16.  
•	Las cabezas las conservamos respecto al modelo anterior.  
•	Learning rate: 0.001.  
•	Épocas optmizadas: 9.  
•	Resultados: IOU validación: 0.2518, acurracy validación: 0.9062, Accuracy Kaggle: 0.5918.  
# 4.	Conclusiones
## Tabla resumen de las métricas de evaluación de los modelos
|Tipo modelo|Nombre modelo|Carpeta|Épocas|Learning rate|IOU validación|Accuracy Validación|Accuracy Kaggle|
|:----|:----|:----|:----|:----|:----|:----|:----|
|CNN Personalizado|2.1 CNN Personalizado|02_01_20241117_0612_CNN_personalizado| | | | | |
|Transfer learming|3.1 VGG16 original con 5 épocas|03_01_20241113_1150_|5|0.004|0.419|0.85|0.7510|
| | |VGG16_original_5_epocas| | | | | |
|Transfer learning|3.2 VGG16_2_epocas|03_02_20241114_0122_|2|0.001|0.2827|1.0|0.7510|
| | |VGG16_2_epocas| | | | | |
|Transfer learning|3.3 VGG16_12_epocas|03_03_20241114_0654_|12|0.001|0.3654|1.0|0.7510|
| | |VGG16_12_epocas| | | | | |
|Transfer learning|3.4 Resnet50_2_epocas|03_04_20241114_1230_Resnet50_2_epocas|2|0.001|0.4345|0.8571|0.73469|
| | | | | | | | |
|Transfer learning|3.5.Efficientnet b0 10 épocas|03_05_20241114_1307_efficientnet_b0_|10|0.001|0.3688|0.4286|0.5102|
| | |10_epocas| | | | | |
|Transfer learning|3.6. Mobilenet 10 épocas|03_06_20241114_1332_mobilenet_V2_|10|0.001|0.3387|0.7142|0.48979|
| | |10_epocas| | | | | |
| | | | | | | | |
|Transfer leraning|3.7 Swin_transformer_3_epocas|03_07_20241114_1403_Swin_transformer_|3|0.001|0.3119|0.7142|0.48979|
| | |3_epocas| | | | | |
|Transfer Learning|3.8 VGG16 con early stopping|03_08_20241117_1711_VGG16__early_stopping|9|0.004|0.2518|0.9062|0.5918|

## 4.1.	Modelo CNN Personalizado.
### 4.1.1
### 4.1.2
## 4.2.	Modelos CNN con transfer learning.
### 4.2.1.	 
Al probar múltiples configuraciones de los modelos con transfer learning, el máximo accuracy obtenido en Kaggle es 0.7510, obtenido con los 3 primeros modelos VGG16 (ver detalles en la tabla anterior). 
### 4.2.2.	 
Al incorporar un early stopping el parámetro de las épocas se calcula automáticamente, evitando usar una cantidad de épocas muy altas.
### 4.2.3.	 
Un learning rate de 0.004 generó el mejor modelo.
### 4.2.4.	 
El IOU es la variable más compleja de optimizar en train.  El valor máximo obtenido es 0.4345.
### 4.2.5.	 
Daniel y Javier: si es posible hacer una clase extra para entender cómo optimizar este modelo, se los agradeceríamos mucho.  Siento que faltó practicar mas el tema de los bounding boxes dentro de las clases ordinarias.





