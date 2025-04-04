
**Git** - это система контроля версий (Version Control Systems, VCS). Она отвечает за отслеживание изменений в коде, откат на предыдущие версии, работу в команде без конфликтов.
Особенность Git в том, что он «распределённый»: у каждого разработчика на компьютере хранится полноценная копия (включая всю историю) проекта. Это даёт большую гибкость и независимость от центрального сервера.


Для того, чтобы задать глобальные настройки для Git используем такие консольные команды
```
git config --global user.email "email.com"
```

# Репозиторий

*Репозиторий* - проект, за которым следит сам Git. В большинстве своём это папка на компьютере. Соответственно, таких репозиториев может быть много.
Репозиторий может быть локальный и удаленный. 

**Локальный** репозиторий - это репозиторий, который находится только на компьютере. **Удаленный** репозиторий хранится в облаке - например в [[GitHub]]. По сути, это копия *локального* репозитория. 

Обычно к команде происходит работа с одним *удаленным репозиторием*. Каждый разработчик создает *локальную* копию такого репозитория. При этом, все внесенные изменения отразятся только на в локальном репозитории.

Для того, чтобы скопировать удаленный репозиторий необходимо 
 1. Перейти в папку с помощью консоли, в которую будет скопирован репозиторий 
 2. Выполнить в консоли команду
```powershell
git clone (URL удаленного репозитория)
```

## Изменения репозитория

После клонирования удаленного репозитория, или создания *удаленного* со своего *локального* *Git* автоматически отслеживает изменения, но не вносит их.

*Для того, чтобы посмотреть все файлы, которые не синхронизированы (то есть, те файлы, которые отличаются на локальном и удаленном репозитории) необходимо выполнить следующую консольную команду:*
```powershell
git status
```


*Для того, чтобы подготовить определенные файлы к сохранению в удаленном репозитории, необходимо выполнить команду, указывая имена файлов или папок, которые мы хотим подготовить к сохранению «../Имя файла»: *
```Powershell
git add имя, имя…
--Если весь репозиторий 
git add .
```


Файлы, которые подготовлены к сохранению Git хранит в индексе и в changing area. Только файлы в индексе будут сохранены и попадут в commit.

После того, как мы подготовили файлы и папки для сохранения, их можно сохранить в истории Git. 
*Для сохранения конкретной версии файлов в истории необходимо выполнить коммит*
```powershell
git commit -m "{message}"
```
В данном случае параметр *message* необязательный, однако, как правило он указывается.
***Коммит*** - это версия файлов в репозитории из индекса. При сохранении (выполнении команды *commit*) такой версии присваивается уникальный хэш код, по которому затем к этой версии можно вернуться.  ^44e002

*Для просмотра всех коммитов в текущей ветке с их хэшами, сообщениями и авторами в хронологическом порядке нужно выполнить команду:*
```powershell
git log
```

*Для того, чтобы вернуться к одному из предыдущих коммитов необходимо выполнить команду с указанием уникального хэшкода:*
```powershell
git checkout <хэшкод коммита>
```

## Сохранение репозитория

Все сделанные [коммиты](#^44e002) Git сохраняет локально на устройстве. Чтобы сохранить эти изменения на удаленном репозитории необходимо выполнить *push*.
*Для публикации коммита из локального репозитория в удаленный с указанным именем в указанной ветке: *
```powershell
git push <имя репозитория> <имя ветки>
```

^2c463a

Локальный репозиторий знает свой удаленный под именем *origin*.

*Для того, чтобы скачать из указанного удаленного репозитория все коммиты в указанной ветке, которых еще нет в локальном репозитории необходимо выполнить команду:*
```powershell
git pull <имя репозитория> <имя ветки>
```
После выполнения команды загружаются не только изменения, но и в принципе коммиты. То есть, копируется и история коммитов, благодаря чему можно так же вернуться к любой версии.

# Ветка

По сути ветка в Git - это последовательность коммитов с заданным именем. В любом репозитории (даже только что созданном) как минимум есть одна ветка с именем "*master*" или "*main*".  ^2c1000

Обычно в главной ветке лежат только корректные версии коммитов, которые загружаются туда в момент релиза. Для разработки фитч и исправления багов используются дополнительные ветки.
Дополнительные ветки создаются от какой-либо существующей ветки и являются изолированными от родительской ветки.

*Для просмотра доступных локальных веток в локальном репозитории:*
```powershell
git branch
```
В полученном списке звездочкой указана та ветка, в которой мы прямо сейчас находимся.

*Для того чтобы создать новую ветку от текущей с заданным именем нужно выполнить команду:*
```powershell
git branch <имя ветки>
```
По умолчанию ветка создается на основе последнего коммита родительской ветки. Ветка создается локально и не видна в удаленном репозитории.

После создания новой ветки, мы все еще остаемся в родительской. 
*Для того, чтобы перейти в другую ветку с указанным именем необходимо выполнить команду:*
```powershell
git checkout <имя ветки>
```
Если перейти в уже существующую ветку, то версия файлов автоматически синхронизируется с последним коммитом.

*Для публикации созданной ветки необходимо выполнить команду находясь в этой ветке, указав имя репозитория и имя публикуемой ветки:*
```powershell
	git push <имя репозитория> <имя публикуемой ветки>
```

## Слияние

Обычно вся работы происходит в дочерних ветках. Когда готовую работу необходимо вынести из дочерней ветки в родительскую это называется **слияние веток.**

Есть несколько вариантов выполнения такого действия.

### Вариант 1

Для начала необходимо перейти в ту ветку, в которую мы хотим сделать коммит. Пусть это будет **master**. Для этого выполним *checkout*
```powershell
git checkout master
```

*Для того, чтобы выполнить слияние указанной ветки в текущую в виде одного нового коммита:*
```powershell
git merge <имя ветки>
```
Git берет все файлы, все изменения и применяет их к текущей ветке в виде одного коммита.

### Варинат 2

Для начала необходимо перейти в ту ветку, в которую мы хотим сделать коммит. Пусть это будет **master**. Для этого выполним *checkout*
```powershell
git checkout master
```

Этот вариант подразумевает, что мы применяем все коммиты из указанной ветки к ветке текущей. Для этого выполним команду:
```powershell
git rebase <имя ветки>
```


ВАЖНО! Все это происходит локально. Чтобы применить merge, необходимо после сделать  *[push](#^2c463a)* измененной ветки.

## Конфликтов

**Конфликт** - это ситуация, когда Git не может автоматически слить (merge) изменения из разных веток или из удалённого репозитория в локальный, потому что в одном и том же файле (или в одной и той же его части) есть взаимоисключающие изменения. Git не знает, какие из них считать правильными, и просит разработчика вручную разрешить конфликт.

Конфликты могут возниктнуть только при выполнении следующих операций и событий:
1. `git merge`
	Когда мы пытаемся объединить две [ветки](#^2c1000) (`branch`), и в обоих ветках есть изменения в одном и том же участке кода (одной и той же строчке или нескольких строчках). Git не может автоматически решить, какие из изменений сохранить.
2. `git pull`
	Фактически `git pull` – это комбинация `git fetch` (загрузить обновления с сервера) и `git merge` (слить эти обновления с локальной веткой). Если локальные изменения пересекаются с тем, что уже есть на сервере, возникает конфликт.
3. `git rebase`
	`rebase` тоже объединяет изменения, но переписывает историю коммитов, что может приводить к конфликтам, аналогичным `merge`, если изменения затрагивают одни и те же участки кода.

### Виды конфликтов

Наиболее часто встречаются **текстовые (content) конфликты**, когда в тексте файла (обычно кода) есть разночтения. Но можно условно выделить несколько видов:
1. **Content Conflict** (Тектовый конфликт)
	Происходит в тексте файлов, где Git просто не может объединить изменения.
	Например:
	```powershell
	<<<<<<< HEAD 
	строка кода: A 
	======= 
	строка кода: B 
	>>>>>>> branch_name
	```
	Git выделяет конфликтующие участки специальными маркерами `<<<<<<<`, `=======`, `>>>>>>>`  
2. **Deletion Conflict** (Конфликт при удалении).
	Когда в одной ветке файл был удалён, а в другой — изменён. Нужно решить, удалить файл или сохранить с изменениями.
3. **Rename Conflict** (Конфликт при переименовании)
	Если в одной ветке файл переименовали, а в другой — этот же файл (под старым именем) изменили или удалили. Git не знает, куда сохранить изменения.
4. **Binary File Conflict** (Бинарный конфликт)
	Если столкнулись изменения в бинарных файлах (например, изображения, PDF, исполняемые файлы), Git не может автоматически объединить их, так как у него нет «стратегии» объединения для бинарных форматов. В таком случае придётся вручную решить, какой бинарный файл оставить.

### Разрешение конфликтов

Сохранить изменения при возникших конфликтах невозможно. Поэтому эти конфликты необходимо разрешать. По сути, разрешение конфликта - это выбор той или иной версии файла, так как сам **Git** не может это решить за нас.

#### Ручное разрешение конфликта

При возникновении конфликта **Git** указывает, в каких файлах эти коныликты возникли.
```PowerShell
PS C:\Users\egor.iakovlev\Documents\Obsidian-Vault> git pull origin master
From https://github.com/ERJYAK/Obsidian-Vault
 * branch            master     -> FETCH_HEAD
Auto-merging .obsidian/workspace.json
CONFLICT (content): Merge conflict in .obsidian/workspace.json
Automatic merge failed; fix conflicts and then commit the result.
```

В самом файле **Git** помечает конфликтующие строки маркерами `<<<<<<<`, `=======`, `>>>>>>>`.
Сам алгоримт решения конфликтов в этом случае будет выглядеть так:
1. **Открыть конфликтующий файл** и найти там маркеры `<<<<<<<`, `=======`, `>>>>>>>`.
2. **Вручную выбрать нужные изменения**:
    - Оставить только локальные изменения.
    - Оставить только удалённые (или из другой ветки) изменения.
    - Объединить оба варианта.
3. **Удалить маркеры** конфликта, чтобы файл снова стал корректным с точки зрения формата (например, кода или JSON).
4. **Сохранить файл**.
5. **Добавить и закоммитить** изменения:
	```bash
    git add <имя файла> 
    git commit -m "Fix merge conflict"
    ```
6. Если конфликтов несколько, повторить то же самое для всех конфликтующих файлов.

#### Разрешение с помощью консоли

Если необходимо выборочно оставить конфликтующие строки
строк