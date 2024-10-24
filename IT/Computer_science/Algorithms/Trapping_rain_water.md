# "Ловушка" для воды

"Ловушка" для воды заключается в определении общего количества воды, которое будет удержано между блоками, представленными как массив неотрицательных чисел. Каждый элемент массива представляет из себя высоту земли, а вода накапливается между высокими столбцами, если между ними есть низкие.

![img350-rain-water](statics/img/Trapping_rain_water/rain.svg)

## Первый способ. Наивный метод

```python
def max_water[T: int](arr: list[T]) -> T:
    res = 0

    for i in range(len(arr) - 1):

        left = arr[i]
        for j in range(i):
            left = max(left, arr[j])

        right = arr[i]
        for j in range(i + 1, len(arr)):
            right = max(right, arr[j])

        res += (min(left, right) - arr[i])

    return res
```

Сначала для каждого столбца массива находим, максимальную высоту всех столбцов слева, включая сам столбец, затем максимальную высоту справа. Вычисляем количество воды, которое будет удержано между. Последним шагом вычисляем разницу, которая и будет количеством удерживаемой воды.

## Второй способ. Предварительное вычисление

Этот метод является оптимизацией наивного метода, позволяющий решить задачу за линейное время $\mathsf{O}(n)$. Он основывается на том, что нам нужно заранее вычислить максимальные значения для каждого столбца, после этого мы можем быстро вычислить минимальную высоту между двумя максимальными столбцами.

```python
def trap_rain_water(arr: list[int]) -> int:
    if not arr:
        return 0
    
    n = len(arr)
    left_max = [0] * n
    right_max = [0] * n
    water_trapped = 0

    left_max[0] = arr[0]
    for i in range(1, n):
        left_max[i] = max(left_max[i - 1], arr[i])

    right_max[n - 1] = arr[n - 1]
    for i in range(n - 2, -1, -1):
        right_max[i] = max(right_max[i + 1], arr[i])

    for i in range(n):
        water_trapped += min(left_max[i], right_max[i]) - arr[i]

    return water_trapped
```

Недостаток данной реализации - дополнительная память $\mathsf{O}(n)$.

## Третий способ. Использование двух указателей.

Данный метод позволяет решить задач за линейную сложность и константное использование памяти. Вместо использования дополнительных массивов, мы используем два объема данных - один в начале, другой в конце. Затем мы сдвигаем их навстречу друг к другу вычисляя количество воды, которое может быть удержано.

```python
def trap_rain_water(arr: list[int]) -> int:
	if not arr:
		return 0

	left, right = 0, len(arr) - 1
	left_max, right_max = arr[left], arr[right]
	water_trapped = 0

	while left < right:
		if arr[left] < arr[right]:
			if arr[left] >= left_max:
				left_max = arr[left]
			else:
				water_trapped += left_max - arr[left]
			left += 1
		else:
			if arr[right] >= right_max:
				right_max = arr[right]
			else:
				water_trapped += right_max - arr[right]
			right -= 1

	return water_trapped
```

## Источник

1. https://www.geeksforgeeks.org/trapping-rain-water/
2. https://algo.monster/liteproblems/42