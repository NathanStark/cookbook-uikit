# Своя тема

Для того чтобы создать свою собственную тему, необходимо соблюдать ряд условий.

Предположим мы собираемся создавать тему и назовем "**shop**".

Необходимо реализовать следующую структуру

```
custom/shop/_import.less
custom/shop/variables.less
custom/shop/base.less
custom/shop.less
```

Это минимальная структура. Содержание файлов **variables** и **base** можно взять тут **src/less/theme/** но необходимо будет почистить от стилей базового шаблона.

В итоге у меня файл **base.less** приобрел такой вид

```
//
// Component: Base
//
// ========================================================================


// Variables
// ========================================================================

//
// New
//

//@base-code-padding-horizontal:                  6px;
//@base-code-padding-vertical:                    2px;
//@base-code-background:                          @global-muted-background;
//
//@base-blockquote-color:                         @global-emphasis-color;
//
//@base-blockquote-footer-color:                  @global-color;
//
//@base-pre-padding:                              10px;
//@base-pre-background:                           @global-background;
//@base-pre-border-width:                         @global-border-width;
//@base-pre-border:                               @global-border;
//@base-pre-border-radius:                        3px;


// Body
// ========================================================================

.hook-base-body() {}


// Links
// ========================================================================

.hook-base-link() {}

.hook-base-link-hover() {}


// Text-level semantics
// ========================================================================

.hook-base-code() {}


// Headings
// ========================================================================

.hook-base-heading() {}

.hook-base-h1() {}

.hook-base-h2() {}

.hook-base-h3() {}

.hook-base-h4() {}

.hook-base-h5() {}

.hook-base-h6() {}


// Horizontal rules
// ========================================================================

.hook-base-hr() {}


// Blockquotes
// ========================================================================

.hook-base-blockquote() {}

.hook-base-blockquote-footer() {}


// Preformatted text
// ========================================================================

.hook-base-pre() {}


// Miscellaneous
// ========================================================================

.hook-base-misc() {}
```

Файл **variables.less **стал таким

```
//
// Component: Variables
//
// ========================================================================


// Global variables
// ========================================================================
@inverse-global-color-mode: none;

//
// Typography
//

//
// Colors
//

//
// Backgrounds
//

//
// Borders
//

//
// Spacings
//

//
// Controls
//

//
// Z-index
//
```

Переменная **inverse-global-color-mode** со значением **none** объявляет что компонент [**inverse**](https://getuikit.com/docs/inverse) не будет использоваться

## Подключение файлов less в теме

Начнем по порядку, сначала описывается подключаемые файлы в файле **custom/shop.less.**

В нашем случаи его содержимое такое

```
// Base
@import "../src/less/components/variables.less";
@import "../src/less/components/mixin.less";
@import "../src/less/components/base.less";

@import "../src/less/components/inverse.less";

@import "shop/_import.less";
```

Первые 4 файла, это базовые компоненты \(каркасы компонентов\) uikit'а без которых сборка не возможна.

Последним, импортируется файл **shop/\_import.less**

Содержимое файла **shop/\_import.less**

```
// Base
@import "variables.less";
@import "base.less";
```

Как видим, в этом файле уже происходит импорт файлов, в которых мы прописываем оформление для компонентов.

## Как подключить нужный компонент ?

Логика подключения простая, в первую очередь подключается каркас, после чего оформление компонента в нашей теме. Подключим на примере компонент [Accordion](https://getuikit.com/docs/accordion#accordion)

Подключаем каркас в файле **custom/shop.less.**

```
// Base
@import "../src/less/components/variables.less";
@import "../src/less/components/mixin.less";
@import "../src/less/components/base.less";

@import "../src/less/components/accordion.less";    //Подключаем "Каркас" "Аккордеона"

@import "../src/less/components/inverse.less";

@import "shop/_import.less";
```

Теперь копируем \(для простоты\) файл из папки **src/less/components/accordion.less** в папку**  custom/shop/accordion.less**

Выполняем его подключение в файле **shop/\_import.less**

```
// Base
@import "variables.less";
@import "base.less";
@import "accordion.less";
```

Остается только отредактировать оформление нашего аккордеона в файле **custom/shop/accordion.less.** Не забываем, что мы его скопировали из "Темы по умолчанию" а значит у него уже внешнее оформление, мы его просто перенесли в нашу тему.

### **!!! Важный момент !!!**

Есть компоненты, которые зависят от других компонентов

Если посмотреть файл **src/less/components/\_import.less, **можно увидеть такие замечания

```
@import "form.less"; // After: Icon, Form Range
```

Это говорит о том, что до подключения from.less так же должны быть подключены компоненты **Icon** и **Form Range.**

Если данная последовательность не будет соблюдена, или необходимые компоненты не будут подключены, наша тема не соберется.

## Последний фокус, как подключить все компоненты ?

Предположим вы решили собрать тему на продажу, логично предположить что вам надо сделать оформление для всех компонентов. Но подключать по одному файлу может быть утомительно. В таком случаи достаточно подключить только один файл **src/less/components/\_import.less **который в свою очередь подключит все каркасы компонентов.

Напомню что этот файл подключается в файле **shop/\_import.less, **который будет иметь следующий вид

```
@import "../src/less/components/_import.less";
@import "shop/_import.less";
```

### Подводя итоги

Наша тема, по очередности подключает **less** файлы, в первую очередь подключаются компоненты которые входят в ядро uikit, они же иными словами "каркас", т.е. стили которые не имеют оформления или он базовый. После подключение всех нужных нам "каркасов", подключаются файлы оформления компонентов нашего шаблона.
