# Trabajo de fin de grado

El trabajo de fin de grado se basa en el desarrollo de un pipeline en ROS y C++, con ayuda
de otras librerías y técnicas como son la Point Cloud Library, OpenCV, paquetes de ROS
de Darknet YOLO, para la detección de objetos en imágenes y de ORB-SLAM2, para
poder realizar la localización y mapeado simultáneos.
El pipeline será compuesto por diferentes nodos, los cuales harán diferentes trabajos,
primero se hará una sincronización de los topics de las imágenes y las nubes de puntos,
para enviar la imagen al nodo de Darknet para la detección de objetos 2D. Luego con los
objetos detectados y la nube de puntos correspondiente, se hará una segmentación de
los objetos de su escena 3D y posteriormente se eliminará los puntos no pertenecientes
al objeto mediante algoritmos proporcionados por la PCL. Al mismo tiempo, se hará
haciendo SLAM con el paquete de ORB-SLAM2 para poder obtener las matrices de
transformación de cada escena. En el último nod, tanto los objetos recortados de la nube
de puntos de la escena, la escena completa y la matriz de SLAM serán recogidos para
poder realizar una reconstrucción de la escena final, para ello se irá generando una nube
de puntos incrementalmente con los objetos recortados de cada una de las escenas,
después de haberles aplicado la matriz. En cambio, si entre un par de escenas hay mucha
diferencia en el vector de traslación de las matrices de SLAM, se les aplicará un registro
de pares de nubes para poder alinear mejor ambas escenas.
Finalmente, el objetivo de este pipeline es obtener una escena con la localización e
información de los objetos detectados por la red neuronal, con tal de dotar con mucha
más información a los usuarios que hagan uso de la escena final obtenida. Toda está
ejecución de nodos se irá haciendo en tiempo real, por eso la nube final se irá generando
incrementalmente.
