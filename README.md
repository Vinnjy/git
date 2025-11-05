# Рабочии ситуации:

  * ### [Исправленные ошибка](#title10)

  * ### [Внесение изменений в более ранний коммит](#title11)

  * ### [Rebase на нескольких ветках](#title14)

  * ### [Определение родителей (~, ^)](#title15)

  * ### [Спутанные ветки](#title16)

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
