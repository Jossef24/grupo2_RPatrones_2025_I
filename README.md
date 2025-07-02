# Grupo 02 - Reconocimiento de Patrones 2025-I
## Presentación del equipo
### Descripción con foto de cada integrante

| Foto | Descripción |
|---|---|
|<div align="center"><image src="https://github.com/Jossef24/grupo2_RPatrones_2025_I/blob/main/Imagenes/Foto_Nicolle.jpeg" width="400px" height="200px">| **Nicolle Muñoz Huamán**<br>*nicolle.munoz@upch.pe*<br> <p align="justify"> Estudiante de Ingeniería Biomédica en 9no ciclo, con interés en la aplicación de tecnologías emergentes en salud como impresión 3D. Tengo experiencia en la investigación de tecnología médica aplicada a la formación de personal de salud, desarrollando simuladores médicos.</p>| 
| | **Jose Rosales Juarez**<br>*jose.rosales@upch.pe*<br> <p align="justify"> Estudiante de Ingeniería Biomédica en 9no ciclo, con interés en la aplicación de tecnologías emergentes en salud como impresión 3D. Tengo experiencia en la investigación de tecnología médica aplicada a la formación de personal de salud, desarrollando simuladores médicos.</p>|
| | **Franco Rozas**<br>*franco.rozas@upch.pe*<br> <p align="justify"> Estudiante de noveno semestre de Ingeniería Biomédica en la Pontificia Universidad Católica del Perú (PUCP) y la Universidad Peruana Cayetano Heredia (UPCH), con un interés en las áreas de ingeniería clínica y procesamiento de señales biomédicas. Apasionado por la aplicación de tecnologías innovadoras para mejorar la atención médica y la calidad de vida de los personas.</p>| 
| | **Jossef Tintaya**<br>*jossef.tintaya@upch.pe*<br> <p align="justify"> Estudiante de Ingeniería Biomédica en 9no ciclo, con interés en la aplicación de tecnologías emergentes en salud como impresión 3D. Tengo experiencia en la investigación de tecnología médica aplicada a la formación de personal de salud, desarrollando simuladores médicos.</p>| 

# Gesture Recognition for Myoelectric Prostheses using HD-sEMG: A Comparative Evaluation of Machine Learning and Deep Learning
## Descripción del proyecto
### Problemática
A nivel mundial, los casos de amputaciones van en aumento y se estima que para el año 2050, la prevalencia alcance los 3.2 millones de personas [1]. La p´erdida de alguna sección corporal, limita significativamente la vida de la persona, no solo a nivel funcional, sino tambi´en en el ámbito emocional y social. Entre las amputaciones de la extremidad superior, el sitio más comú es nivel transhumeral con un 45% de los casos [2]; esto significa que la persona perdió por completo su capacidad de desarrollar tareas que conecten con su entorno, disminuyendo el grado de independencia para realizar sus actividades cotidianas. Es por ello, que el desarrollo de prótesis de miembro superior viene siendo un campo bastante abordado con el fin de brindar una alternativa a los pacientes afectados para mejorar su independencia y restablecer su estilo de vida. </p> 
Entre los diferentes tipos de prótesis, las de tipo mioeléctrica pretenden ser la mejor alternativa; en el caso de las mano, principalmente por su capacidad de realizar diversos tipos de agarres funcionales partir de la actividad muscular del paciente, usando sensores de electromiografıía de superficie (sEMG)[3]. A pesar de los avances en este tipo de prótesis, su eficacia sigue limitada por dificultades en el reconocimiento preciso de gestos musculares, principalmente debido a la baja resolución espacial y temporal de las señales electromiográficas convencionales (sEMG), complicando así el desarrollo de sistemas robustos y precisos. Esta problemática aumenta al intentar reconocer múltiples gestos simultáneamente. </p> 
Para superar esta limitación, es necesario explorar tecnologías avanzadas como la *electromiografía de alta densidad* (HD-sEMG), que proporciona mayor detalle en la captura de patrones musculares. No obstante, aún existe el desafío de identificar los modelos computacionales más adecuados para aprovechar plenamente estas señales en el control de prótesis mioeléctricas.</p>

## Metodología
### Dataset
Se utilizó el conjunto de datos público *Hyser* [4], que contiene señales HD-sEMG de 256 canales adquiridas a 2048 Hz, con 34 gestos manuales registrados en 20 participantes sanos (12 hombres, 8 mujeres, 22–34 años).
Las señales se estructuran en cinco subconjuntos: reconocimiento de patrones (PR), contracción voluntaria máxima (MVC), 1-DoF, N-DoF y tareas aleatorias.

### Preprocesamiento
Se aplicó normalización tipo z-score para reducir la variabilidad entre sujetos. Las señales fueron recortadas a 0.5 segundos finales de cada contracción, eliminando la transición desde el estado relajado.

### Feature Extraction
Para los modelos de ML se extrajeron características temporales y frecuenciales destacadas en la literatura, tales como MAV, RMS, ZC, SSC, WAMP (dominio temporal) y MNF, MDF, PKF (dominio frecuencial)
Las señales se transformaron a espectrogramas mediante la Transformada Rápida de Fourier de Tiempo Corto (STFT), generando tensores multicanal ideales para redes convolucionales 2D (CNN).

### Entrenamiento de modelos
- **Regresión Logística (LR)**: Se optimizó mediante GridSearchCV con validación cruzada estratificada (5-fold), explorando penalizaciones L1, L2 y ElasticNet.
- **SVM lineal (Linear SVC)**: Se entrenó con RandomizedSearchCV (3-fold), explorando penalizaciones y funciones de pérdida (hinge, squared hinge).
- **CNN**: Arquitectura compuesta por capas Conv2D, BatchNorm, ReLU, MaxPooling, Flatten y Linear. Se utilizó el optimizador Adam (LR=1e-3), weight decay de 1e-4, función de pérdida CrossEntropyLoss y scheduler ReduceLROnPlateau.

### Evaluación
Los modelos se evaluaron utilizando métricas de clasificación multiclase. Para asegurar reproducibilidad, se fijó la semilla aleatoria (*random state = 42*) y se implementó paralelización computacional para reducir los tiempos de entrenamiento.

## Resultados 
Para una comparación justa y rigurosa, todos los modelos fueron entrenados y evaluados bajo las mismas condiciones y utilizando las mismas métricas: exactitud (accuracy), precisión (precision), sensibilidad (recall) y F1-score, evidenciando un desempeño inferior respecto a los modelos tradicionales.

En el caso específico de la CNN, aunque durante el entrenamiento se observaron altos valores de exactitud (superiores al 90% en las últimas épocas), este rendimiento no se replicó en el conjunto de prueba, lo que indica un problema de *sobreajuste*. 

## Conclusiones 
✔ Mejor desempeño de los modelos tradicionales de machine learning frente al CNN en este contexto.<br>
✔ **Regresión Logística** alcanzó el máximo accuracy (60.48 %)<br>
✔ Importancia crítica de la selección y optimización de características para aplicaciones protésicas.<br>
✔ Como recomendaciones **futuras** es llegar implementar métodos avanzados de reducción de dimensionalidad y aplicar técnicas de aumento de datos para mejorar la generalización de redes profundas.<br>

# Bibliografía
[1] “Amputaciones y desarticulaciones de los miembros: miembro superior”, EMC - Téc. Quirúrgicas - Ortop. Traumatol., vol. 13, núm. 4, pp. 1–18, dic. 2021, doi: 10.1016/S2211-033X(21)45768-3.
[2] J. L. Vara Mayo, “Evaluación de funcionalidad y calidad de vida en personas con amputación de miembro superior usuarias y no usuarias de prótesis”, bachelor thesis, 2020. Consultado: el 14 de mayo de 2025. [En línea]
[3] W. Nishino, Y. Yamanoi, Y. Sakuma, y R. Kato, “Development of a myoelectric prosthesis simulator using augmented reality”, en 2017 IEEE International Conference on Systems, Man, and Cybernetics (SMC), Banff, AB: IEEE, oct. 2017, pp. 1046–1051. doi: 10.1109/SMC.2017.8122749.
[4] X. Jiang et al., “Open Access Dataset, Toolbox and Benchmark Processing Results of High-Density Surface Electromyogram Recordings” IEEE Transactions on Neural Systems and Rehabilitation Engineering, vol. 29, pp. 1035–1046, 2021, doi: https://doi.org/10.1109/tnsre.2021.3082551.
