#ConceptosAvanzadosJavascript 

## Programación Asíncrona en JavaScript

La **programación asíncrona** en JavaScript es fundamental para manejar operaciones que toman tiempo sin bloquear el hilo principal de ejecución del programa. Imagina que tu código es un chef cocinando: si cada tarea (picar verduras, hervir agua) tuviera que completarse antes de empezar la siguiente, la cocina se paralizaría. La asincronía permite que el chef inicie una tarea que llevará tiempo (ej. hornear pan) y mientras espera, pueda dedicarse a otras tareas.

- **Propósito:** Mejorar la **interactividad** y la **reactividad** de las aplicaciones, evitando que la interfaz de usuario se congele mientras se realizan operaciones largas (como peticiones de red, lectura de archivos, temporizadores).
    
- **JavaScript es Single-Threaded:** Aunque JavaScript es de un solo hilo (ejecuta una cosa a la vez), el **Event Loop** (Bucle de Eventos) le permite simular concurrencia y manejar operaciones asíncronas de manera eficiente.
    

---

### 1. Callback Functions (Funciones de Retrollamada)

Una **callback function** es una función que se pasa como argumento a otra función, y se espera que sea ejecutada por esa otra función en un momento posterior. Históricamente, eran la forma principal de manejar la asincronía.

```javascript
function simularPeticion(callback) {
    setTimeout(function() {
        const datos = "Datos obtenidos";
        callback(datos); // Se ejecuta la callback con los datos
    }, 2000);
}

simularPeticion(function(info) {
    console.log("Procesando: " + info); // Se ejecuta después de 2 segundos
});
```

#### "Callback Hell" (Infierno de Callbacks)

El problema surge cuando tienes múltiples operaciones asíncronas que dependen unas de otras, resultando en un código anidado profundamente y difícil de leer, mantener y depurar.

```javascript
// Ejemplo de Callback Hell (pseudocódigo)
getData(function(a) {
    processData(a, function(b) {
        saveData(b, function(c) {
            uploadFile(c, function(d) {
                console.log("¡Todo listo!");
            }, handleError);
        }, handleError);
    }, handleError);
}, handleError);
```

---

### 2. Promises (Promesas)

Las **Promesas** son objetos que representan la eventual finalización (o fracaso) de una operación asíncrona y su valor resultante. Son una mejora significativa sobre las callbacks anidadas, ofreciendo un código más limpio y legible.

#### ¿Qué son y por qué usarlas?

- **Representación:** Una promesa es un "placeholder" para un valor que aún no está disponible pero que lo estará en el futuro.
    
- **Solución a Callback Hell:** Permiten encadenar operaciones asíncronas de forma secuencial (`.then()`) sin anidación excesiva.
    

#### Estados de una Promesa

Una promesa puede estar en uno de tres estados:

- **`pending` (Pendiente):** Estado inicial; la operación asíncrona aún no ha finalizado.
    
- **`fulfilled` (Cumplida/Resuelta):** La operación asíncrona se completó con éxito. La promesa devuelve un valor.
    
- **`rejected` (Rechazada):** La operación asíncrona falló. La promesa devuelve una razón (error).
    

#### Métodos de las Promesas

- **`.then(onFulfilled, onRejected)`:**
    
    - `onFulfilled`: Una función que se ejecuta cuando la promesa se resuelve exitosamente. Recibe el valor de la promesa.
        
    - `onRejected` (opcional): Una función que se ejecuta si la promesa es rechazada. Recibe la razón del rechazo.
        
    - **Encadenamiento:** `.then()` siempre devuelve una **nueva promesa**, lo que permite encadenar múltiples operaciones.
        
- **`.catch(onRejected)`:** Un atajo para `.then(null, onRejected)`. Se usa para manejar errores de promesas en la cadena.
    
- **`.finally(onFinally)`:** Ejecuta una función cuando la promesa se asienta (ya sea `fulfilled` o `rejected`). Útil para limpieza de recursos, independientemente del resultado.

```javascript
function simularPromesa(exito) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (exito) {
                resolve("¡Datos obtenidos con éxito!"); // Resuelve la promesa
            } else {
                reject("Error al obtener datos."); // Rechaza la promesa
            }
        }, 1500);
    });
}

simularPromesa(true)
    .then(data => {
        console.log("Éxito:", data);
        return "Proceso completado.";
    })
    .catch(error => {
        console.error("Fallo:", error);
    })
    .finally(() => {
        console.log("La promesa ha finalizado.");
    });
```

#### `Promise.all()`

Toma un array de promesas y devuelve una nueva promesa. Esta nueva promesa se **resuelve** cuando **todas** las promesas en el array se han resuelto. Se **rechaza** si **alguna** de las promesas en el array se rechaza.

```javascript
Promise.all([
    simularPromesa(true),
    simularPromesa(true)
])
.then(resultados => console.log("Todos resueltos:", resultados)) // resultados es un array
.catch(error => console.error("Uno falló:", error));
```

#### `Promise.race()`

Toma un array de promesas y devuelve una nueva promesa. Esta nueva promesa se **resuelve o rechaza** tan pronto como **una** de las promesas en el array se resuelve o se rechaza.

```javascript
Promise.race([
    simularPromesa(true), // Esta se resolverá más rápido
    simularPromesa(false)
])
.then(ganador => console.log("El más rápido:", ganador))
.catch(perdedor => console.error("El más rápido falló:", perdedor));
```

---

### 3. Async/Await

**`async/await`** es una característica de ES2017 que permite escribir código asíncrono que parece y se comporta como código síncrono, haciendo que sea aún más legible y fácil de manejar que las promesas con `.then()`. Es una "azúcar sintáctica" sobre las Promesas.

#### ¿Cómo funcionan?

- Las funciones `async` siempre devuelven una Promesa.
    
- `await` solo puede usarse dentro de una función `async`.
    

#### `async` keyword

Se coloca antes de una declaración de función para indicar que la función ejecutará código asíncrono y, por lo tanto, devolverá implícitamente una Promesa.

```javascript
async function miFuncionAsincrona() {
    // ...
}
```

#### `await` keyword

Se usa dentro de una función `async` para **pausar la ejecución de la función** hasta que una Promesa se resuelva o se rechace. Una vez que la Promesa se resuelve, el valor resuelto es el resultado de la expresión `await`.

```javascript
async function obtenerDatos() {
    try {
        console.log("Iniciando obtención de datos...");
        const datos = await simularPromesa(true); // Pausa hasta que la promesa se resuelva
        console.log("Datos obtenidos:", datos);
        const masDatos = await simularPromesa(true);
        console.log("Más datos obtenidos:", masDatos);
    } catch (error) {
        console.error("Ocurrió un error:", error);
    } finally {
        console.log("Función obtenerDatos finalizada.");
    }
}

obtenerDatos();
```

#### Manejo de Errores con `try...catch`

Dentro de una función `async`, puedes usar bloques `try...catch` para manejar los errores de las Promesas rechazadas de forma síncrona.

```javascript
async function obtenerYProcesarDatos() {
    try {
        const usuario = await fetch('/api/user').then(res => res.json());
        const posts = await fetch(`/api/posts/${usuario.id}`).then(res => res.json());
        console.log("Posts del usuario:", posts);
    } catch (error) {
        // Captura cualquier error en las promesas fetch o en el procesamiento
        console.error("Hubo un problema:", error.message);
    }
}
obtenerYProcesarDatos();
```

---

### 4. Event Loop (Bucle de Eventos)

El **Event Loop** es el corazón del modelo de concurrencia de JavaScript. Es lo que permite a JavaScript ser asíncrono a pesar de ser de un solo hilo.

- **Modelo de Concurrencia:** Describe cómo JavaScript ejecuta el código, maneja eventos, realiza operaciones asíncronas y gestiona la pila de llamadas.
    

#### Componentes Clave

1. **Call Stack (Pila de Llamadas):**
    
    - Es una estructura de datos (LIFO - Last In, First Out) que registra dónde estamos en el programa.
        
    - Cuando una función es llamada, se "apila" en el Call Stack. Cuando termina, se "desapila".
        
    - JavaScript solo puede ejecutar una función a la vez en la Call Stack. Si una operación toma mucho tiempo aquí, el hilo se bloquea.
        
2. **Web APIs (APIs del Navegador/Node.js):**
    
    - No son parte del motor de JavaScript, sino funcionalidades proporcionadas por el entorno (navegador, Node.js).
        
    - Ejemplos: `setTimeout()`, `fetch()`, `DOM events`, `XMLHttpRequest`.
        
    - Cuando se llama a una función asíncrona (ej. `setTimeout`), se envía a una de estas APIs para que la maneje.
        
3. **Callback Queue (Task Queue / Cola de Tareas):**
    
    - Cuando una Web API completa su tarea asíncrona, la callback asociada (la función que debe ejecutarse después) se coloca en esta cola.
        
    - También contiene _macrotareas_ como las de `setTimeout`, `setInterval`, `setImmediate`.
        
4. **Microtask Queue (Cola de Microtareas):**
    
    - Una cola de mayor prioridad que la Callback Queue.
        
    - Contiene _microtareas_, principalmente callbacks de **Promesas** (`.then()`, `.catch()`, `.finally()`) y `queueMicrotask()`.
        
5. **El Event Loop en Sí:**
    
    - Es un proceso continuo que monitorea la Call Stack y las colas.
        
    - Si la **Call Stack está vacía**, el Event Loop toma la primera función de la **Microtask Queue** y la empuja a la Call Stack para su ejecución.
        
    - Si la **Microtask Queue también está vacía**, entonces el Event Loop toma la primera función de la **Callback Queue** y la empuja al Call Stack.
        
    - Este ciclo garantiza que las microtareas (`Promise`) se ejecuten antes que las macrotareas (`setTimeout`) si la pila principal está disponible.
        

---

#### Diferencia entre `setTimeout(fn, 0)` y `Promise.resolve().then(fn)`

Esta es una pregunta clásica para entender el Event Loop:

- **`setTimeout(fn, 0)`:**
    
    - Registra `fn` como una **macrotarea** en la Callback Queue.
        
    - Aunque el temporizador sea 0, la función `fn` no se ejecutará hasta que el Call Stack esté vacío y el Event Loop haya procesado todas las **microtareas** pendientes.
        
- **`Promise.resolve().then(fn)`:**
    
    - Crea una promesa ya resuelta, y la callback `fn` se registra como una **microtarea** en la Microtask Queue.
        
    - Las microtareas tienen **mayor prioridad** que las macrotareas. Por lo tanto, `fn` se ejecutará **antes** que una función puesta con `setTimeout(..., 0)`, siempre que la Call Stack esté vacía.

```javascript
console.log("1. Inicio");

setTimeout(() => {
    console.log("3. setTimeout (Macrotarea)");
}, 0);

Promise.resolve().then(() => {
    console.log("2. Promise (Microtarea)");
});

console.log("4. Fin");

// Salida esperada:
// 1. Inicio
// 4. Fin
// 2. Promise (Microtarea)
// 3. setTimeout (Macrotarea)
```

 
