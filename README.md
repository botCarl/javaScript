# javaScript (básico)
## Variables:
JS es debilmente tipado. (weakly typed)

```javascript
var mayoriaEdad = 18 // Magic Number
const MAYORIA_EDAD // constante
```

### Strings
```javascript
var nombre = 'Carlos', apellido = 'Jaramillo'.toLowerCase();
var nombreConcatenado = `${nombre.toUpperCase()} ${apellido}`;

var nombreMayusculas = nombre.toUpperCase();
var apellidoMinusculas = apellido.toLowerCase();

var primeraLetraNombre = nombre.charAt(0);
var cantidadLetrasNombre = nombre.lenght; // attribute.

var nombreCompleto = nombre + '' + apellido;
var nombreCompletoST = `${nombre.toUpperCase()} ${apellido}` // StringTemplate or TemplateLiterals.

var str = nombre.substr(1,2); // (posicion inicial, cantidad de chars).
```

### Números
```javascript
var edad = 27;

edad = edad + 1;
edad += 1;

var precio = 200.3 * 3;
// No da exacto, porque la manera de guardar decimales de JS no es muy precisa.
// Porque destina una cantidad de bytes en la ram, para asignarle un decimal.
var precioFixed = 200.3 * 100 * 3 / 100; // Solo funciona con 1 decimal.
var priceFixed = Math.round(200.3 * 100 * 3) / 100; // es un poco más exacta.

var totalStr = priceFixed.toFixed(3); // Convertir a string y cantidad de decimales.
var totalNum = parseFloat(totalStr); // Convertir a número float.
```
    
## Funciones
Son pedazos de código reutilizables.
    
```javascript
function nombreFuncion(parametrosRecibidos) { // Los Parametros, son opcionales, porque es weakly typed.
    // cuerpo función.
    return // Valor retornado por la función
}
```
Se puede asignar a una variable, una función.
Si una función no tiene nombre, es anonima.

```javascript
var ó const  esMayorEdad = function (persona) {
    return persona.edad >= MAYORIA_EDAD
}

String.prototype.capitalize = function() {
    return this.charAt(0).toUpperCase() + this.slice(1).toLowerCase();
}
```
### Arrow Function 

se le quita la palabra function, y se agrega =>

Si solo recibe un parametro, podemos obviar los parentesis. (persona)
```javascript
const esMayorEdad = persona => { 
    return persona.edad >= MAYORIA_EDAD
}
```
Si una función solo retorna algo, podemos borrar el return y las { llaves }
```javascript
    const esMayorEdad = persona => persona.edad >= MAMAYORIA_EDAD
```
   
### Alcance Funciones (Scopes) - Hoisting
- Las variables se envian por referencia a scopes descendientes predeterminadamente.

#### Hoisting
Declarar una variable, despues de usarla. - Las declaración de las variables declaradas con var, se (suben hasta el comienzo de la ejecución)

Todas las declaraciones (var, let, const, function, function*, class) son "hoisted"
Pero la diferencia entre las declaraciones

var **/** function **/** function* **(** undefined o generator **)**

y  let **/** const **/** class **(** temporal dead zone **)**

es la inicialización. Las segundas, solo se evaluan cuando son evaludas, mientras estan en una temporal dead zone

 
**Global Scope** (*var* o *let*) Estando fuera de una función/clase
```javascript    
a = 'xd'; // Global Scope (Default Scope)

var b; // Global Scope
b = 'xd'; 

var c = 'xd'; // Global Scope - Permite Hoisting 
let c = 'xd'; // Global Scope - No permite Hoisting
```
 **Local Scope** (*var* o *let*) Estando dentro de una función/clase
```javascript
function foo() {
    var d = 'lol'; // Local Scope
    var e = 'lol'; // Local Scope
}
```
- Se puede tener una variable global y una local con el mismo nombre y diferente valor
   
 **block scope** (*let* o *const*) *let* necesita estar dentro de un bloque *(if, while, for, loops, { }, etc)*
```javascript
if (true) {
    let i = 1; // Block Scope
}
console.log(i); // ReferenceError: i is not defined

const f = 'constante'; // No permite hoisting
```
- const crea una referencia inmutable, no variables inmutables
- las constantes no son reasignables, pero pueden ser mutables. 
    
 ### Side Effect (daño colateral)
 Cuando al ejecutar una función, ella modifica variables que no estan definidas dentro de ella.
 
 ## Objetos (JSON)
 Se declara con { claveKey: 'valorValue' } la clave puede ser un número o un string, el valor  puede ser una función, número, decimal, booleano, string..
 - Los Objetos que se pasen por parametro, se pasan por referencia (si los modificamos adentro de la función, se va ver afectado el objeto afuera también) - Side Effect
 
```javascript
var carlos = {
    nombre: 'Carlos',
    apellido: 'Jaramillo',
    edad: 22        
} 
    
function imprimirNombre(persona) {
    console.log(persona.nombre.toUpperCase());
}
imprimirNombre(carlos);

// Destructuring - solo se usa cuando siempre se envia
function imprimirNombre({ nombre }) { 
    console.log(nombre.toUpperCase());
}
imprimirNombre(carlos);
imprimirNombre({ nombre: 'Pepito' });

function imprimirNombre(persona) {
    // var nombre = persona.nombre;
    var { nombre } = persona; // Desestructurar Objetos
    console.log(nombre.toUpperCase());
}    
imprimirNombre(carlos);

//Evitar Side Effect
function cumpleanos(persona) {
    // Retorna un objeto nuevo con la edad modificada 
    return {...persona, edad: persona.edad + 1}
    //(... Spread Operator) clona un objeto o array
}
``` 
## Comparaciones
Si comparara objetos fallaría porque compararía la posición en memoria.
#### Valores primitivos:
- 2 iguales (==) compara convirtiendo ambos valores a string  
- 3 iguales (===) compara tipo y valor

## Condicionales 
```javascript
if (condición) {
    código a ejecutar, si se cumple la función
} else {
    código a ejecutar, cuando no se cumple la función
}
```

## Ciclos
### for