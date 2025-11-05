# Продвинутое использование

  * ### [Push мастер](#title25)

  * ### [Слияние с удаённым репозиторием](#title26)

  * ### [Слежка за удалённым репозиторием](#title27)

  * ### [Аргументы для Push](#title28)

  * ### [Аргументы для Fetch](#title29)

  * ### [Не указываем источник](#title30)

  * ### [Аргументы для Pull](#title31)

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

<br>

<br>

<br>

## <a id ="title27">Cлежка за удалённым репозиторием</a>

### Удалённые-отслеживаемые ветки

* git знает, что ветка main соответствует o/main. Ветки имеют схожие имена и связь между локальной и удалённой ветками main выглядит вполне логично, однако, связь наглядно продемонстрирована в двух сценариях:

1. Во время операции pull коммиты скачиваются в ветку o/main и затем соединяются в ветку main. Подразумеваемая цель слияния определяется исходя из этой связи.

2. Во время операции push наработки из ветки main закачиваются на удалённую ветку main (которая в локальном представлении выглядит как o/main). Пункт назначения операции push определяется исходя из связи между main и o/main.


Связь между main и o/main объясняется не иначе как ***свойство "удалённое отслеживание" веток***:

   * Ветка main настроена так, чтобы следить за o/main -- это подразумевает наличие источника для merge и пункта назначения для push в контексте ветки main. Когда вы клонируете репозиторий, это слежение включается автоматически.

   * В процессе клонирования git локально создаёт удалённые ветки для каждой ветки с удалённого репозитория (такие как o/main).
   
   * Затем git создаёт локальные ветки, которые отслеживают текущую, активную ветку на удалённом репозитории. В большинстве случаев - это main.

К тому моменту как git clone завершит своё выполнение = будет лишь одна локальная ветка, но можете увидеть все удалённые ветки.

Именно это объясняет, почему сразу после клонирования вы видите в консоли надпись:
```
local branch "main" set to track remote branch "o/main" (локальная ветка "main" теперь следит за удалённой веткой "o/main")
```

### Можно сделать самостоятельно

### Cпособ 1 = git checkout -b векта o/main

Можете сказать любой из веток, чтобы отслеживала o/main, и если так сделать, ветка будет иметь такой же пункт назначения для push и merge как и локальная ветка main. 

* Значит, что можете выполнить git push, находясь на ветке totallyNotMain, и наработки с ветки totallyNotMain будут закачены на ветку main удалённого репозитория!

Выполнить checkout для новой ветки, указав удалённую ветку в качестве ссылки. Для этого необходимо выполнить команду:
```
git checkout -b totallyNotMain o/main
```
* ***Cоздаст новую ветку с именем totallyNotMain и укажет ей следить за o/main***.

### Пример.

Выполним checkout для новой ветки foo и укажем ей, чтобы она отслеживала main с удалённого репозитория.

<img width="299" height="309" alt="image" src="https://github.com/user-attachments/assets/c4508ad3-ba1e-4d2e-b88d-3880a1c4dee5" />

### Решение.

1. Пропишем команды:
```
git checkout -b foo o/main
git pull
```
Результат:

<img width="298" height="313" alt="image" src="https://github.com/user-attachments/assets/2e7b102d-2971-4656-a1c6-4a5c1989faf2" />

* использовали o/main, чтобы обновить ветку foo.

### Пример.

<img width="302" height="169" alt="image" src="https://github.com/user-attachments/assets/6a738bff-d561-4aeb-9151-1957b730fc58" />

### Решение.

1. Пропишем команды:
```
git checkout -b foo o/main
git commit
git push
```
Результат:

<img width="300" height="311" alt="image" src="https://github.com/user-attachments/assets/1824306b-7b07-45ac-b561-de32f6a5c939" />

* Закачали наработки на ветку main удалённого репозитория. Докальная ветка называется абсолютно по-другому.

### Способ 2 = git branch -u o/main ветка

Указать ветке отслеживать удалённую ветку — это просто использовать команду git branch -u. Выполнив команду:
```
git branch -u o/main foo
```
* Укажете ветке foo следить за o/main.

Если вы ещё при этом находитесь на ветке foo, то её можно не указывать:
```
git branch -u o/main
```

### Пример.

<img width="299" height="175" alt="image" src="https://github.com/user-attachments/assets/dd6a6cae-d7ac-4e78-8829-f2f33994e96c" />

### Решение.

1. Пропишем команды:
```
git branch -u o/main foo
git commit
git push
```
Результат:

<img width="291" height="303" alt="image" src="https://github.com/user-attachments/assets/f1c21188-8f32-49af-a1a1-f05b75d53b80" />

### Пример.

Дано:

<img width="589" height="258" alt="image" src="https://github.com/user-attachments/assets/7f8635c5-1fcc-4ab7-9283-85479636dd41" />

1. Выполним push наших наработок в ветку main на удалённом репозитории, при этом не скачивая и не создавая ветку main локально. Вместо этого вам следует создать ветку с именем side.

2. Нужно получить визулизацию, как на картинке.

<img width="360" height="574" alt="image" src="https://github.com/user-attachments/assets/2e7cfdcb-00fc-4673-bb77-ed4d8e14ef95" />

### Решение.

1. Пропишем команды:
```
git checkout -b side o/main
git commit
git pull --rebase
git push
```
Результат:

<img width="1171" height="379" alt="image" src="https://github.com/user-attachments/assets/dcac60c1-caa4-46a8-a74a-88a5a4ee3029" />

<br>

<br>

<br>

## <a id ="title28">Аргументы Push</a>

Команда:
```
git push <удалённый_репозиторий> <целевая_ветка>
```

### Что за такой параметр <целевая_ветка>? 

### Пример.

Выполняем такую команду:
```
git push origin main
```
Дословный перевод с английского будет таким:

   * Перейди в ветку с именем "main" в локальном репозитории, возьми все коммиты и затем перейди на ветку "main" на удалённом репозитории "origin". На удалённую ветку скопируй все отсутствующие коммиты, которые есть у меня, и скажи, когда закончишь.

Указывая main в качестве аргумента "целевая_ветка", тем самым говорим git:
   
   * ***откуда*** будут приходить и ***куда*** будут уходить наши коммиты.
   
   * Аргумент "целевая_ветка" или "местонахождение" = ***синхронизация между двумя репозиториями***.

### Пример.

1. Указаны оба этих аргумента. Обратите внимание на местоположение, в котором мы находимся после чекаута.

<img width="301" height="309" alt="image" src="https://github.com/user-attachments/assets/e781ae4a-a017-49b5-8807-7048453a7fb0" />

### Решение.

1. Пропишем команды:
```
git checkout С0
git push origin main
```
Результат:

<img width="376" height="308" alt="image" src="https://github.com/user-attachments/assets/c110a206-8791-4791-86b5-ae9c0cd80c2e" />

* Обновили main на удалённом репозитории, принудительно указав аргументы в push.

### Пример.

1. Тоже самое.

<img width="301" height="309" alt="image" src="https://github.com/user-attachments/assets/e781ae4a-a017-49b5-8807-7048453a7fb0" />

### Решение.

1. Пропишем команды:
```
git checkout С0
git push 
```
Результат:

<img width="378" height="308" alt="image" src="https://github.com/user-attachments/assets/ac7ef1cc-9bd8-4188-acc1-bbce98426853" />

* Команда -, так как HEAD потерялся и не находится на удалённо-отслеживаемой ветке.

### Пример.

Дано:

<img width="709" height="292" alt="image" src="https://github.com/user-attachments/assets/b24972f8-2a9d-4846-b9e8-e1aea4a44507" />

1. Обновим обе ветки foo и main на удалённом репозитории.

2. Нужно получить визулизацию, как на картинке.

<img width="330" height="618" alt="image" src="https://github.com/user-attachments/assets/d2c13edd-36e2-495e-8d21-fe15bf050b49" />

### Решение.

1. Пропишем команды:
```
git push origin foo
git push origin main
```
Результат:

<img width="1133" height="308" alt="image" src="https://github.com/user-attachments/assets/6c118782-e8eb-42d5-921a-474431a552a6" />

### Подробности аргумента <пункт назначения>

* Источник и получатель коммитов были различными? 

* Что, еслизапушить коммиты из локальной ветки foo в ветку bar на удалённом репозитории?

Разделить источник и получатель аргумента <пункт назначения>, соедините их вместе, используя двоеточие:
```
git push origin <источник>:<получатель>
```

* Обычно это называется ***refspec***.

* **Refspec** — это всего лишь модное имя для определения местоположения, которое git может распознать (например, ветка foo или просто HEAD~1).

### Пример.

* **Источник** = ***местоположение, которое git должен понять***.

<img width="296" height="309" alt="image" src="https://github.com/user-attachments/assets/96dbc8dc-fdff-4118-81d9-90ddca0263da" />

### Решение.

1. Пропишем команду:
```
git push origin foo^:main
```
Результат:

<img width="297" height="311" alt="image" src="https://github.com/user-attachments/assets/7005d9e9-af0c-454a-96a3-08b57aafd6d0" />

* git видит в foo^ не что иное, как местоположение, закачивает все коммиты, которые не присутствуют на удалённом репозитории, и затем обновляет получателя.

### А что если пункт назначения, в который запушить, не существует? Без проблем! Укажите имя ветки, и git сам создаст ветку на удалённом репозитории для вас.

### Пример.

<img width="290" height="302" alt="image" src="https://github.com/user-attachments/assets/97d5a9d8-4c51-42df-a035-24e52a5d8bd4" />

### Решение.

1. Пропишем команду:
```
git push origin main:newBranch
```
Результат:

<img width="313" height="311" alt="image" src="https://github.com/user-attachments/assets/a70c36a8-277d-433e-b7ca-92834b323c15" />

### Пример.

Дано:

<img width="745" height="486" alt="image" src="https://github.com/user-attachments/assets/c6585f64-3810-4cde-aaf1-fb8c5693057c" />

1. Нужно получить визулизацию, как на картинке.

<img width="336" height="574" alt="image" src="https://github.com/user-attachments/assets/6d14c202-426b-41b7-ab75-9f23a16d0ed0" />

### Решение.

1. Пропишем команды:
```
git push origin foo^:foo
git push origin foo:main
git push origin main^:foo
```
```
git push origin main^:foo
git push origin foo:main
```
Результат:

<img width="1256" height="486" alt="image" src="https://github.com/user-attachments/assets/cdfe62c1-bb33-47a6-8a83-71169a9ba7b5" />

<br>

<br>

<br>

## <a id ="title29">Аргументы Fetch</a>

### Параметр <пункт назначения>

Если указываете пункт назначения в команде git fetch, например так, как в следующем примере:
```
git fetch origin foo
```
* Git отправится в ветку foo на удалённом репозитории, соберёт с собой все коммиты, которые не присутствуют локально, и затем поместит их в локальную ветку под названием o/foo.

### Пример.

<img width="296" height="312" alt="image" src="https://github.com/user-attachments/assets/4f2e80c5-70cb-4151-8d40-29ef75c021ea" />

### Решение.

1. Пропишем команду:
```
git fetch origin foo
```
Результат:

<img width="298" height="308" alt="image" src="https://github.com/user-attachments/assets/0e7931f7-44be-4ae1-a9e9-2147bf7cb791" />

* Cкачали только коммиты с ветки foo и поместили их в o/foo.

### Зачем git поместил экоммиты в ветку o/foo вместо того, чтобы разместить их в локальной ветке foo ? 

Думали о параметре <пункт назначения>, как о месте, ветке, которая существует в обоих - локальном и удалённом репозитории. Верно?

На самом деле:

В данном случае git делает исключение, потому что вы, возможно, работаете над веткой foo, которую не хотите привести в беспорядок. Об этом упоминалось в ранних уроках по git fetch - эта команда не обновляет локальные 'не удалённые', она лишь скачивает коммиты (соответственно, можете инспектировать / объединять их позже).

### "Что же тогда произойдёт, если я явно укажу оба параметра: и источник и получатель, пользуясь синтаксисом <источник>:<получатель> ?"

Если уверены в том, что закачать коммиты прямиком в вашу локальную ветку, ***тогда да***, можете явно указать источник и получатель через двоеточние = таким приёмом лишь для ветки, на которой ***не находитесь в настоящий момент checkout***. Теперь:

   * <источник> - это место на удалённом репозитории.
   
   * <получатель> - место в локальном репозитории, в который следует помещать коммиты.

Как уже было сказано, разработчики редко используют такой подход на практике.

### Пример.

<img width="294" height="306" alt="image" src="https://github.com/user-attachments/assets/913f72cf-520e-4e0e-9155-9a370b6c449e" />

### Решение.

1. Пропишем команду:
```
git fetch origin C2:bar
```
Результат:

<img width="300" height="311" alt="image" src="https://github.com/user-attachments/assets/0aa45ac1-ab1b-4e42-ad1a-2c0c5b20d84b" />

* git распознал C2 как место в origin и затем скачал эти коммиты в bar, которая является локальной веткой.

### Если ветка-получатель не существует на момент запуска команды? 

Поведение будет такое же, как и у git push.

### А если вообще без аргументов ? 

Если команда git fetch выполняется без аргументов, она скачивает все-все коммиты с удалённого репозитория и помещает их в соответствующие удалённо-локальные ветки в локальном репозитории...

### Пример.

<img width="269" height="336" alt="image" src="https://github.com/user-attachments/assets/20e095cf-466f-4047-bb17-e01a8ce5d370" />

### Решение.

1. Пропишем команду:
```
git fetch
```
Результат:

<img width="323" height="341" alt="image" src="https://github.com/user-attachments/assets/5a2506fe-0db4-4bbf-90d6-2f9fa94ff962" />

### Пример.

Дано:

1. Cкачайте лишь определённые коммиты так, как представлено в визуализации цели. Cледует явно указывать источник и получателя для обеих команд fetch.

2. Нужно получить визулизацию, как на картинке.

### Решение.

1. Пропишем команды:
```
git fetch origin C3:foo
git fetch origin C6:main
git checkout foo
git merge main
```
Результат:

<img width="1135" height="487" alt="image" src="https://github.com/user-attachments/assets/4fc11a39-21fa-407a-bcf4-fe9c54c6ec0d" />

<br>

<br>

<br>

## <a id ="title30">Пустой источник</a>

Git использует параметр <источник> странным образом. Странность заключается в том, что Вы можете оставить пустым параметр <источник> для команд git push и git fetch:
```
git push origin :side
```
```
git fetch origin :bugFix
```

### Пример.

Что же будет с веткой, на которую мы делаем git push с пустым аргументом <источник>? 

Она будет удалена.

<img width="298" height="178" alt="image" src="https://github.com/user-attachments/assets/50da57aa-d9d6-4e8c-a123-947609ef21a4" />

### Решение.

1. Пропишем команду:
```
git push origin :foo
```
Результат:

<img width="300" height="173" alt="image" src="https://github.com/user-attachments/assets/768c291b-c77b-4603-8dca-b677a25e58cd" />

* Удалили ветку foo в удаленном репозитории, попытавшить протолкнуть(git push) в неё "ничего".

### Пример.

1. Если попытаемся притянуть изменения (git fetch) из "ничего" к нам в локальный репозиторий, то это создаст новую ветку:

<img width="298" height="172" alt="image" src="https://github.com/user-attachments/assets/49838abd-6f6b-4baa-9831-2ddb267eda86" />

### Решение.

1. Пропишем команду:
```
git fetch origin :bar
```
Результат:

<img width="297" height="175" alt="image" src="https://github.com/user-attachments/assets/d1849178-de3e-4801-b635-af60ccc8e8ac" />

* Появилась локальная ветка bar.

### Пример.

Дано:

<img width="587" height="148" alt="image" src="https://github.com/user-attachments/assets/9d8f09c5-34be-4b82-92b2-dbf452cc2248" />

1. Удалить одну ветку в удаленном репозитории и создать новую ветку в локальном

2. Нужно получить визулизацию, как на картинке.

<img width="284" height="310" alt="image" src="https://github.com/user-attachments/assets/4064877a-eb56-4762-874d-fab0696d2259" />

### Решение.

1. Пропишем команды:
```
git push origin :foo (удалит)
git fetch origin :bar (добавит)
```
Результат:

<img width="827" height="146" alt="image" src="https://github.com/user-attachments/assets/3585dbb3-a0d2-4589-8b75-fb4024cc645e" />

<br>

<br>

<br>

## <a id ="title31">Аргументы для Pull</a>

* **git pull**:
     
     * Cначала выполняет git fetch
     
     * Cледом сразу git merge с той веткой, в которую притянулись обновления командой fetch.

Другими словами, это все равно, что выполнить git fetch с теми же аргументами, которые вы указали для pull, а затем выполнить git merge с веткой, указанной в аргументе <приемник> команды pull.

Эквивалентны:
```
git pull origin foo
```
```
git fetch origin foo
git merge o/foo
```
Эквивалентны:
```
git pull origin bar:bugFix
```
```
git fetch origin bar:BugFix
git merge bugFix
```

### Пример.

Cначала выполнится fetch с аргументом указанным к pull, а merge выполняется с теми изменениями, которые будут скачаны командой fetch.

<img width="296" height="312" alt="image" src="https://github.com/user-attachments/assets/19b514ac-0706-4948-b4f2-d430a3819b92" />

### Решение.

1. Пропишем команду:
```
git pull origin main
```
Результат:

<img width="346" height="308" alt="image" src="https://github.com/user-attachments/assets/1cc11a26-b8de-4ca8-912b-9fc8636f4610" />

* Указали main, поэтому как обычно все обновления притянулись на ветку o/main. Затем мы слили (merge) обновленную ветку o/main с веткой, на которой мы находимся.

### Пример.

Будет ли это работать, если указать <источник> и <приемник>? Проверим:

<img width="299" height="309" alt="image" src="https://github.com/user-attachments/assets/7327bbbf-7015-4c37-8233-aa4170eafd7e" />

### Решение.

1. Пропишем команду:
```
git pull origin main:foo
```
Результат:

<img width="347" height="309" alt="image" src="https://github.com/user-attachments/assets/ac540cdc-6ebd-4f2a-a427-2f64e98bd8e1" />

* Cоздали новую ветку foo в локальном репозитории, скачали на неё изменения с ветки main удаленного репозитория, а затем слили ветку с веткой bar, на которой находились.

### Пример.

Дано:

<img width="636" height="296" alt="image" src="https://github.com/user-attachments/assets/fcbd4df3-f9a8-4b19-b6f9-f4eba50608a1" />

1. Cкачать несколько изменений, создать несколько новых веток, слить одни ветки в другие.

2. Нужно получить визулизацию, как на картинке.

<img width="315" height="601" alt="image" src="https://github.com/user-attachments/assets/bc226325-e3d7-407c-aca0-ad3013471e66" />

### Решение.

1. Пропишем команды:
```
git pull origin C3:foo
git pull origin C2:main
```
Результат:

<img width="1194" height="487" alt="image" src="https://github.com/user-attachments/assets/d4039903-1dd3-4969-92e8-ed3cd83a295e" />
