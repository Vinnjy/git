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
