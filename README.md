- [Общие](#)
   * [Типы данных](#-data_types)
   * [Неявная типизация](#-implicit_typing)
   * [Типобезопасность](#-type_safety)
   * [Преобразование типов](#-type_conversion)
   * [Арифметические операции](#-arithmetic_operations)
   * [nil и опциональные типы](#-nil)
   * [Условные конструкции](#-conditional_constructions)
   * [Кортежи](#-tuples)
   * [Циклы](#-cycles)
   * [Функции и методы](#-functions)


<!-- TOC --><a name=""></a>
## Общие

<!-- TOC --><a name="-data_types"></a>

### Типы данных
- `Int`: представляет целые числа со знаком, например, 1, -30, 458. На 32-разрядных платформах эквивалентен Int32, а на 64-разрядных - Int64
- `Double`: 64-битное число с плавающей точкой, содержит до 15 чисел в дробной части
- `Bool`: представляет логическое значение true или false
- `String`: представляет строку
- `Character`: представляет отдельный символ

`let` - указание того, что перменная константна
`var` - указание того, что перменной можно присвоить др. значение

---

<!-- TOC --><a name="-implicit_typing"></a>

### Неявная типизация
Если мы явным образом не указываем тип переменных и констант, то он автоматически выводится системой на основании хранящегося значения.
`var name = "Tom"`

---

<!-- TOC --><a name="-type_safety"></a>

### Типобезопасность
`var age: Int = 22`

---

<!-- TOC --><a name="-type_conversion"></a>

### Преобразование типов
```
var x = 5
var y = 7.5

let tempY = Int(7.5) // 7
let tempX = Double(x) // 5.0 
```

---

<!-- TOC --><a name="-arithmetic_operations"></a>

### Арифметические операции
- `+`: Сложение
- `-`: Вычитание 
- `*`: Умножение 
- `/`: Деление 
- `%`: Возвращает остаток от деления 

---

<!-- TOC --><a name="-nil"></a>

### nil и опциональные типы
```
var number: Int? = 12
number = nil
```

---

<!-- TOC --><a name="-conditional_constructions"></a>

### Условные конструкции
#### if/else if/ else
```
et num1 = 22
let num2 = 15

if num1 > num2{
     
    print("num1 больше чем num2")
}
else if (num1 < num2){
 
    print("num1 меньше чем num2")
}
else{
 
    print("num1 и num2 равны")
}
```

#### Тернарный оператор
```
var num1 = 10
var num2 = 6

var num3 = num1 > num2 ? num1 - num2 : num1 + num2
```

#### Конструкция `switch/case`
```
var num: Int = 22
 
switch num {
case 0:
    print("Переменная равна 0")
case 10:
    print("Переменная равна 10")
case 22:
    print("Переменная равна 22")
default:
    break // Прервать
}
```
С помощью знака подчеркивания `_` можно задать соответствие всем остальным значениям:
```
let number = 5
switch number {
case 1:
    print("Number = 1")
case 2:
    print("Number = 2")
case _:
    print("Number не равно ни 1, ни 2, но это не точно")
}
```
Также мы можем сравнивать выражение не с одним значением, а с группой значений:
```
var num: Int = 20
 
switch num {
case 0, 10:     // если num равно 0 или 10
    print("Переменная равна 0 или 10")
case 11..<20:    // если num в диапазоне от 11 до 20, не включая 20
    print("Переменная находится в диапазоне от 11 до 20")
case 20...30:   // если num в диапазоне от 20 до 30
    print("Переменная находится в диапазоне от 20 до 30")
default:
    print("не удалось распознать число")
```
Мы можем опускать одну границу диапазона:
```
let i = 8
switch i {
case ...<0:
    print("i - отрицательное число")
case 1...:
    print("i - положительное число")
case 0:
    print("i равно 0")
default:break
}
```
Кроме выражений простых типов можно сравнивать кортежи:
```
let personInfo = ("Tom", 22)
switch personInfo {
case ("Bob", 33):
    print("Имя: Bob, возраст: 33")
case (_, 22):
    print("Имя: \(personInfo.0) и возраст: 22")
case ("Tom", _):
    print("Имя: Tom и возраст: \(personInfo.1)")
case ("Tom", 1...30):
    print("Имя: Tom и возраст от 1 до 30")
default:
    print("Информация не распознана")
}
```
Если мы хотим, чтобы также выполнялся и следующий оператор case (или оператор default), то в конце предыдущего блока case следует использовать оператор `fallthrough`:
```
let personInfo = ("Tom", 22)
switch personInfo {
case ("Bob", 33):
    print("Имя: Bob, возраст: 33")
case (_, 22):
    print("Имя: \(personInfo.0) и возраст: 22")
    fallthrough
case ("Tom", _):
    print("Имя: Tom и возраст: \(personInfo.1)")
default:
    print("Информация не распознана")
}
```
Связывание значений
```
let personInfo = ("Tom", 22)
switch personInfo {
case (let name, 22):
    print("Имя: \(name) и возраст: 22")
case ("Tom", let age):
    print("Имя: Tom и возраст: \(age)")
case let (name, age):
    print("Имя: \(name) и возраст: \(age)")
}
```
Оператор `where` - задает дополнительные условия:
```
let i = 8
switch i {
case let k where k < 0:
    print("i - отрицательное число")
case let k where k > 0:
    print("i - положительное число")
case 0:
    print("i is 0")
default:break
}
```

#### if let
Конструкция `if let` позволяет безопасно извлечь значение из опционала и использовать его внутри блока `if`. Если опционал содержит значение, то оно извлекается и может быть использовано внутри блока. Если опционал равен `nil`, то блок `if` не выполняется.
```
let optionalName: String? = "John"

if let name = optionalName {
    print("Hello, \(name)!")
} else {
    print("Hello, anonymous!")
}
```

#### guard let
Конструкция ```guard let``` также используется для безопасного извлечения значения из опционала, но она работает немного иначе. ```guard let``` используется для раннего выхода из функции, метода или замыкания, если опционал равен ```nil```. Если значение извлечено успешно, оно может быть использовано за пределами блока ```guard```.
```
func greet(name: String?) {
    guard let name = name else {
        print("Hello, anonymous!")
        return
    }
    
    print("Hello, \(name)!")
}

greet(name: "John")  // Выведет: Hello, John!
greet(name: nil)     // Выведет: Hello, anonymous!
```

Область видимости:
- `if let` ограничивает область видимости извлеченного значения блоком `if`.
- `guard let` делает извлеченное значение доступным за пределами блока `guard`.

Использование:
- `if let` используется, когда вам нужно выполнить код только если опционал содержит значение.
- `guard let` используется для раннего выхода из функции или метода, если опционал равен `nil`.

---

<!-- TOC --><a name="-tuples"></a>

### Кортежи
Кортежи или Tuples представляют набор значений, которые рассматриваются как один объект. Для создания кортежа используются скобки, внутри которых записываются все элементы кортежа:
```
let props = (22, "age")
var userInfo = (true, 34, "Tom")
```
||
```
let props: (Int, String) = (22, "age")
var userInfo: (Bool, Int, String) = (true, 34, "Tom")
```

Если необходимо игнорировать при присвоении некоторые значения, то для них можно использовать знак подчеркивания `_`.
```
var userInfo: (Bool, Int, String) = (true, 34, "Tom")
let(_, age, name) = userInfo
```

Также при определении кортежа мы можем именовать его отдельные элементы.
`var userInfo = (married: true, age: 34, name: "Tom")`

---

<!-- TOC --><a name="-cycles"></a>

### Циклы

#### Цикл for-in
```
for item in 1...5 {
     
    print(item)
}
```

#### Цикл while
```
while условие {
     
    // действия
}
```

#### Цикл repeat-while
```
repeat {
     
    print(i)
    i-=1
} while i > 0
```

---

<!-- TOC --><a name="-functions"></a>

### Функции и методы
```
func имя_функции (параметры) -> тип_возвращаемого_значения {
     
    // набор инструкций
}
```

#### Параметры функции
```
func printInfo(name: String, age: Int){
 
    print("Имя: \(name) ; возраст: \(age)")
}
```

#### Значения параметров по умолчанию
```
func printInfo(name: String = "Tom", age: Int = 22){
 
    print("Имя: \(name) ; возраст: \(age)")
}
```

#### Дополнительно о параметрах функций
С помощью оператора многоточия (`...`) можно устанавливать произвольное количество параметров одного типа.
```
func sum(numbers: Int...) -> Int{
 
    var total: Int = 0
    for number in numbers{
     
        total+=number
    }
    return total
}
 
sum(1, 2, 3, 4, 5)  // 15
```

#### Выходные параметры inout
Если  необходимо изменить значение параметра, то его надо определить с ключевым словом `inout`:
```
func increase(_ n : inout Int){
    n += 10
}
 
var d = 20
increase(&d)
print(d)        // 30
```

#### Перегрузка функций
Нам доступен механизм перегрузки функций, то есть мы можем определять функции с одним и тем же именем, но разным количеством или типом параметров:
```
func sum(_ x: Int, _ y : Int){
    print(x+y)
}
func sum(_ x: Double, _ y: Double){
    print(x+y)
}
 
func sum(_ x: Int, _ y: Int, _ z: Int ){
    print(x + y + z)
}
 
sum(1, 2)           // 3
sum(1.2, 2.3)       // 3.5
sum(2, 3, 4)        // 9
```

#### Замыкания
Замыкания (сlosures) представляют самодостаточные блоки кода, которые могут использоваться многократно в различных частях программы, в том числе в виде параметров в функциях.
Замыкающие выражения в общем случае имеют следующий синтаксис:
```
{ (параметры) -> тип_возвращаемого_значения in
 
    инструкции
}
```

Подобно тому, как переменная или константа могут представлять ссылку на функцию, они также могут представлять ссылку на замыкание:
```
let hello = { print("Hello world")}
hello()
```

Дополнительно можно определить список параметров с помощью ключевого слова in:
```
let hello = {
    (message: String) in
    print(message)
}
hello("Hello")
hello("Salut")
hello("Ni hao")
```

Также можно определить возвращаемое значение:
```
let sum = {
    (x: Int, y: Int) -> Int in
    return x + y
}
print(sum(2, 5))        // 7
print(sum(12, 15))      // 27
print(sum(5, 3))        // 8
```

Мы можем зафиксировать начальные значения переменных:
```
var a = 14
var b = 2
 
let myClosure: () -> Int = {[a, b] in return a + b}
print(myClosure())  // 16
 
a = 5
b = 6
print(myClosure())  // 16
```
