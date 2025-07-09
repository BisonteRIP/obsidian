#FundamentosJavascript

### ¿Qué son las Variables?

En JavaScript, las [[variables]] son como **contenedores con nombre** que usamos para almacenar información. Piensa en ellas como cajas etiquetadas donde guardas distintos tipos de datos (números, texto, etc.).

- **Propósito:** Guardar datos que pueden ser utilizados y modificados a lo largo de tu código.
    
- **Declaración:** Se declaran con las palabras clave:
    
    - **`var`**: Antigua, con un alcance (scope) más amplio y a veces confuso. (Menos usada hoy).
        
    - **`let`**: Moderna, permite reasignar el valor y tiene un alcance de bloque. **(¡Recomendada!)**
        
    - **`const`**: Moderna, para valores que **no van a cambiar** una vez asignados (constantes). También tiene alcance de bloque. **(¡Recomendada para valores fijos!)**


```Javascript
let nombre = "Juan"; // Declara y asigna
const PI = 3.14159;  // Declara una constante
var edad = 30;       // Ejemplo con var (evitar en código nuevo)
```

### Tipos de Datos

Los **tipos de datos** en JavaScript definen la **naturaleza del valor** que una variable puede contener. JavaScript es un lenguaje de **tipado dinámico**, lo que significa que no necesitas especificar el tipo de dato al declarar una variable; el intérprete lo determina en tiempo de ejecución.

Aquí están los tipos de datos más importantes:

| Categoría     | Tipo de Dato          | Descripción                                                | Ejemplos Generales            | Ejemplos en JavaScript                          |
| ------------- | --------------------- | ---------------------------------------------------------- | ----------------------------- | ----------------------------------------------- |
| Primitivos    | **Enteros**           | Números Completos, sin decimales                           | `5`, `-100`, `0`              | `let edad = 30;`                                |
|               | **Flotantes**         | Números con decimales                                      | `3.14`, `-0.5`, `9.99`        | `let precio = 19.99`                            |
|               | **Cadenas de Texto**  | Secuencias de caracteres (texto).                          | `"Hola"`, `'Mundo'`,`"123"`   | `let esMayor = true;` `let estaActivo = false;` |
|               | **Undefined**         | (Solo JS) Variables declaradas pero sin valor asignado.    | N/A                           | `let variableSinValor;`                         |
|               | **Null**              | (Solo JS) Ausencia intencionada de valor.                  | N/A                           | `let opcion = null;`                            |
|               | **Symbol**            | (Solo JS) Valor único e inmutable (para claves de objetos) | N/A                           | `const id = Symbol('usuario');`                 |
|               | **BigInt**            | (Solo JS) Numero enteros muy grandes                       | N/A                           | `const numGrande = 12345678901234567890n;`      |
| No Primitivos | **Objetos**           | Colecciones de pares clave-valor (propiedades)             | Objeto con<br>`nombre`,`edad` | `let persona = { nombre: "Juan", edad: 25 };`   |
|               | **Arrays**/**Listas** | Colecciones ordenadas de elementos.                        | `[1, 2, 3]`,<br>`["a", "b"]`  | `let numeros = [10, 20, 30];`                   |
|               | **Funciones**         | Bloques de Código reutilizable                             | Función `sumar(a, b)`         | `let hoy = new Date();`                         |
|               | **RegExp**            | Expresiones para buscar patrones de texto.                 | `/abc/`                       | `let patron = /[0-9]+/;`                        |
