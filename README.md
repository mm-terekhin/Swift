- [Общие](#)
   * [Типы данных](#-data_types)
   * [Неявная типизация](#-implicit_typing)
   * [Типобезопасность](#-type_safety)
   * [Преобразование типов](#-type_conversion)
   * [Арифметические операции](#-arithmetic_operations)
   * [Условные конструкции](#-conditional_constructions)
   * [Тернарный оператор](#-ternary_operator)
   * [Конструкция switch/case](#-switch)
   * [Кортежи](#-tuples)
   * [nil и опциональные типы](#-nil)


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

<!-- TOC --><a name="-conditional_constructions"></a>

### Условные конструкции
`if/else if/ else` 
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

---

<!-- TOC --><a name="-ternary_operator"></a>

### Тернарный оператор
```
var num1 = 10
var num2 = 6

var num3 = num1 > num2 ? num1 - num2 : num1 + num2
```

---

<!-- TOC --><a name="-switch"></a>

Конструкция `switch/case`
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

<!-- TOC --><a name="-nil"></a>

### nil и опциональные типы
```
var number: Int? = 12
number = nil
```

---