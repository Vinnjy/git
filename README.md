# Основы:

## [Base](https://github.com/winnca/git/tree/1_base)

  * ### Коммиты
      
      * git commit

  * ### Ветвление
      
      * git branch или git checkout -b

  * ### Ветки и слияние
      
      * git merge

  * ### Ветки и слияние-копией
  
      * git rebase

<br>

## [Base-Pro](https://github.com/winnca/git/tree/2_base_pro)

  * ### HEAD
  
      * git checkout <коммит ИЛИ ветка>
  
  * ### Относительные ссылки (^, ~)
  
      * git checkout <ветка ИЛИ head^>

  * ### Перемещение ветки
  
      * git branch -f <перемещаемая ветка И ветка-куда>
  
  * ### Отмена изменений
  
      * git reset или git revert

<br>

## [Pro](https://github.com/winnca/git/tree/3_pro)

  * ### Перемещение изменений
  
      * git cherry-pick

  * ### Перемещение изменений (интерактивный rebase)
  
      * git rebase -i

  * ### Теги
  
      * git tag

  * ### Описание тегов
  
      * git describe

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

  * ### Клонирование
  
       * git clone

  * ### Удалённые ветки
  
       * "git checkout origin/main

  * ### Извлечение/скачивание данных из удаленного репозитория
  
       * git fetch

  * ### git fetch и git merge
  
       * git pull

  * ### Коллективная работа
  
       * git fakeTeamwork

  * ### Загрузка изменений в удалённый репозиторий
  
       * git push

  * ### Расхождение в истории
  
       * git pull --rebase + git push ИЛИ git pull + git push

  * ### Заблокированная ветвь main
  
       * git checkout -b <ветка И коммит> + git push

<br>

## [Продвинутое использование](https://github.com/winnca/git/tree/6_pro_pull_push)

  * ### Push мастер
  
       * git fetch + git rebase <ветка куда И ветка-копия>

  * ### Слияние с удаённым репозиторием
  
       * git pull + git merge

  * ### Слежка за удалённым репозиторием
  
       * git checkout -b <ветка> o/main (+ git pull) + git push ИЛИ git branch -u o/main <ветка> (+ git pull) + git push

  * ### Аргументы для Push
  
       * git push <удалённый_репозиторий> <целевая_ветка> ИЛИ git push origin <источник>:<получатель>

  * ### Аргументы для Fetch
  
       * git fetch <удалённая ветка ИЛИ коммит>:<ветка локального репозитория> ИЛИ git fetch <удалённая ветка ИЛИ коммит>
  
  * ### Не указываем источник
  
       * git push origin  :<ветка> = удалить ИЛИ git fetch origin  :<ветка> = добавить

  * ### Аргументы для Pull
       
      * git pull <удалённая ветка ИЛИ коммит>:<ветка локального репозитория> ИЛИ git pull <удалённая ветка ИЛИ коммит>
