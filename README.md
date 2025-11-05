# Основы:

## [Base](https://github.com/winnca/git/tree/1_base)

<details>
 <summary>Коммиты</summary>
<br>

```
git commit
```
</details>

<details>
 <summary>Ветвление</summary>
<br>

```
git branch
```
```
git checkout -b
```
</details>

<details>
 <summary>Ветки и слияние</summary>
<br>

```
git merge
```
</details>

<details>
 <summary>Ветки и слияние-копией</summary>
<br>

```
git rebase
```
</details>

<br>

## [Base-Pro](https://github.com/winnca/git/tree/2_base_pro)

<details>
 <summary>HEAD</summary>
<br>

```
git checkout <коммит ИЛИ ветка>
```
</details>

<details>
 <summary>Относительные ссылки (^, ~)</summary>
<br>

```
git checkout <ветка ИЛИ head^>
```
</details>

<details>
 <summary>Перемещение ветки</summary>
<br>

```
git branch -f <перемещаемая ветка И ветка-куда>
```
</details>

<details>
 <summary>Отмена изменений</summary>
<br>

```
git reset
```
```
git revert
```
</details>

<br>

## [Pro](https://github.com/winnca/git/tree/3_pro)

<details>
 <summary>Перемещение изменений</summary>
<br>

```
git cherry-pick
```
</details>

<details>
 <summary>Перемещение изменений (интерактивный rebase)</summary>
<br>

```
git rebase -i
```
</details>

<details>
 <summary>Теги</summary>
<br>

```
git tag
```
</details>

<details>
 <summary>Описание тегов</summary>
<br>

```
git describe
```
</details>

<br>

## [Рабочии ситуации](https://github.com/winnca/git/tree/4_job)

  * ### Исправленные ошибка

  * ### Внесение изменений в более ранний коммит

  * ### Rebase на нескольких ветках

  * ### Определение родителей (~, ^)

  * ### Спутанные ветки

<br>

<br>

<br>

# Удалённые репозитории

## [Pull & Push](https://github.com/winnca/git/tree/5_pull_push)

<details>
 <summary>Клонирование</summary>
<br>

```
git clone
```
</details>

<details>
 <summary>Удалённые ветки</summary>
<br>

```
git checkout origin/main
```
</details>

<details>
 <summary>Извлечение/скачивание данных из удаленного репозитория</summary>
<br>

```
git fetch
```
</details>

<details>
 <summary>git fetch и git merge</summary>
<br>

```
git pull
```
</details>

<details>
 <summary>Коллективная работа</summary>
<br>

```
git fakeTeamwork
```
</details>

<details>
 <summary>Загрузка изменений в удалённый репозиторий</summary>
<br>

```
git push
```
</details>

<details>
 <summary>Расхождение в истории</summary>
<br>

```
git pull --rebase
git push
```
```
git pull
git push
```
</details>

<details>
 <summary>Заблокированная ветвь main</summary>
<br>

```
git checkout -b <ветка И коммит>
git push
```
</details>

<br>

## [Продвинутое использование](https://github.com/winnca/git/tree/6_pro_pull_push)

<details>
 <summary>Push мастер</summary>
<br>

```
git fetch
git rebase <ветка куда И ветка-копия>
```
</details>

<details>
 <summary>Слияние с удаённым репозиторием</summary>
<br>

```
git pull
git merge
```
</details>

<details>
 <summary>Слежка за удалённым репозиторием</summary>
<br>

```
git checkout -b <ветка> o/main
git pull
git push
```
```
git checkout -b <ветка> o/main
git push
```
```
git branch -u o/main <ветка>
git pull
git push
```
```
git branch -u o/main <ветка>
git push
```
</details>

<details>
 <summary>Аргументы для Push</summary>
<br>

```
git push <удалённый_репозиторий> <целевая_ветка>
```
```
git push origin <источник>:<получатель>
```
</details>

<details>
 <summary>Аргументы для Fetch</summary>
<br>

```
git fetch <удалённая ветка ИЛИ коммит>:<ветка локального репозитория>
```
```
git fetch <удалённая ветка ИЛИ коммит>
```
</details>

<details>
 <summary>Не указываем источник</summary>
<br>

удалить
```
git push origin  :<ветка>
```
добавить
```
git fetch origin  :<ветка>
```
</details>

<details>
 <summary>Аргументы для Pull</summary>
<br>

```
git pull <удалённая ветка ИЛИ коммит>:<ветка локального репозитория>
```
```
git pull <удалённая ветка ИЛИ коммит>
```
</details>
