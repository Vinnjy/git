# Pro:

  * ### [Перемещение изменений = "git cherry-pick"](#title8)

  * ### [Перемещение изменений (интерактивный rebase) = "git rebase -i"](#title9)

  * ### [Теги = "git tag"](#title12)

  * ### [Описание тегов = "git describe"](#title13)

<br>

<br>

<br>

## <a id ="title8">Перемещение изменений</a>

Итак, мы уже освоили основы Git: 

 * коммиты
 * ветки
 * перемещение по дереву изменений.

Теперь речь пойдёт о перемещении изменений — возможности, позволяющей разработчику сказать "Хочу, чтобы эти изменения были вот тут, а вот эти — вон там" и получить точные, правильные результаты, не теряя при этом гибкости разработки.

* ***Cherry pick*** =  **копировать несколько коммитов на место, где сейчас находишься (HEAD)**.

Делается с помощью команды:
```
git cherry-pick <Commit1> <Commit2> <...>
```
### Пример.

1. Вот репозиторий, где есть некие изменения в ветке side, которые мы хотим применить и в ветку main.

2. Мы можем сделать это при помощи команды rebase, которую мы уже прошли, но давай посмотрим, как cherry-pick справится с этой задачей.

<img width="237" height="338" alt="image" src="https://github.com/user-attachments/assets/03591807-b225-47d4-9be1-6babb06088bc" />

### Решение.

1. Пропишем команду:
```
git cherry-pick C2 C4
```
Результат:

<img width="247" height="364" alt="image" src="https://github.com/user-attachments/assets/bdc2f14f-6d6a-4650-9412-5dd912df2f15" />

* Копии С2 и С4 теперь в ветке, где был HEAD.

### Пример.

Дано:

<img width="682" height="440" alt="image" src="https://github.com/user-attachments/assets/afddf65b-37bc-4275-a13f-553f7037f391" />

1. Cкопируй изменения из этих трёх веток в мастер. Чтобы понять, какие коммиты копировать, посмотри на визуализацию уровня.

<img width="320" height="640" alt="image" src="https://github.com/user-attachments/assets/dd0710c0-561b-422b-a4b5-f58837227b45" />

### Решение.

1. Пропишем команду:
```
git cherry-pick C3 C4 C7
```
Результат:

<img width="1156" height="558" alt="image" src="https://github.com/user-attachments/assets/36f5f6ba-968c-4c8e-ae70-8de7e944dd3a" />

<br>

<br>

<br>

## <a id ="title9">Перемещение изменений (интерактивный rebase)</a>

* Git cherry-pick прекрасен = **когда точно известно, какие коммиты нужны** = ***известны их точные хеши***.

* Когда нет, то ***интерактивный rebase*** = опция **-i**.

* Git откроет интерфейс просмотра того, **какие коммиты готовы к копированию на цель rebase (target)**.

* Показываются ***хеши коммитов*** и ***комментарии*** к ним, так что можно легко понять что к чему.

Для "реального" Git, этот интерфейс означает просто открытие файла в редакторе типа vim. Редактор заменит диалоговое окно (делают одно и тоже).

После открытия окна интерактивного rebase есть три варианта для каждого коммита:

* **Сменить положение коммита по порядку**, переставив строчку с ним в редакторе.

* "Выкинуть" коммит из ребейза. Для этого есть ***pick*** - переключение его означает, что нужно выкинуть коммит.

* **Соединить коммиты**.

### Пример.

1. Появится окно интерактивного rebase.

2. Переставляем несколько коммитов (или удали кое-какие) и посмотри, что получится в итоге.

<img width="127" height="337" alt="image" src="https://github.com/user-attachments/assets/25c7bd8b-1bfc-4701-b4f7-7957af5fd62b" />

### Решение.

1. Пропишем команду:
```
git rebase -i HEAD~4
```
Результат:

<img width="898" height="535" alt="image" src="https://github.com/user-attachments/assets/d5b219e3-f5b6-407d-ad51-0fe20f100330" />

<img width="305" height="329" alt="image" src="https://github.com/user-attachments/assets/da1ae7da-6112-4b23-8d16-6e40b54cbd11" />

* Скопировали коммиты, как сами и указали.

### Пример.

Дано:

<img width="141" height="646" alt="image" src="https://github.com/user-attachments/assets/b763b72f-7e02-4414-8d3a-20a5359451e3" />

1. Переставь коммиты при помощи интерактивного rebase в таком порядке, как указано на визуализации.

<img width="291" height="605" alt="image" src="https://github.com/user-attachments/assets/035463e6-627d-448c-ae7a-97753e47cbfa" />

### Решение.

1. Пропишем команду:
```
git rebase -i HEAD~4
```
Результат:

<img width="893" height="524" alt="image" src="https://github.com/user-attachments/assets/e52f4cd9-07b5-451e-a558-1d72d008b37a" />

2. Удаляем С2 через фиолетовую кнопку, переставляем С5 и С4 и нажимаем "Подтвержить".

<img width="890" height="534" alt="image" src="https://github.com/user-attachments/assets/a635ea21-6709-4a97-a460-cea3f3f99fb8" />

<img width="856" height="648" alt="image" src="https://github.com/user-attachments/assets/75e9977a-29a3-416c-aa40-e53790179035" />

<br>

<br>

<br>

## <a id ="title12">Теги</a>

Ветки ***просто двигать туда-сюда*** и они ***часто ссылаются на разные коммиты как на изменения данных в ветке***. 

* Ветки ***просто изменить***, ***часто временны***, ***постоянно меняют своё состояние***.

В таком случае, где взять постоянную ссылку на момент в истории изменений? Для таких вещей, как релиз и большие слияния, нужно нечто более постоянное, чем ветка.

* Git предоставляет нам **теги**.

* Основная задача – ***ссылаться постоянно на конкретный коммит***.

* После создания ***никогда не сменят своего положения***, так что можно с лёгкостью сделать checkout конкретного момента в истории изменений.

### Пример.

Создадим тег на C1, который будет нашей версией 1.

<img width="134" height="333" alt="image" src="https://github.com/user-attachments/assets/6ee002ed-9798-4a31-a589-b4c7d7a071ad" />

### Решение.

1. Пропишем команду:
```
git tag v1 C1
```
Результат:

<img width="130" height="324" alt="image" src="https://github.com/user-attachments/assets/2e819ba4-cccb-42e1-87c0-fe7a435c57da" />

* **Тег v1** = ссылается на C1 явным образом.

* Если конкретный коммит не указан, гит пометит тегом HEAD.

### Пример.

Дано:

<img width="678" height="415" alt="image" src="https://github.com/user-attachments/assets/25b3979a-9f8c-4d93-b02f-be995a80e0f1" />

1. Создайте теги так, как показано на визуализации, и потом перейди на тег v1. Обрати внимание, что ты перейдёте в состояние detached HEAD, так как нельзя сделать коммит прямо в тег v1.

<img width="270" height="625" alt="image" src="https://github.com/user-attachments/assets/197116fc-177c-4aff-9572-0b895886ee2b" />

### Решение.

1. Пропишем команды:
```
git checkout C2
git tag v1 C2
git tag v0 C1
```
Результат:

<img width="1014" height="404" alt="image" src="https://github.com/user-attachments/assets/284c83d4-4f79-4844-a69b-3d8b11983150" />

<br>

<br>

<br>

## <a id ="title13">Описание тегов</a>

Теги являются прекрасными ориентирами в истории изменений, поэтому в git есть команда, которая показывает, как далеко текущее состояние от ближайшего тега. И эта команда называется git describe

Git describe помогает сориентироваться после отката на много коммитов по истории изменений. Такое может случиться, когда вы сделали git bisect или если вы недавно вернулись из отпуска.
```
git describe <ref>
```
* **ref** — это что-либо, что ***указывает на конкретный коммит***. Если не указать ref, то git будет считать, что указано текущее положение (HEAD).

Вывод команды выглядит примерно так:
```
<tag>-<numCommits>-g<hash>
```
* **tag** – ***ближайший тег в истории изменений***. 

* **numCommits** – ***на сколько далеко мы от этого тега***.

* **hash** – ***хеш коммита, который описывается***.

### Пример.

<img width="229" height="360" alt="image" src="https://github.com/user-attachments/assets/de99ffad-b680-4930-a42f-da73800e1607" />

### Решение.

1. Пропишем команду:
```
git tag v2 C3
```
Результат:

<img width="249" height="353" alt="image" src="https://github.com/user-attachments/assets/6187768c-108b-475b-8fcf-75ca2d1afa9f" />

* git describe main выведет:

  * v1-2-gC2

* git describe side выведет:

  * v2-1-gC4

### Пример.

Дано:

<img width="675" height="565" alt="image" src="https://github.com/user-attachments/assets/4fdbca82-3d5f-4e1e-8cbe-7c321cbbe886" />

1. Нужно получить визулизацию, как на картинке.

<img width="278" height="660" alt="image" src="https://github.com/user-attachments/assets/8def800a-8b99-450a-a3aa-749df5ce52cc" />

### Решение.

1. Пропишем команды:
```
git commit
git describe main
git describe bugFix
```
Результат:

<img width="374" height="66" alt="image" src="https://github.com/user-attachments/assets/059e9782-2568-4022-b806-e5ce43218cad" />

<img width="376" height="54" alt="image" src="https://github.com/user-attachments/assets/fe55c42e-afe8-4064-8472-669ebcd6b5da" />
