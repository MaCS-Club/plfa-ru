---
title: С чего начать
permalink: /GettingStarted/
---

<!-- Status & Version Badges -->

[![CI][plfa-badge-status-svg]][plfa-badge-status-url]
[![pre-commit.ci status][pre-commit-status-svg]][pre-commit-status-url]
[![Release Version][plfa-badge-version-svg]][plfa-badge-version-url]
[![agda][agda-badge-version-svg]][agda-badge-version-url]
[![standard-library][agda-stdlib-version-svg]][agda-stdlib-version-url]

## С чего начать Читателям

Вы можете читать PLFA [online[plfa] без установки чего-либо. Однако, если вы хотите взаимодействовать с кодом или выполнять упражнения, то вам понадобится:

- На macOS: [The XCode Command Line Tools](#on-macos-install-the-xcode-command-line-tools)
- [Git](#install-git)
- [GHC and Cabal](#install-ghc-and-cabal)
- [Agda](#install-agda)
- [Agda standard library](#install-plfa-and-the-agda-standard-library)
- [PLFA](#install-plfa-and-the-agda-standard-library)

PLFA тестируется на конкретных версиях Agda и стандартной библиотеки, которые отображаются в бейджах выше. Agda и стандартная библиотека меняются быстро, и эти изменения часто нарушают работу PLFA, поэтому использование более старых или более новых версий обычно вызывает проблемы.

В сети существует несколько версий Agda и её стандартной библиотеки. Если вы используете менеджер пакетов, такой как Homebrew или Debian apt, доступная там версия Agda может быть устаревшей. Более того, Agda активно разрабатывается, поэтому, если вы установите версию "в разработке" с GitHub, вы можете обнаружить, что разработчики внесли изменения, которые нарушают работу кода здесь. Поэтому важно иметь конкретные версии Agda и стандартной библиотеки, показанные выше.

### На macOS: Установка XCode Command Line Tools

На macOS, вам нужно установить [The XCode Command Line Tools][xcode]. Для большинства версий macOS, вы можете установить их запустив следующие команды:

```bash
xcode-select --install
```

### Установка Git

Вы можете проверить, установлен ли у вас Git, выполнив следующую команду:

```bash
git --version
```

Если у вас не установлен Git, смотрите [страница загрузки Git][git].

### Установка GHC и Cabal

Agda написана на Haskell, поэтому для её установки нам понадобится _Великолепный компилятор Haskell(Glorious Haskell Compiler)_ и его менеджер пакетов _Cabal_. PLFA должна работать с любой версией GHC >=8.10, но тестирование проводится с версиями 8.10 – 9.8. Мы рекомендуем устанавливать GHC и Cabal, используя [ghcup][ghcup]. Например, после установки ghcup, введя

```bash
ghcup install ghc 9.4.8
ghcup install cabal recommended

ghcup set ghc 9.4.8
ghcup set cabal recommended
```
или используя `ghcup tui` и выбрав  `set` соответствующие утилиты.

### Установка Agda

Самый простой способ установить Agda - использовать Cabal. PLFA использует версию Agda 2.6.3. Выполните следующую команду:

```bash
cabal update
cabal install Agda-2.6.3
```

Этот шаг займет много времени и потребует много памяти.

Если у вас возникнут проблемы или вам нужны альтернативы, смотрите [инструкции по установке Agda][agda-readthedocs-installation].

Если хотите, вы можете [проверить, правильно ли установлена Agda][agda-readthedocs-hello-world].

### Установка PLFA и стандартной библиотеки Agda

Мы рекоммендуем устанавливать PLFA с Github в вашу домашнюю директорию, запустив следующую команду:

```bash
git clone --depth 1 --recurse-submodules --shallow-submodules https://github.com/macs-club/plfa-ru plfa
```

PLFA поставляется с необходимой версией стандартной библиотеки Agda, так что, если вы клонировали с флагом `--recurse-submodules`, вы уже получили её в директории `standard-library`!

Наконец, нам нужно сообщить Agda, где искать стандартную библиотеку Agda и PLFA. Требуются два файла конфигурации: один, который перечисляет пути к библиотекам, и один, который указывает, какие библиотеки загружать по умолчанию.

На macOS и Unix, если PLFA установлена в домашнем каталоге и у вас нет существующих файлов конфигурации библиотек, которые вы хотели бы сохранить, выполните следующие команды:

```bash
mkdir -p ~/.agda
cp ~/plfa/data/dotagda/* ~/.agda
```

Это обеспечивает доступ как к стандартной библиотеке Agda, так и к PLFA как к библиотеке Agda.

В противном случае вам потребуется отредактировать соответствующие файлы. Оба файла конфигурации находятся в каталоге `AGDA_DIR`. На UNIX и macOS `AGDA_DIR` по умолчанию устанавливается в `~/.agda`. На Windows `AGDA_DIR` обычно устанавливается в `%AppData%\agda`, где `%AppData%` обычно соответствует `C:\Users\USERNAME\AppData\Roaming`.

- Если каталог `AGDA_DIR` еще не существует, создайте его.
- В `AGDA_DIR` создайте простой текстовый файл с именем `libraries`, содержащий `AGDA_STDLIB/standard-library.agda-lib`, где `AGDA_STDLIB` - это путь к местоположению стандартной библиотеки Agda (например, `~/plfa/standard-library/`). Это сообщает Agda о том, что библиотека Agda под названием `standard-library` доступна.
- В `AGDA_DIR` создайте простой текстовый файл с именем `defaults`, содержащий _только_ строку `standard-library`.
- Если вы хотите импортировать модули из книги, вам также потребуется предоставить доступ к PLFA как к библиотеке Agda. Для этого пусть `PLFA` будет путем к корневому каталогу для PLFA.
  Добавьте `PLFA/src/plfa.agda-lib` в `AGDA_DIR/libraries` и добавьте `plfa` в `AGDA_DIR/defaults`, каждый в своей собственной строке.

Больше информации о размещении стандартных библиотек доступно на [странице управления библиотеками][agda-readthedocs-package-system] в документации Agda.

## Настройка редактора для Agda

### Emacs

Рекомендованный редактор для Agda это Emacs.(_примечание переводчика: а вот мы предпочитаем VS Code, о его установке можно прочитать дальше_)

Установка Emacs:

- _На UNIX_, версия Emacs в вашем репозитории, вероятно, подойдет, если она достаточно современная. Также есть ссылки на самую последнюю версию на [странице загрузки GNU Emacs][emacs].

- _На MacOS_, [Aquamacs][aquamacs] вероятно, предпочтительная версия Emacs, но GNU Emacs также можно установить через Homebrew или MacPorts. Смотрите [страницу загрузки GNU Emacs][emacs] для инструкций.

- _На Windows_. Смотрите [страница загрузки GNU Emacs][emacs] для инструкций.

Убедитесь, что вы можете открывать, редактировать и сохранять текстовые файлы с вашей установкой. Страница [обзор Emacs][emacs-tour] на сайте GNU Emacs описывает, как получить доступ к учебнику в вашей установке Emacs.

Agda поставляется со встроенной поддержкой редактора для Emacs, так что если вы установили Agda, все, что вам нужно сделать для настройки Emacs, это выполнить:

```bash
agda-mode setup
agda-mode compile
```

Если вы уже используете Emacs и настроили его под себя, вам, возможно, стоит обратить внимание на конфигурацию, которую программа установки добавляет в ваш файл .emacs, и интегрировать ее с вашими предпочтительными настройками.

#### Автозагрузка `agda-mode` в Emacs

С версии 2.6.0 Agda поддерживает литературное редактирование с использованием Markdown, используя расширение `.lagda.md`. Одна из проблем заключается в том, что Emacs по умолчанию будет переходить в режим редактирования Markdown для файлов с суффиксом `.md`. Чтобы `agda-mode` автоматически загружался каждый раз, когда вы открываете файл, оканчивающийся на `.agda` или `.lagda.md`, добавьте следующую строку в файл конфигурации Emacs:

```elisp
;; auto-load agda-mode for .agda and .lagda.md
(setq auto-mode-alist
   (append
     '(("\\.agda\\'" . agda2-mode)
       ("\\.lagda.md\\'" . agda2-mode))
     auto-mode-alist))
```

Если у вас уже есть настройки, которые изменяют ваш `auto-mode-alist` в вашей конфигурации, поместите их _после_ тех, что у вас уже есть, или объедините их, если вы хорошо знакомы с Emacs Lisp. Файл конфигурации для Emacs обычно находится в `HOME/.emacs` или `HOME/.emacs.d/init.el`, но пользователям Aquamacs может потребоваться переместить их настройки запуска в файл "Preferences.el" в `HOME/Library/Preferences/Aquamacs Emacs/Preferences`. Для Windows см. [документацию GNU Emacs][emacs-home] для описания расположения конфигурации Emacs.

#### Опционально: использование шрифта mononoki с Emacs

Agda использует Unicode для многих ключевых символов, и важно, чтобы шрифт, который вы используете для просмотра и редактирования программ на Agda, корректно отображал эти символы. Самое важное, чтобы шрифт, который вы используете, имел хорошую поддержку Unicode, поэтому, хотя мы рекомендуем [mononoki][font-mononoki], шрифты, такие как [Source Code Pro][font-sourcecodepro], [DejaVu Sans Mono][font-dejavusansmono] и [FreeMono][font-freemono], являются хорошими альтернативами.

Вы можете скачать и установить mononoki напрямую с [веб-сайта][font-mononoki]. Для большинства систем установка шрифта сводится просто к клику на скачанный файл `.otf` или `.ttf`. Если ваш менеджер пакетов предлагает пакет для mononoki, это может быть проще. Например, Homebrew на macOS предлагает пакет `font-mononoki`, а APT на Debian предлагает пакет `fonts-mononoki`. Чтобы настроить Emacs на использование mononoki в качестве шрифта по умолчанию, добавьте следующее в конец вашего конфигурационного файла Emacs:

```elisp
;; default to mononoki
(set-face-attribute 'default nil
                    :family "mononoki"
                    :height 120
                    :weight 'normal
                    :width  'normal)
```

#### Проверка корректности установки `agda-mode`

Откройте первую главу книги (`plfa/src/plfa/part1/Naturals.lagda.md`) в Emacs. Вы можете загрузить и выполнить проверку типов в файле введя [`C-c C-l`][agda-readthedocs-emacs-notation].

#### Использование `agda-mode` в Emacs

Для загрузки и проверки типов в файле используйте [`C-c C-l`][agda-readthedocs-emacs-notation].

Agda редактируется интерактивно с использованием ["дырок"][agda-readthedocs-holes], которые представляют собой части программы, которые еще не заполнены. Если вы используете вопросительный знак в качестве выражения и загружаете буфер с помощью `C-c C-l`, Agda заменяет вопросительный знак на дырку. Есть несколько вещей, которые вы можете делать, пока курсор находится в дырке:

- `C-c C-c`: **c**ase split -- разделение на случаи (запрашивает имя переменной)
- `C-c C-space`: заполнить дырку
- `C-c C-r`: **r**efine with constructor -- уточнить с помощью конструктора
- `C-c C-a`: **a**utomatically fill in hole -- автоматически заполнить дырку
- `C-c C-,`: тип дырки и контекст
- `C-c C-.`: тип дырки, контекст и выведенный тип

Смотрите [документацию emacs-mode][agda-readthedocs-emacs-mode] для подробностей.

Если вы хотите видеть сообщения рядом с вашим кодом Agda, а не под ним, вы можете сделать следующее:

- Откройте ваш файл Agda и загрузите его, используя `C-c C-l`;
- нажмите `C-x 1`, чтобы отобразить только ваш файл Agda;
- нажмите `C-x 3`, чтобы разделить окно по горизонтали;
- переместите курсор в правую половину вашего фрейма;
- нажмите `C-x b` и переключитесь на буфер под названием “Agda information”.

Теперь сообщения об ошибках от Agda будут появляться рядом с вашим файлом, а не под ним.

#### Ввод Unicode символов в Emacs с `agda-mode`

Когда вы пишете код на Agda, вам потребуется вставлять символы, которых нет на стандартных клавиатурах. Режим "agda-mode" в Emacs облегчает эту задачу, определяя переводы символов: когда вы вводите определенные последовательности обычных символов (те, которые можно найти на любой клавиатуре), Emacs заменит их в вашем файле Agda соответствующим специальным символом.

Например, мы можем добавить строку комментария в один из тестовых файлов `.agda`.
Допустим, мы хотим добавить строку комментария, которая гласит:

```agda
{- Я в восторге от возможности печатать ∀ и → и ≤ и ≡ !! -}
```


Первые несколько символов обычные, так что мы бы набрали их как обычно…
```agda
{- Я в восторге от возможности печатать
```

Но после последнего пробела мы не найдем символ ∀ на клавиатуре. Код этого символа состоит из четырех символов `\all`, так что мы вводим эти четыре символа, и когда закончим, Emacs заменит их на то, что нам нужно...

```agda
{- Я в восторге от возможности печатать ∀
```

Мы можем продолжить с кодами для других символов. Иногда символы будут изменяться по мере их набора, потому что префикс кода нашего символа является кодом другого символа. Это происходит со стрелкой, код которой `\->`. После набора `\-` мы видим…

```agda
{- Я в восторге от возможности печатать ∀ и -
```

...потому что код `\-` соответствует дефису определённой ширины. Когда мы добавляем `>`, `-` превращается в `→`! Код для `≤` это `\<=`, а код для `≡` это `\==`.

```agda
{- Я в восторге от возможности печатать ∀ и → и ≤ и ≡
```

Наконец, последние несколько символов снова становятся обычными...

```agda
{- Я в восторге от возможности печатать ∀ и → и ≤ и ≡ !! -}
```

Если у вас возникают проблемы с вводом символов Unicode в Emacs, в конце каждой главы должен быть предоставлен список символов Unicode, введённых в этой главе.

Emacs с `agda-mode` предлагает множество полезных команд, и две из них особенно полезны при работе с символами Unicode. Для полного списка поддерживаемых символов используйте `agda-input-show-translations` с:

    M-x agda-input-show-translations

Показаны все поддерживаемые символы в `agda-mode`.

Если вы хотите узнать, как ввести определённый символ Unicode в файле agda, переместите курсор на символ и введите следующую команду:

    M-x quail-show-key

Вы увидите последовательность клавиш символа в мини-буфере.

### Spacemacs

[Spacemacs][spacemacs] — это "распространение Emacs, управляемое сообществом", с родной поддержкой стилей редактирования как Emacs, так и Vim. Он поставляется с [интеграцией для agda-mode][spacemacs-agda] "из коробки". Всё, что требуется, — это включить слой Agda в вашем файле `.spacemacs`.

### Visual Studio Code

[Visual Studio Code][vscode] — это бесплатный редактор исходного кода, разработанный Microsoft. В магазине Visual Studio Marketplace доступен [плагин для поддержки Agda][vscode-agda].

## С чего начать Контрибьютерам

Если вы собираетесь собирать PLFA локально, обратитесь к [Contributing][plfa-contributing] за дополнительными инструкциями.

<!-- Links -->

[plfa-badge-status-svg]: https://github.com/plfa/plfa.github.io/actions/workflows/ci.yml/badge.svg
[plfa-badge-status-url]: https://github.com/plfa/plfa.github.io/actions/workflows/ci.yml
[pre-commit-status-svg]: https://results.pre-commit.ci/badge/github/plfa/plfa.github.io/dev.svg
[pre-commit-status-url]: https://results.pre-commit.ci/latest/github/plfa/plfa.github.io/dev
[plfa-badge-version-svg]: https://img.shields.io/github/v/tag/plfa/plfa.github.io?label=release
[plfa-badge-version-url]: https://github.com/plfa/plfa.github.io/releases/latest
[agda-badge-version-svg]: https://img.shields.io/badge/agda-v2.6.3-blue.svg
[agda-badge-version-url]: https://github.com/agda/agda/releases/tag/v2.6.3.
[agda-stdlib-version-svg]: https://img.shields.io/badge/agda--stdlib-v1.7.2-blue.svg
[agda-stdlib-version-url]: https://github.com/agda/agda-stdlib/releases/tag/v1.7.2
[plfa]: https://plfa.inf.ed.ac.uk
[plfa-epub]: https://plfa.github.io/plfa.epub
[plfa-contributing]: https://plfa.github.io/Contributing/
[ghcup]: https://www.haskell.org/ghcup/
[git]: https://git-scm.com/downloads
[xcode]: https://developer.apple.com/xcode/
[agda-readthedocs-installation]: https://agda.readthedocs.io/en/v2.6.3/getting-started/installation.html
[agda-readthedocs-hello-world]: https://agda.readthedocs.io/en/v2.6.3/getting-started/hello-world.html
[agda-readthedocs-holes]: https://agda.readthedocs.io/en/v2.6.3/getting-started/a-taste-of-agda.html#preliminaries
[agda-readthedocs-emacs-mode]: https://agda.readthedocs.io/en/v2.6.3/tools/emacs-mode.html
[agda-readthedocs-emacs-notation]: https://agda.readthedocs.io/en/v2.6.3/tools/emacs-mode.html#notation-for-key-combinations
[agda-readthedocs-package-system]: https://agda.readthedocs.io/en/v2.6.3/tools/package-system.html#example-using-the-standard-library
[emacs]: https://www.gnu.org/software/emacs/download.html
[emacs-tour]: https://www.gnu.org/software/emacs/tour/
[emacs-home]: https://www.gnu.org/software/emacs/manual/html_node/efaq-w32/Location-of-init-file.html
[aquamacs]: https://aquamacs.org/
[spacemacs]: https://www.spacemacs.org/
[spacemacs-agda]: https://develop.spacemacs.org/layers/+lang/agda/README.html
[vscode]: https://code.visualstudio.com/
[vscode-agda]: https://marketplace.visualstudio.com/items?itemName=banacorn.agda-mode
[font-sourcecodepro]: https://github.com/adobe-fonts/source-code-pro
[font-dejavusansmono]: https://dejavu-fonts.github.io/
[font-freemono]: https://www.gnu.org/software/freefont/
[font-mononoki]: https://madmalik.github.io/mononoki/
[font-mononoki-debian]: https://packages.debian.org/sid/fonts/fonts-mononoki
