---
layout:     post
title:      "Как использовать консоль в&nbsp;Windows"
subtitle:   "Как перестать беспокоиться и&nbsp;полюбить консоль на&nbsp;Windows, если Вы&nbsp;—&nbsp;фронтендер"
permalink:  /page/:title
categories: web
---

Предполагается, что вопрос «зачем?» уже не стоит. Мне в моей работе консоль нужна для автоматизации сборки фронтенда (компиляция препроцессоров, сборка спрайтов, оптимизация кода и т.п.).

Будем ставить Git Bash ([Git](https://git-scm.com/) — система контроля версий, он нам очень пригодится в работе и поставляется с консолью Git Bash) и [cmder](http://cmder.net/) (эмулятор консоли, позволяющий использовать несколько разных консолей, имеющий вкладки, нормальную работу с буфером обмена и прочие плюшки).

## Почему не Power Shell

Power Shell — неплохая консоль, встроенная в Windows. Однако, среди веб-разработчиков множество пользователей OS X и Linux — эти ОС более стабильны, безопасны, а Linux — еще и на пару порядков более распространен на серверах, в сравнении с Windows. На OS X и Linux «из коробки» есть вменяемые консоли, имеющие много общего. Привыкайте сразу к хорошему, функциональному и универсальному.

Лично я, во-первых, всерьез исследую возможность выноса всей работы с автоматизацией фронтенда в виртуальную машину с Ubuntu (я бы перешел на Ubuntu полностью, но Photoshop не позволяет), а во вторых, мой рабочий компьютер Windows 10, а ноутбук — старенький MacBook Air и хочется иметь хоть какую-то унификацию работы с консолью.

## Как получить нормальную консоль

1.  Скачать и установить [Git](https://git-scm.com/download/win) (если еще не ставили). Установщик спрашивает добавлять ли в контекстное меню проводника пункты запуска Git Bash и Git GUI. Я отказался, ибо планирую использовать эмулятор консоли. Прочее можно оставить по умолчанию.
2.  Скачать с [http://cmder.net](http://cmder.net/) mini-версию и распаковать в `C:/cmder` . Запустить `C:/cmder/Cmder.exe` от имени администратора (безразлично что именно он напишет при первом запуске), нажать Win + Alt + P для перехода к настройкам.
3.  В настройках: Startup → Tasks. Нажать кнопку Add dafault tasks... для добавления задач по умолчанию. В списке Predefined tasks (это все возможные к запуску внутри эмулятора консоли) появится несколько дополнительных пунктов, среди которых должен быть `{Bash::Git bash}` (иногда таких пунктов два).
4.  В настройках: Startup → выбираем радиокнопку Auto save/restore opened task. Теперь при открытии cmder Вы будете видеть вкладки с теми же консолями, с которыми работали перед закрытием. Сохранить.
5.  В главном окне программы нажать Ctrl + T для создания новой вкладки с консолью и в секции Create new console выбрать `{Bash::Git bash}` . При необходимости, можно поставить флажок «run as Administrator».
6.  Закрыть открытую изначально вкладку (самая первая, почти наверняка, powershell.exe) кликом средней кнопки мыши или из контекстного меню вкладки.

## Как использовать полученную консоль

Тут важно понимать, с чем работаешь. Консоль — возможность «текстового» общения с компьютером: набираем команду — получаем реакцию. Если набранная команда запускает какой-то постоянно выполняющийся процесс (веб-сервер, к примеру), остановить выполнение можно по Ctrl + C. Да-да, то самое «копировать». Как же скопировать что-то из консоли? — спросите Вы. С cmder — просто выделите нужный фрагмент мышью и он окажется в буфере обмена. Crtl + V работает штатно («вставить»).

Чаще всего, мы набираем какую то команду и передаваемый ей параметр (один или несколько) и/или ключи (указания как ей работать). Иногда, сразу же набираем еще несколько команд, разделяя их символами `&&` (команды будут выполнены в набранной последовательности, это не единственный возможный разделитель).

Для команд, которые используются часто, можно придумать сокращения (алиасы), чтобы вызывать их быстрее.

### Файловая система

Пользователь всегда находится в какой-то папке. К примеру, Вы видите в консоли: `nikname@computer /c/cmder` — значит сейчас Вы в папке `C:/cmder` . Чтобы перейти в другую папку, наберите команду `[cd](https://ru.wikipedia.org/wiki/Cd_(%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0))` и укажите ей абсолютный или относительный путь — куда переходить. К примеру:

*   `cd projects` — переход в папку projects, которая есть текущей папке
*   `cd /d/projects` — переход в папку projects, расположенную по адресу `D:/projects`
    (где бы не находился пользователь)
*   `cd /c/Program Files` — переход в `C/:Program Files`
    (пробел в имени папки экранирован)
*   `cd ..` — переход к к родительской папке
    (вверх на 1 уровень)
*   `cd -` — переход к последней рабочей папке
    (что-то вроде команды «назад»)

Чтобы не набирать имя папки целиком, наберите первые пару символов и нажмите Tab — произойдет автодополнение (если нет двух папок, начинающихся с введенных символов, иначе будут показаны сами эти папки).

#### Посмотреть содержимое папки позволяет команда [ls](https://ru.wikipedia.org/wiki/Ls):

*   `ls` — показать содержимое папки
    (сортировка по имени, папки и файлы вперемешку, несколько столбцов)
*   `ls -a` — то же, но показывать и скрытые файлы и папки
*   `ls -a -1` — то же, но в один столбец
*   `ls -hF -1 --sort=extension` — показать содержимое папки «красиво, в один столбец»
*   `ls build/css` — показать содержимое папки `ТЕКУЩАЯ_ПАПКА/build/css`

#### Создание папок и файлов — команды [mkdir](https://ru.wikipedia.org/wiki/Mkdir) и [touch](https://ru.wikipedia.org/wiki/Touch).

*   `mkdir project` — создать папку с именем «project»
*   `mkdir project project/css project/js` — создать несколько папок
*   `mkdir -p project/{css,js}` — то же, что выше
*   `touch index.html` — создать файл
*   `touch index.html css/style.css js/script.js` — создать файлы
    (папки `css/` и `js/` должны уже существовать)

#### Копирование файлов — команда [cp](https://ru.wikipedia.org/wiki/Cp)

*   `cp index.html catalog.html` — копирование файла index.html в тот же каталог с переименованием в `catalog.html`
*   `cp index.html old/` — копирование файла `index.html` в папку `old/`
    (все произойдет в текущей папке)
*   `cp temp/ temp2/ -r` — копирование каталога

#### Переименование или перемещение файлов — команда [mv](https://ru.wikipedia.org/wiki/Mv)

*   `mv index.html old` — перемещение файла в папку
*   `mv index.html old/new_name.txt` — перемещение файла в папку с переименованием файла
*   `mv order.txt orderNew.txt` — переименовать файл

#### Удаление папок и файлов — команда [rm](https://ru.wikipedia.org/wiki/Rm)

*   `rm ghost.png` — удалить файл
*   `rm -rf old` — удалить папку и все из нее

#### Разные мелочи (как вдохновение для последующего изучения консольных команд):

*   `df -h` — показать статистику использования пространства на дисках
*   `grep -i -n --color 'carousel' index.html css/style.css` — найти слово `carousel` в двух указанных файлах (с игнором регистра), вывести строки с этим словом и номера строк (искомое слово подсветить)
*   `find . -iname '*ind*'` — найти в текущей папке (и подпапках) все файлы, имена которых содержат `ind` и показать списком
*   `ls -a | tee file.txt` — записать в `file.txt` результат вывода команды `ls -a`

### Алиасы

Для команд можно создавать алиасы (синонимы). Для этого в файл `C:/Users/ИМЯ_ПОЛЬЗОВАТЕЛЯ/.bashrc` нужно вписать строки, наподобие `alias subl='/c/Program Files/Sublime Text 3/sublime_text.exe' $*` (одна строка в файле — один алиас). Приведенный пример создает команду `subl` , которая открывает переданный ей файл или папку в Sublime Text 3 (будет работать если путь установки ST3 совпадает с прописанным в алиасе). Если этой команде ничего не передать, она просто откроет Sublime Text 3.

Применительно к `subl` , разумнее [добавление его в PATH](http://nicothin.pro/page/windows-path)

*   `alias pro='cd /d/projects'` — перейти к папке `d:/projects/` (у меня это папка для всех проектов)
*   `alias s='npm start'` — сокращение для команды запуска сервера
*   `alias ls='ls -hF -1 --color=tty --sort=extension'` — вывод файловой структуры в столбец, сначала папки, потом файлы, с цветовой подсветкой

ВНИМАНИЕ: чтобы алиасы, добавленные в `c:/Users/ИМЯ_ПОЛЬЗОВАТЕЛЯ/.bashrc` заработали, нужно перезапустить консоль.

### Мелкие хитрости

*   Ctrl + ~ — показать или скрыть консоль
*   Ctrl + L — очистить экран
*   Ctrl + U — полностью убрать всю набранную команду
*   Ctrl + R — поиск по истории команд
*   Alt + ←/→ — перемещение курсора по словам набранной команды

Кнопки клавиатуры «стрелка вверх» и «стрелка вниз» — переход по истории введенных команд (удобно для повтора команды с чуть измененными параметрами).

[Можно](https://youtu.be/InDJwlCULuQ?t=53s) использовать команду `subl index.html:73` — откроется указанный файл и курсор поместится на 73-ю строку (удобно после консольного поиска по файлу). А по `subl .` в Sublime Text откроется текущая папка (будет показана в сайдбаре).

## Важный момент

Не рекомендуются использовать кириллические символы в имени и пути рабочей папки (общей папки для всех проектов), равно как в папке с именем пользователя (которая `c:/Users/ИМЯ_ПОЛЬЗОВАТЕЛЯ/.bashrc` ), ибо на Windows это может вызвать непредсказуемое поведение консольных утилит (да, лучше создать нового пользователя, если при установке Windows Вы указали кириллическое имя).

## Заключение

Если Вы уже используете консоль на Windows, поделитесь опытом.