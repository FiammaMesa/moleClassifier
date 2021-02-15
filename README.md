# moleClassifier
Classification of seven mole types from a prebuild dataset.

GitHub: https://github.com/FiammaMesa

En este trabajo se pretende construir una red neuronal que sea capaz de clasificar correctamente diferentes tipos de patologías relacionadas con lunares. Para ello se parte de un dataset obtenido de Kaggle (https://www.kaggle.com/kmader/skin-cancer-mnist-ham10000) que contiene imágenes de lunares pertenecientes a siete clases de patologías.

Lo primero que se realiza es la separación de las imágenes en carpetas según a qué patología pertenezca. Esto se hace gracias al fichero "HAM10000_metadata.csv" que recoge los datos de las imágenes. Para ello se puede utilizar el fichero "Preparación datos lunares.ipynb"

Al contar con unas patologías más comunes que otras, en el dataset existe un desbalance que se solventa mediante la realización de oversampling por un lado, y undersampling por otro. Para realizar el oversampling, se toma como referencia la carpeta de patologías con menos imágenes, y se aumentan sus muestras con ayuda de la librería Albumentations (https://albumentations.ai/docs/), generando nueve muestras más por cada imagen original. Para el resto de patologías, se genera este aumento de muestras hasta que se obtienen tantas como para alcanzar la cantidad de muestras aumentadas de la patología con menos imágenes.

Por otro lado, para las carpetas que exceden el tamaño de la carpeta más pequeña una vez se hace el oversampling, se eliminan muestras aleatoriamente con el fin de balancear todo el conjunto.

Obtenidos los datos balanceados, se extrae un 30% de dichas muestras y se almacenan con la misma estructura en una carpeta de test.

Con esto ya se tiene el dataset listo para entrenar nuestro modelo, para ello utilizamos el fichero "Entrenamiento Image Data Generator-balanced.ipynb".

En el entrenamiento se hace uso del paquete Image Data Generator, gracias al cual se reduce el tamaño de la imagen, que originalmente es de 600x450, a 120x90, 200x150 y 300x225. 

Posteriormente se crea el modelo de entrenamiento, con distintos tipos de configuración para llegar al mayor valor de accuracy posible. El modelo que mejor resultado genera (53%) está formado por cinco redes convolutivas, intercaladas con maxpooling, y finalmente dos redes densas, la última con siete entradas que son los tipos de patología.

La configuración del modelo se comenzó con un tamaño de 120x90 y tres redes convolutivas más tres niveles de maxpooling, dando un resultado muy pobre (33%).

A continuación, se aumentó el número de capas convolutivas y maxpooling, consiguiendo un mejor valor de accuracy. También se aumentó el tamaño de resolución de la imagen en el data image generator, lo que dió como resultado un peor rendimiento en tiempo de ejecución y no llegando al mismo valor de accuracy. En ocasiones el accuracy se igualaba al mejor valor, pero al necesitar más recursos, nos quedamos con la configuración que menos rendimiento necesita, es decir, tamaño de imagen a 120x90 y la estructura de convolutivas y maxpooling que se nombró anteriormente.

English //TO DO
