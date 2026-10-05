# Practica 2 VC

Ejercicios de la segunda práctica de laboratorio de VC.

Nicolás Hernández Castro y Gabriel Godoy Navarro - EII ULPGC 5 de octubre de 2026

## Tarea 1: Pixeles blancos por fila

En primer lugar, se lee la imagen del mandril y se convierte a niveles de grises con `cv2.cvtColor` para el procesamiento posterior. Luego, se aplica en la imagen el detector de contornos de Canny con umbral inferior 100 y umbral superior 200 con `cv2.Canny(gris, 100, 200)` para generar una imagen binaria limpia donde los píxeles con borde valen 255 y sin borde valen 0.

A continuación, se realiza el conteo de los valores de los pixeles por fila mediante la función `cv2.reduce(canny, 1, cv2.REDUCE_SUM, dtype=cv2.CV_32SC1)`. Se aplana la matriz vertical 2D a un vector unidimensional y como cada píxel blanco suma 255, se divide cada fila por 255 para saber el numero exacto de pixeles blanco por fila `(row_counts.flatten() / 255).astype(int)`. Sobre este vector se determina el valor máximo (220) usando `np.max` y se establece el umbral del 90% (198). Se localiza mediante `np.where(filas >= umbral)[0]` las 7 filas que cumplen dicha condición (corresponden a las posiciones 6, 12, 15, 20, 21, 88 y 100).

Por último, para señalizar estas posiciones de forma visible, se convierte la imagen binaria de Canny a tres canales con `cv2.cvtColor(canny, cv2.COLOR_GRAY2BGR)`, lo que permite dibujar en color sobre ella y se itera sobre las filas que cumplen la condición para trazar líneas horizontales sobre ellas con `cv2.line(canny_color, (0, y), (ancho - 1, y), (255, 0, 0), 1)`. En la imagen y en la gráfica se observa que las filas con mayor densidad de bordes se concentran en la parte superior del rostro del mandril.

![alt text](image.png)