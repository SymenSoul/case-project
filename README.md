# Инструкция по работе с Git
## 1. Основы взаимодействия с консолью
Помимо типичного интрфейса (GUI) также есть взаимодействия с файлами через консольные команды. Их нужно знать и уметь ими пользоваться для того, чтобы пользоваться Git.

Для начала нужно открыть консоль. Её можно открыть либо через стандартное меню приложений (Пуск), либо сочетанием клавиш. У меня Linux, поэтому для меня это будет Ctrl+Alt+T. Если у тебя что-то другое, то лучше посмотри, как это делается у тебя. (Далее всё будет применяться касаемо Linux, однако зачастую такие же действия и команды будут работать и на других системах)

Команды, которые понадобятся:
```bash
pwd #Позволяет вывести текущую директорию
ls #Позволяет вывести на экран список файлов в текущей директории (папке)
cd /Имя_директории #Позволяет перемещаться между директориями ("cd .." - позволяет вернуться на уровень выше, "~" - по умолчанию обозначает домашнюю директорию)
touch #Для создания любого файла в текущей директории
mkdir #Для создания директории внутри текущей
rm, rmdir, rm -r #Различные варианты удаления: файла, директории, директории и всех файлов и директорий внутри
mv, cp #Перместить, копировать. Сначала прописывается что, потом прописывается путь куда
cat #Прочитать текстовый файл
```
## 2. Установка и настройка Git и подключение к GitHub
### 1. Установка
Когда ты уже разобрался с консолью и командами необходимо создать свой первый проект (просто папка с файлами). Далее нужно установить __Git__.

Для начала узнаем, установлен ли **Git** уже. Прописываем:
```bash
$ git version
```
Если он не установлен, то необходимо установить его, как любое консольное приложение через пакетный менеджер, который используется в твоей OS. У меня стоит ArchLinux, поэтому мне стоит лишь в очередной раз ~~порвать себе ***~~ прописать:
```bash
pacman -S git
```
Если у тебя Linux, то вот [тут можно](https://git-scm.com/download/linux) посмотреть консольные команды для установки Git в зависимости от твоей системы.

После установки Git в очередной раз проверяем его версию и если всё работает, то двигаемся дальше.
### 2. Настройка
В директории вашего первого проекта прописываем команду `git init`

Если всё хорошо, то она должна создать в директории папку .git, которая и будет означать, что Git настроен.

Далее мы создаём несколько файлов и уже используем git для синхронизации.
```bash
$ touch file1.txt file2.txt
$ git status
```
После этого мы увидим, что два файла в данной дирректории находятся в состаянии untracked. Для того, чтобы Git смог начать их отслеживать мы прописываем команду `git add`. После неё вписываем имена файлов (в данном случае file1.txt и file2.txt). Также, если нам нужно добавить абсолютно все файлы в дирректории, то можно просто прописать:
```bash
$ git add --all
```
Команда добавит сразу все файлы и начнёт отслеживать их содержимое. Однако это не позволит сохранить текущую версию файлов при их дальнейшем изменении и не позволит при необходимости откатиться назад. Для этого существует команда *git commit*. С помощью неё мы окончательно синхронизируем файлы, выполняется так называемый коммит. 
```bash
$ git commit -m 'Мой первый коммит!' #Ключ -m позволяет прописать дополнительное сообщение к выполненному коммиту. Обычно они содержат дельную информацию, например, о том, какой файл был изменён и т.д.
```
Если проводить аналогию для лучшего понимания, то **`git add` добавляет вещи в интернет магазине в корзину**, а **`git commit` уже совершает окончательную покупку**.

После нескольких совершённых коммитов можно посмотреть их историю с помощью команды `git log`.
### 3. Подключение к GitHub
#### 1. Регистрация
Для начала нужно зарегестрировать свой аккаунт на GitHub. Это делается так же, как и на любом другом сайте.

Далее зайдя в свой профиль на сайте необходимо создать новый репозиторий (Вкладка *Repositories*, нужно нажать кнопку *New*). Жмём далее и вкладка с ним откроется автоматически.
#### 2. Создание SSH-ключа
Один из наиболее распространённых сетевых протоколов — SSH (от англ. Secure Shell Protocol). Он обеспечивает безопасный обмен данными в сети.

SSH использует пару ключей для обеспечения безопасности — публичный и приватный: 
Приватный ключ (англ. private key) хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для расшифровки данных.
Публичный ключ (англ. public key) доступен всем и используется для шифрования данных. Они могут быть расшифрованы парным приватным ключом.

Для начала узнаем, есть ли уже сгенерированные SSH-ключи. Если в домашней директории нет папки *.ssh*, то вам нужно генерировать ключ, если есть, то пропусти этот шаг.

**ИНСТРУКЦИЯ ПО ГЕНЕРАЦИИ SSH-КЛЮЧА**
Вводим в консоль:
```bash
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
```
Далее просто нажимаем Enter, если нет необходимости создавать ssh-ключ не в домашнем каталоге. И так же оставляем поле пустым, если нет необходимости в установке пароля для вашего ssh-ключа.
#### 3. Привязка ключа к GitHub
 Когда ключи готовы, то нам необходимо скопировать содержимое ключа с расширением *.pub*.

 Далее заходим на GitHub и в настройках добавляем содержимое публичного ключа в соответствующее поле.

 После этого в консоли прописываем:
 ```bash
 $ ssh -T git@github.com
 ```
 Если ключ совпадает с одним из тех, что есть на странице [по этой ссылке](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints), то пишем *yes*.

#### 4. Связываем локальный и удалённый репозиторий
Для того, чтобы связать локальный и удалённый репозитории прописываем `git remote add`
```bash
$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git
```
Осталось убедиться, что репозитории связаны с помощью команды — `git remote -v`

#### 5. Синхронизируем локальный и удалённый репозиторий
Теперь нужно отправить изменения на удалённый репозиторий. Для этого мы прописываем в первый раз `git push -u origin main`. Далее мы просто будем прописывать `git push` 

P.S. В первый раз эту команду нужно вызвать с флагом `-u` и параметрами `origin` (имя удалённого репозитория) и `main` или `master` (название текущей ветки). Флаг `-u` свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории в предыдущем уроке, так же и здесь нужно дополнительно связать ветки.

#### 6. Файл README.md
Чтобы другие пользователи, а также потенциальные клиенты или работодатели могли понять, что представляет собой проект, его нужно описать. Такое описание принято указывать в файле `README.md`.

Преимущество `README.md` в том, что средства командной работы (такие, как GitHub) могут отображать его содержимое в браузере в виде удобной разметки. Для этого нужно не просто залить текст, но и настроить шрифт, заголовки и отступы с помощью markdown. Маркда́ун — это специальный язык разметки. Он позволяет красиво отформатировать текстовый документ.

Вдаваться в подробности синтаксиса Я не буду, тк это займёт много времени. Кратко и быстро о нём можно почитать, например, [здесь](https://www.markdownguide.org/basic-syntax/)
## 3. Навигация по Git
### 1. Хэш и HEAD
У каждого коммита есть свой хэш. Мы можем видеть его после того, как прописали `git log` вверху каждого коммита.

Хэш это идентификатор, который содержит в себе информацию об авторе, времени коммита, сообщении и самом изменении. Для хэширования используется SHA-1.

Если нужно вывести список всех коммитов, но коротко, то можно прописать `git log --oneline`

Путь к хэшу последнего коммита хранится в файле `HEAD`. Так же сам Git при ссылке на HEAD поймёт, что имеется ввиду последний коммит.
### 2. Статусы файлов в Git
Статусы `untracked`/`tracked`, `staged` и `modified`

`untracked` - изменения файлов не отслеживаются

`staged` - файлы в списке на коммит

`modified` - файлы были изменены по сравнению с предыдущим `git add`

`tracked` - последние изменения файлов закоммичены

Путь файла в системе Git:
```mermaid
stateDiagram-v2
    direction LR
    state "<b>untracked</b><br>(неотслеживаемый)" as s1
    s2 : <b>staged</b><br>(в списке на коммит)<br>+<b>tracked</b>
    s3 : <b>tracked</b><br>(отслеживаемый)
    s4 : <b>modified<br>(изменённый)
    s1 --> s2: git add
    s2--> s3: git commit
    s3 --> s4: Изменения в файле
    s4 --> s2: git add
    s2 --> s4: изменения
```
### 3. Как читать git status
Команда `git status` может показать только следущие состойния файлов
* `staged`(`Changes to be committed` в выводе `git status`);
* `modified` (`Changes not staged for commit`);
* `untracked` (`Untracked files`).
### 4. Оформление сообщений к коммитам
Есть общие рекомендации по тому, как правильно составить сообщение. Оно должно быть:
* относительно коротким, чтобы его было легко прочитать;
* информативным.

Пример неинформативного сообщения: `bug fix`

Пример информативного сообщения: `feat: exit button now red`

Также существуют различные правила и стили, которые приняты в команде или даже во всей компании. Однако существует стандарт Conventional Commits, который отличается качетсвенной документацией и подробной проработкой. 

Он предлагает такой формат коммита: `<type>: <сообщение>`. Подробнее можно ознакомиться с данным стандартом [на оффициальном сайте с описанием этого стиля](https://www.conventionalcommits.org/ru/v1.0.0-beta.4/#%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F)

Для сообщений на английском рекомендуется использовать **повелительное наклонение** (англ. *imperative*). Например: `Use library mega_lib_300`, `Fix exit button` и так далее.
