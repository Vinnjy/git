# Основы:

## Base:

  * ### [Коммиты = "git commit"](#title0)

  * ### [Ветвление = "git branch или git checkout -b"](#title1)

  * ### [Ветки и слияние = "git merge"](#title2)

  * ### [Ветки и слияние-копией = "git rebase"](#title3)

<br>

## Base-Pro:

  * ### [HEAD = "git checkout (коммит или ветка)"](#title4)
  
  * ### [Относительные ссылки (^, ~) = "git checkout (ветка или HEAD)^"](#title5)

  * ### [Перемещение ветки = "git branch -f"](#title6)
  
  * ### [Отмена изменений = "git reset или git revert"](#title7)

<br>

## Pro:

  * ### [Перемещение изменений = "git cherry-pick"](#title8)

  * ### [Перемещение изменений (интерактивный rebase) = "git rebase -i"](#title9)

  * ### [Теги = "git tag"](#title12)

  * ### [Описание тегов = "git describe"](#title13)

<br>

## Рабочии ситуации:

  * ### [Исправленные ошибка](#title10)

  * ### [Внесение изменений в более ранний коммит](#title11)

  * ### [Rebase на нескольких ветках](#title14)

  * ### [Определение родителей (~, ^)](#title15)

  * ### [Спутанные ветки](#title16)

<br>

<br>

<br>

# Удалённые репозитории:

## Pull & Push

  * ### [Клонирование = "git clone"](#title17)

  * ### [Удалённые ветки = "git checkout origin/main"](#title18)

  * ### [Извлечение/скачивание данных из удаленного репозитория = "git fetch"](#title19)

  * ### [git fetch и git merge = "git pull"](#title20)

  * ### [Коллективная работа = "git fakeTeamwork"](#title21)

  * ### [Загрузка изменений в удалённый репозиторий = "git push"](#title22)

  * ### [Расхождение в истории](#title23)

  * ### [Заблокированная ветвь main](#title24)

<br>

## Продвинутое использование

  * ### [Push мастер](#title25)

  * ### [Слияение с удаённым репозиторием](#title26)

<br>

<br>

<br>

## <a id ="title0">Коммиты</a>

* Коммит в git репозитории хранит **снимок всех файлов в директории** = **огромная копия**, только лучше.

* Git пытается быть лёгким и быстрым насколько это только возможно, так что он не просто слепо копирует всю директорию каждый раз, а ужимает (когда это возможно) коммит **в набор изменений** или «дельту» = **между текущей версией и предыдущей**.

* Git хранит **всю историю о том, когда какой коммит был сделан**. Вот почему большинство коммитов имеют предков - мы указываем на предков стрелками при визуализации. Поддержка истории коммитов более чем важна для всех, кто работает над проектом.

### Пример.

1. Визуализация небольшого git репозитория.

2. Сейчас в нём два коммита: первый, исходный коммит С0 и один коммит С1 после него, содержащий изменения.

<img width="205" height="201" alt="image" src="https://github.com/user-attachments/assets/344fada6-32ba-4a6c-b084-fe6bb554a5d4" />

### Решение.

1. Пропишем команду:
```
git commit
```
Результат:

<img width="181" height="340" alt="image" src="https://github.com/user-attachments/assets/3a25665c-510b-4fa2-9b43-2cc46132cc71" />

* Только что внесли изменения в репозиторий и сохранили их как коммит. У коммита, который мы только что сделали, есть родитель, С1, который указывает на предыдущий коммит.

### Пример.

Дано:

<img width="205" height="201" alt="image" src="https://github.com/user-attachments/assets/344fada6-32ba-4a6c-b084-fe6bb554a5d4" />

1. Сделайте 2 коммита, чтобы получить визулизацию, как на картинке.

<img width="171" height="651" alt="image" src="https://github.com/user-attachments/assets/58585f29-1b2e-4f30-8ddf-40a614cd1553" />

### Решение.

1. Пропишем в командной строке:
```
git commit
git commit
```
Результат:

<img width="155" height="415" alt="image" src="https://github.com/user-attachments/assets/f297c0d2-2c77-4087-b455-13cbdb8c5f13" />

<br>

<br>

<br>

## <a id ="title1">Ветвление</a>

* Ветки в Git, как и коммиты, невероятно легковесны. Это просто **ссылки на определённый коммит** — ничего более. Вот почему многие фанаты Git повторяют мантру: "делай ветки сразу, делай ветки часто".

* Cоздание множества веток никак не отражается на памяти или жестком диске, удобнее и проще разбивать свою работу на много маленьких веток, чем хранить все изменения в одной огромной ветке.

* Cозданная ветка хранит изменения текущего коммита и всех его родителей.

### Пример.

Создадим новую ветку с именем newImage.

<img width="205" height="201" alt="image" src="https://github.com/user-attachments/assets/344fada6-32ba-4a6c-b084-fe6bb554a5d4" />

### Решение.

1. Пропишем команду (создание ветки):
```
git branch newImage
```
Результат:

<img width="187" height="192" alt="image" src="https://github.com/user-attachments/assets/ff7e5934-8d3f-46eb-aa90-ce75b801a799" />

* Ветка newImage указывает на коммит С1.

2. Теперь сделаем коммит. Пропишем команду:
```
git commit
```
Результат:

<img width="160" height="338" alt="image" src="https://github.com/user-attachments/assets/3c29db28-b96f-4336-a47b-59d08ad44507" />

* Ветка main сдвинулась, тогда как ветка newImage - нет. Всё из-за того, что мы не переключились на новую ветку, а остались в старой, о чём говорит звёздочка около ветки main.

3. Чтобы сделать коммит для ветки newImage, нужно **переключиься на ветку**, а затем сделать коммит. Вернёмся к пукнту 1:

<img width="187" height="192" alt="image" src="https://github.com/user-attachments/assets/ff7e5934-8d3f-46eb-aa90-ce75b801a799" />

4. Пропишем 2 команды:
```
git checkout newImage
git commit
```
Результат:

<img width="158" height="339" alt="image" src="https://github.com/user-attachments/assets/d6da4af7-1528-4e12-afe8-99c20183cc99" />

### Пример.

Дано:

<img width="169" height="170" alt="image" src="https://github.com/user-attachments/assets/eac38e5f-e298-4e90-8a45-559f0b8dbd87" />

1. Создай ветку с именем bugFix и переключись на неё.

2. Нужно получить визулизацию, как на картинке.

<img width="167" height="342" alt="image" src="https://github.com/user-attachments/assets/e77783db-5e0b-4aa0-8aaf-8f338bdd0725" />

### Решение.

1. Пропишем команду:
```
git checkout -b bugFix
```
* Создаст ветку и переключиться на неё.

Результат:

<img width="160" height="165" alt="image" src="https://github.com/user-attachments/assets/ff978f1d-36f4-4090-9f86-416376771299" />

<br>

<br>

<br>

## <a id ="title2">Ветки и слияние (merge)</a>

+ Как объединять изменения из двух разных веток.

   * Очень удобно создать ветку, сделать свою часть работы в ней и потом объединить изменения из своей ветки с общими.

+ Первый способ объединения изменений, который мы рассмотрим - **git merge** - слияние.

   * Слияния в Git создают особый вид коммита, который **имеет сразу двух родителей**. Коммит с двумя родителями обычно означает, что мы хотим **объединить изменения из одного коммита с другим коммитом и всеми их родительскими коммитами**.

### Пример.

1. Две ветки, каждая содержит по одному уникальному коммиту.

2. Это означает, что ни одна из веток не содержит полный набор "работ", выполненных в этом репозитории.

3. Можно исправить эту ситуацию, выполнив слияние.

<img width="241" height="374" alt="image" src="https://github.com/user-attachments/assets/111b05fd-c3b3-4f66-a591-53bfce5cfb26" />

### Решение.

1. Пропишем комвнду (слияние bugFix в main):
```
git merge bugFix
```
Результат:

<img width="295" height="363" alt="image" src="https://github.com/user-attachments/assets/103822a7-af38-4101-8df9-b8a55b6a6c86" />

+ Ветка main теперь указывает на коммит, у которого два родителя.

   * Если проследовать по стрелкам от этого коммита, вы пройдёте через каждый коммит в дереве прямиком к началу.

   * Это означает, что теперь **в ветке main содержатся все изменения репозитория**.


   * У каждой ветки — свой цвет. Каждый коммит становится того цвета, какого его ветка.

   * Если в нём изменения сразу двух веток - он становится цветом, смешанным из цветов родительских веток.

   * Цвет ветки main подмешан к каждому коммиту, а ветки bugFix - нет.

### Продлжим пример.

Cделаем слияние ветки main в ветку bugFix.

2. Пропишем комвнды:
```
git checkоut bugFix
git merge main
```
Результат:

<img width="263" height="383" alt="image" src="https://github.com/user-attachments/assets/c1ac4f63-e714-47d1-92ff-11285a45896b" />

* Так как ветка bugFix была предшественницей main, Git не делал ничего, только сдвинул bugFix на тот же коммит, где находится main.

* Теперь все коммиты одного цвета, что означает, что каждая ветка содержит все изменения репозитория.

### Пример.

Дано:

<img width="184" height="174" alt="image" src="https://github.com/user-attachments/assets/0efa73d2-fb33-451a-8e54-8974a19a1765" />

1. Создай новую ветку под названием bugFix.

2. Переключись на новую ветку bugFix командой git checkout bugFix.

3. Сделай один коммит.

4. Вернись на ветку main при помощи git checkout.

5. Сделай ещё один коммит.

6. Слей ветку bugFix с веткой main при помощи git merge.

7. Нужно получить визулизацию, как на картинке.

<img width="248" height="684" alt="image" src="https://github.com/user-attachments/assets/2422e86b-c625-4d40-8e1e-c321a864b4c5" />

### Решение.

1. Пропишем команды:
```
git checkout -b bugFix
git commit
git checkout main
git commit
git merge bugFix
```
Результат:

<img width="793" height="439" alt="image" src="https://github.com/user-attachments/assets/a5fe328d-df90-421b-a8f6-8d9aec0e04a2" />

<br>

<br>

<br>

## <a id ="title3">Ветки и слияние (rebase)</a>

* Oбъединения изменений в ветках - это rebasing. При ребейзе Git **по сути копирует набор коммитов и переносит их в другое место**.

* Преимущество rebase в том, что c его помощью можно делать чистые и красивые линейные последовательности коммитов. История коммитов будет чище, если вы применяете rebase.

### Пример.

1. Две ветки.
  
2. Выбрана ветка bugFix (отмечена звёздочкой).

3. Сдвинуть наши изменения из bugFix прямо на вершину ветки main.
   
4. Благодаря этому всё будет выглядеть, как будто эти изменения делались последовательно, хотя на самом деле - параллельно.

<img width="262" height="370" alt="image" src="https://github.com/user-attachments/assets/050f2a8a-afb4-47b5-83f4-f4c2fbd3295b" />

### Решение.

1. Пропишем командцу:
```
git rebase main
```
Результат:

<img width="253" height="334" alt="image" src="https://github.com/user-attachments/assets/625ea1a9-b18d-4251-8301-f4b1d688a60b" />

* изменения из bugFix находятся в конце ветки main и являют собой линейную последовательность коммитов.

* С3' - это его "копия" в ветке main.

+ **Ветка main не обновлена до последних изменений**

2. Пропишем команду:
```
git checkout main
```
Результат:

<img width="243" height="334" alt="image" src="https://github.com/user-attachments/assets/1051ad1c-8afd-4196-a67e-f8b6833f7687" />

3. Пропишем команду:
```
git rebase bugFix
```
Результат:

<img width="247" height="329" alt="image" src="https://github.com/user-attachments/assets/13789d63-182a-4af5-8ef1-3307f23a0e72" />

* Так как ветка main был предком bugFix, git просто сдвинул ссылку на main вперёд.

### Пример.

Дано:

<img width="145" height="162" alt="image" src="https://github.com/user-attachments/assets/26bc6d56-318e-49ad-9a3d-6bd9b4fb0643" />

1. Переключись на ветку bugFix.

2. Сделай коммит.

3. Вернись на main и сделай коммит ещё раз.

4. Переключись на bugFix и сделай rebase на main.

5. Нужно получить визулизацию, как на картинке.

<img width="323" height="637" alt="image" src="https://github.com/user-attachments/assets/56618dcd-479f-49a3-b3cc-70e8d73c1930" />

### Решение.

1. Пропишем команды:
```
git checkout -b bugFix
git commit
git checkout main
git commit
git checkout bugFix
git rebase main
```
Результат:

<img width="868" height="407" alt="image" src="https://github.com/user-attachments/assets/516bef45-4136-455f-95af-f9414c616df2" />

<br>

<br>

<br>

## <a id ="title4">HEAD</a>

* HEAD - это символическое имя **текущего выбранного коммита** — это, по сути, тот коммит, над которым мы **в данный момент** работаем.

* HEAD всегда **указывает на последний коммит из вашего локального дерева**.

* Большинство **команд Git**, изменяющих рабочее дерево, **начнут с изменения HEAD**.

* Обычно HEAD указывает на имя ветки (например, main). Когда вы делаете коммит, статус ветки main меняется и это **изменение видно через HEAD**.

### Пример.

Смотрим, где находится HEAD до коммита и после при выполненных командах (в решении).

ДО:

<img width="193" height="216" alt="image" src="https://github.com/user-attachments/assets/9ffaacc6-6626-414b-bc9d-9481bbf918b8" />

### Решение.

1. Пропишем команды:
```
git checkout C1
git checkout main
git commit
git checkout C2
```

ПОСЛЕ:

<img width="194" height="363" alt="image" src="https://github.com/user-attachments/assets/11b981f5-9dae-4564-a75f-b96294255a1d" />

* HEAD скрывался за ветке main.

### Detaching HEAD.

* **Отделение HEAD** = присвоение не ветке, а конкретному коммиту.

* Нужно для того, чтобы ***временно работать с конкретным коммитом***, не привязывая его к основной линии разработки, что позволяет экспериментировать без риска потерять данные.

* Новые коммиты, сделанные в этом состоянии, будут "осиротевшими", так как они ***не принадлежат ни одной ветке***, и их сложнее найти. 

Зачем это нужно ?

* **Изучение истории**: позволяет посмотреть на состояние проекта в прошлом, например, чтобы найти ошибку или изучить код определенного коммита.

* **Временные эксперименты**: Дает возможность проверить какой-либо код или исправление, не создавая новую ветку. Если эксперимент окажется неудачным, просто переключитесь обратно на нужную ветку, и "осиротевшие" коммиты будут проигнорированы, пока их не удалит сборщик мусора Git. 

Когда следует быть осторожным ?

* **Создание коммитов**: если вы создадите новые коммиты в состоянии "отсоединенного HEAD", они не будут прикреплены к какой-либо ветке. Это может привести к их потере.

* **Потеря данных**: Это может быть опасно, если вы забудете, что находитесь в "отсоединенном" состоянии, и случайно сделаете коммиты. Чтобы избежать этого, лучше сразу создать новую ветку для любых изменений. 

### Пример.

ДО:

* HEAD -> main -> C1.

<img width="144" height="188" alt="image" src="https://github.com/user-attachments/assets/d744bee3-b4cd-4196-a305-2336efd6a710" />

### Решение.

1. Пропишем команду:
```
git checkout C1
```
Результат:

<img width="195" height="218" alt="image" src="https://github.com/user-attachments/assets/eae41f89-fda2-47da-8da4-e73809ef4f10" />

ПОСЛЕ:

* HEAD -> C1.

### Пример.

Дано:

<img width="528" height="438" alt="image" src="https://github.com/user-attachments/assets/cec3f95d-18b3-4ebd-8625-9b2ecb1f69f9" />

1. Отделим HEAD от ветки bugFix и присвоим его последнему коммиту в этой же ветке.

2. Укажи коммит при помощи его идентификатора (hash). Hash для каждого коммита указан в кружке на схеме.

3. Нужно получить визулизацию, как на картинке.

<img width="297" height="669" alt="image" src="https://github.com/user-attachments/assets/99116e07-5c9f-41d7-8437-cf4e0d899294" />

### Решение.

1. Пропишем команду:
```
git checkout C4
```
Результат:

<img width="847" height="435" alt="image" src="https://github.com/user-attachments/assets/47a178cc-bb46-467b-8238-ad66f2e6f4bd" />

<br>

<br>

<br>

## <a id ="title5">Относительные ссылки (^, ~)</a>

* Передвигаться по дереву Git при помощи указания хешей коммитов так себе.

* В реальной ситуации у вас вряд ли будет красивая визуализация дерева в терминале, так что придётся каждый раз использовать **git log** = **чтобы найти хеш нужного коммита**.

* Более того, хеши в реальном репозитории Git намного более длинные. Например, хеш для коммита, который приведён в предыдущем уровне - fed2da64c0efc5293610bdd892f82a58e8cbc5d8.

* Git достаточно умён в работе с хешами. Ему нужны лишь первые несколько символов для того, чтобы идентифицировать конкретный коммит. Так что можно написать просто fed2 вместо колбасы выше.

С относительными ссылками можно **начать с какого-либо удобного места** (например, с ветки bugFix или от HEAD) и двигаться от него.

* **Относительные ссылки** - мощный инструмент, но мы покажем два простых способа использования:

  * **Перемещение на один коммит назад** = ***^***.
    
  * **Перемещение на несколько коммитов назад** = ***~<num>***.

### Пример.

1. Когда мы добавляем ***^*** к имени ссылки, Git воспринимает это как указание найти родителя указанного коммита.

* Так что main^ означает "первый родитель ветки main".

* main^^ означает прародитель (родитель родителя) main

2. Давайте переключимся на коммит Выше main

<img width="137" height="332" alt="image" src="https://github.com/user-attachments/assets/bb5dbd7d-9516-42cc-a681-a0041501b0b6" />

### Решение.

1. Пропишем команду:
```
git checkout main^
```
Результат:

<img width="138" height="337" alt="image" src="https://github.com/user-attachments/assets/bed77b43-0c40-47bf-acf1-949707c71a79" />

### Вместо ветки, как относительная ссылка, можно использовать HEAD.

### Пример.

1. Пройдёмся несколько раз по дереву коммитов.

<img width="140" height="335" alt="image" src="https://github.com/user-attachments/assets/5d6bf45d-3ef1-4b6c-adea-560b4b2c0495" />

### Решение.

1. Пропишем команды:
```
git checkout C3
git checkout HEAD^
git checkout HEAD^
git checkout HEAD^
```
Результат:

<img width="202" height="336" alt="image" src="https://github.com/user-attachments/assets/5175bda5-03c6-49f8-94a2-f650562af843" />

### Пример.

Дано:

<img width="515" height="434" alt="image" src="https://github.com/user-attachments/assets/544cb5d5-024d-49eb-a7ca-467aeda74a3d" />

1. Переместись на первого родителя ветки bugFix. Это отделит HEAD от ветки.

2. Нужно получить визулизацию, как на картинке.

<img width="229" height="684" alt="image" src="https://github.com/user-attachments/assets/882e287a-26aa-463b-98a8-d0ccec9ab504" />

### Решение.

1. Пропишите команду:
```
git checkout HEAD^
```
Результат:

<img width="784" height="432" alt="image" src="https://github.com/user-attachments/assets/e46675ef-5065-4184-800a-8331d29d2092" />

### Пример.

Переместиться на 4 коммита назад.

<img width="129" height="329" alt="image" src="https://github.com/user-attachments/assets/507b327a-ba6c-4c57-a5eb-bb420ca614c9" />

### Решение.

1. Пропишите команды:
```
git checkout HEAD~4
```
Результат:

<img width="198" height="343" alt="image" src="https://github.com/user-attachments/assets/9f121820-e1dd-4010-8549-28fe1e6ec0bf" />

<br>

<br>

<br>

## <a id ="title6">Перемещение ветки</a>

* Одна из наиболее распространённых целей, для которых используются ***относительные ссылки*** - **перемещение веток**.

* Можно напрямую **прикрепить ветку к коммиту** при помощи опции ***-f***, n - количество шагов назад.

1. Пропишем команду:
```
git branch -f main HEAD~n
```
* **Переместит (принудительно) ветку main на n родителей назад от HEAD**.

### Пример.

Переместить ветку main на 3 родителя назад.

<img width="154" height="339" alt="image" src="https://github.com/user-attachments/assets/deecf336-83f1-467e-b0db-232eacb2d8ef" />

### Решение.

1. Пропишем команду:
```
git branch -f main HEAD~3
```
Результат:

<img width="154" height="327" alt="image" src="https://github.com/user-attachments/assets/20580fd9-3ecc-474e-8696-5ca4f21ee32a" />

* Относительная ссылка дала нам возможность просто сослаться на C1, а branch forcing (-f) позволил быстро переместить указатель ветки на этот коммит.

### Пример.

Дано:

<img width="537" height="534" alt="image" src="https://github.com/user-attachments/assets/80538d9b-447b-4896-ae4a-2ad9760afc95" />

Передвинь HEAD, main и bugFix так, как показано на визуализации.

<img width="304" height="637" alt="image" src="https://github.com/user-attachments/assets/c2a36331-9ee9-4ef2-96d5-ad5ffa424c39" />

### Решение.

1. Пропишем команды:
```
git branch -f main C6
git branch -f bugFix HEAD~2
git checkout HEAD~1
```
Результат:

<img width="852" height="523" alt="image" src="https://github.com/user-attachments/assets/5fabdc46-e6c4-4796-a9b3-8f118b387d48" />

<br>

<br>

<br>

## <a id ="title7">Отмена изменений (reset, revert)</a>

* Есть много путей для отмены изменений в Git.

* ***На низком уровне*** = **добавление в коммит отдельных файлов и наборов строк**.

* ***На высоком*** = **как изменения реально отменяются**.

2 способа:
```
git reset
```
```
git revert
```

### git reset.

* **Отменяет изменения, перенося ссылку на ветку назад, на более старый коммит**.

* Это своего рода "переписывание истории".

* git reset перенесёт ветку назад, как будто некоторых коммитов вовсе и не было.

### Пример.

Посмотрим, как это работает.

<img width="131" height="332" alt="image" src="https://github.com/user-attachments/assets/f37c4e60-02d9-49e4-89fb-86e817fab253" />

### Решение.

1. Пропишем команду:
```
git reset HEAD~1
```
Результат:

<img width="127" height="333" alt="image" src="https://github.com/user-attachments/assets/75116e9d-6c9c-4491-afee-e752a091a4c6" />

* Git просто ***перенёс ссылку на main обратно на коммит C1***. Теперь наш локальный репозиторий в состоянии, как будто C2 никогда не существовал.

### git revert.

* Reset отлично работает **на локальных ветках**, **в локальных репозиториях**. Но этот метод переписывания истории не сработает на удалённых ветках, которые используют другие пользователи.

* Чтобы ***отменить изменения и поделиться отменёнными изменениями с остальными*** = git revert.

### Пример.

Посмотрим, как это работает.

<img width="131" height="330" alt="image" src="https://github.com/user-attachments/assets/d2bbf86f-bcd3-4d5e-9c56-6634739a519b" />

### Решение.

1. Пропишем команду:
```
git revert HEAD
```
Результат:

<img width="130" height="329" alt="image" src="https://github.com/user-attachments/assets/dbe8eff1-d356-42d1-ba12-a2d63916d251" />

* появился новый коммит. Дело в том, что ***новый коммит C2' просто содержит изменения, полностью противоположные тем, что сделаны в коммите C2***. После revert можно сделать push и поделиться изменениями с остальными.

### Пример.

Дано:

<img width="519" height="316" alt="image" src="https://github.com/user-attachments/assets/d884b7ae-776c-4e79-8888-ffd6100ce462" />

1. Отмени самый последний коммит на ветках local и pushed. Всего будет отменено два коммита (по одному на ветку).

2. Помни, что pushed - это remote ветка, а local - это локальная ветка.

3. Нужно получить визулизацию, как на картинке.

<img width="218" height="632" alt="image" src="https://github.com/user-attachments/assets/41feaec2-06d9-47a8-80d2-5dc560ff7289" />

### Решение.

1. Пропишем команды:
```
git reset local~1
git checkout pushed
git revert pushed
```
Результат:

<img width="769" height="403" alt="image" src="https://github.com/user-attachments/assets/97e7e88d-c2cb-48ef-b036-981479583a61" />

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

## <a id ="title10">Исправленные ошибка</a>

Вот ситуация, которая часто случается при разработке: мы пытаемся ***отследить ошибку, но она не очень очевидна***. 

Для того, чтобы достичь успеха на этом поприще, мы используем ***несколько команд для отладки и вывода***.

**Каждая отладочная команда (команды) вывода находится в своём коммите**. 

В итоге мы нашли ошибку, исправили её и порадовались!

Но проблема в том, что мы хотим ***добавить в main только исправление ошибки из ветки bugFix***. Если мы воспользуемся простым fast-forward, то в main попадут также отладочные команды. Должен быть другой способ...

### Пример.

Дано:

<img width="138" height="532" alt="image" src="https://github.com/user-attachments/assets/94435d46-4d47-4b15-bd62-1cd14fe35f37" />

1. Git копировать только один из коммитов.

2. Убедись, что в ветку main попал коммит, на который ссылается bugFix.

3. Нужно получить визулизацию, как на картинке.

<img width="214" height="602" alt="image" src="https://github.com/user-attachments/assets/f5e95439-48e1-4852-afa2-9c0926c4293f" />

### Решение.

1. Пропишем команды:
```
git rebase -i HEAD~3
git branch -f main HEAD (или bugFix или С4)
```
```
git checkout main
git cherry-pick C4 (или bugFix)
```
Результат:

<img width="773" height="527" alt="image" src="https://github.com/user-attachments/assets/b1a20a12-bb23-428f-9622-05deadd05090" />

<br>

<br>

<br>

## <a id ="title11">Внесение изменений в более ранний коммит</a>

### git rebase -i.

Есть некоторые изменения "newImage" и другие изменения "caption", которые связаны так, что находятся ***друг поверх друга в репозитории***.

Штука в том, что иногда нужно внести небольшие **изменения в более ранний коммит**. В таком случае надо немного поменять newImage, несмотря на то, что коммит уже в прошлом.

### Пример.

Дано:

<img width="142" height="409" alt="image" src="https://github.com/user-attachments/assets/5c80d2ab-31ce-4b8a-9bbb-60cfb88b86c9" />

1. ***Переставить коммит так, чтобы нужный находился наверху*** при помощи = **git rebase -i**.

2. ***Внести изменения*** при помощи = **git commit --amend** = позволяет добавить новые изменения в последний коммит.

3. ***Переставить всё обратно*** при помощи = **git rebase -i**.

4. Переместить main на изменённую часть дерева, чтобы закончить уровень.

5. Нужно получить визулизацию, как на картинке.

<img width="228" height="654" alt="image" src="https://github.com/user-attachments/assets/ec3ecaa7-b004-4c06-abdc-1fc23a4690ba" />

### Решение.

1. Пропишем команды:
```
git rebase -i HEAD~2 (переставляем С3 и С2 местами при интерактивном окне) (после выполенния ветка caption вместе с HEAD указывает на C2')
git commit --amend (получим коммит С2'')  (C2' и C2'' имеют одного родителя C3')
git rebase -i HEAD~2 (переставляем С3' и С2'' местами при интерактивном окне)
git branch -f main HEAD (перемещаем ветку main в HEAD)
```
Результат:

<img width="842" height="460" alt="image" src="https://github.com/user-attachments/assets/3d38fea1-a74f-4fee-96c8-fba9f8fbbfc8" />

<br>

### git cherry-pick.

До этого использовали rebase -i для перестановки коммитов. Как только нужный нам коммит оказывался в конце, мы могли спокойно изменить его при помощи --amend и переставить обратно.

Такой подход может спровоцировать конфликты. Посмотрим, как справиться с этим **cherry-pick**.

* **Cherry-pick** = ***поместит любой коммит сразу после HEAD*** (только если этот коммит не является предком HEAD).

### Пример.

<img width="235" height="363" alt="image" src="https://github.com/user-attachments/assets/c44b83c7-926f-4bc8-b2da-248e9e1ddcdc" />

### Решение.

1. Пропишем команду:
```
gir cherry-pick C2
```
Результат:

<img width="235" height="373" alt="image" src="https://github.com/user-attachments/assets/539ac6da-43ba-4a28-93e4-54219ac918be" />

### Пример.

Дано:

<img width="142" height="407" alt="image" src="https://github.com/user-attachments/assets/c9178432-f2d5-4ce8-b36c-9d7f9d3bcf2d" />

1. Та же самая задача. Нужно получить визулизацию, как на картинке.

<img width="230" height="640" alt="image" src="https://github.com/user-attachments/assets/8f7d327c-410e-41e6-85af-e6ef671e1b1d" />

### Решение.

1. Пропишем команды:
```
git checkout main
git cherry-pick C2
git branch -f main HEAD~1
git cherry-pick C2' C3
```
Результат:

<img width="810" height="436" alt="image" src="https://github.com/user-attachments/assets/b32044ba-cd4f-4d2a-a048-ab4949534f4e" />

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

<br>

<br>

<br>

## <a id ="title14">Rebase на нескольких ветках</a>

### Пример.

Дано:

<img width="763" height="438" alt="image" src="https://github.com/user-attachments/assets/a6fc0c77-b386-4488-ac9c-62e759a1f314" />

1. У нас тут куча веток! Было бы круто перенести все изменения из них в мастер.

2. Но начальство усложняет нашу задачу тем, что желает видеть все коммиты по порядку. Так что коммит С7' должен идти после коммита С6' и так далее.

3. Нужно получить визулизацию, как на картинке.

<img width="234" height="602" alt="image" src="https://github.com/user-attachments/assets/c7bc8ec1-9a35-45d0-9868-cb9f53607105" />

### Решение.

1. Пропишем команды:
```
git checkout bugFix
git rebase main
git checkout side
git rebase -i bugFix
git checkout another
git rebase -i side
git branch -f main HEAD
```
Результат:

<img width="867" height="892" alt="image" src="https://github.com/user-attachments/assets/dcf00923-cb3a-4601-9ca7-cdefa36c7068" />

<br>

<br>

<br>

## <a id ="title15">Определение родителей</a>

* ***Так же как тильда (~), каретка (^) принимает номер после себя***.

Но в отличие от количества коммитов, на которые нужно откатиться назад (как делает ~). 

* **Номер после ^** ***определяет, на какого из родителей мерджа надо перейти***. Учитывая, что мерджевый коммит имеет двух родителей, просто указать ^ нельзя.

* Git по умолчанию перейдёт на "первого" родителя коммита.

### Пример.

<img width="232" height="330" alt="image" src="https://github.com/user-attachments/assets/e281b805-edc4-4b1d-ab0f-97520df50622" />

### Решение.

1. Пропишем команду:
```
git checkout main^2
```
Результат:

<img width="236" height="328" alt="image" src="https://github.com/user-attachments/assets/3a13ef3c-82be-49f3-9447-f1e6a6e850bb" />

### Пример.

<img width="232" height="327" alt="image" src="https://github.com/user-attachments/assets/1c4f51e9-1938-4466-932e-98377ccd7a69" />

### Решение.

1. Пропишем команды:
```
git checkout HEAD~
git checkout HEAD^2
git checkout HEAD~2
```
```
git checkout HEAD~^2~2
```
Результат:

<img width="231" height="328" alt="image" src="https://github.com/user-attachments/assets/c8f62f35-cc02-41ab-85f0-43b0e422bc2b" />

### Пример.

Дано:

<img width="519" height="677" alt="image" src="https://github.com/user-attachments/assets/2290e9d0-23f5-4377-ae35-f0897a735232" />

1. Cоздай ветку в указанном месте.

2. Нужно получить визулизацию, как на картинке.

<img width="213" height="660" alt="image" src="https://github.com/user-attachments/assets/7c27139a-75f0-4ace-807f-9d17b54e2080" />

### Решение.

1. Пропишем команду:
```
git branch -f bugWork HEAD~^2^
```
Результат:

<img width="768" height="681" alt="image" src="https://github.com/user-attachments/assets/07e17ba0-adaf-4f51-8e04-1f63ea467b47" />

<br>

<br>

<br>

## <a id ="title16">Спутанные ветки</a>

### Пример.

Дано:

<img width="128" height="653" alt="image" src="https://github.com/user-attachments/assets/4cda0654-56f0-49a0-b249-f2a9366ec865" />

1. У нас тут по несколько коммитов в ветках one, two и three. Не важно почему, но нам надо видоизменить эти три ветки при помощи более поздних коммитов из ветки main.

2. Ветка one нуждается в изменении порядка и удалении C5. two требует полного перемешивания, а three хочет получить только один коммит.

3. Нужно получить визулизацию, как на картинке. 

<img width="273" height="657" alt="image" src="https://github.com/user-attachments/assets/3751045b-0321-4255-b36b-07c2fd81042f" />

### Решение.

1. Пропишем команды:
```
git checkout one
git cherry-pick C4 C3 C2
git checkout two
git cherry-pick C5 C4' C3' C2'
git branch -f three C2
```
Результат:

<img width="1020" height="681" alt="image" src="https://github.com/user-attachments/assets/f93f3e79-3912-4d8b-9317-420297063407" />

<br>

<br>

<br>

## <a id ="title17">Клонирование</a>

* Удалённые репозитории — копии репозитория, хранящиеся на другом компьютере. Можете связываться с этим компьютером через Интернет, что позволяет вам передавать коммиты туда и сюда.

Свойства:

* ***средство резервного копирования***. Локальные репозитории способны восстанавливать файлы, используя предыдущие состояния, но информация хранится локально. Потеряв все свои локальные данные, способны восстановить их при наличии копии своего репозитория на другом компьютере.

* ***процесс разработки более социальным***. Когда копия проекта размещена в другом месте, коллеги запросто могут внести свой вклад в ваш проект или забрать последние и актуальные изменения.

### git clone.

* **git clone в реальной жизни** - ***создаст локальную копию удалённого репозитория*** (например, с GitHub).

* В тренажёре - ***создаёт удалённый репозиторий на основе вашего локального репозитория***. На самом деле, это является полной противоположностью реальной команды.

### Пример.

<img width="128" height="189" alt="image" src="https://github.com/user-attachments/assets/5cea807c-b6c2-4f9d-94b2-d239a6f3db82" />

### Решение.

1. Пропишем команду:
```
git clone
```
Результат:

<img width="314" height="182" alt="image" src="https://github.com/user-attachments/assets/71a71bec-063f-4b22-9a7d-6858a94b61d4" />

<br>

<br>

<br>

## <a id ="title18">Удалённые ветки</a>

* В локальном репозитории по предыдущему примеру появилась новая ветка с именем **o/main** = ***удалённой веткой***.

Свойтва:

* ***Отражают состояние удалённых репозиториев*** (с того момента, как обращались к этим удалённым репозиториям в последний раз).

* ***Отслеживать разницу между вашими локальными наработками и тем, что было сделано другими участниками***.

* ***Извлечение их, отделяет*** = **detaching HEAD**. Git делает это потому, что не можете работать непосредственно в этих ветках; сперва вам необходимо сделать наработки где-либо, а уж затем делиться ими с удалёнными репозиториями (после чего удалённые ветки будут обновлены).

### Что такое "o/" в названии ветки?

* **o/** в названии ветки = обозначениe ***удалённых веток***.

Формате:
```
<удалённый репозиторий>/<имя ветки>
```
* Имя ветки **o/main**:

  * ***main** = ***имя ветки***.

  * **o** = ***имя удалённого репозитория***.

* ***В работе не как o, а как origin***.

### Пример.

1. Извлечём (check out) удалённую ветку и посмотрим что произойдёт.

<img width="314" height="180" alt="image" src="https://github.com/user-attachments/assets/cbf38397-ee78-4924-a7cc-6c26b655ce8a" />

### Решение.

1. Пропишем команды:
```
git checkout o/main
git commit
```
Результат:

<img width="315" height="314" alt="image" src="https://github.com/user-attachments/assets/af72ea7f-e4d8-4a30-841d-9defe1ad7688" />

* ***Отделил detached HEAD и не обновил o/main, когда мы добавили новый коммит***. Всё потому, что o/main обновится тогда и только тогда, когда обновится сам удалённый репозиторий.

### Пример.

Дано:

<img width="592" height="268" alt="image" src="https://github.com/user-attachments/assets/f7b86e30-2b0c-4295-b781-a52a4d4a548a" />

1. Выполните коммит единожды на main, а затем на o/main (предварительно переключившись на эту ветку). Это наглядно продемонстрирует поведение удалённых веток, а также покажет, как изменения влияют на состояние удалённых репозиториев.

2. Нужно получить визулизацию, как на картинке.

<img width="300" height="625" alt="image" src="https://github.com/user-attachments/assets/85badfd5-4b38-4691-9e53-160c38204c94" />

### Решение.

1. Пропишем команды:
```
git commit
git checkout o/main
git commit
```
Результат:

<img width="930" height="295" alt="image" src="https://github.com/user-attachments/assets/71c9bfae-16cd-48ba-99b0-88ea65174c16" />

<br>

<br>

<br>

## <a id ="title19">Извлечение данных из удалённого репозитория</a>

Работа с удалёнными git репозиториями сводится к передаче данных "в и из" других репозиториев. 

Отправляя коммиты туда-обратно, можем делиться любыми изменениями, которые отслеживает git (следовательно, делиться новыми файлами, свежими идеями, любовными письмами и т.д.).

### git fetch.

* ***Извлечение данных из удалённого репозитория*** = **git fetch**.

* ***Как только изменим представление удалённого репозитория, удалённые ветки обновятся соответствующим образом и отобразят это представление***.

### Пример.

Имеется удалённый репозиторий, который содержит в себе два коммита, отсутствующих в нашем локальном репозитории.

<img width="300" height="314" alt="image" src="https://github.com/user-attachments/assets/88614291-f792-4cfd-a7a7-1fdfa8b2214a" />

### Решение.

1. Пропишем команду:
```
git fetch
```
Результат:

<img width="305" height="316" alt="image" src="https://github.com/user-attachments/assets/4f0c6319-9e74-4bc1-bc60-af0170617f94" />

* Коммиты C2 и C3 были успешно скачаны в локальный репозиторий.

* Удалённая ветка o/main отобразила эти изменения соответствующим образом.

### Что делает fetch.

**git fetch** выполняет две операции:

1. ***Cвязывается с указанным удалённым репозиторием*** и ***забирает все те данные проекта, которых у вас ещё нет***, при этом...

2. Должны ***появиться ссылки на все ветки из этого удалённого репозитория*** (например, o/main).

Фактически, ***git fetch синхронизирует локальное представление удалённых репозиториев*** с тем, что является актуальным на текущий момент времени.

* **git fetch** 'общается' с удалёнными репозиториями посредством Интернета (через такие протоколы, как http:// или git://).

### Чего fetch не делает

* ***git fetch забирает данные в ваш локальный репозиторий***, но не сливает их с какими-либо вашими наработками и не модифицирует то, над чем вы работаете в данный момент.

Важно это помнить и понимать, потому что многие разработчики думают, что, запустив команду git fetch, они приведут всю свою локальную работу к такому же виду, как и на удалённом репозитории. Команда всего лишь скачивает все необходимые данные, но вам потребуется вручную слить эти данные с вашими, когда вы будете готовы.

* **git fetch** = процедура скачивания новые данные из удаленного репозитория, но не сливает их с вашими локальными файлами.

### Пример.

Дано:

<img width="761" height="521" alt="image" src="https://github.com/user-attachments/assets/cc18ce7b-a369-4a71-a8fa-fe4509e3d47a" />

1. Запустите git fetch и скачайте все коммиты!

2. Нужно получить визулизацию, как на картинке.

<img width="300" height="605" alt="image" src="https://github.com/user-attachments/assets/1a299729-bd53-49f3-98b9-bea9f9573311" />

### Решение.

1. Пропишем команду:
```
git fetch
```
Результат:

<img width="1140" height="525" alt="image" src="https://github.com/user-attachments/assets/c95d9416-d59b-4395-b183-71da1350c7e0" />

<br>

<br>

<br>

## <a id ="title20">git fetch и git merge = "git pull"</a>

git pull состоит из двух команд: 

* **git fetch** = ***загрузка изменений из удаленного репозитория***. Cкачивает новые данные из удаленного репозитория, но не сливает их с вашими локальными файлами.

* **git merge** = ***слияние загруженных изменений с локальной веткой***. Объединяет новые изменения из удаленной ветки с текущей локальной веткой.

* **Коммит слияния**: Если слияние происходит успешно, git автоматически создаст новый "коммит слияния" для фиксации этих изменений. Этот коммит будет иметь два родительских элемента: родительский коммит из вашей локальной ветки и коммит из ветки, которую вы скачали.

### Пример.

<img width="303" height="317" alt="image" src="https://github.com/user-attachments/assets/7c2ee2a6-a0e5-4819-b4ea-faa31f4948e1" />

### Решение.

1. Пропишем команды:
```
git fetch
git merge
```
```
git pull
```
Результат:

<img width="353" height="315" alt="image" src="https://github.com/user-attachments/assets/157439f7-c02f-4760-82a5-dd8467be42aa" />

* Cкачали C3 с помощью команды fetch и затем объединяем эти наработки с помощью git merge o/main.

* Ветка main отображает изменения с удалённого репозитория (в данном случае — с репозитория origin).

* git pull существенно уменьшает работу, если бы использовали git fetch и слияние (merging) скачанной ветки.

### Пример.

Дано:

<img width="595" height="265" alt="image" src="https://github.com/user-attachments/assets/75881f3f-39fe-4c96-9b34-2af9349d855d" />

1. Нужно получить визулизацию, как на картинке.

<img width="332" height="576" alt="image" src="https://github.com/user-attachments/assets/5432d9f2-5ead-4d8b-96e5-cff6133b9bad" />

### Решение.

1. Пропишем команду:
```
git pull
```
Результат:

<img width="1027" height="378" alt="image" src="https://github.com/user-attachments/assets/657c554a-285b-4d10-babf-0be6425b4976" />

<br>

<br>

<br>

## <a id ="title21">Коллективная работа</a>

Cкачивать наработки и изменения, которые были сделаны в удалённом репозитории.

Это означает, что нам следует "сделать вид", как будто знаем о том, что удалённый репозиторий, с которым работаем, был изменён одним из ваших коллег / друзей / единомышленников. Это может быть какая-то ветка, либо же какой-то конкретный коммит.

### git fakeTeamwork.

* Поведение команды ***fakeTeamwork*** по умолчанию заключается в том, чтобы просто ***"инициировать" коммит на main***.

### Пример.

<img width="301" height="175" alt="image" src="https://github.com/user-attachments/assets/d76ce4ba-7e38-4d50-aee5-782014f87aa0" />

### Решение.

1. Пропишем команду:
```
git fakeTeamwork
```
Результат:

<img width="298" height="314" alt="image" src="https://github.com/user-attachments/assets/17ff5b3d-0ebd-449e-872a-54e1036366e0" />

* Удалённый репозиторий был изменён при помощи добавления нового коммита.

### Пример.

<img width="300" height="197" alt="image" src="https://github.com/user-attachments/assets/60fe0e4f-88aa-4c06-9a1c-49d33a5a8989" />

### Решение.

1. Пропишем команду:
```
git fakeTeamwork foo 3
```
Результат:

<img width="301" height="311" alt="image" src="https://github.com/user-attachments/assets/d7eebe39-c462-4720-8529-cd6f3423b766" />

* Добавление трёх коммитов в ветку foo на удалённом репозитории.

### Пример.

Дано:

<img width="104" height="141" alt="image" src="https://github.com/user-attachments/assets/bb0c35b5-4f0b-4805-a797-fe8159a6f315" />

1. Склонируйте удалённый репозиторий (с помощью git clone), симулируйте любые изменения на этом удалённом репозитории, сделайте какие-нибудь коммиты и затем скачайте "чужие" изменения.

2. Нужно получить визулизацию, как на картинке.

<img width="333" height="602" alt="image" src="https://github.com/user-attachments/assets/3b1e29e9-c8c5-48ab-b883-545400845d74" />

### Решение.

1. Пропишем команды:
```
git clone
git fakeTeamwork main 2
git commit
git pull
```
Результат:

<img width="1028" height="483" alt="image" src="https://github.com/user-attachments/assets/40ae23e3-c4d7-4dc5-a4d7-2302fb18f69f" />

<br>

<br>

<br>

## <a id ="title22">Загрузка изменений в удалённый репозиторий</a>

Cкачали изменения с удалённого репозитория и включили их в локальные наработки. 

### Но как нам поделиться своими наработками и изменениями с другими участниками проекта?

Способ противоположным тому, которым пользовались ранее ***для скачивания наработок*** = **git pull**. Cпособ - использование команды **git push**.

* **git push** отвечает:

  * ***за загрузку ваших изменений в указанный удалённый репозиторий***.
  
  * ***включение локальных коммитов в состав удалённого репозитория***.

* **git push** = "публикацию" своей работы.

### Замечание.

Поведение команды git push без аргументов варьируется в зависимости от значения push.default, указанной в настройках git. Значение по умолчанию зависит от версии git, которую вы используете. Здесь используется значение = upstream.

### Пример.

1. У нас имеются изменения, которых нет в удалённом репозитории. Давайте же закачаем их туда!

<img width="300" height="310" alt="image" src="https://github.com/user-attachments/assets/9218c97d-74cf-4c89-9d2d-ce65280c9aff" />

### Решение.

1. Пропишем команду:
```
git push
```
Результат:

<img width="298" height="309" alt="image" src="https://github.com/user-attachments/assets/e82e5ad0-9331-405b-998d-3e9920a542c6" />

* Удалённый репозиторий получил новый коммит C2.

* Ветка main на удалённом репозитории теперь указывает на C2.

* Локальное отображение удалённого репозитория (o/main) изменилось соответственно. Всё синхронизировалось.

### Пример.

Дано:

<img width="590" height="150" alt="image" src="https://github.com/user-attachments/assets/4b830ea8-f493-47b3-b7b7-da30a48b89b2" />

1. Просто поделитесь своими двумя новыми коммитами с удалённым репозиторием

2. Нужно получить визулизацию, как на картинке.

<img width="288" height="573" alt="image" src="https://github.com/user-attachments/assets/cbb51e04-e7f0-4ca1-a7e2-953bc32e7a2c" />

### Решение.

1. Пропишем команды:
```
git commit
git commit
git push
```
Результат:

<img width="841" height="371" alt="image" src="https://github.com/user-attachments/assets/60da85ea-091f-4e6b-93c7-44bea0b38328" />

<br>

<br>

<br>

## <a id ="title23">Расхождение в истории</a>

* Как забирать = pull = чужие коммиты.

* Как закачивать = push = свои наработки и изменения.

***Нюансы возникают тогда, когда история репозитория расходится***.

1. Допустим, склонировали репозиторий в понедельник и начали разрабатывать какую-то новую и уникальную часть приложения. 

2. В пятницу вечером готовы опубликовать фичу. 

3. Но, о нет! Ваш коллега в течение недели написал кучу кода, который делает все наработки устарелыми. Код был также закоммичен и опубликован на удалённом репозитории, поэтому код базируется на устаревшей версии проекта и более не уместен.

   * В этом случае использование команды git push является сомнительным. 

   * Как поведёт себя команда git push, если вы её выполните? 

   * Может быть, она изменит удалённый репозиторий и вернёт всё к тому состоянию, которое было в понедельник? 

   * Может, команда попробует добавить ваш код, не удаляя при этом новый? Или же она проигнорирует ваши изменения, так как они уже устарели?

4. По причине того, что в данной ситуации (когда история расходится) слишком много двусмысленностей и неопределённостей, git не даст закачать (push) ваши изменения.

   * Принуждать ***включить в состав своей работы все те последние наработки и изменения, которые находятся на удалённом репозитории***.
  
### Пример.

<img width="298" height="311" alt="image" src="https://github.com/user-attachments/assets/96124b2a-a849-46e6-8c80-a59fe4025124" />

### Решение.

1. Пропишем команду:
```
git push
```
Результат:

<img width="298" height="311" alt="image" src="https://github.com/user-attachments/assets/96124b2a-a849-46e6-8c80-a59fe4025124" />

* Ничего не произошло.

* Всё потому, что команда git push не выполнилась успешно.

* Дело в том, что ваш последний коммит C3 основан на удалённом коммите C1. В свою очередь, удалённый репозиторий уже изменился под воздействием C2. Вот почему git отклонил ваш push.

### Вариант 1.

* ***Перебазировать свою работу на самую последнюю версию удалённой ветки***.

Существует множество способов сделать это, но наиболее простой способ 'сдвинуть' свои наработки - через перебазировку или rebasing.

### Пример.

<img width="298" height="311" alt="image" src="https://github.com/user-attachments/assets/96124b2a-a849-46e6-8c80-a59fe4025124" />

### Решение.

1. Пропишем команды:
```
git fetch
git rebase o/main
git push
```
Результат:

<img width="387" height="316" alt="image" src="https://github.com/user-attachments/assets/12c973d0-8fc8-448b-b38e-9e198eaeb0b0" />

* Обновили локальный образ удалённого репозитория средствами git fetch.

* Перебазировали наработки, чтобы отражали все изменения с удалённого репозитория.

* Опубликовали их с помощью git push.

### Вариант 2.

* **git merge** ***не передвигает ваши наработки*** = ***создаёт новый коммит, в котором Ваши и удалённые изменения объединены***.

* Такой способ помогает указать git на то, что ***собираетесь включить в состав ваших наработок все изменения с удалённого репозитория*** = ***ваш коммит отразится на всех коммитах удалённой ветки***, поскольку удалённая ветка является предком вашей собственной локальной ветки.

### Пример.

Если мы объединим (merge) вместо перебазирования (rebase)..

<img width="300" height="311" alt="image" src="https://github.com/user-attachments/assets/9abfb263-18a3-4287-b0d7-c32def4ffb35" />

### Решение.

1. Пропишем команды:
```
git fetch
git merge o/main
git push
```
Результат:

<img width="321" height="347" alt="image" src="https://github.com/user-attachments/assets/3dffae11-baf9-4c73-9f85-f4f82806a450" />

* Обновили локальное представление удалённого репозитория с помощью git fetch.

* Объединили ваши новые наработки с нашими наработками (чтобы отразить изменения в удалённом репозитории).

* Затем опубликовали их с помощью git push.

### Вариант 3.

* **git pull --rebase** = ***аналог для совместно вызванных fetch и rebase***.

### Пример.

<img width="297" height="311" alt="image" src="https://github.com/user-attachments/assets/3c29ce53-e10d-45b1-9e8c-9292f02820b0" />

### Решение.

1. Пропишем команды:
```
git pull --rebase
git push
```
Результат:

<img width="385" height="320" alt="image" src="https://github.com/user-attachments/assets/1907fb2c-50f5-4259-b2fd-919f46fafb2c" />

* Тот же результат, как и ранее, но намного короче вызов команд.

### Вариант 4.

### Пример.

<img width="300" height="309" alt="image" src="https://github.com/user-attachments/assets/72ef9acf-80f0-4c50-8771-a6b56d3c7590" />

### Решение.

1. Пропишем команды:
```
git pull
git push
```
Результат:

<img width="317" height="343" alt="image" src="https://github.com/user-attachments/assets/e50679c6-04b8-431e-935f-35211c3bc820" />

* И снова - результат такой же, как и ранее.

### Пример.

Дано:

<img width="119" height="156" alt="image" src="https://github.com/user-attachments/assets/60ed6282-91b6-4d7e-a68f-54dfdc8e82b8" />

1. Рабочий процесс получения изменений (fetching), перебазирования/объединения (rebase/merging) и публикации изменений (pushing):

   * Склонируйте репозиторий.

   * Сфабрикуйте командную работу (1 коммит).

   * Сделайте свой собственный коммит (1 коммит).

   * Опубликуйте свои наработки посредством перебазировки (rebasing).

2. Нужно получить визулизацию, как на картинке.

### Решение.

1. Пропишем команды:
```
git clone
git fakeTeamwork main 1
git commit
git pull --rebase
git push
```
Результат:

<img width="1173" height="377" alt="image" src="https://github.com/user-attachments/assets/d0e19f20-c9ed-46c0-8418-9430bd2b7f4a" />

<br>

<br>

<br>

## <a id ="title24">Заблокированная ветвь main</a>

### Remote Rejected!

Когда работаете в составе большой команды разработчиков над проектом, то, вероятнее всего, ветвь main будет заблокирована. 

Для внесения изменений в неё в git существует ***понятие запроса на слияние Pull Request***. В такой ситуации если закоммитите свои наработки непосредственно в main ветвь, а после выполните git push, то будет сгенерировано сообщение об ошибке:

! [remote rejected] main -> main (TF402455: Pushes to this branch are not permitted; you must use a pull request to update this branch.)
! [удалённо отклонено] main -> main (TF402455: Изменение этой ветви запрещены; вы можете использовать pull request для обновления этой ветви.)

### Почему произошло отклонение моих изменений?

Удалённый репозиторий отклонил загруженные коммиты непосредственно в main ветку потому, что ***на main настроена политика, которая требует использование Pull request вместо обычного git push***:

* Политика подразумевает ***процесс создания новой ветви разработки***, ***внесение в неё всех необходимых коммитов***, ***загрузка изменений в удалённый репозиторий и открытие нового Pull request***.

### Пример.

Дано:

<img width="588" height="269" alt="image" src="https://github.com/user-attachments/assets/8fe5cec0-6cfa-455f-ae51-876697c02ebe" />

1. Создайте ещё одну ветвь под названием feature.

2. Отправьте изменения на удалённый репозиторий.

3. Не забудьте вернуть локальную main ветвь в исходное состояние (чтобы она была синхронизирована с удалённой). В противном случае у вас могут возникнуть проблемы при следующем выполнении git pull.

4. Нужно получить визулизацию, как на картинке.

<img width="302" height="575" alt="image" src="https://github.com/user-attachments/assets/ccd34ed7-bf00-45c3-a6ad-119229578b10" />

### Решение.

1. Пропишем команды:
```
git branch -f main o/main
git checkout -b feature C2
git push 
```
Результат:

<img width="853" height="262" alt="image" src="https://github.com/user-attachments/assets/ee3d9383-7f5a-4784-aed0-7caa9c88f39b" />

<br>

<br>

<br>

## <a id ="title25">Push мастер</a>

### Слияние фича-бранчей (веток)

### Workflow

Среди разработчиков, вовлечённых в большой проект, довольно распространённ приём — ***выполнять всю свою работу в так называемых фича-бранчах (вне main)***. А затем, как только работа выполнена, разработчик ***интегрирует всё, что было им сделано***.

* Ряд разработчиков делают ***push и pull лишь на локальную ветку main*** = таким образом ***ветка main всегда синхронизирована с тем, что находится на удалённом репозитории (o/main)***.

Для этого рабочего процесса совместили две вещи:

   * ***Интеграция фича-бранчей в main***.

   * ***Закачку (push) и скачку (pull) с удалённого репозитория***.

### Пример.

Быстренько вспомним, как нам обновить main и закачать выполненную работу.

<img width="297" height="314" alt="image" src="https://github.com/user-attachments/assets/bc09eb06-b77b-424b-ba96-93ad963339ae" />

### Решение.

1. Пропишем команды:
```
git pull --rebase
git push 
```
Результат:

<img width="380" height="313" alt="image" src="https://github.com/user-attachments/assets/a2e792a6-19b6-4113-a1eb-8ca9753c8fca" />

* Перебазировали нашу работу на новенький коммит, пришедший с удалённого репозитория.

* Закачали свои наработки в удалённый репозиторий.

### Пример.

Дано:

<img width="752" height="516" alt="image" src="https://github.com/user-attachments/assets/f933c53f-23cc-4d49-9338-965604cfd37d" />

1. Есть три фича-бранчи (фича-ветки) - side1 side2 и side3.

2. Нам необходимо закачать каждую из них по очереди на удалённый репозиторий.

3. При этом удалённый репозиторий хранит в себе какие-то наработки, которые также следует скачать к себе.

4. Нужно получить визулизацию, как на картинке.

<img width="358" height="564" alt="image" src="https://github.com/user-attachments/assets/f0643687-6f6c-4c8e-8296-ecc583531ba4" />

### Решение.

1. Пропишем команды:
```
git fetch (main останется на месте, если и использовали pull, то сметилась бы вместе с o/main)
git rebase o/main side1 (side1, указывающая на коммит С2 = перебазирется на ветку o/main и добавит копию С2 к этому коммиту, side1 укажет на С2')
git rebase side1 side2
git rebase side2 side3
git rebase side3 main
git push
```
Результат:

<img width="1175" height="817" alt="image" src="https://github.com/user-attachments/assets/82a649af-e3cd-42bb-ad22-1242f281e26e" />

<br>

<br>

<br>

## <a id ="title26">Cлияение с удалённым репозиторием</a>

* Чтобы закачать (push) новые изменения в удалённый репозиторий, всё, что вам нужно сделать = это ***смешать последние изменения из удалённого репозитория***. 

Можем выполнить rebase или merge на удалённом репозитории (например, o/main).

За:

* Rebasing делает дерево коммитов более чистым и читабельным, потому что всё представляется единой прямой линией.

Против:

* Метод rebasing явно изменяет историю коммитов в дереве. Пример:

* Коммит C1 может быть перебазирован после C3. Соответственно, в дереве работа над C1' будет отображаться как идущая после C3, хотя на самом деле она была выполнена раньше.

Некоторые разработчики любят сохранять историю и предпочитают слияние (merging). Другие предпочитают иметь чистое дерево коммитов, и пользуются перебазировкой (rebasing). Всё зависит от ваших предпочтений и вкусов.

### Пример.

Дано:

<img width="751" height="514" alt="image" src="https://github.com/user-attachments/assets/b675dca8-8199-47b7-b4e9-37d102a6df6c" />

1. Решите предыдущие задачи, но с помощью слияния (merging). Может быть, получится слегка неказисто, однако такое упражнение хорошо отразит суть различий.

2. Нужно получить визулизацию, как на картинке.

<img width="366" height="546" alt="image" src="https://github.com/user-attachments/assets/375be867-bcbc-4567-be79-c558e6a7ff88" />

### Решение.

1. Пропишем команды:
```
git checkout main
git pull
git merge side1
git merge side2
git merge side3
git push
```
Результат:

<img width="1306" height="641" alt="image" src="https://github.com/user-attachments/assets/bf977089-0e3d-468c-b357-87ea19cc0f99" />


