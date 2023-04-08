# Оглавление

{{< toc >}}

# Общие сведения

Анимации объявляются с помощью ключевого слова `animation`.

```ini
animation=NAME,ONOFF,SPEED,CURVE,STYLE
или
animation=NAME,ONOFF,SPEED,CURVE
```

`ONOFF` - может быть либо 0, либо 1, 0 - отключить, 1 - включить.

`SPEED` - количество ds, которое займет анимация.

`CURVE` - имя кривой безье, см. [curves](#curves).

`STYLE` - стиль анимации. (необязательно)

**PS:** 1 ds это 100 милисекунд.

Анимации представляют собой дерево. Если анимация не задана, она наследует свои
родительские значения. См. [дерево анимаций](#animation-tree).

## Примеры

```ini
animation=workspaces,1,8,default
animation=windows,1,10,myepiccurve,slide
```

## Дерево анимации

```txt
global
  ↳ windows - styles: slide, popin
    ↳ windowsIn - открытие окна
    ↳ windowsOut - закрытие окна
    ↳ windowsMove - все, что между ними, перемещение, перетаскивание, изменение размера
  ↳ fade
    ↳ fadeIn - затухание (открытие) -> слои и окна
    ↳ fadeOut - затухание (закрытие) -> слои и окна
    ↳ fadeSwitch - затухание при изменении активного окна, и его непрозрачности
    ↳ fadeShadow - затухание при смене активного окна для теней
    ↳ fadeDim - ослабление тусклости неактивных окон
  ↳ border - для анимации скорости переключения цвета границы
  ↳ borderangle - для анимации угла градиента границы - styles: once, loop
  ↳ workspaces - styles: slide, slidevert, fade
    ↳ specialWorkspace - styles: то же самое, что и рабочие пространства
```

**PS:** borderangle по стандарту стоит стиль once (один раз).


# Кривая

Определить собственную кривую `bezier` можно с помощью ключевого слова `bezier`:

```ini
bezier=NAME,X0,Y0,X1,Y1
```

Где `NAME` - имя, а остальные - две точки для кубического `Bezier`. 

A хороший веб-сайт для проектирования безье можно найти
[здесь, на cssportal.com](https://www.cssportal.com/css-cubic-bezier-generator/), но
если вы хотите выбрать `bezier` из списка, вы можете заглянуть на сайт [easings.net](https://easings.net).

## Пример

```ini
bezier=overshot,0.05,0.9,0.1,1.1
```

# Доп. информация

Для стиля анимации `popin` в `windows` можно указать минимальный процент
от которого следует отталкиваться. 

**Например:**

```ini
animation=windows,1,8,default,popin 80%
```

Сделает анимацию 80% -> 100% от размера.
