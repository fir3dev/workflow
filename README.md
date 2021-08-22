# Регламент

:warning: Убедитесь что все нотификации приходят к вам, не попадают в спам и вы видите все,
что происходит прежде чем их отключать и как-то фильтровать.

:warning: Перед тем как начинать над чем-то работать, убедитесь что для этого есть открытый тикет.

Это облегчит всем жизнь. Изменения будут задокументированы и можно посмотреть о чем шла речь, когда открываешь чужой код.

## Kanban

Мы используем [ZenHub](https://app.zenhub.com/) поверх Github для представления тикетов в виде доски.
Пожалуйста установите [ZenHub Browser Extension](https://www.zenhub.com/extension)

### Поток

`Inbox` → `Next` → `Todo` → `Progress` → `Review` → `Done`

- Таски на текущий спринт берем из `Todo`, это задачи на текущий спринт.
- `Next` это то, что мы планируем на следующий. Если в `Todo` пусто, берите верхнюю задачу из `Next`.
- `Inbox` это то куда приходят новые задачи. Отсюда мы переводим в `Next` то что мы будем делать в следующий спринт.
- Когда вы начинаете работать над чем-то, пожалуйста переведите тикет в `Progress`

Таким образом у нас нет неожиданных задач и приятно работать.

Тикеты зарождаются в `Inbox`. Те над которыми мы будем работать лежат в `Todo`.

### `Icebox` → `Todo` → `Progress` → `Review` → `Done`

- `Icebox` Задачи которые надо разобрать прежде чем понять что с ними делать.
- `Next` Задачи которые готовы но не приоритетны в данный момент.
- `Todo` Задачи на текущий спринт, так же те которые надо улучшить.
- `Progress` То над чем мы работаем сейчас.
- Когда начинаете новую задачу, передвиньте тикет в `Progress`.
- Когда открыт пулл реквест, задача должна попасть в `Review`
- `Review` Чистилище перед мержем. Отсюда задачи попадают либо в `Donе` либо в `Todo` для улучшения.
- `QA` Для ручного тестирования. Отсюда задачи попадают либо в `Done` либо в `Todo` с отметкой `QA Failed`
- `Done` Все в порядке — пулл-реквест смержен, проверен, таски готовы, тикет закрыт.

В начале спринта тикеты которые мы хотим сделать в текущей итерации лежат в `Todo` и назначены на текущий спринт и майлстоун.

Если тикет указан в commit message:

- ZenHub автоматически передвинет задачу в Review при открытии пулл-реквеста.
- ZenHub автоматически передвинет карточку в QA при мерже пулл-реквеста.

## Оценки

Мы пытаемся оценить каждую задачу чтобы знать сколько мы можем сделать и не брать на себя слишком много.
Оценки выставляются относительно "Стандартной задачи" оцененной в 3 story points.

Стандартная задача это что-то что вы сможете полностью сделать до обеда.
Мы используем оценки в `0`, `1`, `2`, `3` и `5` story points относительно Стандартной задачи.

- `0` – Cразу закрыть можно (0~15 мин)
- `1` - За час управлюсь
- `2` – Тут надо в нескольких местах поправить
- `3` – Все утро займет
- `5` - Весь вечер зайдет
- `8` - Если чувствуете что это задача на день или больше, пожалуйста конвертните в Epic и разбейте на подзадачи.

## Итерация

Мы работаем спринтами по две недели.
Одна неделя бодрит, но слишком большой оверхед на менеджмент.
Месяц слишком долго - фокус теряется.
Другие цифры не подходят, потому что не делятся на два.

Приоритеты:

- `Required` должны быть сделаны первым делом. Обычно задачи по которым у нас есть обязательства перед заказчиком
- `Must` важные вещи для включения в текущую итерацию
- `Bug` не каждый баг критичен, но хорошо бы их не было
- `Want` не срочные но важные задачи которые могут подождать
- Все остальное

В конце месяца мы проводим демо результатов и обсуждение планов на след месяц.

## Репозиторий

Мы используем [Trunk-based development](https://trunkbaseddevelopment.com/) это значит
`master` должен быть готов к релизу.

:warning: Пожалуйста форкайте главный репозиторий и работайте в своей копии

Склонируйте свой форк:

```sh
git clone git@github.com:<USERNAME>/xxxxx
```

Добавьте `xxxxx`:

```sh
git remote add xxxxx git@github.com:fir3dev/xxxxx
```

Если вам нужен чей-то пулл реквест - добавьте его <USERNAME> как новый remote.

# Работа над задачей

:warning: Все задачи должны начинаться от открытого тикета и из колонки `Progress`

Не копите задачи в процессе, работайте над одной.

Убедитесь что у вас есть последние изменения из `xxxxx`. И начинайте свою ветку от `xxxxx/master`

```sh
git fetch --all
git checkout xxxxx/master
```

## Именование веток

Пожалуйста начинайте название ветки с номера задачи + заголовок в виде человекопонятного урл (ЧПУ). Это сделает жизнь других легче.

```sh
git checkout -b 123-add-reporting
```

Пулл-реквесты открываем для мержа в `xxxxx/master`.

## Git hooks

Мы проверяем и форматируем код перед отправкой с помощью скрипта `./bin/format-ruby`.
Он работает для staged файлов, и его можно запускать руками.

Подключение его в качестве git hook:

```
$ ./add-git-hooks.sh
```

## Commit messages

```
Кратко объясните зачем этот коммит

Добавьте описание в формате markdown.
Посмотрите в тикете для вдохновения.

- Добавьте список изменений.

Добавьте линк на тикет:

Closes #123
```

:warning: Обязательно добавляйте объяснение и линк на тикет. Если возможно — скришнот, демонстрирующий изменения.

- [GitHub: Autolinked references and URLs](https://docs.github.com/en/github/writing-on-github/working-with-advanced-formatting/autolinked-references-and-urls)

Хотя это удобно - очень часто нумерация оказывается неверной и закрываются
неправильные тикеты. Поэтому аккуратно используйте слова закрывающие задачи:

- [GitHub: Closing Issues via Commit Messages](https://help.github.com/articles/closing-issues-via-commit-messages)

Zenhub автоматически подхватит issue если использован закрывающее слово.
Если нет, пожалуйста залинкуйте тикет при открытии пулл-реквеста.

## Squash коммитов

Ветка должна состоять из одного смыслового коммита. Перед открытием пулл
реквеста сквошните свои коммиты. Если в ветке получилось больше одного
смыслового коммита, лучше их вливать отдельными пулл-реквестами, привязав к
соответствующим тикетам.

```sh
git fetch xxxxx
git rebase -i xxxxx/master
```

`-i` Interactive rebase - создает список изменений. Первый коммит всегда `pick`/`p`,
остальные помечаем как `squash`/`s` или `fixup`/`f`. Разница в том что `Squash` сохраняет
commit message, а `fixup` просто подклеивает к предыдущему. Удаленные линии из rebase plan
удалят и коммиты.

```
pick 0000000 Нужное изменение
s 0000000 Стили забыл...
f 0000000 Теперь точно
```

:warning: Если `vim` не подходит, редактор по умолчанию можно сменить:

```sh
$ git config --global core.editor "code --wait"
```

## Push

:warning: Не пушьте в `xxxxx`, пушьте в свой форк

```sh
$ git push -u <USERNAME>
```

## Изменения в открытых пулл-реквестах

Если вы хотите что-то добавить в коммит, используйте `--amend`:

```sh
$ git commit --amend
```

Или, если нет нужды менять описание:

```sh
$ git commit --amend --no-edit
```

:warning: Аккуратней с amend, вы можете потерять изменения. Не изменяйте мерж-коммиты.

Rebase от `xxxxx/master`:

```sh
$ git fetch xxxxx
$ git rebase xxxxx/master
```

"Force push" изменений:

```sh
$ git push -f
```

## Pull request

Когда открываете пулл реквест, будьте своим первым ревьюером. О чем можно подумать:

- Чистый и аккуратный код без остатков логгирования и закомменченных кусков
- Комменты у классов, методов и регулярных выражений, с примером что это выражение делает.
- Поддерживайте документацию если изменения надо документировать [Yard: GettingStarted](https://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md)
- Код должен быть покрыт тестами

## Миграции

- Используйте атомарные миграции
- Оборачивайте изменения в транзакции
- Старайтесь не использовать Rails модели

## Код Ревью

Мы используем комбинацию GitHub и [Reviewable](https://reviewable.io), сервиса который
помогает следить за ходом ревью.

Ревьюеры назначаются автоматически, если вы назначены, пожалуйста постарайтесь просмотреть
пулл реквест как только появится возможность чтобы позволить другим двигаться вперед.

Комментируйте все что вызывает беспокойство:

- Странности дизайна и кода
- Форматирование и стиль
- Возможности для улучшение и рефакторинга
- Возможные ошибки

Если что-то вызывает сомнения, спросите помощи, упомянув того, кто может помочь в комментариях.

Старайтесь ревьюить в [Reviewable](https://reviewable.io), а не в GitHub.
Отметьте каждый просмотренный файл.
Это не обозначает автоматического согласия с кодом, только что вы видели его.
И позволит прерывать и возобновлять ревью в любой момент.

Если все ок, вы можете сразу влить изменения. Используйте стратегию
[Rebase and Merge](https://github.com/blog/2243-rebase-and-merge-pull-requests)
либо добавляйте комментарий и `Request Changes`.
Все комментарии должны быть разрешены перед слиянием изменений.

Если вы с чем-то не согласны, пожалуйста урегулируйте это с автором пулл
реквеста или в публичной дискуссии.
Фокусируйтесь на важных вещах. См. [Bikeshedding](http://en.wiktionary.org/wiki/bikeshedding)

### Reviewable

:warning: Не оставляйте комментарии в подвешенном состоянии.

Нажимайте каждый раз `Done`, после исправиления. `Resolve` если согласны. `Aknowledge` чтобы отметить просмотренным.

- `x` - переключить просмотреность файла
- `n`/`p` - переход по непросмотренным
- `N`/`P` - переход по всем файлам

## СI/CD

Все проверки должны быть зелеными. Иногда тот или иной тест падает из-за
рассинхронизации с Selenium, в таком случае можно сделать `re-run` билда.

После мержа в мастер приложение будет задеплоено, при условии что миграции прошли успешно.

:warning: Красный билд в мастере или отказ миграции это серьезный инцидент
который должен быть исправлен как можно скорее.

Не принимайте понижение code coverage. Скорее всего можно добавить какой-то
тест основываясь на отчете Codecov.

**ProTip** Ребилд можно вызвать из командной строки используя что-то вроде:

```
$ git commit --amend --no-edit && git push -f
```

# Agile

Мы используем двухнедельные итерации и в конце обсуждаем новые user stories и
оцениваем задачи на предстоящий спринт.

## User stories

Задачи для User Stories должны быть **INVEST**-able:

- **Independent** Независимые - одна фича не зависящая и не блокирующая остальные
- **Negotiable** Обсуждаемые - если что-то выглядит странным, давайте обсудим
- **Valuable** Стоящие - Приносить пользу бизнесу
- **Estimable** Оценяемые — Легкие для оценки
- **Small** Небольшие — Не более одного - двух дней
- **Testable** Проверяемые — Их можно автоматически протестировать

Стандартная задача – 3 points. Что-то что можно сделать до обеда. Другие оценки 1,2,3,5.
Оценки от одного дня и выше - признак того, что внутри есть другие задачи.

## Приоритеты

Мы делим задачи на:

1. `must`
2. `want`
3. и остальное

Начинайте с `must` с наименьшей оценкой трудоемкости. Это самые ценные low-hanging fruits.

`want` это то что мы хотим иметь рано или поздно, но они могут подождать до следущей итерации.

Все остальное - потом.

Следите за тикетами с пометкой `bug`, помня о том, что не каждый баг
заслуживает немедленного исправления.

## Ежедневный митинг

Мы созваниваемся каждый день в 11:00 по Москве для быстрого апдейта

1. Что сделал?
2. Что сделаешь?
3. Что помешало?

## Разработка

- Постарайтесь не назначать тикеты на себя до того как вы будете готовы над ними работать.
- Пожалуйста перемещайте карточку в `Progress` когда приступаете.
- Постарайтесь прикинуть время которое понадобится для закрытия перед тем как начнете.

## Тестирование

Пожалуйста старайтесь использовать Test Driven Development:

1. Начните с теста
2. Перейдите к написанию кода когда тест упал
3. Продолжите написание теста когда тест проходит

Таким образом мы получим минимальный объем кода решающий конкретные задачи.

## Демо

В конце итерации мы проводим ретроспективу и демо для стейкхолдеров в конце месяца.

На Demo мы показываем что было сделано и обсуждаем:

1. Что получилось?
2. Что улучить?

# Code Style

## Первый закон качества кода

# `e = mc²`

`errors = (more code)²`

Держите рабочее место, то есть код в чистоте.

> Чистый код, clean code это тот который легко понять и поменять

## Без ковбойства

- Придерживайтесь гайдлайнов и правил линтинга. Не пишите "хакерский" нечитаемый код.
- Будьте ответственными перед людьми которые будут работать с ним позже.
- Видите что-то странное - выделите с помощью `TODO` коммента с описанием, его
- соберет TODO-bot, и превратит в тикет.

:warning: Не старайтесь пофиксить все сразу. Добавляйте `TODO`.

## Без ошметков

- Не оставляйте комменты, лишние переводы строк, сложные куски. Если код
  нельзя понять без комментариев - вероятно это code smell.
- Пожалуйста **комментируйте** регулярки и сложные непонятные моменты.
- Оставляйте пустые строки вокруг а не внутри методов

## Do not rename

Не переименовывайте переменные методы и тд. Если у вас есть название,
продолжайте его использовать везде вплоть до css. Не переименовывайте
переменные при передаче между методами. Используйте named parameters где
это возможно.

## Inject Dependencies

Не надо глобальных объектов, передавайте зависимости явно.

## Composition over Inheritance

Используйте два вида классов - Abstract/Base и Final. Не наследуйте второй раз.
