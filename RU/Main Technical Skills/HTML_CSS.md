# Вопросы для собеседования по HTML и CSS

## HTML5

<details>
<summary><b>Какие ключевые различия между HTML и HTML5?</b></summary>

HTML5 добавил: семантические элементы (header, nav, article), новые типы input для форм (date, email), теги audio/video, canvas, local storage, geolocation API, web workers. Упрощённый doctype: `<!DOCTYPE html>`. Лучшая поддержка mobile.
</details>

<details>
<summary><b>Что такое web storage в HTML5?</b></summary>

Клиентское хранилище без cookies. Два типа: LocalStorage (сохраняется до очистки, ~5MB) и SessionStorage (очищается при закрытии вкладки). Key-value пары, только строки. Доступ через `localStorage.setItem()/getItem()`.
</details>

<details>
<summary><b>В чём разница между span и div?</b></summary>

- `div`: Block-level элемент, занимает всю ширину, новая строка до/после
- `span`: Inline элемент, занимает только нужную ширину, без переносов строки

Используйте div для секций layout, span для стилизации частей текста.
</details>

<details>
<summary><b>В чём разница между элементами svg и canvas?</b></summary>

- **SVG**: Векторная графика (XML), масштабируется без потери качества, каждый элемент доступен в DOM, хорош для иконок/логотипов
- **Canvas**: Bitmap/растровый, pixel-based, рисуется через JavaScript API, хорош для игр/анимаций

SVG для статической графики, canvas для динамического рендеринга.
</details>

<details>
<summary><b>Что такое Semantic HTML?</b></summary>

Использование HTML-элементов по их смыслу, а не только внешнему виду. Примеры: `<header>`, `<nav>`, `<main>`, `<article>`, `<aside>`, `<footer>`. Преимущества: доступность (screen readers), SEO, читаемость кода.
</details>

<details>
<summary><b>Как оптимизировать ассеты сайта?</b></summary>

Изображения: сжатие, использование WebP, lazy loading, responsive images. CSS/JS: минификация, бандлинг, tree shaking. Включите gzip/brotli сжатие. Используйте CDN. Cache headers. Critical CSS inline. Defer некритичного JS.
</details>

<details>
<summary><b>Почему мы используем HTML5?</b></summary>

Лучшая поддержка мультимедиа (без Flash), чистый код с семантическими тегами, улучшенные формы, offline-возможности, лучшая мобильная поддержка, обратная совместимость, нативные API (geolocation, drag-drop).
</details>

<details>
<summary><b>Объясните новые типы input в HTML5</b></summary>

Новые типы: `email`, `url`, `tel`, `number`, `range`, `date`, `time`, `datetime-local`, `month`, `week`, `color`, `search`. Встроенная валидация, мобильные клавиатуры адаптируются под тип input.
</details>

<details>
<summary><b>Объясните HTML5 Graphics (Canvas, SVG)</b></summary>

- **Canvas**: элемент `<canvas>` + JavaScript API. 2D context для рисования фигур, изображений, текста. Хорош для игр, визуализаций. Нет DOM-доступа к нарисованным элементам
- **SVG**: XML-based разметка. Каждая фигура — DOM-элемент. Масштабируемый, стилизуется CSS. Хорош для иконок, графиков, логотипов
</details>

<details>
<summary><b>Что такое WebGL и когда его использовать?</b></summary>

WebGL — JavaScript API для рендеринга 2D/3D графики через GPU с помощью `<canvas>`.

**Характеристики:**
- Аппаратное ускорение (GPU)
- Shader-based рендеринг
- Высокая производительность для сложной графики
- Сложно реализовать напрямую

**Случаи использования:** 3D-сцены, визуализация данных, игры. Избыточен для простого UI.

**Когда что использовать:**
- SVG → UI-графика, иконки, диаграммы
- Canvas → игры, анимации, высокочастотные обновления
- WebGL → сложная 3D-графика
</details>

<details>
<summary><b>Canvas vs SVG — когда что использовать?</b></summary>

| Критерий | Canvas | SVG |
|----------|--------|-----|
| Тип графики | Растр (пиксели) | Вектор |
| Доступ к DOM | Нет | Да |
| Масштабируемость | Плохая | Отличная |
| Интерактивность | Ручная | Нативная (CSS, events) |
| Производительность | Высокая для многих объектов | Медленнее при тысячах |

**Canvas**: игры, анимации, real-time графика.
**SVG**: иконки, диаграммы, интерактивные графики.
</details>

## Основы CSS

<details>
<summary><b>Опишите различные виды селекторов?</b></summary>

- Element: `div`
- Class: `.classname`
- ID: `#idname`
- Attribute: `[type="text"]`
- Pseudo-class: `:hover`, `:first-child`
- Pseudo-element: `::before`, `::after`
- Combinator: `div > p` (child), `div p` (descendant), `div + p` (adjacent)
</details>

<details>
<summary><b>В чём разница между class и ID?</b></summary>

- **Class**: Переиспользуемый, несколько элементов могут иметь один класс, меньшая специфичность
- **ID**: Уникален на странице, только один элемент, выше специфичность

Используйте классы для стилей, ID для JavaScript или якорей.
</details>

<details>
<summary><b>Какие элементы CSS Box Model?</b></summary>

Каждый элемент — это box с: Content (содержимое) → Padding (отступ внутри border) → Border → Margin (отступ снаружи border). `box-sizing: border-box` включает padding/border в width.
</details>

<details>
<summary><b>Какие ограничения у CSS?</b></summary>

Нет parent selector (`:has()` — новый), нет переменных в старых браузерах (custom properties теперь есть), конфликты специфичности, несовместимость браузеров, нет встроенной логики/циклов (помогают препроцессоры), вертикальное центрирование исторически было сложным.
</details>

<details>
<summary><b>В чём разница между inline, inline-block и block?</b></summary>

- **Block**: Полная ширина, новая строка, учитывает width/height/margin
- **Inline**: Только ширина контента, без переноса строки, игнорирует width/height, только горизонтальный margin
- **Inline-block**: Inline flow, но учитывает width/height/margins
</details>

<details>
<summary><b>В чём различия между adaptive и responsive design?</b></summary>

- **Responsive**: Fluid layouts, flexible images, media queries. Плавно адаптируется к любому размеру экрана
- **Adaptive**: Фиксированные layouts для конкретных breakpoints (320px, 768px и т.д.). Переключается между дизайнами

Responsive более гибкий, adaptive может быть более оптимизирован под устройство.
</details>

## CSS Preprocessors (Sass, Less, Stylus)

<details>
<summary><b>Что такое CSS Preprocessor? Что такое Sass, Less и Stylus? Зачем их используют?</b></summary>

Препроцессоры расширяют CSS: переменные, вложенность, mixins, функции, импорты. Компилируются в обычный CSS. Sass (SCSS синтаксис популярен), Less (похож, на JS), Stylus (минимальный синтаксис). Преимущества: DRY код, поддерживаемость, организация.
</details>

<details>
<summary><b>Почему использовать SCSS вместо чистого CSS?</b></summary>

Переменные для цветов/размеров, вложенность для более чистого кода, mixins для переиспользуемого кода, partials для организации, математические операции, функции. Современный CSS имеет переменные, но SCSS всё ещё предлагает больше фич.
</details>

<details>
<summary><b>Можно ли импортировать только часть Sass-файла? Если да, как?</b></summary>

Используйте partials (файлы, начинающиеся с `_`). Импортируйте через `@use` или `@import`. Для частичного импорта только переменных/mixins используйте `@use 'file' as namespace` и обращайтесь к конкретным элементам: `namespace.$variable`.
</details>

<details>
<summary><b>Что такое nesting в SCSS?</b></summary>

Пишите дочерние селекторы внутри родительских. Отражает структуру HTML. Пример:
```scss
.nav {
  ul { list-style: none; }
  li { display: inline; }
  a { color: blue; &:hover { color: red; } }
}
```
`&` ссылается на родительский селектор.
</details>

<details>
<summary><b>Какова цель mixins в SCSS?</b></summary>

Переиспользуемые блоки CSS. Могут принимать параметры. Пример:
```scss
@mixin flex-center { display: flex; justify-content: center; align-items: center; }
.container { @include flex-center; }
```
Хорошо для vendor prefixes, общих паттернов.
</details>

<details>
<summary><b>Можете объяснить что такое pseudo-classes? Приведите примеры.</b></summary>

Pseudo-classes выбирают элементы в определённом состоянии. Примеры: `:hover` (наведение мыши), `:focus` (в фокусе), `:first-child`, `:last-child`, `:nth-child(n)`, `:not()`, `:disabled`, `:checked`, `:empty`.
</details>

## BEM

<details>
<summary><b>Что такое BEM?</b></summary>

Block Element Modifier — соглашение об именовании CSS. Формат: `block__element--modifier`. Пример: `card__title--large`. Преимущества: понятная структура, избегает войн специфичности, самодокументируемый, переиспользуемый.
</details>

<details>
<summary><b>Что такое block, element, modificator в BEM?</b></summary>

- **Block**: Самостоятельный компонент (`menu`, `card`, `button`)
- **Element**: Часть block, не имеет смысла отдельно (`menu__item`, `card__title`)
- **Modifier**: Вариант или состояние (`button--primary`, `menu__item--active`)
</details>

## CSS Modules

<details>
<summary><b>Что такое CSS modules и чем они отличаются от традиционных CSS stylesheets?</b></summary>

CSS Modules локально скопируют стили к компоненту. Имена классов становятся уникальными (хэшируются). Импортируйте стили как объект: `import styles from './Button.module.css'`. Нет глобальных конфликтов, явные зависимости.
</details>

<details>
<summary><b>Как определить CSS module и какие лучшие практики структурирования CSS module файлов?</b></summary>

Называйте файл с расширением `.module.css`. Один module на компонент. Используйте camelCase для имён классов. Держите связанные стили вместе. Пример: `Button.module.css` рядом с `Button.tsx`.
</details>

<details>
<summary><b>Как CSS modules помогают решить общие проблемы CSS типа global namespace pollution и конфликтов стилей?</b></summary>

Каждое имя класса преобразуется в уникальный хэш при сборке (например, `button` → `Button_button_x7f3d`). Нет global scope по умолчанию. Стили применяются только там, где явно импортированы. Исключает случайные перезаписи.
</details>

<details>
<summary><b>Как интегрировать CSS modules в проект и какие инструменты помогают в этом процессе?</b></summary>

Встроено в Create React App и Next.js. Для кастомной настройки: настройте webpack с `css-loader` и `modules: true`. Импорт: `import styles from './file.module.css'`. Использование: `className={styles.button}`.
</details>

## Bootstrap

<details>
<summary><b>Что такое Bootstrap и чем он отличается от других CSS frameworks?</b></summary>

Популярный CSS framework от Twitter. Предоставляет: grid system, готовые компоненты, утилиты, responsive design. Отличия: наиболее широко используемый, обширная документация, консистентная дизайн-система. Альтернативы: Tailwind (utility-first), Bulma (flexbox-based).
</details>

## Styled-components и Emotion

<details>
<summary><b>Как работают styled-components?</b></summary>

CSS-in-JS библиотека. Пишите CSS в JavaScript template literals. Создаёт React-компонент с прикреплёнными стилями. Scoped по умолчанию, поддерживает props для динамических стилей. Пример:
```javascript
const Button = styled.button`background: ${props => props.primary ? 'blue' : 'gray'}`;
```
</details>

<details>
<summary><b>Какие преимущества CSS-in-JS решений?</b></summary>

Scoped стили (нет конфликтов), динамическая стилизация по props/state, co-located с компонентом, dead code elimination, автоматические vendor prefixes, поддержка тем, интеграция TypeScript.
</details>

## Material-UI и Ant Design

<details>
<summary><b>Какой у вас опыт с Material-UI?</b></summary>

MUI — библиотека React-компонентов, реализующая Material Design. Предоставляет: готовые компоненты (кнопки, формы, диалоги), систему тем, styled-components или emotion под капотом. Хорош для быстрой разработки с консистентным дизайном.
</details>

<details>
<summary><b>Как кастомизировать темы Material-UI?</b></summary>

Используйте `createTheme()` для кастомизации цветов, типографики, отступов. Оберните приложение в `ThemeProvider`. Переопределяйте стили компонентов через `styleOverrides` в теме или проп `sx`. Можно кастомизировать отдельные компоненты или глобальные defaults.
</details>

## CSS Animations

<details>
<summary><b>Как создавать CSS-анимации?</b></summary>

Два способа:
1. `@keyframes` + свойство `animation`: Определите состояния в процентах, применяйте с animation name/duration/timing
2. `transition`: Автоматически анимирует изменения свойств

```css
@keyframes fade { from { opacity: 0; } to { opacity: 1; } }
.element { animation: fade 1s ease-in; }
```
</details>

<details>
<summary><b>В чём разница между transitions и animations?</b></summary>

- **Transitions**: Анимация между двумя состояниями, триггерится изменением состояния (hover, class), проще
- **Animations**: Несколько keyframes, может зацикливаться, воспроизводится автоматически, больше контроля

Используйте transitions для простых hover-эффектов, animations для сложных последовательностей.
</details>

## Storybook

<details>
<summary><b>Что такое Storybook и почему он полезен?</b></summary>

Среда разработки UI для создания компонентов в изоляции. Преимущества: разработка без запуска всего приложения, документация компонентов, визуальное тестирование, демонстрация дизайнерам/stakeholders, тестирование edge cases.
</details>

<details>
<summary><b>Как документировать компоненты в Storybook?</b></summary>

Создавайте файлы `.stories.js` с вариантами компонента. Используйте `args` для контролов props. Добавляйте JSDoc комментарии. Используйте `@storybook/addon-docs` для MDX документации. Настраивайте argTypes для документации props.
</details>

## Практические задания

<details>
<summary><b>Создать простые визуальные компоненты на чистом CSS/SCSS (card component, стилизация формы)</b></summary>

Card: контейнер с padding, border-radius, box-shadow. Form: консистентные стили input, focus states, labels, состояния валидации. Используйте flexbox/grid для layout.
</details>

<details>
<summary><b>Создать сложные визуальные компоненты на чистом CSS/SCSS</b></summary>

Примеры: кастомный checkbox/radio, tooltips, модальные окна, dropdown menus, tabs, accordions. Требуется: pseudo-elements, positioning, transitions, возможно CSS-only state management.
</details>

<details>
<summary><b>Создать стайл-структуру проекта и тему</b></summary>

Организуйте: переменные (цвета, отступы, шрифты), mixins, базовые стили, компоненты. Объект темы с консистентными scales. Подход design tokens. Продумайте dark mode с самого начала.
</details>

## Shadow DOM

<details>
<summary><b>Что такое Shadow DOM?</b></summary>

Shadow DOM изолирует разметку и стили от основной страницы. Предотвращает конфликты — стили внутри не утекают наружу, внешние стили не проникают внутрь. Используется в Web Components. Создаётся через `element.attachShadow({mode: 'open'})`.
</details>

## Browser Rendering

<details>
<summary><b>Что такое Browser Rendering Pipeline?</b></summary>

Браузер превращает код в пиксели в несколько этапов:
1. **Parse** HTML → DOM tree, CSS → CSSOM
2. **Style** calculation (объединение DOM + CSSOM)
3. **Layout** (расчёт позиций/размеров)
4. **Paint** (заполнение пикселей)
5. **Composite** (управление слоями)

Layout и painting дорогие. Их уменьшение улучшает производительность.
</details>

<details>
<summary><b>Что такое Critical Rendering Path?</b></summary>

Последовательность шагов, которые браузер выполняет для рендеринга первых пикселей. Включает: парсинг HTML, парсинг CSS, построение render tree, layout, paint. Оптимизируйте через: минимизацию критических ресурсов, сокращение длины критического пути, инлайнинг critical CSS, defer некритичного JS.
</details>

## Core Web Vitals

<details>
<summary><b>Что такое Core Web Vitals?</b></summary>

Метрики Google, измеряющие пользовательский опыт:
- **LCP** (Largest Contentful Paint): Загрузка — основной контент виден < 2.5s
- **INP** (Interaction to Next Paint): Интерактивность — отклик < 200ms
- **CLS** (Cumulative Layout Shift): Визуальная стабильность — score < 0.1

Влияют на SEO-рейтинг. Измеряйте через Lighthouse, PageSpeed Insights или библиотеку Web Vitals.
</details>

<details>
<summary><b>Что такое Web Vitals (LCP, FID, CLS)?</b></summary>

Web Vitals — стандартизированные метрики для измерения качества навигации на сайте:

- **LCP (Largest Contentful Paint)** — измеряет время, за которое самый большой видимый элемент контента полностью загрузится и отрендерится. Хороший LCP — менее 2.5 секунд.
- **FID (First Input Delay)** — измеряет время, за которое браузер ответит на первое взаимодействие пользователя. Хороший FID — менее 100 миллисекунд. (Примечание: FID заменяется на INP с 2024+)
- **CLS (Cumulative Layout Shift)** — измеряет визуальную стабильность, суммируя все неожиданные сдвиги макета за время жизни страницы. Хороший CLS — менее 0.1.
</details>

## Доступность (Accessibility)

<details>
<summary><b>Что такое стандарт WAI-ARIA?</b></summary>

WAI-ARIA (Web Accessibility Initiative - Accessible Rich Internet Applications) — техническая спецификация, разработанная W3C. Её цель — улучшить доступность веб-контента и приложений, особенно для пользователей с ограниченными возможностями, использующих вспомогательные технологии типа screen readers или альтернативные устройства ввода.

**Ключевые элементы:**
- Roles: Определяют что такое элемент (`role="button"`, `role="navigation"`)
- States: Динамические состояния (`aria-expanded`, `aria-checked`)
- Properties: Характеристики (`aria-label`, `aria-describedby`)

**Использование:**
```html
<button aria-expanded="false" aria-controls="menu">Меню</button>
<nav role="navigation" aria-label="Главная навигация">...</nav>
```

Используйте ARIA только когда нативной HTML-семантики недостаточно.
</details>

## Современные возможности CSS

<details>
<summary><b>Как использовать nesting на чистом CSS?</b></summary>

CSS Nesting теперь нативно поддерживается современными браузерами (2023+). Можно писать вложенные селекторы напрямую в CSS без препроцессоров:

```css
.card {
  padding: 1rem;

  .title {
    font-size: 1.5rem;
  }

  &:hover {
    background: #f0f0f0;
  }

  @media (min-width: 768px) {
    padding: 2rem;
  }
}
```

**Поддержка браузеров:** Chrome 112+, Firefox 117+, Safari 17.2+. Для старых браузеров используйте препроцессоры типа Sass/Less.
</details>

<details>
<summary><b>Что такое container queries?</b></summary>

Container queries позволяют применять стили на основе размера контейнера, а не viewport. Это делает компоненты более отзывчивыми и переиспользуемыми.

```css
.card-container {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card {
    display: flex;
    flex-direction: row;
  }
}
```

**Преимущества:**
- Компоненты адаптируются к контейнеру, а не только к viewport
- Более модульные и переиспользуемые компоненты
- Лучший компонентный дизайн
- Не нужен JavaScript для адаптивных компонентов
</details>

<details>
<summary><b>Как работает CSS Grid subgrid?</b></summary>

CSS Grid subgrid позволяет вложенной grid наследовать строки или колонки родительской grid. Это полезно для выравнивания контента вложенных grid-элементов со структурой родительской grid.

```css
.parent {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  gap: 1rem;
}

.child {
  display: grid;
  grid-column: span 3;
  grid-template-columns: subgrid; /* Наследует колонки родителя */
}
```

**Преимущества:**
- Выравнивание вложенного контента с родительской grid
- Не нужно дублировать определения строк/колонок
- Чище разметка без сложного позиционирования
- Идеально для карточек, форм и таблиц данных
</details>

<details>
<summary><b>Почему Facebook больше не хочет следовать направлению CSS-in-JS?</b></summary>

CSS-in-JS библиотеки (styled-components, Emotion) не генерируют статические CSS-файлы при сборке. Вместо этого они генерируют JavaScript, который устанавливает стили через CSSStyleSheet API в runtime.

**Выявленные проблемы:**
- Runtime overhead: JS должен выполниться для применения стилей
- Больший размер bundle
- Проблемы hydration при SSR
- Потребление памяти

**Решение:** Facebook создал **StyleX** — библиотеку, которая извлекает стили при сборке в статические CSS-файлы, получая преимущества DX от CSS-in-JS (colocation, типобезопасность) при выводе оптимизированного статического CSS.
</details>

<details>
<summary><b>Что предлагает библиотека StyleX?</b></summary>

StyleX — CSS-библиотека от Facebook/Meta для эффективного и модульного управления стилями.

**Ключевые особенности:**
- **Извлечение при сборке**: Стили компилируются в атомарный CSS во время сборки
- **Типобезопасность**: Полная поддержка TypeScript
- **Детерминированность**: Стили всегда разрешаются одинаково
- **Малый output**: Дедупликация стилей, отправляется только используемое
- **Нет runtime-затрат**: В отличие от styled-components, нет JS runtime для стилей

```javascript
import * as stylex from '@stylexjs/stylex';

const styles = stylex.create({
  button: {
    backgroundColor: 'blue',
    padding: '8px 16px',
  }
});

<button {...stylex.props(styles.button)}>Нажми</button>
```
</details>

## Продвинутые техники CSS

<details>
<summary><b>Как спроектировать адаптивную сетку без CSS-фреймворков?</b></summary>

**Современный подход с CSS Grid:**

```css
/* Авто-адаптивная сетка — элементы автоматически подстраиваются */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
}

/* Классическая 12-колоночная система */
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.col-6 { grid-column: span 6; }
.col-4 { grid-column: span 4; }
.col-3 { grid-column: span 3; }

/* Адаптивность с media queries */
@media (max-width: 768px) {
  .col-6, .col-4, .col-3 {
    grid-column: span 12;
  }
}

/* Альтернатива на Flexbox */
.flex-grid {
  display: flex;
  flex-wrap: wrap;
  margin: -10px; /* Компенсация отступов элементов */
}

.flex-item {
  flex: 1 1 calc(33.333% - 20px);
  margin: 10px;
  min-width: 250px; /* Предотвращает слишком узкие элементы */
}
```

**Ключевые техники:**
- `minmax()` для гибких, но ограниченных размеров
- `auto-fit`/`auto-fill` для автоматического количества колонок
- `clamp()` для адаптивных значений: `clamp(300px, 50%, 600px)`
- CSS-переменные для консистентных отступов
</details>

<details>
<summary><b>Объясните CSS containment и как он улучшает производительность</b></summary>

**CSS свойство `contain`** сообщает браузеру, что элемент независим от остальной страницы, включая оптимизации рендеринга.

```css
.card {
  contain: layout style paint;
  /* Или сокращённо: */
  contain: content; /* = layout + style + paint */
  contain: strict;  /* = size + layout + style + paint */
}
```

**Типы containment:**

| Значение | Описание | Случай использования |
|----------|----------|---------------------|
| `layout` | Layout элемента независим | Карточки, элементы списка |
| `paint` | Ничего снаружи не отрисовывается внутри | Виджеты, модалки |
| `style` | Counter/quotes не влияют на внешние | Изолированные компоненты |
| `size` | Размер не зависит от children | Контейнеры фиксированного размера |
| `content` | Всё кроме size | Большинство компонентов |
| `strict` | Полный containment | Полная изоляция |

**Преимущества для производительности:**
1. **Пропуск пересчёта**: Браузер знает, что изменения не влияют на остальную страницу
2. **Ограничение repaints**: Перерисовывается только contained элемент
3. **Включает оптимизацию слоёв**: Может быть promoted в собственный compositing layer

**Лучшие практики:**
```css
/* Хорошо для виртуализированных списков */
.list-item {
  contain: content;
  content-visibility: auto; /* Рендерить только когда во viewport */
}

/* Элементы вне экрана */
.hidden-panel {
  content-visibility: hidden;
}
```
</details>

<details>
<summary><b>Как создавать полностью доступные компоненты (стандарты WCAG)?</b></summary>

**Ключевые принципы WCAG 2.1 (POUR):**

1. **Perceivable (Воспринимаемость):**
```html
<!-- Alt-текст для изображений -->
<img src="chart.png" alt="Продажи выросли на 25% в Q4 2024">

<!-- Субтитры для медиа -->
<video>
  <track kind="captions" src="captions.vtt" srclang="ru">
</video>

<!-- Достаточный контраст цветов (4.5:1 для обычного текста) -->
```

2. **Operable (Управляемость):**
```html
<!-- Доступность с клавиатуры -->
<button onclick="submit()">Отправить</button> <!-- ✓ -->
<div onclick="submit()">Отправить</div> <!-- ✗ Не фокусируемый -->

<!-- Skip links -->
<a href="#main-content" class="skip-link">Перейти к основному контенту</a>

<!-- Видимый фокус -->
<style>
button:focus-visible { outline: 2px solid blue; }
</style>
```

3. **Understandable (Понятность):**
```html
<!-- Декларация языка -->
<html lang="ru">

<!-- Лейблы форм -->
<label for="email">Email адрес</label>
<input id="email" type="email" aria-describedby="email-hint">
<span id="email-hint">Мы никогда не поделимся вашим email</span>

<!-- Сообщения об ошибках -->
<input aria-invalid="true" aria-errormessage="email-error">
<span id="email-error" role="alert">Пожалуйста, введите валидный email</span>
```

4. **Robust (Надёжность):**
```html
<!-- Семантический HTML -->
<nav aria-label="Главная навигация">
  <ul role="menubar">
    <li role="none"><a role="menuitem" href="/">Главная</a></li>
  </ul>
</nav>

<!-- ARIA для кастомных компонентов -->
<div role="tablist">
  <button role="tab" aria-selected="true" aria-controls="panel1">Вкладка 1</button>
</div>
<div role="tabpanel" id="panel1">Контент</div>
```

**Тестирование:** Используйте Axe, Lighthouse, NVDA/VoiceOver для тестирования screen reader.
</details>

<details>
<summary><b>Реализуйте систему модальных окон с focus trapping</b></summary>

```javascript
function Modal({ isOpen, onClose, children }) {
  const modalRef = useRef(null);
  const previousActiveElement = useRef(null);

  useEffect(() => {
    if (isOpen) {
      // Сохраняем текущий сфокусированный элемент
      previousActiveElement.current = document.activeElement;

      // Фокусируем первый фокусируемый элемент в модалке
      const focusableElements = getFocusableElements(modalRef.current);
      focusableElements[0]?.focus();

      // Предотвращаем скролл body
      document.body.style.overflow = 'hidden';
    }

    return () => {
      // Восстанавливаем фокус и скролл
      previousActiveElement.current?.focus();
      document.body.style.overflow = '';
    };
  }, [isOpen]);

  // Focus trap
  const handleKeyDown = (e) => {
    if (e.key === 'Escape') {
      onClose();
      return;
    }

    if (e.key !== 'Tab') return;

    const focusableElements = getFocusableElements(modalRef.current);
    const firstElement = focusableElements[0];
    const lastElement = focusableElements[focusableElements.length - 1];

    // Shift+Tab на первом элементе -> фокус на последний
    if (e.shiftKey && document.activeElement === firstElement) {
      e.preventDefault();
      lastElement.focus();
    }
    // Tab на последнем элементе -> фокус на первый
    else if (!e.shiftKey && document.activeElement === lastElement) {
      e.preventDefault();
      firstElement.focus();
    }
  };

  if (!isOpen) return null;

  return createPortal(
    <div
      className="modal-overlay"
      onClick={(e) => e.target === e.currentTarget && onClose()}
      onKeyDown={handleKeyDown}
    >
      <div
        ref={modalRef}
        role="dialog"
        aria-modal="true"
        aria-labelledby="modal-title"
        className="modal-content"
      >
        {children}
        <button onClick={onClose} aria-label="Закрыть модальное окно">×</button>
      </div>
    </div>,
    document.body
  );
}

function getFocusableElements(container) {
  return container.querySelectorAll(
    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
}
```

```css
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  max-width: 500px;
  max-height: 90vh;
  overflow-y: auto;
}
```
</details>

<details>
<summary><b>Как исправить проблемы со сдвигами layout в UI с большим количеством изображений?</b></summary>

**Распространённые причины и решения:**

1. **Резервируйте место для изображений:**
```css
/* Контейнер с aspect ratio */
.image-container {
  aspect-ratio: 16 / 9;
  background: #f0f0f0; /* Цвет placeholder */
}

/* Или явные размеры */
<img width="800" height="600" src="image.jpg" alt="">
```

2. **Используйте современный CSS:**
```css
img {
  max-width: 100%;
  height: auto;
  /* Предотвращение layout shift при загрузке */
  aspect-ratio: attr(width) / attr(height);
}
```

3. **Skeleton loaders:**
```css
.skeleton {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

4. **Оптимизация загрузки шрифтов:**
```css
/* Предотвращение FOUT (Flash of Unstyled Text) */
@font-face {
  font-family: 'MyFont';
  src: url('font.woff2') format('woff2');
  font-display: swap; /* или optional/fallback */
  size-adjust: 100%; /* Совпадение метрик с fallback */
}

/* Подгонка fallback-шрифта под основной */
body {
  font-family: 'MyFont', system-ui;
}
```

5. **Реклама и embeds:**
```css
/* Резервируем место для динамического контента */
.ad-container {
  min-height: 250px;
  contain: layout;
}
```

6. **Мониторинг метрикой CLS:**
```javascript
// Используйте библиотеку web-vitals
import { getCLS } from 'web-vitals';
getCLS(console.log); // Отслеживание layout shifts
```
</details>

## Оптимизация производительности

<details>
<summary><b>Объясните TBT, LCP, CLS и как улучшить каждую метрику</b></summary>

**TBT (Total Blocking Time):**
Время между FCP и TTI, когда главный поток заблокирован на >50мс.

*Улучшения:*
- Разбивайте длинные JavaScript-задачи
- Откладывайте некритичные скрипты
- Используйте web workers для тяжёлых вычислений
- Уменьшайте влияние сторонних скриптов
- Code splitting и lazy loading

**LCP (Largest Contentful Paint):**
Время до рендеринга самого большого видимого элемента (цель: <2.5s).

*Улучшения:*
```html
<!-- Preload критических ресурсов -->
<link rel="preload" as="image" href="hero.jpg">
<link rel="preload" as="font" href="font.woff2" crossorigin>

<!-- Оптимизация изображений -->
<img
  src="hero.jpg"
  srcset="hero-480.jpg 480w, hero-800.jpg 800w"
  sizes="(max-width: 600px) 480px, 800px"
  loading="eager" <!-- Не используем lazy load для LCP-изображения -->
  fetchpriority="high"
>
```
- Используйте CDN для ассетов
- Оптимизируйте время ответа сервера (TTFB)
- Удалите render-blocking ресурсы

**CLS (Cumulative Layout Shift):**
Сумма неожиданных сдвигов layout (цель: <0.1).

*Улучшения:*
- Устанавливайте явные размеры для медиа
- Резервируйте место для рекламы/embeds
- Избегайте вставки контента выше существующего
- Используйте `transform` для анимаций (не вызывает layout)
- Используйте `content-visibility` для контента вне экрана
```css
img, video { aspect-ratio: 16/9; }
.dynamic-content { min-height: 200px; }
```
</details>

<details>
<summary><b>Как применять code splitting, tree-shaking и deferred loading в SPA?</b></summary>

**Code Splitting:**
```javascript
// Route-based splitting с React.lazy
const Dashboard = lazy(() => import('./Dashboard'));
const Settings = lazy(() => import('./Settings'));

// Component-based splitting
const HeavyChart = lazy(() => import('./HeavyChart'));

// Webpack magic comments для именованных chunks
const AdminPanel = lazy(() =>
  import(/* webpackChunkName: "admin" */ './AdminPanel')
);
```

**Tree-Shaking:**
```javascript
// ✓ Tree-shakable (named exports)
import { debounce } from 'lodash-es';

// ✗ Не tree-shakable (default/namespace import)
import _ from 'lodash';

// Конфигурация в bundler
// webpack.config.js
module.exports = {
  mode: 'production', // Включает tree-shaking
  optimization: {
    usedExports: true,
    sideEffects: true
  }
};

// package.json — помечаем как без побочных эффектов
{
  "sideEffects": false,
  // Или указываем файлы с побочными эффектами
  "sideEffects": ["*.css", "./src/polyfills.js"]
}
```

**Deferred Loading:**
```html
<!-- Откладываем некритичные скрипты -->
<script src="analytics.js" defer></script>
<script src="chat-widget.js" async></script>

<!-- Preload критичное, prefetch будущее -->
<link rel="preload" href="critical.js" as="script">
<link rel="prefetch" href="next-page.js">
```

```javascript
// Dynamic imports для фич
button.addEventListener('click', async () => {
  const { openModal } = await import('./modal');
  openModal();
});

// Intersection Observer для lazy-компонентов
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      import('./heavy-component').then(module => {
        module.init(entry.target);
      });
      observer.unobserve(entry.target);
    }
  });
});
```
</details>

## DOM и Browser APIs

<details>
<summary><b>В чём разница между innerHTML и textContent?</b></summary>

- `innerHTML`: Парсит HTML, может выполнять скрипты. Используйте для добавления HTML структуры. Риск безопасности с пользовательским вводом (XSS)
- `textContent`: Только plain text, быстрее, без парсинга. Безопаснее для пользовательского контента

Используйте `textContent` для текста, `innerHTML` только для доверенного HTML.
</details>

<details>
<summary><b>Как работает делегирование событий?</b></summary>

Вешаем один обработчик на родителя вместо многих на детей. События всплывают вверх от target. Проверяем `event.target` для определения кликнутого элемента:
```javascript
list.addEventListener('click', (e) => {
  if (e.target.matches('li')) handleItemClick(e.target);
});
```
Преимущества: меньше listeners, работает с динамическими элементами.
</details>

<details>
<summary><b>В чём разница между всплытием и погружением событий?</b></summary>

- **Capturing (погружение)**: Событие идёт от корня к target (сверху вниз). Редко используется
- **Bubbling (всплытие)**: Событие идёт от target к корню (снизу вверх). Поведение по умолчанию

```javascript
// Использовать фазу capturing
element.addEventListener('click', handler, true);
```
</details>

<details>
<summary><b>В чём разница между preventDefault и stopPropagation?</b></summary>

- `preventDefault()`: Останавливает дефолтное действие браузера (submit формы, переход по ссылке). Событие всё ещё всплывает
- `stopPropagation()`: Останавливает всплытие события. Дефолтное действие всё ещё происходит

Используйте оба когда нужно: `e.preventDefault(); e.stopPropagation();`
</details>

<details>
<summary><b>Что такое Intersection Observer API?</b></summary>

Асинхронный способ наблюдать видимость элемента во viewport. Лучше чем scroll listeners для: lazy loading изображений, infinite scroll, отслеживания видимости:
```javascript
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) loadContent(entry.target);
  });
}, { threshold: 0.5 });
observer.observe(element);
```
</details>

<details>
<summary><b>Как работает requestAnimationFrame?</b></summary>

Планирует callback перед следующей перерисовкой браузера (~60fps). Лучше чем `setInterval` для анимаций:
```javascript
function animate() {
  updatePosition();
  requestAnimationFrame(animate);
}
requestAnimationFrame(animate);
```
Приостанавливается когда вкладка неактивна, синхронизируется с частотой обновления дисплея.
</details>

<details>
<summary><b>Что такое CORS и как с ним работать?</b></summary>

Cross-Origin Resource Sharing - браузерная защита, ограничивающая запросы к другим доменам. Сервер должен отправлять CORS заголовки:
```
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Methods: GET, POST
```
Решения: серверный proxy, CORS заголовки на API.
</details>

<details>
<summary><b>Что такое reflow vs repaint?</b></summary>

- **Reflow**: Браузер пересчитывает layout (позиции, размеры). Дорого. Триггерится: изменения размеров, структуры DOM, resize окна
- **Repaint**: Перерисовка видимых элементов без изменения layout. Дешевле. Триггерится: цвет, visibility, background

Минимизируйте reflows: группируйте чтения/записи DOM, используйте `transform` для анимаций.
</details>

<details>
<summary><b>Что триггерит browser reflow и как его минимизировать?</b></summary>

**Триггеры reflow:**

1. **Изменение структуры DOM**: Добавление/удаление элементов, изменение innerHTML
2. **Изменение геометрии**: Width, height, padding, margin, border
3. **Изменение позиции**: top, left, свойство position
4. **Изменение display**: display, visibility
5. **Изменение шрифта**: font-size, font-family
6. **Чтение layout-свойств**: offsetWidth, offsetHeight, getBoundingClientRect(), scrollTop

**Частая ошибка — layout thrashing:**
```javascript
// Плохо: Множество reflows
items.forEach(item => {
  const height = element.offsetHeight; // Чтение (триггерит reflow)
  element.style.height = height + 10 + 'px'; // Запись
});

// Хорошо: Все чтения, затем все записи
const heights = items.map(() => element.offsetHeight); // Все чтения
items.forEach((item, i) => {
  element.style.height = heights[i] + 10 + 'px'; // Все записи
});
```

**Стратегии минимизации:**

1. **Группируйте изменения DOM**:
```javascript
// Используйте DocumentFragment
const fragment = document.createDocumentFragment();
items.forEach(item => fragment.appendChild(createNode(item)));
container.appendChild(fragment); // Один reflow
```

2. **Используйте CSS-классы вместо inline-стилей**:
```javascript
// Плохо: Несколько reflows
el.style.width = '100px';
el.style.height = '100px';
el.style.margin = '10px';

// Хорошо: Один reflow
el.classList.add('box-style');
```

3. **Используйте transform/opacity для анимаций** (GPU-ускорение, пропуск layout):
```css
/* Плохо */
.animate { left: 100px; top: 100px; }

/* Хорошо */
.animate { transform: translate(100px, 100px); }
```

4. **Используйте `will-change` для сложных анимаций**:
```css
.animated { will-change: transform, opacity; }
```

5. **Используйте CSS containment**:
```css
.isolated { contain: layout; }
```
</details>

<details>
<summary><b>Как работает History API?</b></summary>

Манипуляция историей браузера без перезагрузки страницы:
```javascript
history.pushState({ page: 1 }, '', '/page-1'); // Добавить запись
history.replaceState({}, '', '/new-url'); // Заменить текущую
history.back(); // Назад
window.onpopstate = (e) => handleNavigation(e.state);
```
Используется SPA роутерами для навигации.
</details>

<details>
<summary><b>Что такое полифиллы и когда они нужны?</b></summary>

Код, реализующий современные фичи в старых браузерах. Примеры: Promise, fetch, Array.includes. Используйте когда:
- Поддерживаете старые браузеры (IE11)
- Используете новые API, ещё не поддерживаемые широко

Инструменты: core-js, polyfill.io. Современные приложения часто пропускают для меньшего bundle.
</details>
