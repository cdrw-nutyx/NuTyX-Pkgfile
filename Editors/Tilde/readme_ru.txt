Хочу показать на примере, как я создавал пакет текстового редактора tilde для консоли.
Читаю очень хорошую документацию на домашней странице tilde.
К tilde прилагаются несколько библиотек.
Смотрите схему на картинке:
<image>
Выясняю очередность зависимостей:

libtranscript
libt3config
libt3window
libt3key
libt3highlight
libt3widget
tilde

Серым цветом отмечены зависимости, которые нужно искать в системе или установить самостоятельно.

libpcre
libsigc++
XCB/Xlib
(n)curces
libunistring
libtranscript

Пытаюсь найти их в Nutyx.

Нахожу:

libpcre          = pcre         (есть, название не совпадает)
libsigc++        = libsigc++    (есть, название совпадает)
XCB/Xlib         = libxcb       (есть, название не совпадает)
(n)curces        = ncurses      (есть, название не совпадает)
libunistring     = libunistring (есть, название совпадает)

Теперь выстраиваю дерево зависимостей.

libtranscript    - без зависимостей
libt3config      - без зависимостей
libt3window      <= ncurses libunistring libtranscript
libt3key         <= libt3config libxcb ncurses
libt3highlight   <= pcre libt3config
libt3widget      <= pcre libsigc++ libt3key libxcb libunistring libt3window libtranscript
tilde            <= libt3config libt3highlight libt3widget libt3window libunistring libtranscript




