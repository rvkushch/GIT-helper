# GIT-helper

You can download git here: http://git-scm.com/downloads

Install Git with default settings.

Generating a pair of ssh keys:

     ssh-keygen -t rsa –C “@example.mail"

The public key (id_rsa) should be sent to the owner of the repository in order to obtain work rights. Or upload to profile settings in bitbucket / github / gitlab.

Username and email settings:

     git config --global user.name “your name“

     git config --global user.email “your email"































Убрать ненужные папки из слежения на примере node_modules:
1. Touch .gitignore - создать, если отсутствует. 
2. echo and >> node_modules/
3. git rm -r --cached node_modules 
4. git status - убедиться в изменениях

git status displays the new changes. A change to .gitignore will appear, while node_modules will not appear as it is no longer being tracked by git.



GIT - global information tracker, cvs - сontrol version system. Используется для осуществления контроля за всеми изменениями файлов, сохраняя при этом предыдущее состояние для сравнения или отката. 

1. Открываем командную строку в необходимой папке, или переходим к ней. инициализируем (превращаем папку) в локальный репозиторий командой "git init" или клонируем репозиторий с сайта "git clone github://path.git"

2. Используем комаду "git status для определения актуального состояния файлов в репозитории(not tracked, staged, commited). Добавляем файлы для слежениz за изменениями командой "git add" и перечень файлов или папок которые нужно загрузить (через пробел) или если нужно отслеживать изменения во всех файлах то через "git add ." или "git add <file>" для 1-го файла или убрать определенный файл из трека "git -rm cached <file>". Если не хотим следить за определенным файлом ставим его в игнор: создаем файл, в котором будем хранить игнорируемые файлы командой "touch .gitignore", затем создаем игнорируемый файл "touch pass.txt". 
Также важно убедиться, что находимся в ветке по умолчанию "git checkout master". Если возникает error: pathspec, ипользовать git checkout -b yourbranchname. Также командой "git status" можно узнать, на какой ветке (branch) репозитория мы находимся, какие изменения присутствуют.

3. Добавляем коммит (сохранение и описание внесенных изменений) к файлу командой "git commit -m "release v.1" (m - message).
Узнать историю коммитов можно командой "git log". Узнать самые последние коммиты командой "git diff". Сбросить файл к последней версии "git checkout -- 'filename'". Чтобы выбрать и изменить самый последний коммит используется команда "git commit --amend"

Лучше всего производить изменения, добавлять или изменять функционал, создав заранее отдельную ветку, чтобы не влиять на основную. Для этого используется команда "git branch my_new_branch", созданная ветка копирует всю информацию главной. После создания переключаемся на нее (switch): "git checkout my_new_branch" или для cоздания и перехода сразу "git checkout -b my_new_branch" (b - branch). Каждая ветка имеет свою историю изменений. Чтобы удалить ненужную ветку "git branch -d my_new_branch".

Для обьединения изменений новой созданной ветки и главной (master) используется команда merge: 
"git chekout master" - переходим к главной ветке
"git merge my_new_branch" - обьединяем. 

4. Получаем доступ к удаленному репозиторию в который хотим запушить файлы командой "git remote add origin https://github.com/path"
и используем команду "git pull origin master --allow-unrelated-histories" для соединения историй 2 несвязанных до этого репозиториев(папок). При данной команде также в созданную локальную папку копируется содержимое репозитория, к которому мы получили доступ.

5. Командой "git push -u origin master"(origin это remote - удаленная ветка, origin - локальная, u - для сохранения параметров пуша на след. раз) пушим необходимые файлы в репозиторий. Если при создании нового репозитория файл readme.md уже был создан, то следует указать "git push -f origin master" (форсированный пуш). Не стоит использовать его если в файле уже имеются записи других участников разработки. Если возникают ошибки стоит попробовать переназначить пользователя и мыло: 
"git config --global user.name "username""
"git config --global user.email user@email.com"
либо переустановить Git. 



6. Если мы клонируем репозиторий с гита, то для нормальной работы следует установить все необходимые зависимости, узнать недостающие можно в package.json > dependencies.

7. При необходимости откатиться к определенному состоянию проекта, следует использовать команду "gitk --all&" (открыть графическую оболочку гита), удалив перед ней файл 'package-lock.json' который будет мешать откату, после чего сделать копию идентификатора нужного коммита (ctrl+ins) и командой "git checkout commitID" (вставить айди коммита shift+ins) переключаемся на определенную ветку состояния. После переключения бранчей состояния важно закоммитить изменения. Если нам нужно отменить новые внесенные изменения следует использовать команду "git status" с помощью который мы узнаем о всех изменениях и пути к измененным файлам, после чего командой "git checkout путь к файлу" можем убрать новые изменения.
