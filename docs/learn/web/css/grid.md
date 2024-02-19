# Grid

CSS Grid Layout (спецификация) или просто Grid — это удобная технология для раскладки элементов на веб-страницах. В отличие от флексбоксов, одновременно работающих только с одним измерением, Grid дают возможность работать одновременно с двумя: горизонталью и вертикалью.

Принцип работы Grid чем-то похож на таблицы. Вместо работы только с рядами или только с колонками с помощью Grid можно работать с так называемыми Grid-ячейками, позиционируя элементы по вертикали и горизонтали одновременно.

-   _min-content_ - минимальный размер контента.
-   _max-content_ - максимальный размер содержимого.
-   _auto_ - это ключевое слово во многом похоже на fr, за исключением того, что они «проигрывают» борьбу по размерам fr при распределении оставшегося пространства.
-   _fr_ - часть оставшегося пространства.
-   _fit-content()_ - использует доступное пространство, но не меньше `min-content` и не больше `max-content`.
-   _minmax()_ - устанавливает минимальное и максимальное значение длины;
-   _auto-fill_ - разместить в строке как можно больше столбцов, даже если они пусты.
-   _auto-fit_ - Вставьте в пространство любые колонки.

## Основные термины

-   **Grid-контейнер**:

    Родительский элемент, к которому применяется свойство `display: grid`. В примере ниже _Grid-контейнером_ является `container`.

    === "HTML"

        ```html
        <div class="container">
            <div class="item item-1"> </div>
            <div class="item item-2"> </div>
            <div class="item item-3"> </div>
        </div>
        ```

-   **Grid-элемент**:

    Дочерний элемент, прямой потомок _Grid-контейнера_. Подчиняется правилам раскладки Grid. Класс `item` является _Grid-элементом_.

    === "HTML"

        ```html
        <div class="container">
            <div class="item"> </div>
            <div class="item">
                <p class="sub-item"> </p>
            </div>
            <div class="item"> </div>
        </div>
        ```

-   **Grid-линия**:

    Разделительная линия, формирующая структуру Grid. Может быть как вертикальной (Grid-линия колонки), так и горизонтальной (Grid-линия ряда). Располагается по обе стороны от колонки или ряда.

      <img src="../images/grid/terms-grid-line.svg" style="background-color: white" alt="grid-line" width="350px">

-   **Grid-ячейка**:

    Пространство между соседними Grid-линиями. Единица Grid-сетки.

    <img src="../images/grid/terms-grid-cell.svg" style="background-color: white" alt="grid-line" width="350px">

-   **Grid-полоса**:

    Пространство между двумя соседними Grid-линиями. Может быть проще думать о Grid-полосе как о ряде или колонке.

    <img src="../images/grid/terms-grid-track.svg" style="background-color: white" alt="grid-line" width="350px">

-   **Grid-область**:

    Область, ограниченная четырьмя Grid-линиями. Может состоять из любого количества ячеек как по горизонтали, так и по вертикали.

    <img src="../images/grid/terms-grid-area.svg" style="background-color: white" alt="grid-line" width="350px">

## Свойства Grid

### Display

Определяет элемент как Grid-контейнер.

Значение:

-   `grid` - создает сетку на уровне блока;
-   `inline-grid` - создает сетку встроенного уровня.

=== "CSS"

    ```css
    .container {
        display: grid | inline-grid;
    }
    ```

### Grid-template-columns и Grid-template-rows

Определяет столбцы и строки сетки с помощью списка значений, разделенных пробелами. Значения представляют размер дорожки, а пространство между ними представляет линию сетки.

Значения:

-   `size` - Размер Grid-ячейки;
-   `name` - Произвольное имя Grid-ячейки.

=== "HTML"

    ```html
    <style>
        .container {
            border: 2px solid;
            display: grid;

            grid-template-columns: [first] 100px [line2] 250px [line3] auto;
        }
    </style>

    <div class="container">
        <div class="item item-1">elem1</div>
        <div class="item item-2">elem2</div>
        <div class="item item-3">elem3</div>
        <div class="item item-3">elem3</div>
        <div class="item item-3">elem3</div>
    </div>
    ```

Единица измерения `fr` позволяет установить долю свободного пространства. Оно рассчитывается после всех фиксированных ячеек.

### Grid-template-areas

Определяет шаблон сетки, ссылаясь на имена областей сетки. Повторение имени области сетки приводит к тому, что содержимое охватывает эти ячейки. Точка означает пустую ячейку.

=== "HTML"

    ```html
    <style>
        .item-a {
            grid-area: header;
        }
        .item-b {
            grid-area: main;
        }
        .item-c {
            grid-area: sidebar;
        }
        .item-d {
            grid-area: footer;
        }

        .container {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-template-rows: auto;
            grid-template-areas:
                "header header header header"
                "main main . sidebar"
                "footer footer footer footer";
        }
    </style>
    <div class="container">
        <div class="item item-a">elem1</div>
        <div class="item item-a">elem1</div>
        <div class="item item-b"></div>
        <div class="item item-c">elem3</div>
        <div class="item item-d">elem3</div>
    </div>
    ```

В результате получаем следующую таблицу.

<img src="../images/grid/dddgrid-template-areas.svg" style="background-color: white" alt="dddgrid-template-areas" width="350px">

### Grid-template

Сокращение для установки `grid-template-rows`, `grid-template-columns` и `grid-template-areas` в одном объявлении.

=== "CSS"

    ```css
    .container {
        grid-template: none | <grid-template-rows> / <grid-template-columns>;
    }
    ```

### Column-gap и row-gap

Определяет размер линий сетки. Вы можете думать об этом как об установке ширины промежутков между столбцами/строками.

=== "CSS"

    ```css
    .container {
        column-gap: <line-size>;
        row-gap: <line-size>;
    }
    ```

Промежутки создаются только между столбцами/строками, а не на внешних краях.

### Gap

Сокращение для `column-gap` и `row-gap`.

=== "CSS"

    ```css
    .container {
        gap: <grid-row-gap> <grid-column-gap>;
    }
    ```

### Justify-items

Выравнивает элементы сетки вдоль строчной оси (строки), значение применяется ко всем элементам сетки внутри контейнера.

=== "CSS"

    ```css
    .container {
        justify-items: start | end | center | stretch;
    }
    ```

-   _stretch_ - заполняет всю ширину ячейки (это значение по умолчанию);
-   _start_ - выравнивает элементы так, чтобы они находились на одном уровне с начальным краем их ячейки;
-   _end_ - выравнивает элементы так, чтобы они находились на одном уровне с конечным краем их ячейки;
-   _center_ - выравнивает элементы по центру их ячейки.

### Align-items

Выравнивает элементы сетки вдоль оси блока (столбца), значение применяется ко всем элементам сетки внутри контейнера.

=== "CSS"

    ```css
    .container {
        align-items: start | end | center | stretch;
    }
    ```

-   _stretch_ - заполняет всю высоту ячейки (это значение по умолчанию);
-   _start_ - выравнивает элементы так, чтобы они находились на одном уровне с начальным краем их ячейки;
-   _end_ - выравнивает элементы так, чтобы они находились на одном уровне с конечным краем их ячейки;
-   _center_ - выравнивает элементы по центру их ячейки;
-   _baseline_ - выравнивание элементов по базовой линии текста.

### Place-items

Устанавливает свойства `align-items` и `justify-items` в одном объявлении.

=== "CSS"

    ```css
    .center {
        display: grid;
        place-items: <align-items> / <justify-items>;
    }
    ```

### Justify-content

Иногда общий размер сетки может быть меньше размера ее контейнера сетки. Это может произойти, если все элементы вашей сетки имеют негибкие единицы измерения, такие как px. В этом случае вы можете настроить выравнивание сетки внутри контейнера сетки. Это свойство выравнивает сетку вдоль встроенной оси (строки).

=== "CSS"

    ```css
    .container {
        justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
    }
    ```

-   _start_ - выравнивает сетку так, чтобы она была на одном уровне с начальным краем контейнера сетки;
-   _end_ - выравнивает сетку так, чтобы она была на одном уровне с конечным краем контейнера сетки;
-   _center_ - выравнивает сетку по центру контейнера сетки;
-   _stretch_ - изменяет размеры элементов сетки, чтобы сетка могла заполнить всю ширину контейнера сетки;
-   _space-around_ - размещает одинаковое пространство между каждым элементом сетки, с пробелами половинного размера на дальних концах;
-   _space-between_ - размещает одинаковое пространство между каждым элементом сетки, без пробелов на дальних концах;
-   _space-evenly_ - размещает одинаковое пространство между каждым элементом сетки, включая дальние концы.

### Align-content

Иногда общий размер сетки может быть меньше размера ее контейнера сетки. Это может произойти, если все элементы вашей сетки имеют негибкие единицы измерения, такие как px. В этом случае вы можете настроить выравнивание сетки внутри контейнера сетки. Это свойство выравнивает сетку вдоль оси блока (столбца).

=== "CSS"

    ```css
    .container {
        align-content: start | end | center | stretch | space-around | space-between | space-evenly;
    }
    ```

-   _start_ - выравнивает сетку так, чтобы она была на одном уровне с начальным краем контейнера сетки;
-   _end_ - выравнивает сетку так, чтобы она была на одном уровне с конечным краем контейнера сетки;
-   _center_ - выравнивает сетку по центру контейнера сетки;
-   _stretch_ - изменяет размеры элементов сетки, чтобы сетка занимала всю высоту контейнера сетки;
-   _space-around_ - размещает одинаковое пространство между каждым элементом сетки, с пробелами половинного размера на дальних концах;
-   _space-between_ - размещает одинаковое пространство между каждым элементом сетки, без пробелов на дальних концах;
-   _space-evenly_ - размещает одинаковое пространство между каждым элементом сетки, включая дальние концы.

### Place-content

Объединение для `align-content` и `justify-content`.

=== "CSS"

    ```css
    .container {
        place-content: <align-content> / <justify-content>
    }
    ```

### Grid-auto-columns и grid-auto-rows

Определяет размер любых автоматически сгенерированных дорожек сетки. Неявные дорожки создаются, когда элементов сетки больше, чем ячеек в сетке, или когда элемент сетки размещается за пределами явной сетки.

=== "CSS"

    ```css
    .container {
        grid-auto-columns: <track-size> ...;
        grid-auto-rows: <track-size> ...;
    }
    ```

Пример:

=== "CSS"

    ```css
    .container {
        grid-auto-columns: 60px;
    }
    .item-a {
        grid-column: 1 / 2;
        grid-row: 2 / 3;
    }
    .item-b {
        grid-column: 5 / 6;
        grid-row: 2 / 3;
    }
    ```

<img src="../images/grid/grid-auto-columns-rows-02.svg" style="background-color: white" alt="dddgrid-template-areas" width="350px">

### Grid-auto-flow

Если у вас есть элементы сетки, которые вы не размещаете в сетке явно, срабатывает алгоритм автоматического размещения.

-   _row_ - сообщает алгоритму авторазмещения поочередно заполнять каждую строку, добавляя новые строки по мере необходимости (по умолчанию);
-   _column_ - сообщает алгоритму авторазмещения поочередно заполнять каждый столбец, добавляя при необходимости новые столбцы;
-   _dense_ - сообщает алгоритму автоматического размещения попытаться заполнить пробелы в сетке раньше, если более мелкие элементы появятся позже.

=== "CSS"

    ```css
    .container {
        grid-auto-flow: row | column | row dense | column dense;
    }
    ```

Пример (row):

<img src="../images/grid/grid-auto-flow-01.svg" style="background-color: white" alt="dddgrid-template-areas" width="350px">

### Grid

Сокращение для установки всех следующих свойств в одном объявлении: `grid-template-rows`, `grid-template-columns`, `grid-template-areas`, `grid-auto-rows`, `grid-auto-columns` и `grid-auto-flow`

## Свойства элементов сетки

### Grid-column-start, grid-column-end, grid-row-start и grid-row-end

Определяет расположение элемента сетки внутри сетки, обращаясь к конкретным линиям сетки. `grid-column-start/grid-row-start` — это строка, в которой начинается элемент, и `grid-column-end/grid-row-end` — это строка, в которой элемент заканчивается.

=== "CSS"

    ```css
    .item {
        grid-column-start: <number> | <name> | span <number> | span <name> | auto;
        grid-column-end: <number> | <name> | span <number> | span <name> | auto;
        grid-row-start: <number> | <name> | span <number> | span <name> | auto;
        grid-row-end: <number> | <name> | span <number> | span <name> | auto;
    }
    ```

-   _line_ - может быть числом для обозначения пронумерованной линии сетки или именем для ссылки на именованную линию сетки;
-   _span number_ - элемент будет охватывать указанное количество дорожек сетки;
-   _span name_ - элемент будет перемещаться до тех пор, пока не достигнет следующей строки с указанным именем;
-   _auto_ - указывает на автоматическое размещение, автоматический интервал или интервал по умолчанию, равный единице.

### Grid-column и grid-row

Сокращение для `grid-column-start/grid-column-end` и `grid-row-start/grid-row-end` соответственно.

=== "CSS"

    ```css
    .item {
        grid-column: <start-line> / <end-line> | <start-line> / span <value>;
        grid-row: <start-line> / <end-line> | <start-line> / span <value>;
    }
    ```

### Grid-area

Дает элементу имя, чтобы на него можно было ссылаться в шаблоне, созданном с помощью этого grid-template-areas свойства. В качестве альтернативы это свойство можно использовать как еще более короткое сокращение для `grid-row-start + grid-column-start + grid-row-end + grid-column-end`.

=== "CSS"

    ```css
    .item {
        grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
    }
    ```

### Justify-self

Выравнивает элемент сетки внутри ячейки по встроенной оси (строки). Это значение применяется к элементу сетки внутри одной ячейки.

=== "CSS"

    ```css
    .item {
        justify-self: start | end | center | stretch;
    }
    ```

-   _stretch_ - заполняет всю ширину ячейки (это значение по умолчанию);
-   _start_ - выравнивает элемент сетки по начальному краю ячейки;
-   _end_ - выравнивает элемент сетки так, чтобы он был на одном уровне с конечным краем ячейки;
-   _center_ - выравнивает элемент сетки по центру ячейки.

### Align-self

Выравнивает элемент сетки внутри ячейки по оси блока (столбца). Это значение применяется к содержимому внутри одного элемента сетки.

=== "CSS"

    ```css
    .item {
        align-self: start | end | center | stretch;
    }
    ```

-   _stretch_ - заполняет всю высоту ячейки (это значение по умолчанию);
-   _start_ - выравнивает элемент сетки по начальному краю ячейки;
-   _end_ - выравнивает элемент сетки так, чтобы он был на одном уровне с конечным краем ячейки;
-   _center_ - выравнивает элемент сетки по центру ячейки.

### Place-self

Устанавливает свойства `align-self` и `justify-self` в одном объявлении.

=== "CSS"

    ```css
    .item-a {
        place-self: <align-self> / <justify-self>;
    }
    ```
