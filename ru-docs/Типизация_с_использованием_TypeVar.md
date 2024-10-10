# 2.1 Типизация с использованием TypeVar
TypeVar - это инструмент, предоставляемый модулем `typing` в `Python`, который позволяет создавать универсальные функции и классы, работающие с различными типами данных. Он дает возможность определять обобщенные типы, которые могут быть заменены конкретными типами во время выполнения программы.

## Создание универсальных функций и классов
С помощью `TypeVar` вы можете создавать функции и классы, которые могут работать с различными типами данных. Это достигается за счет использования переменных типа, которые могут быть заменены на конкретные типы при вызове функции или создании экземпляра класса.

Например, рассмотрим функцию, которая принимает два аргумента одного и того же типа и возвращает их сумму:
```python
from typing import TypeVar

T = TypeVar('T', int, float)

def add(a: T, b: T) -> T:
    return a + b
```

В этом примере `T` - это переменная типа, определенная с помощью `TypeVar`. Она может быть заменена на int или float при вызове функции `add()`. Таким образом, функция может работать как с целыми, так и с плавающими числами.

## Ограничение типов с помощью TypeVar
Вы также можете ограничить типы, которые могут быть использованы с `TypeVar`, используя дополнительные аргументы. Это позволяет вам создавать более специализированные универсальные функции и классы.

Например, вы можете ограничить `TypeVar` до типов, которые поддерживают операцию сложения:
```python
from typing import TypeVar, Addable

AddableT = TypeVar('AddableT', bound=Addable)

def add(a: AddableT, b: AddableT) -> AddableT:
    return a + b
```

В этом примере `AddableT` - это `TypeVar`, ограниченный типами, которые поддерживают операцию сложения (т.е. реализуют протокол `Addable`). Это гарантирует, что функция `add` может работать только с типами, для которых определена операция сложения.

## Практические примеры использования TypeVar
Вот несколько практических примеров использования `TypeVar`:
### 1. Универсальный контейнер:
```python
from typing import TypeVar, Generic

T = TypeVar('T')

class Container(Generic[T]):
	def __init__(self, value: T):
	   self.value = value

def get(self) -> T:
   return self.value
```

Этот класс `Container` может хранить и возвращать значения любого типа, определяемого с помощью `T`.
### 2. Универсальный сортировщик:
```python
from typing import TypeVar, Callable, List

T = TypeVar('T')

def sort(items: List[T], key: Callable[[T], Any]) -> List[T]:
	return sorted(items, key=key)
```
   
Эта функция `sort` может сортировать списки любых типов, используя пользовательскую функцию `key`.
### 3. Универсальный репрезентативный метод:
```python
from typing import TypeVar, Generic

T = TypeVar('T')

class Person(Generic[T]):
   def __init__(self, name: str, data: T):
	   self.name = name
	   self.data = data

   def __repr__(self) -> str:
	   return f"Person(name='{self.name}', data={self.data!r})"
```

В этом примере класс Person использует `TypeVar T`, чтобы позволить хранить данные любого типа в атрибуте data. Метод `__repr__` также использует `T`, чтобы обеспечить универсальное строковое представление объекта.

### 4. Универсальный генератор:
```python
from typing import TypeVar, Iterable, Callable

T = TypeVar('T')
U = TypeVar('U')

def map_generator(iterable: Iterable[T], func: Callable[[T], U]) -> Iterable[U]:
	for item in iterable:
	   yield func(item)
```

Функция `map_generator` использует два `TypeVar` (`T` и `U`), чтобы создать универсальный генератор, который применяет заданную функцию к каждому элементу итерируемого объекта.

***

<div align="center">
	<a href="./Классы_и_типизация.md">
		<img src="./assets/back.png" alt="Назад" style="width: 250px;">
	</a>
	<a href="./Типы_объединений_и_опциональные_типы.md">
		<img src="./assets/next.png" alt="Далее" style="width: 250px;">
	</a>
</div>