# Команды

### Основы:

  * ### [1.1. Коммиты = git commit](#title0)

  * ### [1.2. Ветвление = git branch или git checkout -b](#title1)

  * ### [1.3. Ветки и слияние = git merge](#title2)

  * ### [1.4. Ветки и слияние-копией = git rebase](#title3)

  * ### [2.1. HEAD = git checkout (коммит или ветка)](#title4)
  
  * ### [2.2. Относительные ссылки (^, ~) = git checkout (ветка или HEAD)^](#title5)

  * ### [2.3. Перемещение ветки = git branch -f](#title6)
  
  * ### [2.4. Отмена изменений = git reset или git revert](#title7)

  * ### [3.1. Перемещение изменений = git cherry pick](#title8)

  * ### [3.2. Перемещение изменений (интерактивный rebase) = git rebase -i](#title9)

## <a id ="title0">Коммиты</a>

* Коммит в git репозитории хранит **снимок всех файлов в директории** = **огромная копия**, только лучше.

* Git пытается быть лёгким и быстрым насколько это только возможно, так что он не просто слепо копирует всю директорию каждый раз, а ужимает (когда это возможно) коммит **в набор изменений** или «дельту» = **между текущей версией и предыдущей**.

* Git хранит **всю историю о том, когда какой коммит был сделан**. Вот почему большинство коммитов имеют предков - мы указываем на предков стрелками при визуализации. Поддержка истории коммитов более чем важна для всех, кто работает над проектом.

### Пример.

1. Визуализация небольшого git репозитория.

2. Сейчас в нём два коммита: первый, исходный коммит С0 и один коммит С1 после него, содержащий изменения.

<img width="425" height="397" alt="image" src="https://github.com/user-attachments/assets/0b302147-991c-4c2b-b4b6-b57dc8928c2c" />

### Решение.

1. Пропишем команду:
```
git commit
```
Результат:

<img width="422" height="394" alt="image" src="https://github.com/user-attachments/assets/d2937647-3d52-4a29-af8c-46ca2d2f1e72" />

* Только что внесли изменения в репозиторий и сохранили их как коммит. У коммита, который мы только что сделали, есть родитель, С1, который указывает на предыдущий коммит.

### Пример.

Дано:

<img width="225" height="173" alt="image" src="https://github.com/user-attachments/assets/877769a8-bda2-41c5-98da-012702cae5f0" />

1. Сделайте 2 коммита, чтобы получить визулизацию, как на картинке.

<img width="375" height="699" alt="image" src="https://github.com/user-attachments/assets/de0ef457-d0f3-4008-835c-be0a41813b8f" />

### Решение.

1. Пропишем в командной строке:
```
git commit
git commit
```
Результат:

<img width="311" height="462" alt="image" src="https://github.com/user-attachments/assets/102cc230-28e2-4caa-8d73-1d6917160a0e" />

<br>

<br>

<br>

## <a id ="title1">Ветвление</a>

* Ветки в Git, как и коммиты, невероятно легковесны. Это просто **ссылки на определённый коммит** — ничего более. Вот почему многие фанаты Git повторяют мантру: "делай ветки сразу, делай ветки часто".

* Cоздание множества веток никак не отражается на памяти или жестком диске, удобнее и проще разбивать свою работу на много маленьких веток, чем хранить все изменения в одной огромной ветке.

* Cозданная ветка хранит изменения текущего коммита и всех его родителей.

### Пример.

Создадим новую ветку с именем newImage.

<img width="419" height="393" alt="image" src="https://github.com/user-attachments/assets/b0c2972d-1486-48c0-a2f0-84e3ba2d417a" />

### Решение.

1. Пропишем команду (создание ветки):
```
git branch newImage
```
Результат:

<img width="424" height="391" alt="image" src="https://github.com/user-attachments/assets/8e0afee8-d44f-4324-8628-5da64ac2df26" />

* Ветка newImage указывает на коммит С1.

2. Теперь сделаем коммит. Пропишем команду:
```
git commit
```
Результат:

<img width="415" height="391" alt="image" src="https://github.com/user-attachments/assets/f241f41c-a78d-4b89-b30d-8a5cc16ee8e0" />

* Ветка main сдвинулась, тогда как ветка newImage - нет. Всё из-за того, что мы не переключились на новую ветку, а остались в старой, о чём говорит звёздочка около ветки main.

3. Чтобы сделать коммит для ветки newImage, нужно **переключиься на ветку**, а затем сделать коммит. Вернёмся к пукнту 2:

<img width="424" height="391" alt="image" src="https://github.com/user-attachments/assets/8e0afee8-d44f-4324-8628-5da64ac2df26" />

4. Пропишем 2 команды:
```
git checkout newImage
git commit
```
Результат:

<img width="415" height="391" alt="image" src="https://github.com/user-attachments/assets/4c0a535b-3d49-4c5b-93ef-d326d5615bf5" />

### Пример.

Дано:

<img width="169" height="170" alt="image" src="https://github.com/user-attachments/assets/eac38e5f-e298-4e90-8a45-559f0b8dbd87" />

1. Создай ветку с именем bugFix и переключись на неё.

2. Нужно получить визулизацию, как на картинке.

<img width="366" height="370" alt="image" src="https://github.com/user-attachments/assets/019585f6-14ef-41aa-806a-d827601e81bc" />

### Решение.

1. Пропишем команду:
```
git checkout -b bugFix
```
* Создаст ветку и переключиться на неё.

Результат:

<img width="244" height="181" alt="image" src="https://github.com/user-attachments/assets/c8364015-593e-44fe-a09a-e0d5f9002032" />

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

<img width="420" height="393" alt="image" src="https://github.com/user-attachments/assets/202d34b6-d413-4d32-af0f-ad2a7251264f" />

### Решение.

1. Пропишем комвнду (слияние bugFix в main):
```
git merge bugFix
```
Результат:

<img width="424" height="393" alt="image" src="https://github.com/user-attachments/assets/5516d33e-9e97-4ec6-8f85-c22e1b60ad4f" />

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

<img width="423" height="392" alt="image" src="https://github.com/user-attachments/assets/93006874-f461-4c69-af94-2d6694f6de65" />

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

<img width="394" height="711" alt="image" src="https://github.com/user-attachments/assets/48c634b3-7dc7-4d30-b080-224bad274619" />

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

<img width="962" height="467" alt="image" src="https://github.com/user-attachments/assets/e9b4a701-0946-4841-a2ed-a1c91a246fd7" />

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

<img width="415" height="393" alt="image" src="https://github.com/user-attachments/assets/711d373f-3b31-4244-9936-9785f7073195" />

### Решение.

1. Пропишем командцу:
```
git rebase main
```
Результат:

<img width="416" height="392" alt="image" src="https://github.com/user-attachments/assets/79d5033b-d59d-4ca7-bb9d-8800eb3f18f6" />

* изменения из bugFix находятся в конце ветки main и являют собой линейную последовательность коммитов.

* С3' - это его "копия" в ветке main.

+ **Ветка main не обновлена до последних изменений**

2. Пропишем команду:
```
git checkout main
```
Результат:

<img width="422" height="389" alt="image" src="https://github.com/user-attachments/assets/8dfe3abd-dd38-4783-8972-f24b6567ba83" />

3. Пропишем команду:
```
git rebase bugFix
```
Результат:

<img width="413" height="389" alt="image" src="https://github.com/user-attachments/assets/073c697b-b47e-44ef-ac59-d788250a3dbb" />

* Так как ветка main был предком bugFix, git просто сдвинул ссылку на main вперёд.

### Пример.

Дано:

<img width="200" height="181" alt="image" src="https://github.com/user-attachments/assets/70ae9e87-1a15-41aa-b9cb-0e6422e2502a" />

1. Переключись на ветку bugFix.

2. Сделай коммит.

3. Вернись на main и сделай коммит ещё раз.

4. Переключись на bugFix и сделай rebase на main.

5. Нужно получить визулизацию, как на картинке.

<img width="368" height="696" alt="image" src="https://github.com/user-attachments/assets/f89d1557-9daa-4112-aa1c-ecb241be4401" />

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

<img width="1019" height="418" alt="image" src="https://github.com/user-attachments/assets/f2db3c4a-71bd-4255-9c46-1ff2eebe1d6f" />

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

<img width="422" height="393" alt="image" src="https://github.com/user-attachments/assets/13437b5b-2d82-445c-808b-30d9b9ceb225" />

### Решение.

1. Пропишем команды:
```
git checkout C1
git checkout main
git commit
git checkout C2
```

ПОСЛЕ:

<img width="422" height="393" alt="image" src="https://github.com/user-attachments/assets/671d1ecd-5c03-42be-af83-eb4c048ae584" />

* HEAD скрывался за ветке main.

### Deatching HEAD.

* Отделение HEAD = присвоение не ветке, а конкретному коммиту.

### Пример.

ДО:

* HEAD -> main -> C1.

<img width="413" height="390" alt="image" src="https://github.com/user-attachments/assets/fa4d0066-f168-4672-a83e-9e5aef80198f" />

### Решение.

1. Пропишем команду:
```
git checkout C1
```
Результат:

<img width="418" height="393" alt="image" src="https://github.com/user-attachments/assets/236fbbe5-7f55-4d61-ba85-1a8caaa011fd" />

ПОСЛЕ:

* HEAD -> C1.

### Пример.

Дано:

<img width="604" height="477" alt="image" src="https://github.com/user-attachments/assets/d95569dc-bf51-4e5c-9307-a3b681df716a" />

1. Отделим HEAD от ветки bugFix и присвоим его последнему коммиту в этой же ветке.

2. Укажи коммит при помощи его идентификатора (hash). Hash для каждого коммита указан в кружке на схеме.

3. Нужно получить визулизацию, как на картинке.

<img width="391" height="712" alt="image" src="https://github.com/user-attachments/assets/89166ebf-1330-486b-a2e5-e7208075b140" />

### Решение.

1. Пропишем команду:
```
git checkout C4
```
Результат:

<img width="960" height="461" alt="image" src="https://github.com/user-attachments/assets/6ac6f4a3-69a1-422f-b7f6-cad0a6c00d55" />

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

<img width="413" height="388" alt="image" src="https://github.com/user-attachments/assets/1b35cae2-0f07-4219-94da-a48da63d450b" />

### Решение.

1. Пропишем команду:
```
git checkout main^
```
Результат:

<img width="413" height="392" alt="image" src="https://github.com/user-attachments/assets/22084f27-550e-4f21-82b4-ddf69b64f981" />

### Вместо ветки, как относительная ссылка, можно использовать HEAD.

### Пример.

1. Пройдёмся несколько раз по дереву коммитов.

<img width="413" height="394" alt="image" src="https://github.com/user-attachments/assets/003ea055-8e83-4113-9bc5-2a7a1c9f7d76" />

### Решение.

1. Пропишем команды:
```
git checkout C3
git checkout HEAD^
git checkout HEAD^
git checkout HEAD^
```
Результат:

<img width="419" height="396" alt="image" src="https://github.com/user-attachments/assets/9bd897a0-a8cc-40d0-a3a9-b06e93f8270e" />

### Пример.

Дано:

<img width="609" height="474" alt="image" src="https://github.com/user-attachments/assets/5c5be9f5-3236-412f-8db2-0814e6a2ddda" />

1. Переместись на первого родителя ветки bugFix. Это отделит HEAD от ветки.

2. Нужно получить визулизацию, как на картинке.

<img width="390" height="711" alt="image" src="https://github.com/user-attachments/assets/5c516907-83d0-45c6-bd5f-ce0ff118ec02" />

### Решение.

1. Пропишите команду:
```
git checkout HEAD^
```
Результат:

<img width="880" height="469" alt="image" src="https://github.com/user-attachments/assets/d918bf9e-c197-4449-8c46-a48fce30cd50" />

### Пример.

Переместиться на 4 коммита назад.

<img width="411" height="390" alt="image" src="https://github.com/user-attachments/assets/47fc2cb0-6235-47e7-9b34-85a21f48592a" />

### Решение.

1. Пропишите команды:
```
git checkout HEAD~4
```
Результат:

<img width="420" height="396" alt="image" src="https://github.com/user-attachments/assets/91243475-63d6-414e-9d9c-18b1001a2113" />

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

<img width="418" height="390" alt="image" src="https://github.com/user-attachments/assets/efa82b5a-6edb-40a7-a330-56afe5113399" />

### Решение.

1. Пропишем команду:
```
git branch -f main HEAD~3
```
Результат:

<img width="415" height="388" alt="image" src="https://github.com/user-attachments/assets/a96f99b9-d4f9-41eb-9a98-b14c9c2d5bba" />

* Относительная ссылка дала нам возможность просто сослаться на C1, а branch forcing (-f) позволил быстро переместить указатель ветки на этот коммит.

### Пример.

Дано:

<img width="655" height="580" alt="image" src="https://github.com/user-attachments/assets/962471c9-ab74-4630-b407-de459c8255dc" />

Передвинь HEAD, main и bugFix так, как показано на визуализации.

<img width="381" height="711" alt="image" src="https://github.com/user-attachments/assets/ced03939-1e5e-451e-bc65-c14c669b8887" />

### Решение.

1. Пропишем команды:
```
git braanch -f main C6
git branch -f bugFix HEAD~2
git checkout HEAD~1
```
Результат:

<img width="906" height="550" alt="image" src="https://github.com/user-attachments/assets/01c4a745-9f76-4a1a-b0fd-3f9d1bd30b0c" />

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

<img width="411" height="391" alt="image" src="https://github.com/user-attachments/assets/2a946cfe-b773-4b15-99de-7ae41c96b502" />

### Решение.

1. Пропишем команду:
```
git reset HEAD~1
```
Результат:

<img width="418" height="390" alt="image" src="https://github.com/user-attachments/assets/6b3c4354-1437-4983-b020-615c8e799bd0" />

* Git просто ***перенёс ссылку на main обратно на коммит C1***. Теперь наш локальный репозиторий в состоянии, как будто C2 никогда не существовал.

### git revert.

* Reset отлично работает **на локальных ветках**, **в локальных репозиториях**. Но этот метод переписывания истории не сработает на удалённых ветках, которые используют другие пользователи.

* Чтобы ***отменить изменения и поделиться отменёнными изменениями с остальными*** = git revert.

### Пример.

Посмотрим, как это работает.

<img width="418" height="393" alt="image" src="https://github.com/user-attachments/assets/81e01aff-4d4c-44ec-8568-298e0fe26f4c" />

### Решение.

1. Пропишем команду:
```
git revert HEAD
```
Результат:

<img width="416" height="392" alt="image" src="https://github.com/user-attachments/assets/b1e6515c-c814-4839-8763-28e227be8eb7" />

* появился новый коммит. Дело в том, что ***новый коммит C2' просто содержит изменения, полностью противоположные тем, что сделаны в коммите C2***. После revert можно сделать push и поделиться изменениями с остальными.

### Пример.

Дано:

<img width="609" height="339" alt="image" src="https://github.com/user-attachments/assets/93fda058-6ff1-4656-b259-86c6d4a272f1" />

1. Отмени самый последний коммит на ветках local и pushed. Всего будет отменено два коммита (по одному на ветку).

2. Помни, что pushed - это remote ветка, а local - это локальная ветка.

3. Нужно получить визулизацию, как на картинке.

<img width="387" height="702" alt="image" src="https://github.com/user-attachments/assets/7c3361fd-296b-42a8-82a1-dfb92262c885" />

### Решение.

1. Пропишем команды:
```
git reset local~1
git checkout pushed
git revert pushed
```
Результат:

<img width="837" height="435" alt="image" src="https://github.com/user-attachments/assets/10efb6a2-9f95-4d97-b025-2c9ef1c64c57" />

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

<img width="419" height="394" alt="image" src="https://github.com/user-attachments/assets/2712dec9-f759-4103-b67a-f1d126520ebd" />

### Решение.

1. Пропишем команды:
```
git cherry pick C2 C4
```
Результат:

<img width="426" height="394" alt="image" src="https://github.com/user-attachments/assets/359b6267-b28a-4bb1-a216-07f0b554b64c" />

* Копии С2 и С4 теперь в ветке, где был HEAD.

### Пример.

Дано:

<img width="739" height="459" alt="image" src="https://github.com/user-attachments/assets/7e42691a-f595-4027-ab68-805c7bc76a6f" />

1. Cкопируй изменения из этих трёх веток в мастер. Чтобы понять, какие коммиты копировать, посмотри на визуализацию уровня.

<img width="393" height="685" alt="image" src="https://github.com/user-attachments/assets/30631e76-b048-4b80-85a8-145e0ac1488d" />

### Решение.

1. Пропишем команды:
```
git cherry pick C3 C4 C7
```
Результат:

<img width="1273" height="588" alt="image" src="https://github.com/user-attachments/assets/276bfd8a-7823-4d27-865c-667dd99f3dc3" />

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

<img width="421" height="398" alt="image" src="https://github.com/user-attachments/assets/02d866ac-d8c2-4135-ba50-8cc057b9e008" />

### Решение.

1. Пропишем команды:
```
git reabse -i HEAD~4
```
Результат:

<img width="898" height="535" alt="image" src="https://github.com/user-attachments/assets/d5b219e3-f5b6-407d-ad51-0fe20f100330" />

<img width="418" height="392" alt="image" src="https://github.com/user-attachments/assets/42465ad9-c18c-4fc4-b828-c7d9c69f712a" />

* Скопировали коммиты, как сами и указали.

### Пример.

Дано:

<img width="203" height="655" alt="image" src="https://github.com/user-attachments/assets/6e0e1192-2d97-47a4-8aa8-961cb8a3843c" />

1. Переставь коммиты при помощи интерактивного rebase в таком порядке, как указано на визуализации.

<img width="394" height="678" alt="image" src="https://github.com/user-attachments/assets/20c1cff4-3b76-448d-9cdf-44fce14b0ff5" />

1. Пропишем команды:
```
git reabse -i HEAD~4
```
Результат:

<img width="893" height="524" alt="image" src="https://github.com/user-attachments/assets/e52f4cd9-07b5-451e-a558-1d72d008b37a" />

2. Удаляем С2 через фиолетовую кнопку, переставляем С5 и С4 и нажимаем "Подтвержить".

<img width="890" height="534" alt="image" src="https://github.com/user-attachments/assets/a635ea21-6709-4a97-a460-cea3f3f99fb8" />

<img width="947" height="670" alt="image" src="https://github.com/user-attachments/assets/b1fc55bf-9b1a-4b30-be9b-e3f9f4b436c3" />


<br>

<br>

<br>


## <a id ="title10"></a>





