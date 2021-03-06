# BEM-диалект iDeus

Мы используем BEM CSS — т.е. BEM-методологию только применительно к CSS: без i-bem.js, bemjson, bem-tools — вот этого вот всего.
Согласно [классификации Харисова](http://download.yandex.ru/company/experience/subbotnik/minsk_harisov.pdf) (страница 83) у нас схема:
* Блоки в отдельных файлах-папках (разделены внутри scss,img,js, а не по блокам)
* + Префиксы
* + АНБ
* + Модикаторы в одном файле (нет уровней переопределения)
* нет i-bem.js
* нет сборки

## Отличия от канонического Yandex BEM-диалекта
1. Код пишется вручную без bem-tools (объяснение: второй коммент в http://clubs.ya.ru/bem/replies.xml?item_no=3905)
2. Все блоки и модификаторы в одном файле
3. js-хуки вместо i-bem.js
3. Используются префиксы, т.к. есть legacy-код (старый + сторонних библиотек)
 * b — блок
 * l — layout (блок использующийся для раскладки)
 * g — глобальный модификатор (например g-tel)
 * js — для jQuery-хуков
4. Сокращенные модификаторы через multiple classes `class="b-blockName__elName -mod_val"`.
Стили модификаторов не пишутся без привязки к имени блока `.b-block_mod_val {} = .b-block.-mod_val {}`
5. Синтаксис вида: `.b-blockName__elName.-mod_val {}`

## Техпроцесс
 * Генерации html-кода нет (увы, мы хотим, но у нас нет одного большого проекта объединяющего всё, а как у большинства — куча мелких).
 * Сборка происходит через Grunt+Sass.
 * Библиотека блоков — пишется руками, используется копипаст и правки под конкретные нужны. Обновление блоков происходит по принципу «новый проект → полезли скопипастить код из библиотеки → увидели что там чего-то нехватает или что-то неправильно → обновили в библиотеке». В существующие проекты обновления блоков из библиотеки не раскатываются, все проекты автономны.
 * Модификаторы утяжеляют вес селекторов, за 7 лет проблем ни разу не было.
