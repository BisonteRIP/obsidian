#ConceptosAvanzadosJavascript 

## Arrays en JavaScript

En JavaScript, un **Array** (o arreglo/matriz) es un tipo especial de **objeto** que se usa para almacenar una **colección ordenada de elementos**. Piensa en un array como una **lista** o una **caja con compartimentos numerados**, donde cada compartimento puede guardar un valor distinto (números, cadenas, otros arrays, objetos, etc.).

- **Características clave:**
    
    - **Ordenados:** Los elementos tienen un orden específico y se acceden por su **índice numérico** (que empieza en `0`).
        
    - **Indexados:** Cada elemento tiene una posición numérica única.
        
    - **Heterogéneos:** Pueden contener elementos de diferentes tipos de datos en el mismo array.
        
    - **Mutables:** La mayoría de los arrays se pueden modificar (agregar, quitar o cambiar elementos) después de su creación.
        

---

### Creación de Arrays

Hay varias formas de crear arrays en JavaScript:

#### 1. Literal de Array (Array Literal)

La forma más común, sencilla y recomendada.

```javascript
const frutas = ["Manzana", "Banana", "Cereza"];
const numeros = [1, 2, 3, 4, 5];
const mixto = [1, "Hola", true, { clave: "valor" }];
```

#### 2. Constructor `Array()` (Menos común)

Puedes usar el constructor `Array`, aunque generalmente se prefiere el literal por su concisión.

```javascript
const dias = new Array("Lunes", "Martes", "Miércoles");
// Si pasas un solo número, crea un array vacío con esa longitud
const arrayVacioConLongitud = new Array(5); // Crea [empty × 5]
```

---

### Métodos Comunes de Arrays (Modificadores)

Estos métodos suelen **modificar el array original** (`mutan` el array).

- **`push(elemento1, ...)`**: Agrega uno o más elementos al **final** del array y devuelve la nueva longitud.
  
    ```javascript
    const colores = ["rojo", "verde"];
    colores.push("azul"); // colores ahora es ["rojo", "verde", "azul"]
    ```

- **`pop()`**: Elimina el **último** elemento del array y lo devuelve.

    ```javascript
    const numeros = [1, 2, 3];
    const ultimo = numeros.pop(); // ultimo es 3, numeros ahora es [1, 2]
    ```

- **`shift()`**: Elimina el **primer** elemento del array y lo devuelve. Los demás elementos se "desplazan" para ocupar su lugar.
  
    ```javascript
    const letras = ["a", "b", "c"];
    const primero = letras.shift(); // primero es "a", letras ahora es ["b", "c"]
    ```

- **`unshift(elemento1, ...)`**: Agrega uno o más elementos al **principio** del array y devuelve la nueva longitud.
  
    ```javascript
    const paises = ["España", "Francia"];
    paises.unshift("Alemania"); // paises ahora es ["Alemania", "España", "Francia"]
    ```

- **`splice(inicio, cantidadAEliminar, elemento1, ...)`**: Un método muy versátil para **agregar, eliminar o reemplazar** elementos en cualquier posición del array. Devuelve un array con los elementos eliminados.
    
    - Eliminar: `array.splice(1, 2);` (desde índice 1, elimina 2 elementos)
        
    - Agregar: `array.splice(1, 0, "nuevo1", "nuevo2");` (desde índice 1, no elimina, agrega 2 elementos)
        
    - Reemplazar: `array.splice(1, 1, "reemplazo");` (desde índice 1, elimina 1, agrega "reemplazo")
        
 
    ```javascript
    const frutas = ["Manzana", "Banana", "Cereza", "Fresa"];
    frutas.splice(1, 2, "Kiwi", "Mango"); // Elimina "Banana", "Cereza", y agrega "Kiwi", "Mango"
    // frutas ahora es ["Manzana", "Kiwi", "Mango", "Fresa"]
    ```

- **`concat(array1, array2, ...)`**: **Crea un nuevo array** uniendo el array original con uno o más arrays y/o valores. **No modifica** el array original.
  
    ```javascript
    const arr1 = [1, 2];
    const arr2 = [3, 4];
    const nuevoArr = arr1.concat(arr2, 5); // nuevoArr es [1, 2, 3, 4, 5], arr1 sigue siendo [1, 2]
    ```

- **`slice(inicio, fin)`**: **Crea una copia superficial** de una porción del array original, desde `inicio` (inclusive) hasta `fin` (exclusivo). **No modifica** el array original.
   
    ```javascript
    const animales = ["perro", "gato", "pez", "ave"];
    const subAnimales = animales.slice(1, 3); // subAnimales es ["gato", "pez"]
    // animales sigue siendo ["perro", "gato", "pez", "ave"]
    ```

---

### Métodos de Iteración de Arrays (No modificadores)

Estos métodos no suelen modificar el array original; en cambio, iteran sobre él o devuelven un nuevo array/valor.

- **`forEach(callbackFunction)`**: Ejecuta una función **por cada elemento** del array. Ideal para efectos secundarios (ej: imprimir, modificar un DOM). No devuelve un nuevo array.

    ```javascript
    const numeros = [1, 2, 3];
    numeros.forEach(function(num) {
        console.log(num * 2);
    });
    // Salida: 2, 4, 6
    ```

- **`map(callbackFunction)`**: **Crea un nuevo array** con los resultados de llamar a una función proporcionada en cada elemento del array original. Ideal para transformar datos.
 
    ```javascript
    const nums = [1, 2, 3];
    const dobles = nums.map(num => num * 2); // dobles es [2, 4, 6]
    ```

- **`filter(callbackFunction)`**: **Crea un nuevo array** con todos los elementos que pasan la prueba implementada por la función proporcionada (es decir, aquellos para los que la función devuelve `true`).

    ```javascript
    const edades = [12, 18, 25, 8];
    const mayoresEdad = edades.filter(edad => edad >= 18); // mayoresEdad es [18, 25]
    ```

- **`reduce(callbackFunction, valorInicial)`**: Ejecuta una función **reductora** sobre cada elemento del array (de izquierda a derecha), resultando en un **único valor** de retorno. Muy potente para sumar, aplanar arrays, etc.

    ```javascript
    const valores = [1, 2, 3, 4];
    const suma = valores.reduce((acumulador, valorActual) => acumulador + valorActual, 0); // suma es 10
    ```

- **`find(callbackFunction)`**: Devuelve el **primer elemento** del array que cumple con la condición de la función de prueba. Si no encuentra ninguno, devuelve `undefined`.
   
    ```javascript
    const productos = [{ id: 1, nombre: "Laptop" }, { id: 2, nombre: "Mouse" }];
    const mouse = productos.find(prod => prod.nombre === "Mouse"); // mouse es { id: 2, nombre: "Mouse" }
    ```

- **`some(callbackFunction)`**: Comprueba si **al menos un elemento** del array cumple con la condición. Devuelve `true` o `false`.

    ```javascript
    const numeros = [1, 5, 10, 15];
    const tieneMayorDeDiez = numeros.some(num => num > 10); // tieneMayorDeDiez es true
    ```

- **`every(callbackFunction)`**: Comprueba si **todos los elementos** del array cumplen con la condición. Devuelve `true` o `false`.
   
    ```javascript
    const edades = [20, 22, 25];
    const todosAdultos = edades.every(edad => edad >= 18); // todosAdultos es true
    ```