# Структура проекта

Представленная ниже структура, имеет немного модифицированый вид под мои личные проекта, на данных изменениях будет акцентировано внимание.

**Структура папок**

```
build
custom
    bitexpert
    bitexpert.less
dist
site
src
tests
```

* **build** - В папке располагаются скрипты, обеспечивающие работу сборщиков проекта.
* **custom** - В папке, располагаются создаваемые кастомные темы.
  * **bitexpert** - Папка шаблона "**bitexpert**", в нем лежат все подключаемы компоненты и дополнительные less файлы.
  * **bitexpert.less** - главный файл шаблона "**bitexpert**", он подключает все файлы из папки "**bitexpert".**
* **dist** - В эту папку собираются готовые css и js файлы всех тем.
* **site** - Папка, в которой создается html файлы проекта и верстается сайт. Данный каталог является _**личной доработкой**_.
* **src** - исходный код uikit, категорически запрещается модификация файлов в этой папке
* **tests** - Папка где лежит страница с для проверки тем \(тест\).