#ConceptosAvanzadosJavascript 

## Objetos en JavaScript

En JavaScript, los **objetos** son colecciones de **propiedades** y **métodos**. Piensa en ellos como entidades que agrupan datos (propiedades) y comportamientos (métodos) relacionados. Casi todo en JavaScript es un objeto o se comporta como tal (excepto los tipos primitivos `string`, `number`, `boolean`, `symbol`, `null`, `undefined`, `bigint`).

- **Propósito principal:**
    
    - **Representar entidades:** Modelar cosas del mundo real (una persona, un coche, un producto).
        
    - **Organizar datos:** Agrupar información relacionada de manera estructurada.
        
    - **Encapsular lógica:** Asociar funciones (métodos) directamente a los datos con los que operan.
        

---

### Creación de Objetos

Hay varias formas de crear objetos en JavaScript, cada una útil en diferentes escenarios.

#### 1. Literales de Objeto (Object Literals)

La forma más común y sencilla de crear un objeto. Ideal para crear objetos únicos y estáticos.

```javascript
const persona = {
    nombre: "Juan",
    edad: 30,
    saludar: function() { // Esto es un método
        console.log("Hola, soy " + this.nombre);
    }
};

console.log(persona.nombre); // Acceso a propiedad
persona.saludar();           // Llamada a método
```

#### 2. Función Constructora (Constructor Function)

Una función regular que se utiliza con la palabra clave `new` para crear múltiples objetos con la misma estructura. Las propiedades y métodos se asignan usando `this`.

```javascript
function Coche(marca, modelo) {
    this.marca = marca;
    this.modelo = modelo;
    this.mostrarInfo = function() {
        console.log(`Coche: ${this.marca} ${this.modelo}`);
    };
}

const miCoche = new Coche("Toyota", "Corolla");
const otroCoche = new Coche("Honda", "Civic");

miCoche.mostrarInfo();   // Salida: Coche: Toyota Corolla
otroCoche.mostrarInfo(); // Salida: Coche: Honda Civic
```

#### 3. `Object.create()`

Crea un nuevo objeto utilizando un objeto existente como prototipo del recién creado. Es útil para implementar herencia prototípica directamente.

```javascript
const prototipoPersona = {
    saludar: function() {
        console.log("Hola, mi nombre es " + this.nombre);
    }
};

const ana = Object.create(prototipoPersona);
ana.nombre = "Ana";
ana.saludar(); // Salida: Hola, mi nombre es Ana
```

---

### Propiedades y Métodos

- **Propiedades:** Son las variables asociadas a un objeto. Representan las características o atributos del objeto. Se definen como pares `clave: valor`.
    
    - _Ejemplo:_ `nombre: "Juan"`, `edad: 30`
        
- **Métodos:** Son las funciones asociadas a un objeto. Representan las acciones o comportamientos que el objeto puede realizar.
    
    - _Ejemplo:_ `saludar: function() { ... }`
        

---

### Acceso a Propiedades

Hay dos formas principales de acceder a las propiedades de un objeto:

- **Notación de Punto (`.`):** La forma más común y recomendada cuando conoces el nombre de la propiedad de antemano.

    ```javascript
    const producto = { nombre: "Laptop", precio: 1200 };
    console.log(producto.nombre); // Salida: "Laptop"
    ```

- **Notación de Corchetes (`[]`):** Útil cuando el nombre de la propiedad está en una variable, contiene caracteres especiales o espacios, o es dinámico.

    ```javascript
    const producto = { "nombre del producto": "Teclado", stock: 50 };
    console.log(producto["nombre del producto"]); // Salida: "Teclado"
    
    let claveDinamica = "stock";
    console.log(producto[claveDinamica]); // Salida: 50
    ```
    

---

### `this` en JavaScript: Contexto y Cómo Cambia

`this` es una palabra clave especial que se refiere al **contexto de ejecución** actual. Su valor **cambia dinámicamente** dependiendo de cómo se llama una función. Esto es una de las partes más confusas de JavaScript.

- **Reglas principales para `this`:**
    
    - **En un método de objeto:** `this` se refiere al objeto que posee el método.
       
        ```javascript
        const user = {
            name: "Carlos",
            getName: function() {
                console.log(this.name); // 'this' es 'user'
            }
        };
        user.getName(); // Salida: Carlos
        ```

    - **En una función simple (no método):** En modo no estricto, `this` se refiere al objeto global (`window` en navegadores, `global` en Node.js). En modo estricto, `this` es `undefined`.

        ```javascript
        function mostrarThis() {
            console.log(this); // 'window' o 'undefined' (en modo estricto)
        }
        mostrarThis();
        ```

    - **En una función constructora:** `this` se refiere a la nueva instancia del objeto que se está creando.

        ```javascript
        function Perro(nombre) {
            this.nombre = nombre; // 'this' es la nueva instancia de Perro
        }
        const miPerro = new Perro("Fido");
        console.log(miPerro.nombre); // Salida: Fido
        ```

    - **En una Arrow Function (`=>`):** Las _arrow functions_ **no tienen su propio `this`**. Heredan el `this` del ámbito léxico (el `this` del contexto donde fueron definidas, no donde fueron llamadas).

        ``` javascript
        const app = {
            name: "MyApp",
            logName: function() {
                setTimeout(() => {
                    console.log(this.name); // 'this' es 'app' (heredado del logName)
                }, 100);
            }
        };
        app.logName(); // Salida: MyApp
        ```

#### Métodos para Manipular `this` (`call`, `apply`, `bind`)

Estos métodos, presentes en todas las funciones, permiten controlar explícitamente el valor de `this`.

- **`call(thisArg, arg1, arg2, ...)`:** Invoca la función con un `this` especificado y argumentos pasados individualmente.

    ```javascript
    function saludarA(saludo) {
        console.log(saludo + ", " + this.nombre);
    }
    const persona2 = { nombre: "Laura" };
    saludarA.call(persona2, "Hola"); // Salida: Hola, Laura
    ```

- **`apply(thisArg, [argsArray])`:** Invoca la función con un `this` especificado y argumentos pasados como un array.
   
    ```javascript
    function sumarNumeros(a, b) {
        console.log(this.mensaje + (a + b));
    }
    const contexto = { mensaje: "La suma es: " };
    sumarNumeros.apply(contexto, [10, 5]); // Salida: La suma es: 15
    ```

- **`bind(thisArg, arg1, arg2, ...)`:** Devuelve una **nueva función** donde `this` está permanentemente vinculado al valor especificado. Los argumentos adicionales se fijan (curry).

    ```javascript
    const libro = {
        titulo: "El Quijote",
        mostrarTitulo: function() {
            console.log(this.titulo);
        }
    };
    
    const funcionVinculada = libro.mostrarTitulo.bind(libro);
    setTimeout(funcionVinculada, 100); // Salida: El Quijote (funciona a pesar del setTimeout)
    ```


---

### Clases (ES6)

Las **clases** en JavaScript (introducidas en ES6) son una **azúcar sintáctica** sobre el modelo de herencia prototípica existente. No introducen un nuevo modelo de objetos, sino que proporcionan una sintaxis más limpia y familiar (similar a lenguajes orientados a objetos tradicionales) para crear objetos y manejar la herencia.

#### Sintaxis Básica

JavaScript

```javascript
class Animal {
    // Constructor: Método especial para inicializar el objeto al crearse
    constructor(nombre, especie) {
        this.nombre = nombre;
        this.especie = especie;
    }

    // Método: Una función asociada a la clase
    emitirSonido() {
        console.log("El " + this.especie + " hace un sonido.");
    }
}

const miAnimal = new Animal("Rex", "Perro");
console.log(miAnimal.nombre);     // Salida: Rex
miAnimal.emitirSonido();          // Salida: El Perro hace un sonido.
```

#### Herencia con `extends` y `super`

Las clases permiten la herencia usando la palabra clave `extends` para crear subclases.

- **`extends`:** Permite que una clase herede propiedades y métodos de otra clase.
    
- **`super()`:** Se usa en el constructor de la subclase para llamar al constructor de la clase padre. Es **obligatorio** llamarlo antes de usar `this` en la subclase.

```javascript
class Perro extends Animal { // Perro hereda de Animal
    constructor(nombre, raza) {
        super(nombre, "Perro"); // Llama al constructor de Animal
        this.raza = raza;
    }

    ladrar() { // Método específico de Perro
        console.log(this.nombre + " ladra: ¡Guau! ¡Guau!");
    }

    // Sobreescribir un método del padre
    emitirSonido() {
        console.log(this.nombre + " hace un ladrido característico.");
    }
}

const lassie = new Perro("Lassie", "Collie");
console.log(lassie.especie);      // Salida: Perro (heredado de Animal)
lassie.emitirSonido();            // Salida: Lassie hace un ladrido característico.
lassie.ladrar();                  // Salida: Lassie ladra: ¡Guau! ¡Guau!
```