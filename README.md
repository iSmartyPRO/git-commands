# Команды GIT

## Проверка установки:
```
git --version
```
## Справка:
```
git help
git help [command-name]
git [command-name] --help | -h
```

## Минимальные настройки:
```
// --local - настройки для текущего репо
// --global - настройки для текущего пользователя
// --system - настройки для всей системы, т.е. для всех пользователей
git config --global user.name "My Name"
git config --global user.email "myemail@example.com"
```

### Дополнительные настройки:
```
// список глобальных настроек
git config --list | -l --global
```

// редактирование глобальных настроек
git config --global --edit | -e

## Создание репозитория:
```
git init
```

## Очистка репозитория:
```
// -d - включая директории, -x - включая игнорируемые файлы, -f - принудительная
git clean | -dxf
```

## Удаление файлов и директорий:
```
// remove
git rm [file-name]
git rm -r [dir-name]
git rm --force | -f
```
## Перемещение файлов:
```
// git add + git remove
// move
git mv [old-file] [new-file]
```

## Просмотр состояния репозитория:
```
git status
```

## Добавление изменений:
```
git add [file-name]

git add --force | -f

// все файлы
git add . | --all | -A

// для добавления пустой директории можно создать в ней пустой файл .gitkeep
```

## Добавление сообщения (коммита):
```
// редактирование коммита
git commit

// коммит для одного изменения, если не выполнялось git add . | -A
// если выполнялось, сообщение будет добавлено для всех изменений
git commit --message | -m "My Message"

// для всех изменений, если git add [file-name] выполнялось несколько раз
git commit --all | -a -m | -am "My Message"

// исправление коммита
git commit --amend "My Message" | --no-edit
```

## Просмотр коммита:
```
// последний коммит
git show

// другой коммит
git show [hash] // минимум первые 4 символа

// поиск изменений по сообщению или части сообщения
git show :/[string]

// поиск коммита по тегу
git show [tag-name]
```

# Просмотр разницы между коммитами:
```
git diff HEAD | @ // HEAD - как правило, текущая ветка; @ - алиас для HEAD

// staged
git diff --staged | --cached

git diff [hash1] [hash2]

// разница между ветками
git diff [branch1]...[branch2]

// просмотр разницы между коммитами при редактировании сообщения
git commit --verbose | -v

// кастомизация выводимого сообщения
git diff --word-diff | --color-words
```

## Просмотр истории изменений:
```
git log

// n - количество изменений
git log -n
// --since, --after - после
// --until, --before – до

// разница
git log -p

// быстрое форматирование
git log --graph --oneline --stat

// кастомное форматирование
git log --pretty=format
// пример
git log --pretty=format:'%C(red)%h %C(green)%cd %C(reset)| %C(blue)%s%d %C(yellow)[%an]' --date=short | format-local:'%F %R'

// поиск изменений по слову, файлу, ветке; i - без учета регистра
git log --grep | -G [string] | [file] | [branch] & -i

// поиск по нескольким строкам
git log --grep [string1] --grep [string2] --all-match

// поиск в определенном блоке файла
git log -L '/<head>/','/<\/head>/':index.html
// поиск по автору
git log --author=[name]
```

## Отмена изменений:
```
git reset
// --hard - включая рабочую директорию и индекс
// --soft - без рабочей директории и индекса
// --mixed - по умолчанию: без рабочей директории, но с индексом

git reset --hard [hash] | @~ // @~ - последний коммит в HEAD

// аналогично
git reset --hard ORIG_HEAD

// не путать с переключением ветки
git checkout
git restore
```

## Работа с ветками:
```
// список веток
git branch

// создание ветки
git branch [branch-name]

// переключение на ветку
git checkout [branch-name]

// branch + checkout
git checkout -b [branch-name]

// переименование
git branch -m [old-branch] [new-branch]

// удаление ветки
git branch -d [branch-name]

// слияние веток
git merge [branch-name]
```

## Разрешение конфликтов при слиянии:
```
// обычно, при возникновении конфликта, открывается редактор
// принять изменения из сливаемой ветки
git checkout --ours

// принять изменения из текущей ветки
git checkout --theirs

// отмена слияния
git reset –merge
git merge –abort

// получение дополнительной информации
git checkout --conflict=diff3 --merge [file-name]

// продолжить слияние
git merge --continue
```

## Удаленный репозиторий:
```
// клонирование
git clone [url] & [dir]

// просмотр
git remote
git remote show
git remote add [shortname] [url]
git remote rename [old-name] [new-name]
// получение изменений
// git fetch + git merge
git pull

// отправка изменений
git push
```

## Теги:
```
// просмотр
git tag

// легковесная метка
git tag [tag-name]
//пример
git tag v1-beta

// аннотированная метка
git tag -a v1 -m "My Version 1"

// удаление
git tag -d [tag-name]
```

## Отладка
```
git bisect

git blame

git grep
```

## Сохранение незакоммиченных изменений:
```
// сохранение
git stash

// извлечение
git stash pop
```

## Копирование коммита:
```
git cherry-pick | -x [hash]

// если возник конфликт
// отмена
git cherry-pick --abort

// продолжить
git cherry-pick –continue

git cherry-pick --no-commit | -n

// --cherry = --cherry-mark --left-right --no-merges
git log --oneline --cherry [branch1] [branch2]
```

## Перебазирование:
```
git rebase [branch]

// при возникновении конфликта
// отмена
git rebase –abort

// пропустить
git rebase –skip

// продолжить
git rebase –continue

// предпочтение коммитов слияния
git rebase --preserve-merges | -p

// интерактивное перебазирование
git rebase -i [branch]
```

## Автозавершение повторных конфликтов:
```
// rerere - reuse recorder resolution
// rerere.enabled true | false
// rerere.autoUpdate true | false
// rerere-train.sh - скрипт для обучения rerere
git rerere forget [file-name]
```

## Обратные коммиты:
```
git revert @ | [hash]

// отмена слияния
// git reset --hard @~ не сработает
git revert [hash] -m 1

// git merge [branch] не сработает
// отмена отмены
git revert [hash]

// повторное слияние с rebase
git rebase [branch1] [branch2] | --onto [branch1] [hash] [branch2]

git merge [branch]

git rebase [hash] --no-ff
```

## Пример алиасов (сокращений) для .gitconfig:
```
[alias]
    aa = add -A
    co = checkout
    ci = commit –m
    st = status
    br = branch
```