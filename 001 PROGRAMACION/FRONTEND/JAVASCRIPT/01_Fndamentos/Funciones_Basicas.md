#FundamentosJavascript

## Funciones en JavaScript

Las **funciones** en JavaScript son como **"cajas de herramientas" reutilizables** que contienen bloques de código diseñados para realizar una tarea específica. Son uno de los pilares fundamentales de JavaScript, permitiéndonos organizar, estructurar y reutilizar nuestro código de manera eficiente.

- **Propósito principal:**
    
    - **Reusabilidad:** Escribir código una vez y usarlo múltiples veces.
        
    - **Modularidad:** Dividir un problema grande en partes más pequeñas y manejables.
        
    - **Organización:** Mantener el código limpio y fácil de entender.
        

---

### Tipos de Declaración de Funciones

JavaScript ofrece varias formas de definir funciones, cada una con sus propias características.

#### 1. Declaración de Función (Function Declaration)

Es la forma más tradicional y común de definir una función. Son "elevadas" (hoisted), lo que significa que puedes llamarlas antes de su definición en el código.

JavaScript

```javascript
function saludar(nombre) {
    console.log("Hola, " + nombre + "!");
}

saludar("Ana"); // Puedes llamarla antes de su definición
```

#### 2. Expresiones de Función (Function Expressions)

Una función definida como parte de una expresión. A menudo se asignan a una variable. No son "elevadas" (no-hoisted), por lo que debes definirlas antes de llamarlas.

JavaScript

```javascript
const sumar = function(a, b) {
    return a + b;
};

// sumar(5, 3); // Esto funcionaría si estuviera aquí
console.log(sumar(5, 3)); // Salida: 8
```

#### 3. Arrow Functions (Funciones Flecha) `() => {}`

Introducidas en ES6, son una sintaxis más corta y concisa para escribir expresiones de función.

- **Sintaxis Concisa:**
    
    - Si solo hay un parámetro, los paréntesis son opcionales: `param => { ... }`
        
    - Si no hay parámetros o más de uno, los paréntesis son obligatorios: `(param1, param2) => { ... }`
        
    - Si el cuerpo de la función es una sola expresión, las llaves y el `return` implícito: `(a, b) => a + b;`
        
- **Contexto de `this`:**
    
    - La característica más distintiva de las _arrow functions_ es cómo manejan el `this`. **No tienen su propio `this`**. Heredan el `this` del contexto léxico (el ámbito donde fueron definidas). Esto las hace ideales para _callbacks_ donde necesitas mantener el `this` del contexto exterior.
        

JavaScript

```javascript
// Ejemplos de Arrow Functions
const multiplicar = (num1, num2) => num1 * num2;
console.log(multiplicar(4, 2)); // Salida: 8

const decirHola = () => console.log("¡Hola!");
decirHola(); // Salida: ¡Hola!

// Contexto de 'this' en Arrow Functions
const obj = {
    nombre: "Objeto",
    saludarConRetraso: function() {
        setTimeout(() => {
            console.log("Hola desde " + this.nombre); // 'this' se refiere a 'obj'
        }, 1000);
    }
};
obj.saludarConRetraso(); // Salida: "Hola desde Objeto" después de 1 segundo
```

---

### Parámetros y Argumentos

- **Parámetros:** Son los nombres listados en la definición de la función. Actúan como marcadores de posición para los valores que la función espera recibir.
    
- **Argumentos:** Son los valores reales que se pasan a la función cuando esta es llamada.
    

JavaScript

```javascript
function saludar(parametroNombre, parametroApellido) { // parametroNombre, parametroApellido son parámetros
    console.log("Hola, " + parametroNombre + " " + parametroApellido);
}

saludar("Pedro", "Gómez"); // "Pedro" y "Gómez" son argumentos
```

---

### `return` Statement

La sentencia `return` se usa para **enviar un valor de vuelta** desde la función al lugar donde fue llamada. Una vez que se ejecuta `return`, la función termina su ejecución.

- Si una función no tiene `return` explícito, implícitamente devuelve `undefined`.
    

JavaScript

```javascript
function calcularAreaRectangulo(ancho, alto) {
    const area = ancho * alto;
    return area; // Devuelve el valor del área
}

let resultado = calcularAreaRectangulo(5, 4);
console.log(resultado); // Salida: 20
```

---

### Scope de las Funciones

El **ámbito (scope)** define la accesibilidad de variables, funciones y objetos en tu código. En JavaScript, las funciones juegan un papel crucial en la creación de nuevos ámbitos.

- **Global Scope:** Las variables declaradas fuera de cualquier función son accesibles desde cualquier parte del código.
    
- **Function Scope (o Local Scope):** Las variables declaradas _dentro_ de una función (usando `var`, `let`, o `const`) son accesibles solo dentro de esa función. Cada llamada a la función crea un nuevo _scope_ local.
    
- **Block Scope:** Con `let` y `const`, se introdujo el _block scope_. Las variables declaradas dentro de un bloque de código (como un `if`, `for`, `while`, o simplemente `{}`) solo son accesibles dentro de ese bloque. Las variables con `var` no tienen _block scope_.
    
- **Lexical Scope (Ámbito Léxico):** Una función anidada (definida dentro de otra función) tiene acceso a las variables de su función "padre" (exterior), incluso después de que la función padre haya terminado de ejecutarse. Este acceso se basa en dónde se define la función, no dónde se llama.
    

JavaScript

```javascript
let variableGlobal = "Soy global"; // Global Scope

function funcionExterna() {
    let variableLocalExterna = "Soy local externa"; // Function Scope para funcionExterna

    if (true) {
        let variableBloque = "Soy de bloque"; // Block Scope
        console.log(variableBloque);
    }
    // console.log(variableBloque); // Error: variableBloque no está definida aquí

    function funcionInterna() {
        // Acceso a variableLocalExterna gracias al Lexical Scope
        console.log(variableGlobal);        // Accede a global
        console.log(variableLocalExterna); // Accede a la de la función externa
        // console.log(variableBloque);    // Error: no tiene acceso al scope de bloque if
    }
    funcionInterna();
}
funcionExterna();
```

---

### Funciones Anidadas (Nested Functions)

Son funciones definidas _dentro_ de otras funciones. Aprovechan el **Ámbito Léxico** para acceder a variables de sus funciones contenedoras.

JavaScript

```javascript
function obtenerNombreCompleto(nombre, apellido) {
    let prefijo = "Sr(a). "; // Variable local de obtenerNombreCompleto

    function formatoNombre() { // Función anidada
        // Accede a 'prefijo', 'nombre', y 'apellido' gracias al ámbito léxico
        return prefijo + nombre + " " + apellido;
    }

    return formatoNombre(); // La función interna se llama aquí
}

console.log(obtenerNombreCompleto("María", "Pérez")); // Salida: Sr(a). María Pérez
```