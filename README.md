### Репозитой с инструкцией Git
# Работа с Git
## Проверка наличия установленного Git
В терминале выполнить команду
```
git --version
```
Если Git установлен правильно - мы получим версию программы.
В противном случае мы получим сообщение об ошибке!
## Установка Git
Загружаем последнюю версию Git  с сайта:
https://git-scm.com/download/win
и устанавливаем с настройками "по умолчанию".
## Установка Visual Studio Code
Загружаем последнюю версию Git  с сайта:
https://code.visualstudio.com/download
и устанавливаем с настройками " по умолчанию ".
## Настройка Git
При первом использовании Git необходимо представиться
```
git config --global user.name your name
git config --global user.email your e-mail
```
## Создание и инициализация репозитория
*Репозиторием называют хранилище вашего кода и историю его изменений. Git работает локально и все ваши репозитории хранятся в определенных папках на жёстком диске.*

Для начала нужно создать папку, в которой будут храниться файлы нашего проекта и которую будет отслеживать Git.
Затем открыть её, используя меню "Файл".

Инициализируем наш репозиторий, используя следующую команду в терминале:
```
git init
```
## Проверка статуса репозитория
Для проверки текущего состояния репозитория следует воспользоваться командой:
```
git status
```
## Добавление файла
Для начала, в проводнике VSC создадим новый файл "Git_instruction.md"
Для добавления этого файла в наш репозиторий мы будем использовать в терминале команду:
```
git add <File.name>
```
*Важно отметить, что команда `git add` не только добавляет новые файлы, но и все изменения в файлах, которые были внесены ранее.*
## Создание версии проекта (коммита)
После того, как мы добавили файл в наш репозиторий, мы можем создать версию проекта. С помощью команды:
```
git commit -m "comment"
```

*По-английски commit значит «фиксировать». Git-коммит — это операция, которая берет все подготовленные изменения и отправляет их в репозиторий как единое целое.*

То есть **_коммит_** — это некое логически завершённое изменение внутри проекта и понятная (в том числе и другим разработчикам) точка, к которой можно вернуться, если возникнут какие-то проблемы.

Каждая новая версия должна сопровождаться комментарием. Это делает работу над проектом понятной, прозрачной и структурированной.

Как правило, рабочий процесс представляет собой цикл: коммит — изменение файлов — коммит.
## Просмотр коммитов и возврат 
Для просмотра изменений, сделанных в последнем коммите, используем команду:
```
git show
```
Для просмотра списка всех коммитов, воспользуйтесь командой:
```
git log
```
Однако же, стоит заметить, что существует ещё один способ, позволяющий уменьшить количество информации, выдаваемой на экран. С параметром `--oneline` каждый коммит показывается в одну строчку, но в данном случае вы не видим информации о времени и авторе коммитов.

*В Git не существует традиционной системы отмены, как в текстовых редакторах. Лучше воздержаться от сопоставления операций Git с какой бы то ни было привычной для нас концепцией отмены изменений. Кроме того, Git имеет собственную систему терминов для операций отмены. В числе таких терминов — `сброс (reset),` `возврат (revert),` `переключение (checkout),` `очистка (clean)` и другие.*

Применительно к нашему случаю, в Git под возвратом или переключением между различными версиями целевого объекта - коммитами - понимают термин checkout.
Для возврата, прежде всего, нужно найти идентификатор редакции (коммита), в которую вы хотите вернуться. Для этого используем команду:
```
git log
```
После того как мы нашли ссылку на нужный коммит в истории, для перехода к нему можно использовать команду:
```
git checkout "уникальный идентифицирующий хеш коммита" (использовать без кавычек)
```
После внесения необходимых изменений их следует добавить и вернуться в актуальное состояние командой:
```
git checkout <название ветки> (в нашем случае master)
```
## Сравнение внесённых изменений
Для вывода изменений в файлах по сравнению с последним коммитом, используется команда 
```
git diff (без параметров)
```
Важно, что в данном случае команда выводит изменения в файлах, которые ещё не были добавлены в индекс. Сравнение происходит с последним коммитом.

Однако, если мы изменили какие-нибудь файлы в вашем рабочем каталоге и добавили один или несколько из них в индекс (`с помощью git add`), то команда `git diff` не покажет изменения в этих файлах. Для того, чтобы показать изменения в наших файлах, включая файлы, которые были добавлены нами в индекс, используется уже известную комманду с ключом
```
git diff --cached
```
## Игнорирование файлов
Для того, чтобы исключить из отслеживания в репозитории определённый файл (группу файлов и папок).В случае необходимости следует создать там файл `.gitignore` и записать в него их названия или шаблоны, соответствующие таким файлам или папкам.

`.gitignore` использует glob шаблоны для сопоставления имен файлов с символами подстановки. Это может напоминать регулярные выражения. Если у нас есть файлы или папки, содержащие шаблон подстановки (например *), вы можете использовать один обратный слеш ( \ *), чтобы экранировать такой символ.

Строки, начинающиеся со знака хэша (#), являются комментариями и игнорируются. Пустые строки могут быть использованы для улучшения читабельности файла и группировки связанных строк шаблонов.

Символ косой черты, слэш, (/) является разделителем адреса папок. Слэш в начале шаблона относится к директории, в которой находится файл `.gitignore`.
Если шаблон начинается со слеша, то он соответствует файлам и каталогам только в корне хранилища.
Однако, если шаблон не начинается со слэша, он соответствует файлам и каталогам в любом каталоге или подкаталоге.
В случае, когда шаблон заканчивается знаком слэш, он соответствует только каталогам. Когда каталог игнорируется, все его файлы и подкаталоги также игнорируются.
## Создание веток в Git
Ветка в Git простой перемещаемый указатель на один из коммитов, обычно последний в цепочке коммитов. По уполчанию, имя овновной ветки в Git - `master`.  Создать ветку можно коммандой:
```
git branch <название новой ветки>
```
Чтобы при создании ветки сразу на неё переключиться необходимо воспользоваться командой:
```
git checkout -b <имя новой ветки>
```
## Слияние веток
Для начала необходимо определиться с терминологией:

**_Ветка_** – независимая последовательность коммитов.

**_Сливаемая ветка_** – ветка, из которой мы берем изменения, чтобы влить их в целевую.

**_Целевая ветка_** – ветка, в которую мы сливаем наши изменения.

**_Слияние веток_** – это перенос изменений из одной ветки в другую. При этом слияние не затрагивает сливаемую ветку, то есть она остается в том же состоянии, что позволяет нам потом продолжить работу с ней.

Первоначально мы работаем в основной (целевой) ветке. Она называется master.
Целью создания дополнительных веток является проработка отдельных элементов проекта автономно, а затем присоединение их к проекту. В большинстве случаев эти ветки в итоге объединяются с веткой *master*. Процедура объединения веток называется *слиянием (merge)*.

Для слияния текущей ветки с либой дрйгой веткой используем команду:
```
git merge <имя ветки, которую хотим присоединить>
```
## Разрешение конфликтов
При слиянии может возникнуть ситуация, когда фрагмент в каком-либо файле проекта в различных ветках отредактирован по разному. Такая ситуация называется конфликт (**_conflict_**).

Иными словами, если мы изменили одну и ту же часть одного и того же файла по-разному в двух объединяемых ветках, Git не сможет их чисто объединить и мы получим сообщение о конфликте слияния. И, следовательно, Git не создал коммит слияния автоматически. Он остановил процесс до тех пор, пока мы не разрешим конфликт. 
Начало конфликтного фрагмента помечается строкой, начинающиеся с символов 
< и содержащей имя первой ветки, а заканчивается строкой, начинающиеся с символов > и содержащей имя вливаемой ветки. Версии из каждой ветки разделяются строкой с символами =. Такой файл получает статус не объединенный (**_unmerged_**).

На выбор мы получаем четыре команды:
```
accept current change - принять текущее изменение
accept incoming change - принять входящие изменения
accept both changes - принять оба изменения
compare changes - сравнить изменения
```

При возникновении конфликта мы должны в ручном режиме его устранить. После редактирования конфликтной области и сохранения файла, нужно сообщить git о разрешении конфликта с помощью индексирования этого файла (после чего он перейдет в состояние «измененный»).
## Удаление веток
Для организации разработки различных версий дркумента в Git, как было описано выше, мы используем ветки. Ветки также очень часто используются для разработки какого-либо нового функционала или инструментария. Если разработкой продукта занимается группа, каждый разработчик может работать над своей частью функциональности в отдельной ветке.

В итоге, когда работы будут завершены, получившуюся ветку мы совмещаем с основной перед этим отправив её на проверку коллегам. При таком типе организации рабочего процесса со временем в нашем репозитории накапливается очень много ненужных или пустых веток, которые надо удалять.

Прежде чем что-либо удалять следует проверить, какие ветки есть в проекте. Для того чтобы посмотреть ветки используем команду:
```
git branch
```
Данная команда выведет список наших веток, а текущая ветка, в ктороый мы находимся, будет выделена зеленым цветом и звездочкой.

Для того чтобы удалить ветку необходимо использовать комманду:
```
git branch -d <название ветки>
```
Если в этой ветке есть не зафиксированные изменения или коммиты, то Git откажется её удалять. Для того чтобы всё же удалить такую ветку используйте комманду:
```
git branch -D <название ветки>
```
После этого проверяем список веток коммандой:
```
git branch
```
Если всё сделано верно, то удалённой ветки мы не увидим.
## Полезные комманды Git
Обычно, для просмотра лога и коммитов мы используем комманду:
```
git log
```
На выводе мы получаем не очень удобный для чтения ворох данных. Для формирования лога в удобном для чтения и понимания виде предлагаю использовать комманду:
```
git log --pretty=format:"%H [%cd]: %an - %s" --graph --date=format:%c
```
### Переключиться на другой коммит и продолжить работу с него
Если потребовалось создание новой ветки, которая будет начинаться с указаного коммита, выполняем команду:
```
git checkout -b <new branch name> <commit hash> 
```
**_Пояснение_**: _создать ветку new-branch, начинающуюся с коммита c хешем 5589877 (переместить HEAD на указанный коммит, рабочую директорию вернуть к состоянию, на момент этого коммита, создать указатель на этот коммит (ветку) с указанным именем)_
## Работа с удалёнными репозиториями
**_Удалённый репозиторий_** (внешний репозиторий) – представляет собой версии вашего проекта, размещённые на каком-либо удалённом сервере (в нашем случае это GitHub). Доступ к такому репозиторию удалённом сервере может осуществляться по средствам сети интернет или же через локальную сеть.

_Удалённый репозиторий_ – это абсолютно полноценный репозиторий, не имеющий никаких отличий от локального: у удалённого репозитория есть собственные ветки, собственный указатель HEAD, своя история коммитов и так далее.
### 1. Регистрация аккаунта на [GitHub](https://github.com/)
Для этого yнеобходимо перейти на [GitHub]( https://github.com/). Далее, находим и нажимаем кнопку «Sign up» (зарегистрироваться). На странице регистрации вам предложат ввести обязательные данные: имя пользователя; адрес электронной почты; пароль. После на указанную ранее почту придёт письмо с просьбой подтвердить электронный адрес. Для завершения регистрации необходимо перейти по полученной ссылке.
### 2. Создаём и связываем локальный и удалённый репозиторий
В обычных случаях мы получаем репозиторий Git двумя способами:
* Берём локальную папку, которая не находится под контролем (не индексируется), и превращаем её в репозиторий Git:
```
git init
git add Git_instruction.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/wargie/git_seminag_homewor_2.git
git push -u origin main
```
* Если репозиторий был создан ранее на локальном пк:
```
git remote add origin https://github.com/wargie/git_seminag_homewor_2.git
git branch -M main
git push -u origin main
```
Кроме того, используя ключ -v, мы можем просмотреть адреса для чтения и записи, привязанные к репозиторию, в нашем случае:
```
origin https://github.com/wargie/git_seminag_homewor_2.git (fetch)
origin https://github.com/wargie/git_seminag_homewor_2.git (push)
prime_master https://github.com/wargie/git_seminag_homewor_2.git (fetch)
prime_master https://github.com/wargie/git_seminag_homewor_2.git (push)
```
* Мы можем клонировать существующий удалённый репозиторий Git, используя команду:
```
git clone <адрес удалённого репозитория>
```
### 3. Загрузка данных из удалённого репозитория
Если наша текущая ветка настроена на отслеживание удалённой ветки, то мы можем использовать команду `git pull` для того, чтобы в автоматическом режиме получить изменения из нашей удалённой ветки и слить их со своей текущей. По умолчанию команда `git clone` автоматически настраивает локальную ветку master на отслеживание удалённой ветки master на сервере, с которого клонировали репозиторий. Название веток может быть и другим, и зависит от ветки по умолчанию на сервере. Выполнение команды `git pull`, как правило, скачивает данные с сервера, с которого вы изначально клонировали, и автоматически пытается слить `merge` их с кодом, над которым мы в данный момент работаем.
Однако, при определённых обстоятельствах, есть cмысл использовать команду:
```
git fetch <назвение незвание>
```
Эта команда связывается с указанным удалённым проектом и забирает все те данные проекта, которых у нас пока ещё нет. После того как мы выполнили команду, у нас должны появиться ссылки на все ветки из этого удалённого проекта, которые мы можем просмотреть или слить в любой момент.

Важно понимать, что когда мы клонировали репозиторий, команда `git clone` автоматически добавляет этот удалённый репозиторий под именем «origin». Таким образом, `git fetch origin` извлекает все наработки, отправленные на этот сервер после того, как мы его клонировали. принципиальным является то, что команда `git fetch` забирает данные в наш локальный репозиторий, но не сливает их с какими-либо нашими наработками и не модифицирует то, над чем вы работаете в данный момент. После выплнения команды нам необходимо вручную слить эти данные с нашими, когда это потребуется.
### 4. Отправка изменений в удалённый репозиторий
В случае, если мы хотим поделиться своими наработками в репозитории, нам необходимо отправить их в удалённый репозиторий. Для этого выполняем команду: 
``` 
git push <remote-name> <branch-name>
```
Чтобы отправить нашу ветку master на сервер origin (повторимся, что клонирование обычно настраивает оба этих имени автоматически), вы можете выполнить следующую команду для отправки ваших коммитов:
```
git push origin master
```
### 5. Просмотр удаленного репозитория
Для обычного просмотра содержимого удалённого репозитория используем команду:
```
git remote show
```
Однако, если мы хотим получить больше информации об одном из удалённых репозиториев, вы можете использовать команду:
```
git remote show <branch_name>
```
Выполнив эту команду с некоторым именем, например, origin, вы получите следующий результат:
```
remote origin
  Fetch URL: https://github.com/wargie/git_seminag_homewor_2.git
  Push  URL: https://github.com/wargie/git_seminag_homewor_2.git
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (fast-forwardable)
```
Команда выдала нам URL удалённого репозитория, а также информацию об отслеживаемых ветках, а так же сообщает, что если мы, находясь на ветке main, выполните `git pull`, ветка main с удалённого сервера будет автоматически влита в нашу сразу после получения всех необходимых данных. Она также выдаёт список всех полученных ею ссылок.
## Работа с `pull request`
Находясь в чужом репозитории на [GitHub](https://github.com/), в правом верхнем углу, нажать кнопку `Fork`.
![Fork](1.jpg)

Чужой репозиторий будет разветвлен и скопирован в наш аккаунт на [GitHub](https://github.com/)
![repo](2.jpg)

После этого, копию репозитория клонируем на наш компьютер. Для этого используем команду:
```
git clone <адрес удалённого репозитория
```
Сейчас, сделав необходимые правки, сделав коммит, сделав commit, загружаем изменения в свой репозиторий на [GitHub](https://github.com/). Для этого используем команды:
```
git add <file.name>
git commit -m "Change details"
git push 
```
После этого необходимо сделать _pull request_.

Для этого необходимо перейти на вкладку
`Pull Request`
![PullRequests_vkladka](3.jpg)

и справа вверху нажмите кнопку
`«New pull request»`.

![New pull request_knopka](4.jpg)

После этого требуется нажать кнопку
`«Create pull request»`.
![Create pull request_knopka](5.jpg)
Если есть необходимость, то следует добавить какой-либо комментарий к нашему `pull request`. После этого еще раз нажимаем кнопку `«Create pull request»`.

Pull Request отправлен!

P.S.

## ОГРОМНАЯ БЛАГОДАРНОСТЬ ОТ СТУДЕНТА
## С УВАЖЕНИЕМ, _**Гасанов Назим**_
