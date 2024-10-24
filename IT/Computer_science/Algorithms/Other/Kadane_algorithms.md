---
tags:
  - "#array"
  - algorithms
---
# Алгоритм Кадане

**Алгоритм Кадане** - метод динамического программирования, используемый для нахождения максимальной суммы в подмассиве. Данный алгоритм имеет временную сложность $\mathsf{O}(n)$ и пространственную сложность $\mathsf{O}(1)$. Алгоритм эффективно обрабатывает как отрицательные, так и положительные числа, что делает универсальным инструментом для решения задач. 

**Подмассив** - непрерывная последовательность элементов.

Например:

Для массива [2, 3, -10, 2, 3, -4] подмассивом является [2, 3, -10] или [3, -4], но [2, -10, 2] не является подмассивом. 

## Метод грубой силы

Задачу поиска максимальной суммы в подмассиве можно решить и "методом грубой силы". Для этого нужно вычислить сумму каждого возможного подмассива и найти максимальную. 

```python
def kadane[T: (int, float)](arr: list[T]) -> T:
	max_sum = 0

	for i in range(len(arr)):
		current_sum = 0
		for j in range(i, len(arr)):
			current_sum += arr[j]

			if current_sum < max_sum:
				break
			
			max_sum = current_sum

	return max_sum
```

Данное решение имеет временную сложность $\mathsf{O}(n^2)$. Алгоритм Кадане позволяет уменьшить временную сложность до $\mathsf{O}(n)$.

## Алгоритм Кадане

Разберем теперь как работает алгоритм Кадане. Допустим у нас есть массив [-2, -2, 4, -1, 2, 1, -2]. На каждом шагу мы можем определить локальный максимум. Нам не нужно вычислять сумму всех подмассивов, поскольку нам уже известна сумма максимального подмассива с предыдущего шага.

```ad-info
title: Принцип алгоритма Кадане

Локальный максимум в индексе $i$ - максимум $\mathsf{A}[i]$ и сумма $\mathsf{A}[i]$ + локальный максимум в индексе $i-1$.  

$local\_max[i] = \max (\mathsf{A}[i], \mathsf{A}[i] + local\_max[i - 1])$
```

![kadane-1](statics/img/kadane/kadane.svg)

```python
def kadane[T: (int, float)](arr: list[T]) -> T:
	local_max = arr[0]
	global_max = arr[0]

	for num in arr[1:]:
		if num > local_max + num:
			local_max = num

		if local_max > global_max:
			global_max = local_max

	return global_max
```

## Преимущества и недостатки

### Преимущества

- Эффективен;
- Обрабатывает как положительные, так и отрицательные числа;
- Прост в реализации

### Недостатки

- Предоставляет только сумму подмассива, а не сам подмассив. (Требует доработок)

## Применение алгоритма

- *Анализ временных рядов*. Например, поиск периода с максимальным количеством пользователей на сайте;
- *Обработка сигналов*. Например, поиск участка сигнала с максимальной амплитудой;
- *Обработка изображений*. Например, задачи, связанные с поиском области изображения с максимальной интенсивностью или контрастом;
- *Финансовый анализ*. Например, нахождение периода с наибольшим ростом прибыли на рынке;

## Источники

1. https://medium.com/@rsinghal757/kadanes-algorithm-dynamic-programming-how-and-why-does-it-work-3fd8849ed73d;
2. https://www.simplilearn.com/kadanes-algorithm-article;