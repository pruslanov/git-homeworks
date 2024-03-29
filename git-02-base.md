# Домашнее задание к занятию «Основы Git»

### Цель задания

В результате выполнения задания вы:

* научитесь работать с Git, как с распределённой системой контроля версий; 
* сможете создавать и настраивать репозиторий для работы в GitHub, GitLab и Bitbucket; 
* попрактикуетесь работать с тегами;
* поработаете с Git при помощи визуального редактора.

------

## Задание 1. Знакомимся с GitLab и Bitbucket 

Из-за сложности доступа к Bitbucket в работе достаточно использовать два репозитория: GitHub и GitLab.

Иногда при работе с Git-репозиториями надо настроить свой локальный репозиторий так, чтобы можно было 
отправлять и принимать изменения из нескольких удалённых репозиториев. 

Это может понадобиться при работе над проектом с открытым исходным кодом, если автор проекта не даёт права на запись в основной репозиторий.

Также некоторые распределённые команды используют такой принцип работы, когда каждый разработчик имеет свой репозиторий, а в основной репозиторий пушатся только конечные результаты 
работы над задачами. 

### GitLab

Создадим аккаунт в GitLab, если у вас его ещё нет:

1. GitLab. Для [регистрации](https://gitlab.com/users/sign_up)  можно использовать аккаунт Google, GitHub и другие. 
2. После регистрации или авторизации в GitLab создайте новый проект, нажав на ссылку `Create a projet`. 
Желательно назвать также, как и в GitHub — `devops-netology` и `visibility level`, выбрать `Public`.
3. Галочку `Initialize repository with a README` лучше не ставить, чтобы не пришлось разрешать конфликты.
4. Если вы зарегистрировались при помощи аккаунта в другой системе и не указали пароль, то увидите сообщение:
`You won't be able to pull or push project code via HTTPS until you set a password on your account`. 
Тогда перейдите [по ссылке](https://gitlab.com/profile/password/edit) из этого сообщения и задайте пароль. 
Если вы уже умеете пользоваться SSH-ключами, то воспользуйтесь этой возможностью (подробнее про SSH мы поговорим в следующем учебном блоке).
5. Перейдите на страницу созданного вами репозитория, URL будет примерно такой:
https://gitlab.com/YOUR_LOGIN/devops-netology. Изучите предлагаемые варианты для начала работы в репозитории в секции
`Command line instructions`. 

[Ссылка на созданный репозиторий на GitLab](https://gitlab.com/pruslanov1/devops-netology)

![репозиторий на GitLab](img/hw-git-02-001.png)

6. Запомните вывод команды `git remote -v`.

![репозиторий на GitLab](img/hw-git-02-002.png)

7. Из-за того, что это будет наш дополнительный репозиторий, ни один вариант из перечисленных в инструкции (на странице 
вновь созданного репозитория) нам не подходит. Поэтому добавляем этот репозиторий, как дополнительный `remote`, к созданному
репозиторию в рамках предыдущего домашнего задания:
`git remote add gitlab https://gitlab.com/YOUR_LOGIN/devops-netology.git`.

Добавялем удаленный репозиторий с доступом по SSH

`git remote add gitlab git@gitlab.com:pruslanov1/devops-netology.git`

![Добавляем удаленный репозиторий на GitLab](img/hw-git-02-003.png)

8. Отправьте изменения в новый удалённый репозиторий `git push -u gitlab main`.
9. Обратите внимание, как изменился результат работы команды `git remote -v`.

![PUSH в удаленный репозиторий на GitLab](img/hw-git-02-004.png)

![Просмотр удаленного репозитория на GitLab](img/hw-git-02-005.png)

#### Как изменить видимость репозитория в  GitLab — сделать его публичным 

* На верхней панели выберите «Меню» -> «Проекты» и найдите свой проект.
* На левой боковой панели выберите «Настройки» -> «Основные».
* Разверните раздел «Видимость» -> «Функции проекта» -> «Разрешения».
* Измените видимость проекта на Public.
* Нажмите «Сохранить изменения».

> Дополyнительно пришлось группу проектов сначала сделать Public, а потом уже Public свойство стало достпно для проекта 

### Bitbucket* (задание со звёздочкой) 

Это самостоятельное задание, его выполнение необязательно.
____

Теперь необходимо проделать всё то же самое с [Bitbucket](https://bitbucket.org/). 

1. Обратите внимание, что репозиторий должен быть публичным — отключите галочку `private repository` при создании репозитория.
1. На вопрос `Include a README?` отвечайте отказом. 
1. В отличии от GitHub и GitLab в Bitbucket репозиторий должен принадлежать проекту, поэтому во время создания репозитория 
надо создать и проект, который можно назвать, например, `netology`.
1. Аналогично GitLab на странице вновь созданного проекта выберите `https`, чтобы получить ссылку, и добавьте этот репозиторий, как 
`git remote add bitbucket ...`.
1. Обратите внимание, как изменился результат работы команды `git remote -v`.

Если всё проделано правильно, то результат команды `git remote -v` должен быть следующий:

```bash
$ git remote -v
bitbucket https://andreyborue@bitbucket.org/andreyborue/devops-netology.git (fetch)
bitbucket https://andreyborue@bitbucket.org/andreyborue/devops-netology.git (push)
gitlab	  https://gitlab.com/andrey.borue/devops-netology.git (fetch)
gitlab	  https://gitlab.com/andrey.borue/devops-netology.git (push)
origin	  https://github.com/andrey-borue/devops-netology.git (fetch)
origin	  https://github.com/andrey-borue/devops-netology.git (push)
```

Дополнительно можете добавить удалённые репозитории по `ssh`, тогда результат будет примерно такой:

```bash
git remote -v
bitbucket	git@bitbucket.org:andreyborue/devops-netology.git (fetch)
bitbucket	git@bitbucket.org:andreyborue/devops-netology.git (push)
bitbucket-https	https://andreyborue@bitbucket.org/andreyborue/devops-netology.git (fetch)
bitbucket-https	https://andreyborue@bitbucket.org/andreyborue/devops-netology.git (push)
gitlab	git@gitlab.com:andrey.borue/devops-netology.git (fetch)
gitlab	git@gitlab.com:andrey.borue/devops-netology.git (push)
gitlab-https	https://gitlab.com/andrey.borue/devops-netology.git (fetch)
gitlab-https	https://gitlab.com/andrey.borue/devops-netology.git (push)
origin	git@github.com:andrey-borue/devops-netology.git (fetch)
origin	git@github.com:andrey-borue/devops-netology.git (push)
origin-https	https://github.com/andrey-borue/devops-netology.git (fetch)
origin-https	https://github.com/andrey-borue/devops-netology.git (push)
```

Выполните push локальной ветки `main` в новые репозитории. 

Подсказка: `git push -u gitlab main`. На этом этапе история коммитов во всех трёх репозиториях должна совпадать. 

## Задание 2. Теги

Представьте ситуацию, когда в коде была обнаружена ошибка — надо вернуться на предыдущую версию кода,
исправить её и выложить исправленный код в продакшн. Мы никуда не будем выкладывать код, но пометим некоторые коммиты тегами и создадим от них ветки. 

1. Создайте легковестный тег `v0.0` на HEAD-коммите и запуште его во все три добавленных на предыдущем этапе `upstream`.

Создание tag

```bash
git tag v0.0
git tag
```

![Создание легковесного тэга](img/hw-git-02-006.png)

PUSH в два удаленных репозитория

```bash
git push origin v0.0
git push gitlab v0.0
```

![PUSH в удаленные репозитории](img/hw-git-02-007.png)

2. Аналогично создайте аннотированный тег `v0.1`.

```bash
git tag -a v0.1 -m 'Annotated tag creation'
git tag
git push origin v0.1
git push gitlab v0.1
```

![Создание аннотированного тэга](img/hw-git-02-008.png)

![PUSH в удаленные репозитории](img/hw-git-02-009.png)

3. Перейдите на страницу просмотра тегов в GitHab (и в других репозиториях) и посмотрите, чем отличаются созданные теги. 
    * в GitHub — https://github.com/pruslanov/devops-netology/tags;

    Раздел Tags в удаленном репозитории GitHub 

    ![Раздел Tags в удаленном репозитории GitHub](img/hw-git-02-010.png) 

    Видно, что легковесный тег `v0.0` просто сылается на последний commmit и его дата равна дате commitа и комментарий взят из coomit
    Аннотированный тег `v0.1` продатирован датой создания tag со своим комментарием

    * в GitLab — https://gitlab.com/pruslanov1/devops-netology/-/tags;

    Раздел Tags в удаленном репозитории GitLab

    ![Раздел Tags в удаленном репозитории GitLab](img/hw-git-02-011.png) 

    Даты тегов совпадают и указывают на дату commit, в обоих tag выводится комментарий в commit в аннотированный теге `v0.1` дополнительно выводиться комментарий кag

    * в Bitbucket — список тегов расположен в выпадающем меню веток на отдельной вкладке. 

## Задание 3. Ветки 

Давайте посмотрим, как будет выглядеть история коммитов при создании веток. 

1. Переключитесь обратно на ветку `main`, которая должна быть связана с веткой `main` репозитория на `github`.

```bash
git checkout origin/main
git status
```

![Переключение ветки main репозитория на github](img/hw-git-02-012.png)

2. Посмотрите лог коммитов и найдите хеш коммита с названием `Prepare to delete and move`, который был создан в пределах предыдущего домашнего задания. 

```bash
git log --grep "Prepare to delete and move" --oneline
git log --grep "Prepare to delete and move"
```

![Commit с названием `Prepare to delete and move`](img/hw-git-02-013.png)

3. Выполните `git checkout` по хешу найденного коммита. 

`git checkout 615ecd6`

![Commit с названием `Prepare to delete and move`](img/hw-git-02-014.png)

4. Создайте новую ветку `fix`, базируясь на этом коммите `git switch -c fix`.
5. Отправьте новую ветку в репозиторий на GitHub `git push -u origin fix`.

```bash
git switch -c fix
git push -u origin fix
```

![Switch to brunch](img/hw-git-02-015.png)

6. Посмотрите, как визуально выглядит ваша схема коммитов: https://github.com/pruslanov/devops-netology/network.

![Схема коммитов на GitHub](img/hw-git-02-016.png)

7. Теперь измените содержание файла `README.md`, добавив новую строчку.

```bash
git status
echo "ADD ONE NEW LINE TO THE END" >> README.md
git status
git add README.md
git status
```

![Изменение файла README.md](img/hw-git-02-017.png)

8. Отправьте изменения в репозиторий и посмотрите, как изменится схема на странице https://github.com/pruslanov/devops-netology/network 
и как изменится вывод команды `git log`.

```bash
git commit -m "README.md file add one line to the end"
git push -u origin fix
```

![КОммит и PUSH](img/hw-git-02-018.png)

![Схема коммитов на GitHub](img/hw-git-02-019.png)

`git log`

![Схема коммитов на GitHub](img/hw-git-02-020.png)

## Задание 4. Упрощаем себе жизнь

Попробуем поработь с Git при помощи визуального редактора. 

1. В используемой IDE PyCharm откройте визуальный редактор работы с Git, находящийся в меню View -> Tool Windows -> Git.
2. Измените какой-нибудь файл, и он сразу появится на вкладке `Local Changes`, отсюда можно выполнить коммит, нажав на кнопку внизу этого диалога. 

Установлено приложение изменен один файл и добавлен еще один через IDE PyCharm

![IDE PyCharm](img/hw-git-02-021.png)

3. Элементы управления для работы с Git будут выглядеть примерно так:

   ![Работа с гитом](img/ide-git-01.jpg)
   
4. Попробуйте выполнить пару коммитов, используя IDE. 

Commit

![IDE PyCharm COMMIT](img/hw-git-02-022.png)

PUSH

![IDE PyCharm COMMIT](img/hw-git-02-023.png)

GitHub

![FitHub COMMIT](img/hw-git-02-024.png)

[По ссылке](https://www.jetbrains.com/help/pycharm/commit-and-push-changes.html) можно найти справочную информацию по визуальному интерфейсу. 

Если вверху экрана выбрать свою операционную систему, можно посмотреть горячие клавиши для работы с Git. 
Подробней о визуальном интерфейсе мы расскажем на одной из следующих лекций.

*В качестве результата работы по всем заданиям приложите ссылки на ваши репозитории в GitHub, GitLab и Bitbucket*.  
 
----

### Правила приёма домашнего задания

В личном кабинете отправлены ссылки на ваши репозитории.


### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки.  
 
Обязательными являются задачи без звёздочки. Их выполнение необходимо для получения зачёта и диплома о профессиональной переподготовке.

Задачи со звёздочкой (*) являются дополнительными или задачами повышенной сложности. Они необязательные, но их выполнение поможет лучше разобраться в теме.