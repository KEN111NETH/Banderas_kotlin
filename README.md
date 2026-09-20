# Banderas del mundo con Jetpack Compose

Este proyecto consiste en realizar diferentes prácticas de la materia de Desarrollo Móvil (Android), utilizando Jetpack Compose para crear las banderas de diferentes países.

Cada bandera se encuentra en su propia rama de Git. Todas las ramas deben salir de `main` para que cada práctica sea independiente y no dependa de otra.

## Prácticas

### Práctica 01 — México

Rama: `practica-01-mexico`

Para hacer la bandera de México se utiliza principalmente un `Row`, `weight` y un `Box` para colocar el escudo en el centro.

Archivo: `BanderaMexico.kt`

### Práctica 02 — Francia

Rama: `practica-02-francia`

La bandera de Francia se realiza utilizando un `Row`, dividido en tres partes iguales.

Archivo: `BanderaFrancia.kt`

### Práctica 03 — Italia

Rama: `practica-03-italia`

La bandera de Italia utiliza también un `Row` con tres franjas. Se reutiliza prácticamente el mismo patrón que en la bandera de Francia.

Archivo: `BanderaItalia.kt`

### Práctica 04 — Alemania

Rama: `practica-04-alemania`

Para Alemania se utiliza un `Column`, ya que las tres franjas de la bandera están colocadas de manera horizontal, una encima de otra.

Las tres franjas tienen el mismo tamaño.

Archivo: `BanderaAlemania.kt`

### Práctica 05 — España

Rama: `practica-05-espana`

La bandera de España utiliza un `Column`, pero las franjas no tienen el mismo tamaño.

Se utiliza una proporción de `1:2:1`, haciendo que la franja del centro sea más grande que las otras dos.

Archivo: `BanderaEspana.kt`

### Práctica 06 — Colombia

Rama: `practica-06-colombia`

La bandera de Colombia también utiliza un `Column`, pero en este caso se utiliza una proporción de `2:1:1`.

Esto hace que la franja amarilla sea más grande que las franjas azul y roja.

Archivo: `BanderaColombia.kt`

### Práctica 07 — Argentina

Rama: `practica-07-argentina`

Para Argentina se utiliza un `Box` junto con `Canvas`.

El `Canvas` permite dibujar el sol que aparece en el centro de la bandera, incluyendo sus rayos.

Archivo: `BanderaArgentina.kt`

### Práctica 08 — Brasil

Rama: `practica-08-brasil`

La bandera de Brasil utiliza `GenericShape` para crear el rombo amarillo y `CircleShape` para crear los elementos circulares.

Archivo: `BanderaBrasil.kt`

### Práctica 09 — Japón

Rama: `practica-09-japon`

La bandera de Japón es más sencilla. Se utiliza un `Box` para la bandera y un `CircleShape` para crear el círculo rojo del centro.

Archivo: `BanderaJapon.kt`

### Práctica 10 — Estados Unidos

Rama: `practica-10-estados-unidos`

Para la bandera de Estados Unidos se utiliza `repeat()` para generar las 50 estrellas.

También se utiliza un cantón para la parte azul y `drawPath` para crear las estrellas.

Archivo: `BanderaEEUU.kt`

### Práctica 11 — Chile (bonus)

Rama: `practica-11-chile`

Esta práctica es un bonus y utiliza `GenericShape` junto con algunos cálculos de trigonometría para crear las formas necesarias.

Archivo: `BanderaChile.kt`

## Dónde colocar los archivos

Los archivos de las banderas deben colocarse dentro del paquete del proyecto.

Por ejemplo:

```text
app/src/main/java/com/example/banderascompose/BanderaMexico.kt
```

Es importante revisar el `package` que aparece al inicio de cada archivo.

Si el proyecto utiliza otro `applicationId` o un paquete diferente, se debe cambiar esa primera línea para que coincida con la ubicación real del archivo.

Si no coincide, Android Studio puede marcar errores.

## Cómo trabajar con Git en cada práctica

Para cada práctica se debe empezar desde `main` y no desde la rama anterior.

Primero se cambia a `main`:

```bash
git checkout main
```

Después se actualiza con los últimos cambios del repositorio:

```bash
git pull origin main
```

Luego se crea la rama de la práctica.

Por ejemplo, para México:

```bash
git checkout -b practica-01-mexico
```

Después se coloca el archivo `BanderaMexico.kt` dentro del proyecto y se prueba utilizando el `@Preview`.

Cuando la práctica ya esté terminada, se agregan los cambios:

```bash
git add .
```

Después se hace el commit:

```bash
git commit -m "Practica 01: Bandera de Mexico con Row y Box"
```

Y finalmente se sube la rama al repositorio:

```bash
git push origin practica-01-mexico
```

Si se necesita, también se puede crear un Pull Request para pasar los cambios de la rama a `main`.

Este proceso se repite con cada bandera.

La idea de que todas las ramas salgan de `main` es que cada práctica sea independiente. Por eso algunos elementos pueden aparecer repetidos en diferentes ramas.

Por ejemplo, la estrella utilizada en Estados Unidos y la de Chile pueden estar duplicadas intencionalmente para que ninguna práctica dependa de otra rama.

## Cómo mostrar la bandera en el emulador

Para mostrar una bandera en la aplicación se debe llamar al composable correspondiente desde `MainActivity.kt`.

Dentro de `setContent` se puede colocar algo como:

```kotlin
setContent {
    BanderasComposeTheme {
        Surface(modifier = Modifier.fillMaxSize()) {
            BanderaMexico(modifier = Modifier.fillMaxSize())
        }
    }
}
```

En este caso se está mostrando la bandera de México mediante:

```kotlin
BanderaMexico(modifier = Modifier.fillMaxSize())
```

Si se quiere probar otra bandera, solamente se cambia ese composable.

Por ejemplo:

```kotlin
BanderaFrancia(modifier = Modifier.fillMaxSize())
```

o:

```kotlin
BanderaItalia(modifier = Modifier.fillMaxSize())
```

De esta manera se puede cambiar rápidamente entre las diferentes prácticas.

## Algunas cosas importantes de la implementación

### `weight()` y `fillMaxWidth()`

Aunque los dos sirven para controlar el tamaño de los elementos, no funcionan exactamente de la misma manera.

`weight()` sirve para repartir el espacio disponible entre elementos que son hermanos dentro de un `Row` o `Column`.

Por ejemplo, si tenemos tres elementos y cada uno tiene `weight(1f)`, los tres van a ocupar la misma cantidad de espacio.

En cambio, `fillMaxWidth(0.4f)` utiliza una parte específica del ancho disponible del elemento padre.

En la bandera de Estados Unidos se utiliza esta segunda opción para el cantón porque está colocado de manera independiente sobre las franjas y no funciona como una franja más.

### `aspectRatio(1f)`

`aspectRatio(1f)` sirve para mantener una proporción de 1:1 entre el ancho y el alto.

Esto es útil principalmente para los círculos.

Por ejemplo, si tenemos un círculo y la pantalla cambia de tamaño, `aspectRatio(1f)` ayuda a evitar que se vea estirado o deformado.

Aunque `size(60.dp)` puede verse bien en el `Preview`, puede comportarse diferente cuando el tamaño disponible cambia.

### Orden de `clip()` y `background()`

El orden de los modificadores también importa.

Por ejemplo:

```kotlin
clip(...)
background(...)
```

Primero se define la forma con `clip()` y después se aplica el fondo.

Si se utiliza `background()` antes de `clip()`, primero se pinta todo el fondo y después se realiza el recorte.

Por eso es importante tener cuidado con el orden de los modificadores cuando se están creando formas personalizadas.

### `GenericShape`

`GenericShape` sirve para crear formas que no tenemos directamente disponibles en Compose.

Para hacerlo se recibe el tamaño disponible y se construye un `Path` con la forma que queremos.

Puede utilizarse, por ejemplo, para crear:

* Un rombo.
* Una estrella.
* Otras formas personalizadas.

En este proyecto se utiliza principalmente para formas como el rombo de la bandera de Brasil.

### `Canvas`

`Canvas` sirve cuando necesitamos dibujar directamente diferentes elementos.

Por ejemplo, en la bandera de Argentina se utiliza para hacer el sol y sus rayos.

También resulta útil en la bandera de Estados Unidos para dibujar las estrellas.

Cuando tenemos muchos elementos que necesitamos colocar o dibujar dentro de una misma área, `Canvas` puede ser una buena opción.

### Proporción de una estrella de cinco puntas

Para hacer una estrella de cinco puntas se utiliza una relación entre el radio interno y el radio externo.

La relación utilizada es aproximadamente:

```text
sin(18°) / sin(126°) ≈ 0.382
```

Este valor ayuda a que las puntas de la estrella tengan una proporción adecuada.

Si se utiliza un valor diferente, la estrella puede terminar viéndose demasiado ancha o demasiado picuda.

## Resumen del proyecto

En estas prácticas se utilizan diferentes elementos de Jetpack Compose para aprender a construir interfaces y formas utilizando código.

Entre los conceptos que se practican están:

* `Row`
* `Column`
* `Box`
* `weight()`
* `fillMaxWidth()`
* `aspectRatio()`
* `clip()`
* `background()`
* `CircleShape`
* `GenericShape`
* `Canvas`
* `drawPath`
* `repeat()`
* Trigonometría
* Ramas de Git
* Commits
* Pull Requests

La idea principal es que cada bandera esté en su propia rama y que todas comiencen desde un `main` limpio. De esta manera, cada práctica se puede trabajar y probar de forma independiente.
