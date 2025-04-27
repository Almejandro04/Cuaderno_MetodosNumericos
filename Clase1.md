# Clase 21/04/2025

## Metodos Analiticos

Se usan para el manejo de grandes cantidades de datos y las busqueda de soluciones exactas.
La desventaja es que no siempre es posible obtener una solucion analitica en ecuaciones mas complejas o no lineales.

**Ejemplo:**

Mediante el metodo analitico se podria resolver ecuaciones cuadraticas aplicando factorizacion, T.C.P o la formula general.

``` Python
#Resolucion de una ecuacion cuadratica mediante la formula general
import math

def formula_general(a, b, c):
    discriminante = b**2 - 4*a*c

    if discriminante >= 0:
        x1 = (-b + math.sqrt(discriminante)) / (2*a)
        x2 = (-b - math.sqrt(discriminante)) / (2*a)

        print(f"Las soluciones son x1 = {x1} y x2 = {x2}")
    else:
        print("El sistema no tiene soluciones reales")

#Ecuacion a resolver
print("x^2 + 2x - 3 = 0")

#Llamada a la funcion 
formula_general(1, 2, -3)

```

## Metodos Numericos

Se usan aproximaciones para encontrar soluciones cuando no se puede resolver analiticamente, por lo tanto, el resultado puede contener algun tipo de error.

**Ejemplo:**

Se podira aplicar metodos como el de biseccion o Newton-Raphson para encontrar raices.  

## Exactitud vs Precision  

* **Exactitud:** Es que tan cerca esta el reusltado del valor real o verdadero.

* **Precision:** Se refiere a que tan consistentes son los resultados obtenidos.

![Exactitud y Precision](https://www.wikiversus.com/blog/diferencia-entre-precision-y-exactitud/img/exactitud-vs-precision-featured_hu401876fdba8597e9d7c0132daf7f3ad1_74313_1200x900_fill_lanczos_center_2.png)

## Tipos de Errores

* **Error de corte o truncamiento:** Se produce cuando se le quitan valores a un numero decimal.
**Ejemplo:**
Pi con sus primeros 15 decimales:
Pi = 3.141592653589793
Pi con error de truncamiento y 4 cifras significativas:
Pi = 3.141

```Python
#Definicion de la constante Pi con 15 decimales como float y String
constante_pi = 3.141592653589793
constante_pi_string = str(constante_pi)

#Calculo de la constante Pi con error de truncamiento y 4 cifras significativas
constante_pi_truncamiento = ""
contador = 0
while contador < 5:
        constante_pi_truncamiento += constante_pi_string[contador]
        contador += 1

print("Constante con error de truncamiento: " + constante_pi_truncamiento)
```

* **Error de redondeo:** Se produce cuando se redondean los valores.
**Ejemplo:**
Pi con sus primeros 15 decimales:
Pi = 3.141592653589793
Pi con error de redondeo y 4 cifras significativas:
Pi = 3.142

``` Python
#Definicion de la constante Pi con 15 decimales como float 
constante_pi = 3.141592653589793

#Calculo de la constante Pi con error de redondeo y 4 cifras significativas
constante_pi_redondeo = f"{constante_pi:.3f}"

print("Constante con error de redondeo: " + constante_pi_redondeo)
```

* **Error de desbordamiento:** Se produce al superar el limite para almacenar numeros.
**Ejemplo en Python:**

```Python
#Modulo sys que da acceso a la informacion del sistema
import sys

# Tamaño máximo de un entero (en Python  es ilimitado, depende de la RAM)
print(f"Máximo valor de int: Ilimitado (limitado solo por la memoria)")

#Tiene un limite fijo porque se basa en la representacion IEEE 754
#Pasado los 15 digitos pueden existir errores de redondeo debido a como la representacion
#IEEE 754 maneja los numeros flotantes
print(f"Máximo valor de float: {sys.float_info.max}")
print(f"Precisión decimal de float: {sys.float_info.dig} dígitos")
a = 1e309
print(a)  # si se excede se obtiene infinito

# Tamaño máximo de estructuras como listas o strings, devuelve el mayor indice posible que se puede usar en una lista
# Solo si se tiene suficiente memoria, sino, se obtiene un "Memory Error"
print(f"Tamaño máximo de lista/str (en teoría): {sys.maxsize}")
```

## Representacion Numerica del IEEE 754

La representacion IEEE 754 es una forma de representar numeros de coma flotante que no pueden ser representados de forma exacta con un numero fijo.

* **Signo:** Un bit que indica si el numero es positivo o negativo (0 para negativo y 1 para positivo)

* **Exponente:** Es la representacion de un numero entero que determina cuanto hay que mover el punto decimal para obtener el numero correcto.

* **Mantisa:** La parte que contiene los digitos significativos de la representacion.

## Calculo de error

* **Error real:** Es la diferencia entre el valor real y el valor obtenido.

```Python
#Definicion de la constante Pi con 15 decimales como float 
constante_pi = 3.141592653589793

#Calculo de la constante Pi con error de redondeo y 4 cifras significativas
constante_pi_redondeo = f"{constante_pi:.3f}"
print("Constante con error de redondeo: " + constante_pi_redondeo)

#Funcion para el calculo del error real.
def error_real (valor_verdadero, valor_aproximado):
    return valor_verdadero - valor_aproximado

print(f"Error Real de la constante con error de redondeo: {error_real(constante_pi, float(constante_pi_redondeo))}")
```

* **Error absoluto:** Es la magnitud del error real.

```Python
#Definicion de la constante Pi con 15 decimales como float 
constante_pi = 3.141592653589793

#Calculo de la constante Pi con error de redondeo y 4 cifras significativas
constante_pi_redondeo = f"{constante_pi:.3f}"
print("Constante con error de redondeo: " + constante_pi_redondeo)

#Funcion para el calculo del error absoluto.
def error_absoluto (valor_verdadero, valor_aproximado):
    return abs(valor_verdadero - valor_aproximado)

print(f"Error Absoluto de la constante con error de redondeo: {error_absoluto(constante_pi, float(constante_pi_redondeo))}")
```

* **Error relativo:** Es una medida proporcional entre el error absoluto y el verdadero.

```Python
#Definicion de la constante Pi con 15 decimales como float 
constante_pi = 3.141592653589793

#Calculo de la constante Pi con error de redondeo y 4 cifras significativas
constante_pi_redondeo = f"{constante_pi:.3f}"
print("Constante con error de redondeo: " + constante_pi_redondeo)

#Funcion para el calculo del error relativo.
def error_relativo (valor_verdadero, valor_aproximado):
    if valor_verdadero != 0:
        return (abs((valor_verdadero - valor_aproximado)/valor_verdadero))
    else:
        print("No se puede dividir para 0")

print(f"Error Relativo de la constante con error de redondeo: {error_relativo(constante_pi, float(constante_pi_redondeo))}")
```

* **Error relativo porcentual:** Es el error relativo expresado como porcentaje.

```Python
#Definicion de la constante Pi con 15 decimales como float 
constante_pi = 3.141592653589793

#Calculo de la constante Pi con error de redondeo y 4 cifras significativas
constante_pi_redondeo = f"{constante_pi:.3f}"
print("Constante con error de redondeo: " + constante_pi_redondeo)

#Funcion para el calculo del error relativo porcentual.
def error_porcentual (valor_verdadero, valor_aproximado):
    if valor_verdadero != 0:
        return (abs((valor_verdadero - valor_aproximado)/valor_verdadero))*100
    else:
        print("No se puede dividir para 0")

print(f"Error Relativo Porcentual de la constante con error de redondeo: {error_porcentual(constante_pi, float(constante_pi_redondeo))}")
```
