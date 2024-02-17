# Что такое система контроля версий и Git

Система контроля версий(СКС) — это система, записывающая изменения в файл или набор файлов в течение времени и
позволяющая вернуться позже к определённой версии.

Существуют следующие СКС:

* Локальные;
* Централизованные;
* Распределенные.

Git является распределенной СКС. В распределенных СКС каждый участник имеет свою полную копию репозитория. Тем самым,
если какой-то из серверов сломается, у каждого будет своя копия, что позволит без проблем восстановить проект.

```mermaid
---
title: Пример работы РСКС
---
graph LR
    PC1 <--> Server;
    PC1 <--> PC2;
    Server <--> PC2;
```

<p id="snapshot">Git не хранит изменения в виде набора файлов, он хранит изменения в виде потока снимков.</p>

```mermaid
---
title: Поток снимков
---
flowchart TD
    v1([version1]):::ver --- fileA1([file A]):::change  --- fileB1([file B]):::change --- fileC1([file C]):::change
    v2([version2]):::ver --- fileA2([file A]):::change --- fileB2([file B]):::no_change --- fileC2([file C]):::change
    v3([version3]):::ver --- fileA3([file A]):::change --- fileB3([file B]):::change --- fileC3([file C]):::no_change
    v4([version4]):::ver --- fileA4([file A]):::no_change --- fileB4([file B]):::change --- fileC4([file C]):::change

classDef ver fill:#d3942f, color: #000, stroke: #000
classDef change fill: #bab193, color: #000,stroke: #000
classDef no_change fill: #bab193,color: #000, stroke: #000, stroke-dasharray: 5 5
```

При сохранении состояния, Git сохраняет новые изменения, а на файлы, которые не были затронуты изменениями, создает
ссылку.

Перед сохранением Git сначала вычисляет хеш-сумму, а только потом производит сохранение. Это означает, что нельзя
изменить файл или директорию, чтобы Git об этом не узнал.

У Git есть три основных состояния:

* Измененный (modified) - файл был изменен;
* Индексированный (staged) - файл готов к сохранению;
* Зафиксированный (committed) - файл сохранен в локальной БД.

```mermaid
sequenceDiagram
    participant wd as Working Directory
    participant sa as Staging Area
    participant gr as .git (repo)
    wd ->> sa: Stage Fixed
    sa ->> gr: Commit
    gr ->> wd: Checkout the project
```

Рабочая директория - это снимок определенной версии проекта.

Индекс - файл, содержащий информацию об изменениях для следующего коммита.

Каталог Git - хранит метаинформацию и базу объектов проекта.
