#FundamentosJavascript


JavaScript cuenta con una variedad de operadores, que se clasifican según el tipo de operación que realizan.

#### 1. Operadores Aritméticos

Para realizar cálculos matemáticos básicos.

- **`+` (Suma):** Adición. `5 + 3` resulta `8`.
    
- **`-` (Resta):** Sustracción. `10 - 4` resulta `6`.
    
- **`*` (Multiplicación):** Multiplicación. `6 * 2` resulta `12`.
    
- **`/` (División):** División. `10 / 2` resulta `5`.
    
- **`%` (Módulo/Resto):** Devuelve el resto de una división. `10 % 3` resulta `1` (porque 10 dividido 3 es 3 con un resto de 1).
    
- **`**` (Exponenciación):** Eleva un número a la potencia de otro. `2 ** 3` resulta `8` (2 elevado a la 3).
    
- **`++` (Incremento):** Aumenta el valor de una variable en 1.
    
    - `x++` (post-incremento): Usa el valor actual de `x`, luego lo incrementa.
        
    - `++x` (pre-incremento): Incrementa `x`, luego usa el nuevo valor.
        
- **`--` (Decremento):** Disminuye el valor de una variable en 1.
    
    - `x--` (post-decremento): Usa el valor actual de `x`, luego lo decrementa.
        
    - `--x` (pre-decremento): Decrementa `x`, luego usa el nuevo valor.
        

---

#### 2. Operadores de Asignación

Para asignar un valor a una variable.

- **`=` (Asignación simple):** Asigna el valor del operando derecho al izquierdo.
    
    - `let x = 10;`
        
- **Asignación con operación combinada:** Realizan una operación y luego asignan el resultado.
    
    - `+=` (Suma y asigna): `x += 5;` es lo mismo que `x = x + 5;`
        
    - `-=` (Resta y asigna): `x -= 3;` es lo mismo que `x = x - 3;`
        
    - `*=` (Multiplica y asigna): `x *= 2;` es lo mismo que `x = x * 2;`
        
    - `/=` (Divide y asigna): `x /= 4;` es lo mismo que `x = x / 4;`
        
    - `%=` (Módulo y asigna): `x %= 3;` es lo mismo que `x = x % 3;`
        
    - `**=` (Exponencia y asigna): `x **= 2;` es lo mismo que `x = x ** 2;`
        

---

#### 3. Operadores de Comparación

Para comparar dos valores y devolver un **booleano** (`true` o `false`).

- **`==` (Igualdad abstracta):** Compara valores, intentando convertir los tipos si son diferentes.
    
    - `5 == '5'` resulta `true`. **(¡Puede ser confuso, mejor evitarlo!)**
        
- **`===` (Igualdad estricta):** Compara valores Y tipos de dato.
    
    - `5 === '5'` resulta `false`. **(¡¡Siempre usa este!!) `5 === 5` resulta `true`.**
        
- **`!=` (Desigualdad abstracta):** `5 != '5'` resulta `false`.
    
- **`!==` (Desigualdad estricta):** `5 !== '5'` resulta `true`. **(¡¡Siempre usa este!!)**
    
- **`>` (Mayor que):** `10 > 5` resulta `true`.
    
- **`<` (Menor que):** `5 < 10` resulta `true`.
    
- **`>=` (Mayor o igual que):** `10 >= 10` resulta `true`.
    
- **`<=` (Menor o igual que):** `5 <= 10` resulta `true`.
    

---

#### 4. Operadores Lógicos

Para combinar expresiones booleanas y devolver un **booleano** (`true` o `false`).

- **`&&` (AND lógico):** `true` si AMBAS condiciones son `true`.
    
    - `edad > 18 && tieneLicencia`
        
- **`||` (OR lógico):** `true` si AL MENOS UNA de las condiciones es `true`.
    
    - `esEstudiante || esProfesor`
        
- **`!` (NOT lógico):** Invierte el valor booleano.
    
    - `!esActivo` (si `esActivo` es `true`, `!esActivo` es `false`).
        

---

#### 5. Operador Ternario (Condicional)

Una forma concisa de escribir una sentencia `if-else` en una sola línea.

- **`condicion ? expresionSiVerdadero : expresionSiFalso`**
    
    - `let mensaje = (edad >= 18) ? "Adulto" : "Menor";`
        

---

#### 6. Operadores de Cadena (Strings)

- **`+` (Concatenación):** Une dos o más cadenas de texto.
    
    - `"Hola" + " " + "Mundo"` resulta `"Hola Mundo"`.
        

---

#### 7. Operadores de Tipo

- **`typeof`:** Devuelve una cadena indicando el tipo de dato de un operando.
    
    - `typeof 10` resulta `"number"`.
        
    - `typeof "Hola"` resulta `"string"`.
        
    - `typeof true` resulta `"boolean"`.
        
    - `typeof {}` resulta `"object"`.
        
    - `typeof []` resulta `"object"`.
        
    - `typeof null` resulta `"object"` **(¡Es una peculiaridad de JavaScript!)**.