# Структуры данных

***Структуры данных*** - способ хранения и организации данных для их эффективного использования. Ни одна структура данных не является универсальной и не может подходить для всех целей, поэтому важно знать преимущества и ограничения, присущие некоторым из них. Распространенными типами структур данных являются:

- _[[Array|Массив]]_;
- _[[Linked_list|Связанный список]]_;
- _[[Queue|Очередь]]_;
- _[[Stack|Стек]]_;
- _деревья_.

Выбор структуры данных часто начинается с выбора абстрактного типа данных, широкого типа, инкапсулирующего различные возможные структуры данных.

Структуры данных важны, т.к. позволяют организовывать данные в эффективном и управляемом формате. Структуры составляют важную часть для создания алгоритмов. Выбор правильной структуры позволит создать эффективное решение, что позволит значительно снизить сложность кода.

Структуры данных делятся на:

- _Линейные_ - в таких структурах данные организованны последовательно, друг за другом. Примеры, стеки, очереди и т.д.
- _Нелинейные_ - такие структуры имеют более сложные связи, например иерархические. Примеры, деревья, графы

## Разница между **типами данных** и **структурами данных**:

- _Типы данных_ — говорят о том, что хранят данные, но не о том, как они организованы и как с ними работать. Они бывают:
  - _Примитивные_: например, целые числа (int), числа с плавающей точкой (float), символы (char), логические значения (boolean).
  - _Составные_: создаются из примитивных типов. Примеры: строки, массивы, структуры.
- _Структуры данных_ — описывают способ организации данных и набор операций, которые можно выполнять над этими данными.

Примитивные типы данных отвечают за представление значения в памяти, тогда как структуры данных определяют, как эти значения организованы для эффективного выполнения операций (например, вставки, удаления, поиска и т.д.).

## Абстрактный тип данных (АТД)

***Абстрактный тип данных*** - описыовает набор данных и операций, которые можно выполнять над этими данными, независимо от реализации.

Когда мы работаем с абстрактным типом данных нам важно понимать логику работы операций, а не внутреннюю реализацию.

Различие между АТД и структурами данных:

- _АТД_ описывает **поведение и интерфейс** работы с данными (например, стек или очередь).
- _Структура данных_ — это **конкретная реализация** АТД на уровне программирования.