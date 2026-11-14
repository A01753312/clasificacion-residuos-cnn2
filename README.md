Clasificación de residuos mediante deep learning
Este proyecto forma parte del portafolio de implementación de deep learning. Su objetivo es desarrollar y evaluar una red neuronal convolucional con Keras y TensorFlow para clasificar imágenes de residuos y envases en seis categorías: botellas de plástico, envases de cartón para bebidas, envases metálicos, basura doméstica, papel y cartón, y vidrio.
Datos y preparación
Utilicé el dataset Garbage classification, publicado por Manon_str en Kaggle. Revisé la lectura de las imágenes, identifiqué duplicados y excluí los grupos con etiquetas contradictorias. Después de la limpieza quedaron 7,041 imágenes, distribuidas en 5,508 para entrenamiento, 1,377 para validación y 156 para prueba.

Las imágenes se convirtieron a RGB y se redimensionaron a 160 × 160 píxeles. La normalización se incluyó dentro del modelo. El notebook contiene el código para descargar los datos, por lo que no es necesario incluirlos en el repositorio.
Modelo y ajuste
Implementé una CNN con tres bloques de capas convolucionales y agrupamiento, seguidos de GlobalAveragePooling y capas densas para la clasificación. Para evaluar una posible mejora, continué el entrenamiento desde los mejores pesos del modelo inicial y reduje la tasa de aprendizaje de 0.001 a 0.0003.
Versión	Exactitud de validación	Pérdida de validación
Inicial	69.57 %	0.7973
Ajustada	70.88 %	0.7384


El ajuste mejoró la exactitud de validación en 1.31 puntos porcentuales. Como también se añadieron épocas de entrenamiento, no es posible atribuir toda la mejora únicamente al cambio en la tasa de aprendizaje.
Resultados y limitaciones
El modelo ajustado obtuvo 32.05 % de exactitud en prueba y un F1 macro de 0.280. Estos resultados muestran que todavía tiene dificultades para generalizar. En la inspección de ejemplos observé diferencias de orientación, fondos e iluminación entre entrenamiento y prueba, que podrían contribuir a esa diferencia de desempeño.

Como posibles mejoras, considero ampliar la variedad de imágenes, revisar las etiquetas y aplicar aumento de datos durante el entrenamiento. El notebook también incluye una función para clasificar imágenes nuevas y ejemplos de su uso.
Archivos y uso
- Clasificacion_Residuos_Portafolio.ipynb: implementación, análisis y resultados ejecutados.
- modelo_ajustado.keras: arquitectura y pesos del modelo final.
- clases.json: orden de las categorías utilizadas por el modelo.
- README.md: descripción del proyecto.
El notebook puede revisarse en Google Colab o Jupyter. Para realizar predicciones sin repetir el entrenamiento, se carga el archivo .keras, se recuperan las categorías de clases.json y se utiliza la función predecir_imagen(ruta) de la sección Aplicación. La puntuación que devuelve el modelo no garantiza que la clasificación sea correcta.
