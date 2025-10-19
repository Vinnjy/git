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

### Deatching HEAD.

* Отделение HEAD = присвоение не ветке, а конкретному коммиту.

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

1. Пропишем команды:
```
git cherry pick C2 C4
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

1. Пропишем команды:
```
git cherry pick C3 C4 C7
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

1. Пропишем команды:
```
git reabse -i HEAD~4
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

1. Пропишем команды:
```
git reabse -i HEAD~4
```
Результат:

<img width="893" height="524" alt="image" src="https://github.com/user-attachments/assets/e52f4cd9-07b5-451e-a558-1d72d008b37a" />

2. Удаляем С2 через фиолетовую кнопку, переставляем С5 и С4 и нажимаем "Подтвержить".

<img width="890" height="534" alt="image" src="https://github.com/user-attachments/assets/a635ea21-6709-4a97-a460-cea3f3f99fb8" />

<img width="856" height="648" alt="image" src="https://github.com/user-attachments/assets/75e9977a-29a3-416c-aa40-e53790179035" />

<br>

<br>

<br>


## <a id ="title10"></a>





