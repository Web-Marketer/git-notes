# Шпаргалка по Git

## Работа с Git

### Начало работы
- **```git init```** — создать локальный репозиторий в текущей папке
- **```rm -rf .git```** - удалили подпапку .git («Разгитить» папку)
- - **ключ ```-r```** (от англ. recursive — «рекурсивно») позволяет удалять папки вместе с их содержимым;
- - **ключ ```-f```** (от англ. force — «заставить») избавит вас от вопросов вроде «Вы точно хотите удалить этот файл? А этот? И этот тоже?».

### Последовательность действий с новым проектом

1. Создаем папку проекта локально
2. **```git init```**
3. Добавляем файлы проекта
4. **```git add -A```**
5. **```git commit```**
6. Создаем удаленный репозиторий (например, на GitHub)
7. **```git remote add origin <ссылка на удаленый репозиторий>```** — связываем локальный и удаленный репозитории (удаленный будет называться origin)
8. **```git remote -v```** - убедиться, что локальный и удаленный репозитории связаны
9. **```git push -u origin master```** - отправляем первый коммит в ветку master удаленного репозитория + фиксируем сокращенную команду **```git push```**, чтобы не добавлять каждый раз origin master

### Последовательность действий при подключении к существующему проекту

1. Создаем папку проекта локально
2. **```git clone <ссылка на удаленный репозиторий> <ссылка на локальный репозиторий```** - клонируем удаленный репозиторий (создастся новая папка)
3. **```git remote show <remote>```** - для получения удаленных веток и дополнительной информации из удаленного репозитория:
4. **```git pull```** - тоже самое что git fetch + git merge (загрузить коммиты, файлы и ссылки из удаленного репозитория + сделать их слияние с текущей веткой)

### Работа с изменениями
- **```git status```** — Проверить состояние репозитория
- **```git add file.txt```** — добавить в индекс файл file.txt (подготовить к коммиту)
- **```git add --all```** — добавить в индекс все измененные файлы/папки (подготовить к коммиту)
- **```git add dir```** — добавить в индекс папку dir (подготовить к коммиту)
- **```git add .```** — добавить в индекс все измененные файлы/папки в текущей папке (подготовить к коммиту)
- **```git commit -m 'Описание коммита'```** - зафиксировать изменения (закоммитить)
- **```git cm 'Описание коммита'```** - краткая версия git commit -m 'Описание коммита'
- **```git push origin master```** - отправить новые коммиты в ветку master удаленного репозитория origin
- **```git log```** - посмотреть историю коммитов
- **```git log --oneline```** - Получить сокращённый лог (первые несколько символов хеша каждого коммита и их комментарии)
- **```git diff <keys> <path to file> <path to file>```** - просмотреть различия между коммитами
- **```git diff origin/master```** - сравним локальную ветку с обновленной удаленной веткой, чтобы увидеть различия:
- **```git fetch```** - получить коммиты, файлы и ссылки текущий репозиторий. Команда не вынуждает выполнять слияние изменений с текущим репозиторием.
- **```git fetch --dry-run```** - проверяем работу git fetch без дальнейшего обновления каких-либо локальных веток (для теста и просмотра изменений, которые будут получены в результате выполнения git fetch)
- **```git branch <название ветки>```** - создать новую ветку

### Ветвление

- **```git branch <название ветки>```** - создать новую ветку
- **```git checkout <название ветки>```** - переключиться на ветку (файлы и папки в репозитории изменятся до стстояния этой ветки)
- **```git checkout -b <название ветки>```** — создать новую ветку и переключение на нее
- **```git merge source```** - влить ветку source в текущую ветку
- **```git checkout branch -- folder```** - извлечь отдельный файл/папку folder из другой ветки и получить его, предварительно перейдя в ту ветку, куда вы собираетесь перенести файл (branch)

### SSH

- **```ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"```** — cгенерировать SSH-ключи
- **```ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" ```** — cгенерировать SSH-ключи (альтернативный вариант)
- **```pbcopy < ~/.ssh/id_ed25519.pub```** - скопировать содержимое ключа id_ed25519.pub в буфер обмена
- Добавляем ключ в GitHub: аватарка / Settings / SSH and GPG keys / New SSH key
 - **```ssh -T git@github.com```** - Проверить правильность ключа для GitHub

## Статусы
- **untracked** - неотслеживаемый
- **staged** - подготовленный (войдет в коммит)
- **modified** - измененн, но не подготовлен к добавлению в следующий коммит
- **tracked** - все отслеживаемые файлы

```mermaid
graph LR;
  untracked -- "git add" --> staged;
  staged    -- "???"     --> tracked/comitted;

  A[modified + git add] --> B[staged]
```

## Прочее

- HEAD — файл в папке .git, в котором записана ссылка (или ссылка на ссылку) на последний коммит. Это синоним хеша последнего коммита — его можно передавать командам Git в качестве параметра.

## Базовые команды в консоли

### Навигация

- **```pwd```** — покажи, в какой я папке;
- **```ls```** — покажи файлы и папки в текущей папке;
- **```ls -a```** — покажи также скрытые файлы и папки, названия которых начинаются с символа .;
- **```cd папка```** — перейди в папку "папка";
- **```cd папка/html```** — перейди в папку html, которая находится в папке "папка";
- **```cd ..```** — перейди на уровень выше, в родительскую папку;
- **```cd ~```** — перейди в домашнюю директорию (/Users/Username);
- **```cd /```** — перейди в корневую директорию.

## Работа с файлами и папками

### Создание

- **```touch index.html```** — создай файл index.html в текущей папке;
- **```touch index.html style.css script.js```** — если нужно создать сразу несколько файлов, можно напечатать их имена в одну строку через пробел;
- **```mkdir second-project```** — создай папку с именем second-project в текущей папке.

### Копирование и перемещение

- **```cp file.txt ~/my-dir```** — скопируй файл в другое место (~/my-dir);
- **```mv file.txt ~/my-dir```** — перемести файл или папку в другое место (~/my-dir).

### Чтение

- **```cat file.txt```** — распечатай (покажи) содержимое текстового файла file.txt.

### Удаление

- **```rm about.html```** — удали файл about.html;
- **```rmdir images```** — удали папку images;
- **```rm -r second-project```** — рекурсивное удаление = удали папку second-project и всё, что она содержит.

### Полезные возможности

 - Команды необязательно печатать и выполнять по очереди. Можно указать их списком — разделить двумя амперсандами (&&).
 - У консоли есть собственная память — буфер с несколькими последними командами. По ним можно перемещаться с помощью клавиш со стрелками вверх (↑) и вниз (↓).
 - Чтобы не вводить название файла или папки полностью, можно набрать первые символы имени и дважды нажать Tab. Если файл или папка есть в текущей директории, командная строка допишет путь сама.
Например, вы находитесь в папке dev. Начните вводить cd first и дважды нажмите Tab. Если папка first-project есть внутри dev, командная строка автоматически подставит её имя. Останется только нажать Enter.