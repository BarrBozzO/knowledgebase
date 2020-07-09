# CSS - селекторы

Селектор определяет, к какому элементу применять то или иное CSS-правило. Браузер читает CSS-селекторы справа налево.

Важно: не существует селекторов, которые бы позволили выбрать родителя (содержащий контейнер) или соседа родителя или потомков соседа родителя.

## Базовые селекторы

- Униваресальный селектор `*` - выбирает элементы любого типа

```
* {
    color: green;
}
```

- Селектор по типу элемента - выбирает все элементы данного типа

```
input {
    padding: 10px;
}
```

- Селектор по классу - выбирает элементы основываясь на значении атрибута `class`

```
.red {
    background: red;
}
```

- Селектор по идентификатору - выбирает элементы основываясь на значении атрибута `id`. Важно: идентификатор должен быть уникальным на странице.

```
#great {
    text-transform: uppercase;
}
```

- Селектор по атрибуту - выбирает элементы имеющие данный атрибут или атрибут с определенным значением

```
[attr] {} // элементы с атрибутом имеющим имя attr

[attr=value] {} // элементы с атрибутом имеющим имя attr и значение value

[attr~=value] {} // элементы с именем атрибута attr значением которого является набор слов разделенных пробелами, одно из которых в точности равно value

[attr|=value] {} // элементы с именем атрибута attr. Его значение при этом может быть или в точности равно "value" или может начинаться с "value" со сразу же следующим "-" (U+002D).

[attr^=value] {} // элементы с именем атрибута значение которого начинается на "value"

[attr$=value] {} // элементы с именем атрибута attr значение которого заканчивается с "value"

[attr*=value] {} // элементы с именем атрибута attr значение которого содержит по крайней мере одно вхождение строки "value" как подстроки.
```

## Группивка селекторов

`,` - метод группировки. Выбирает все совпадающие элементы

```
div, span {
    color: black;
}
```

## Комбинаторы

- Комбинатор потомков
  Комбинатор `" "` (пробел) выбирает элементы соответствующие 2-му селектору, которые находятся внутри указанного (1-го) элемента вне зависимости уровня вложенности

```
div span {}
```

- Комбинатор дочерних элементов
  Комбинатор `>` выбирает все элементы соответствующие 2-му селектору, которые являются дочерними непосредственно к 1-му селектору

```
.blog > .post {}
```

- Комбинатор всех соседних элементов
  Комбинатор `~` выбирает все элементы, которые соответствуют 2-му селектору и находятся на том же уровне вложенности, что и элемент соответствующий 1-му селектору, с тем же родителем
  В примере ниже: `p ~ span` выберет все элементы `<span>`, которые находятся после элемента `<p>` внутри одного родителя.

```
p ~ span {}
```

- Комбинатор следующего соседнего элемента
  Комбинатор `+` выбирает все элементы, которые соответствуют 2-му селектору и следуют за элементом, который соответствует 1-му селектору и у них общий родитель.
  В примере ниже: селектор `ul + li` выберет любой `<li>` элемент, который находится непосредственно после элемента `<ul>`.

```
ul + li {}
```

## Псевдо

- Псевдокласс - это ключевое слово, добавленное к селектору, чтобы определить его особое состояние.

```
button:hover {}
```

- Псевдоэлемент - это ключевое слово, добавляемое к селектору, которое позволяет стилизовать определённую часть выбранного элемента

```
p::first-line {} // первая строка элемента <p>
```

### Links

[почему браузер читает CSS-селекторы справа налево](https://vk.com/@webcademy-laifhak-pochemu-brauzer-chitaet-css-selektory-sprava-nalevo)