#FundamentosJavascript


## Estructuras de Control en JavaScript

Las **estructuras de control** en JavaScript son sentencias que te permiten **controlar el flujo de ejecución** de tu código. Imagina que son como las "señales de tráfico" o los "planos" que le dicen a tu programa qué caminos tomar y cuántas veces debe repetir una acción.

- **Propósito:** Tomar decisiones (ejecutar un bloque de código u otro) y repetir tareas (ejecutar un bloque de código varias veces).
    

---

### 1. Estructuras Condicionales

Permiten que tu código tome **decisiones** y ejecute diferentes bloques de código basándose en si una condición es verdadera (`true`) o falsa (`false`).

#### a. `if`, `else if`, `else`

La estructura más fundamental para la toma de decisiones.

- **`if`**: Ejecuta un bloque de código si una condición es `true`.
    
    JavaScript
    
    ```javascript
    let edad = 18;
    if (edad >= 18) {
        console.log("Eres mayor de edad."); // Se ejecuta
    }
    ```
    
- **`else if`**: Evalúa una nueva condición si la condición `if` (o `else if` anteriores) fue `false`. Puedes tener múltiples `else if`.
    
    JavaScript
    
    ```javascript
    let temperatura = 20;
    if (temperatura > 25) {
        console.log("Hace calor.");
    } else if (temperatura < 10) {
        console.log("Hace frío.");
    } else { // Si ninguna de las anteriores es verdadera
        console.log("Temperatura agradable."); // Se ejecuta
    }
    ```
    
- **`else`**: Ejecuta un bloque de código si ninguna de las condiciones `if` o `else if` anteriores fue `true`. Es opcional y debe ir al final.
    

#### b. `switch`

Una alternativa más limpia para manejar múltiples condiciones basadas en el **valor de una única expresión**.

- Evalúa una expresión y compara su valor con diferentes casos (`case`).
    
- Cuando encuentra una coincidencia, ejecuta el bloque de código asociado.
    
- La palabra clave `break` es crucial para salir del `switch` una vez que se encuentra un caso; de lo contrario, continuará ejecutando los casos siguientes (`fall-through`).
    
- `default`: Es opcional y se ejecuta si ningún caso coincide.
    
    JavaScript
    
    ```javascript
    let dia = "Martes";
    switch (dia) {
        case "Lunes":
            console.log("Inicio de semana.");
            break;
        case "Martes":
            console.log("Segundo día."); // Se ejecuta
            break; // Importante para salir
        case "Viernes":
            console.log("Casi fin de semana.");
            break;
        default:
            console.log("Día no reconocido.");
    }
    ```
    

---

### 2. Estructuras de Bucle (Loops)

Permiten que tu código **repita** un bloque de código varias veces, ya sea un número específico de veces o hasta que una condición deje de ser `true`.

#### a. `for`

Ideal cuando sabes **cuántas veces** quieres que se repita el bucle.

- Sintaxis: `for (inicialización; condición; actualización)`
    
    1. **Inicialización:** Se ejecuta una vez al inicio del bucle.
        
    2. **Condición:** Se evalúa antes de cada iteración. Si es `true`, el bucle continúa; si es `false`, el bucle termina.
        
    3. **Actualización:** Se ejecuta después de cada iteración.
        
    
    JavaScript
    
    ```javascript
    for (let i = 0; i < 5; i++) {
        console.log("Iteración número: " + i); // Se ejecuta 5 veces (0, 1, 2, 3, 4)
    }
    ```
    

#### b. `for...in`

Para **iterar sobre las propiedades (claves)** enumerables de un objeto.

- No es recomendable para arrays porque puede iterar en un orden impredecible y también propiedades no numéricas.
    
    JavaScript
    
    ```javascript
    const persona = { nombre: "Luis", edad: 28 };
    for (let clave in persona) {
        console.log(clave + ": " + persona[clave]);
        // Salida: "nombre: Luis", "edad: 28"
    }
    ```
    

#### c. `for...of`

Para **iterar sobre los valores** de objetos iterables como `Arrays`, `Strings`, `Maps`, `Sets`, etc. **(¡Recomendado para arrays!)**

- Mucho más moderno y seguro para recorrer arrays.
    
    JavaScript
    
    ```javascript
    const frutas = ["manzana", "banana", "cereza"];
    for (let fruta of frutas) {
        console.log(fruta);
        // Salida: "manzana", "banana", "cereza"
    }
    
    const texto = "Hola";
    for (let caracter of texto) {
        console.log(caracter);
        // Salida: "H", "o", "l", "a"
    }
    ```
    

#### d. `while`

Ejecuta un bloque de código **mientras una condición sea `true`**. La condición se evalúa _antes_ de cada iteración.

- Asegúrate de que la condición eventualmente se vuelva `false` para evitar un bucle infinito.
    
    JavaScript
    
    ```javascript
    let contador = 0;
    while (contador < 3) {
        console.log("Contador: " + contador);
        contador++; // Importante para que el bucle termine
    }
    // Salida: "Contador: 0", "Contador: 1", "Contador: 2"
    ```
    

#### e. `do...while`

Similar a `while`, pero garantiza que el bloque de código se ejecute **al menos una vez**, ya que la condición se evalúa _después_ de la primera iteración.

JavaScript

```javascript
let i = 0;
do {
    console.log("Valor de i: " + i);
    i++;
} while (i < 0);
// Salida: "Valor de i: 0" (Se ejecuta una vez, aunque la condición sea falsa inicialmente)
```