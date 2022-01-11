# devops-netology
first line

qw

qwe

___
Исключаются все файлы директории .terraform, находящейся в любом месте начиная от директории, в которой расположен файл .gitignore

`**/.terraform/*`

Исключаются все файлы с данными именами, находящиеся в любом месте дерева каталогов, от директории, где расположен .gitignore :
`crash.log`
`override.tf`
`override.tf.json`
`.terraformrc`
`terraform.rc`

Исключаются все файлы с масками имен (где * - любое количество символов, в том числе и 0), находящиеся в любом месте дерева каталогов, от директории, где расположен .gitignore :
`*.tfstate` 
`*.tfstate.*`
`*.tfvars`
`*_override.tf`
`*_override.tf.json`

another new line from PyCharm

---
# Домашнее задание к занятию «2.4. Инструменты Git»
### 1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`
Ответ: 
```shell
aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Update CHANGELOG.md
```
Решение:
```shell
git show -s --format=%H%n%s aefea
или 
git show -s --oneline aefea
```
где `git show aefea` - показать информацию о коммите, `-s` - не показывать diff коммита, `--format=%H%n%s` - форматировать вывод комманды в формате: полный хэш, новая строка, комментарий.

При опции `--oneline` будет показан сокращенный хэш и комментарий.
### 2. Какому тегу соответствует коммит `85024d3`?
Ответ:
```shell
v0.12.23
```
Решение:
```shell
git show -s --oneline 85024d3
```
Полный вывод комманды, где после хэша мы видим тэг
```shell
85024d310 (tag: v0.12.23) v0.12.23
```
### 3. Сколько родителей у коммита `b8d720`? Напишите их хеши.
Ответ:
```shell
т.к. коммит `b8d720` - мерж коммит, то у него 2 родителя: 56cd7859e05c36c06b56d013b55a252d0bb7e158 и 9ea88f22fc6269854151c571162c5bcf958bee2b
```
Решение:
```shell
git show -s b8d720
видим строку, в которой указано, что это мерж коммит и перечислены его 2 родителя
Merge: 56cd7859e 9ea88f22f

Далее с помощью
git show -s 56cd7859e 9ea88f22f
или
git show -s b8d720^1 b8d720^2 # где указатель ^1 - первый родитель ^2 - второй родитель
или
git rev-parse b8d720^1 b8d720^2 
узнаем полные хэши родителей коммита
```

### 4. Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24
Ответ:
```
33ff1c03bb960b332be3af2e333462dde88b279e
v0.12.24


b14b74c4939dcab573326f4e3ee2a62e23e12f89
[Website] vmc provider links

3f235065b9347a758efadc92295b540ee0a5e26e
Update CHANGELOG.md


6ae64e247b332925b872447e9ce869657281c2bf
registry: Fix panic when server is unreachable

Non-HTTP errors previously resulted in a panic due to dereferencing the
resp pointer while it was nil, as part of rendering the error message.
This commit changes the error message formatting to cope with a nil
response, and extends test coverage.

Fixes #24384


5c619ca1baf2e21a155fcdb4c264cc9e24a2a353
website: Remove links to the getting started guide's old location

Since these links were in the soon-to-be-deprecated 0.11 language section, I
think we can just remove them without needing to find an equivalent link.


06275647e2b53d97d4f0a19a0fec11f6d69820b5
Update CHANGELOG.md

d5f9411f5108260320064349b757f55c09bc4b80
command: Fix bug when using terraform login on Windows


4b6d06cc5dcb78af637bbb19c198faff37a066ed
Update CHANGELOG.md

dd01a35078f040ca984cdd349f18d0b67e486c35
Update CHANGELOG.md

225466bc3e5f35baa5d07197bbc079345b77525e
Cleanup after v0.12.23 release

```
Решение:
```shell
git show -s --format=%H%n%B%n v0.12.23..v0.12.24
или
git log --format=%H%n%B%n v0.12.23..v0.12.24
```

### 5. Найдите коммит в котором была создана функция `func providerSource`, ее определение в коде выглядит так `func providerSource(...)` (вместо троеточего перечислены аргументы).
Ответ:
```shell
8c928e83589d90a031f811fae52a81be7153e82f
```
Решение:
```shell
git log -p -S'func providerSource('
```
где `-S` - поиск по логу строки, которая была добавлена или удалена
`-p` - выводит патч, то есть что было изменено в файлах в пределах этого коммита, это нужно для самопроверки, и мы видим что была добавлена строка `+func providerSource(services *disco.Disco) getproviders.Source {
`, то есть это и есть создание функции.

### 6. Найдите все коммиты в которых была изменена функция `globalPluginDirs`
Ответ:
```
commit 78b12205587fe839f10d946ea3fdc06719decb05
Author: Pam Selle <204372+pselle@users.noreply.github.com>
Date:   Mon Jan 13 16:50:05 2020 -0500

    Remove config.go and update things using its aliases

commit 52dbf94834cb970b510f2fba853a5b49ad9b1a46
Author: James Bardin <j.bardin@gmail.com>
Date:   Wed Aug 9 17:46:49 2017 -0400

    keep .terraform.d/plugins for discovery

commit 41ab0aef7a0fe030e84018973a64135b11abcd70
Author: James Bardin <j.bardin@gmail.com>
Date:   Wed Aug 9 10:34:11 2017 -0400

    Add missing OS_ARCH dir to global plugin paths

    When the global directory was added, the discovery system still
    attempted to search for OS_ARCH subdirectories. It has since been
    changed only search explicit paths.

commit 66ebff90cdfaa6938f26f908c7ebad8d547fea17
Author: James Bardin <j.bardin@gmail.com>
Date:   Wed May 3 22:24:51 2017 -0400

    move some more plugin search path logic to command

    Make less to change when we remove the old search path

commit 8364383c359a6b738a436d1b7745ccdce178df47
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Thu Apr 13 18:05:58 2017 -0700

    Push plugin discovery down into command package

    Previously we did plugin discovery in the main package, but as we move
    towards versioned plugins we need more information available in order to
    resolve plugins, so we move this responsibility into the command package
    itself.

    For the moment this is just preserving the existing behavior as long as
    there are only internal and unversioned plugins present. This is the
    final state for provisioners in 0.10, since we don't want to support
    versioned provisioners yet. For providers this is just a checkpoint along
    the way, since further work is required to apply version constraints from
    configuration and support additional plugin search directories.

    The automatic plugin discovery behavior is not desirable for tests because
    we want to mock the plugins there, so we add a new backdoor for the tests
    to use to skip the plugin discovery and just provide their own mock
    implementations. Most of this diff is thus noisy rework of the tests to
    use this new mechanism.
```
Решение:
```shell
git grep globalPluginDirs
commands.go:            GlobalPluginDirs: globalPluginDirs(),
commands.go:    helperPlugins := pluginDiscovery.FindPlugins("credentials", globalPluginDirs())
internal/command/cliconfig/config_unix.go:              // FIXME: homeDir gets called from globalPluginDirs during init, before
plugins.go:// globalPluginDirs returns directories that should be searched for
plugins.go:func globalPluginDirs() []string {
```
Ищем по файлам рабочего каталога строку `globalPluginDirs`, видим что эта функция изменяется только в файле `plugins.go`

Далее выводим все коммиты, где в файле `plugins.go` имеется строка `globalPluginDirs`
```shell
git log -L:globalPluginDirs:plugins.go
```
удостоверяемся, что во всех коммитах присутствует эта строка и сокращаем вывод `git log`
```shell
git log -s -L:globalPluginDirs:plugins.go
```

### 7. Кто автор функции `synchronizedWriters`
Ответ:
```
Martin Atkins <mart@degeneration.co.uk>
```
Решение:
```shell
git log -p -SsynchronizedWriters | grep synchronizedWriters
```
Сначала ищем строку `synchronizedWriters` в логе коммитов и выводим только те строки, которые совпадают с `synchronizedWriters`, так мы определим как выглядит определение функции:
```
-// synchronizedWriters takes a set of writers and returns wrappers that ensure
-func synchronizedWriters(targets ...io.Writer) []io.Writer {
-               wrapped := synchronizedWriters(stdout, stderr)
+               wrapped := synchronizedWriters(stdout, stderr)
+// synchronizedWriters takes a set of writers and returns wrappers that ensure
+func synchronizedWriters(targets ...io.Writer) []io.Writer {
```
далее уже ищем строку `func synchronizedWriters(` и выводим лог с изменениями `-p`
```shell
git log -p -S'func synchronizedWriters('
```
Находим коммит, где присутствует строка `+func synchronizedWriters(targets ...io.Writer) []io.Writer {
`, автор коммита и будет автором этой функции.