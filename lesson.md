![logo](4844446.png)
# Работа с GIT

## 1. проверка наличия установленного GIT на компьютере
В терминале выполнить комманду `git version`
Если GIT устоновлен, то появился сообщение о версии программы, инче будет сообщение об ошибке.

## 2. Установка GIT
Загружаем последнюю версию GIT с сайта https://git-scm.com/downloads. Устанавливаем с настройками по умолчанию.

## 3. Настройка GIT
При первом использовании GIT необходимо представиться
Для этого нужно выполнить 2 команды в терминале
```
git config --global user.name "Ваше имя на английском языке"
git config --global user.email "Ваша почта"
```

## 4. Инициализация репозитория
Для начала работы нам необходимо определить паку в которой мы будем производить создание и редактирование файлов, изменение которых хотим отслеживать - репозиторий.
Для этого нм нужно ввести команду `git init`

## 5. Запись изменений в репозиторий status add commit diff

Далее нам требуется:
* определить внутри папки файл который мы отслеживаем - команда `git add "имя файла с расширением"` 
* ! Мы это делаем при каждом сохранении новой версии файла, либо используем параметр **-a** в команде `git commit`
* после того как мы показали программе GIT изменения в каком файле мы хотим сохранить, мы сохраняем сами изменения используя команду `git commit` и параметр **-m "text"** для внесения комменартия чем эта версия отличается от предыдущих. Вот два примера использования этой команды:
1. `git commit -m "new inf"` - сохранили версию файла и написали комментарий *new inf*.
2. `git commit -a -m "new inf"` - сохранили изменнения в текущем файле (без его принудительного выбора и написали комментарий *new inf*)
* если мы хотим увидеть какие изменения в файле были осуществленны, то мы используем команду `git diff`
! Если при использовании этой команды или какой-то иной у вас в окне терминала пропала сторока для ввода команд это значит, что сообщение очень длинное и вы можете:
1. перемещаться по сообщению используя стрели вверх или вниз
2. выйти из этого сообщения используя клавишу q.
* отдельно скажу, что вы всегда можете проверить статус файлов которые сохранены у вас в Репозитарии (отслеживается по ним изменение или нет) командой `git status` и по ее информации добавить нужный файл к отслеживанию. Какой командой? Правильно `git add "имя файла с расширением"`  

## 6. Просмотр истории сохранений log

Для того чтобы посмотреть историю сохраненных версий вы можете выполнить команду `git log`. При этом вы можете:
* вывести на экран всю инфорамацию: хеш-код изменений, комментарии к изменению, кто их автор и когда эти изменения были сделаны, просто написав `git log`
* или использовать сокращенный вариант вывода инфрмации: хеш-код изменений и комментарий к ним `git log --oneline`
! Если при использовании этой команды или какой-то иной у вас в окне терминала пропала сторока для ввода команд это значит, что сообщение очень длинное и вы можете:
1. перемещаться по сообщению используя стрели вверх или вниз
2. выйти из этого сообщения используя клавишу q.

## 7. Перемещение между сохранениями checkout + хеш-код и checkout master 

Для тогда чтобы посмотреть состояние файла в любой из сохраненных версий нам требуется загрузить его. Именно для этого нам нужны хеш-коды, причем нам достаточно указать первые 4 значения и мы перейдем в эту версию файла.

* для этого используется команда `git checkout "хеш-код, без ковычек"`
* если мы хотим вернуться к последней версии редактируемого файла, то мы используем команду `git checkout master`
* ! Обратите внимание, что пока вы не сохраните текущие изменения в файле командой `git commit`, вы не сможете выполнить команду `git checkout "хеш-код, без ковычек"` и перейти к более ранней версии файла.

## 8. Игнорирование файлов
Для того чтобы исключить из отслеживания в репозитории определенные файлы или папки необходимо в репозитории создать файл ***_.gitignore_*** и записать в него названия или шаблоны тем файлам или папкам, которые мы хотим игнорировать.

## 9. Создание веток в Git

Ветка Git - это простой перемещаемы указатель на одно из сохранений, обычно последний в цепочке коммитов.
По умолчанию имя основной ветки в Git - **master**.

Создать ветку можно командой:
```
git branch <имя новой ветки>
```
В результате создается новый указатель на текущий коммит.

Список веток в репозитории можно посмотреть с помощью команды
```
git branch
```
Текущая ветка будет отмечена (*): **\*master** 

*А как ещё можно создать новую ветку?*
Для того чтобы создать ветку и сразу перейти на нее можно использовать команду
```
git checkout -b <NewBranch>
или
git switch -c <NewBranch>
```
Между командами *checkout* и *switch* есть некоторая разница, о которой я расскажу в одном из следующих разделов.

Если нам требуется переименовать текущую ветку, то мы используем параметр -M (большая M)
```
git branch -M NewName
```

## 10. Слияние веток и разрешение конфликтов
Для слияния выбраной ветки с текущей. нужно выполнить команду
```
git merge <название выбранной ветки>
```
Если была изменена одна и та же часть файла в обеих ветках, то может возникнуть конфликт, который при слиянии потребует участия пользователя. VS Code предлагает варианты решения:
1. Принять текущие изменения
2. Принять входящие изменения
3. Принять оба изменения
4. Сравнить изменения

Выбранное решение записывается в ветку, для которой происходит сохранение и является итоговым.
После разрешение кофликта требуется сохранение итогово состояния!

## 11. Удаление веток.
После того, как вы сохранили информацию в основной версии файла, по-умолчанию это ветка __master__ и созданная ветка вам не требуется для дальнейшей работы, то вы можете ее удалить, используя команду:
```
git branch -d <NameBranch>
```
Обратите внимание, что в качестве параметра может выступать малая буква **-d** или заглавная **-D**.

При использовании **-d**, система проверит статус сохраненя информации в текущей ветки в основною и не даст ее удалить, пока такой перенос не будет выполнен. А **-D**, удалит информацию в любом случае.

**Будьте внимательны при выборе параметра!**

После удаления ветки, без внесения каких-либо изменений в любую другую ветку не происходит сохранение нового состояния.

Без внесения любой информации, сохранения не происходит.

тестовый текст перед удалением ветки без внесения инфомации из нее.

```
Запустил git log --graph --oneline и не вижу информацию и предыдущем сохранении.
$ git commit -am "добавили текст в строке 105 для промежуточнго сохранения перед удалением с параметром -D"
[branch_11_1 b2f4c22] добавили текст в строке 105 для промежуточнго сохранения перед удалением с параметром -D
 1 file changed, 1 insertion(+), 1 deletion(-)
```

## 12 Работа со своим удаленным репозиторием
1. Создаем или входим в аккаунт на GitHub
2. Создаем удаленный репозиторий на GitHuB.com
    * Для этого в своём профиле выбираем раздел *Your repositories*, переходим на страницу, где сохранены все ваши рабочие репозитории и в правом верхнем углу нажимаем зеленую кнопку <span style="color:green"> **NEW**.</span>
    * Далее в графе *Repository name* вводим имя нового репозитория на **английском языке**.
    * Оставляем "галочку" в пункте **Public**
    * Листаем в самый низ и нажимаем кнопку <span style="color:green"> **Creat repository**.</span> 
    * после этого мы автоматически попадем в окно с <span style="color:red"> **подсказками**</span>  о том, что нам делать далее.
3. Открываем в Visual Studio Code папку в которой будем сохранять данные с удаленного репозитория, расположенного на **GitHub.com** и выполняем одну из <span style="color:red"> **подсказок**</span>.    

 Связать удаленный репозиторий на GitHuB.com с локальным репозиторием можно выполнив команду:
```
git remote add <имя для репозитория> <url-адрес репозитория>
```
* <имя для репозитория> - пишите любое имя, оно не является названием репозитория, которое мы создавали ранее в графе *Repository name*. Чаще всего использут имя **origin** 
* <url-адрес репозитория> - это адрес где ваш репозиторий будет храниться на GitHub-е. Он состоит из следующих частей:
```
1. https://github.com/
2. BudyakSergey/ - ваш ник на GitHub
3. name.git - имя созданного репозитория
https://github.com/BudyakSergey/name.git
```
* <span style="color:red"> Если мы сохраняем удаленный репозиторий в новую папку на компьтере, то нам нужно ее инициализиторовать <span style="color:green"> **git init** </span> </span>.

При выполнении любой из двух подсказок мы  переименовываем ветку **master** в **main**
```
git branch -M main
```
и загружаем удаленный репозиторий командой
```
git push -u origin main
где
*origin* - имя репозитория
*main* - имя загружаемой ветки
``` 
4. После того, как оба ваши репозитория связаны вы можете сохранять изменения с локального в удаленный и с удаленного в локальный.
* Для отправки данных с локального на удаленный репозиторий, используется команда
  * git push
* Для сохранения в локальном репозитории информации с удаленного, используется команда
  * git pull

## 13 Работа с чужим удаленным репозиторием

GitHub позволяет нам работать с чужими репозиторием, только после того как мы сохраним его в своём аккуанте. После этого мы вносим требуемые изменения **! вновую ветку** и отправляем наш репозиторий (наши предложения) автору исходного репозитория.
1. Находим нужный для редактирования репозиторий:
* в строке поиска
* перейдя по ссылке, которую получили от автора
2. Переходим на страницу репозитория и нажимаем кнопку **Fork**. После этого мы попадем на страницу создания нового удаленного репозитория в своей аккаунте на GitHub.
3. Создаем:
  * на компьютере папку в которую будет копировать удаленный репозиторий.
  * инициализируем её для работы с Git
  ```
  git init
  ```
  * копируем удаленный репозиторий в локальный
  ```
  git clone https://github.com/ваш_аккаунт_GitHub/название_редактируемого_репозитория

  git clone https://github.com/BudyakSergey/name.git
  ```
  * если скопированный репоизиторий был перенесен на локальный компьютер в отдельную папку, то нужно в эту папку перейти
  ```
  cd <имя папки>
  ```
  * в локальном репозитории переименовываем ветку **master** в **main**
```
git branch -M main
```
  * в локальном репозитории создаём новую ветку 
```
git branch <имя ветки>
```
* переходим в нее и вносим нужные нам изменения.
```
git checkout <имя ветки>
```
4. Добавляем файл/-лы в котором/ых вносили изменения или редактировали в статус для отслеживания командой **git add** и сохраняем наши изменения **git commit -m "_text_"** 
5. Отправляем данные с локального репозитория в удаленный
```
git push -u <имя репозитория> <имя ветки>
```
* <имя репозитория> - чаще всего *origin*
* <имя ветки> - которую мы создали в пункте 3.
Таким образом наши локальные изменения сохраняются на удаленном репозитории, в новой ветке.
6. Переходим на сайт GitHub, выбираем редактируемый репозиторий (у него будет пометка <span style="color:red"> **forked from <имя автора/название его репозитория**</span> и вверху находим кнопку кнопку **Pull requests**. Далее нажимаем зеленую кнопку <span style="color:green"> **New Pull requests**</span> и выбираем имя нашей ветки (в которой мы вновисли изменения) в раскрывающемся списке **compare** и отправляем данные автору.
* результатом должна быть надпись в новом окне **This branch has no conflicts with the base branch** и <span style="color:green"> **зелёная галочка**</span> 



Итоговое сохранение

Описание языка markdown
https://docs.microsoft.com/ru-ru/contribute/markdown-reference


Порядок цифр написанный в тексте не влияет на порядок в итоговом отображении, если мы не выделяем поле тремя знаками ` (в файле зачения цифр 1. 1. 4.)

1.
1.
4.
Если идет выделение, то там будет указаны именно те цифры, которые мы пишем
```
1.
1.
4.
```