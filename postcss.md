# Inversion Of Control

[Алексей Плуталов](https://twitter.com/demiazz), [Злые марсиане](http://evilmartians.ru/)

## **Inversion Of Control** in <strike>the wild</strike> frontend
!type is-title

*Алексей Плуталов, Злые марсиане*

## План

1. Что такое IoC?
2. Factory Method
3. Service Locator
4. Dependency Injection
5. IoC Container
6. IoC в Ember.js

## *Часть 1* Что такое IoC?
!cover evilmartians.png

## *Что такое IoC?* Аксиома
!type is-default

<figure>
  <blockquote>
    <p>
      Чем сложнее класс или компонент, тем меньше должно быть внешних связей.
    </p>
  </blockquote>
  <figcaption>
    Тед Фейсон, Event-Based Programming
  </figcaption>
</figure>

## *Что такое IoC?* Определение
!type is-default

Важный принцип используемый для уменьшения связанности кода

- все модули зависят от абстракций
- модули верхнего уровня не зависят от модулей нижнего уровня
- абстракции не зависят от деталей
- детали зависят от абстракций

## *Что такое IoC?* Способы реализации
!type is-default

- Factory Method
- Service Locator
- Dependency Injection
- IoC-container

## *Часть 2* Factory Method
!cover evilmartians.png

## *Factory Method* Схема
!type is-default
!type is-scheme
!type is-factory

!image factory.png

## *Factory Method* Описание
!type is-default

- определяет единый интерфейс создания объекта
- реализация инстанцирования делегируется подклассам
- возможность создания объектов оперируя лишь общим интерфейсом
- нужно создавать много шаблонных классов

## *Часть 3* Service Locator
!cover evilmartians.png

## *Service Locator* Схема
!type is-default
!type is-scheme
!type is-service-locator

!image service-locator.png

## *Service Locator* Описание
!type is-default

Паттерн скрывающий процессы связанные с получением модуля с сильным уровнем абстракции

Реализуется в виде центрального реестра ресурсов, возвращающего нужную информацию по запросу

## *Service Locator* Пример
!type is-default

```javascript

var Connection = function () {
  this.logger = require("logger")();

  /* реализация логики */
}
```

## *Service Locator* Достоинства
!type is-default

- разрывает жесткую связь между модулями
- добавление модулей на лету
- возможность автоматической настройки приложения

## *Service Locator* Недостатки
!type is-default

- жесткие связи только ослабляются, но не контролируются
- невозможно определить зависимости модуля
- изменение приложения не становится проще
- Service Locator всегда представлен глобальным объектом

## *Часть 4* Dependency Injection
!cover evilmartians.png

## *Dependency Injection* Описание
!type is-default

Процесс предоставления внешней зависимости программному компоненту

- внедрение через конструктор (Constructor Injection)
- внедрение через метод класса (Setter Injection)
- внедрение через интерфейс (Interface Injection)

## *Dependency Injection* Пример Constructor Injection
!type is-default

```javascript
// adapter      - клиент хранилища (например, REST)
// serializator - сериализатор данных
var Resource = function (adapter, serializator) {
  this.adapter      = adapter;
  this.serializator = serializator;
};
```

## *Dependency Injection* Пример Setter Injection
!type is-default

```javascript
var Resource = function () { };
Resource.prototype.setAdapter = function (adapter) {
  this.adapter = adapter;
};
Resource.prototype.setSerializator = function (srl) {
  this.serializator = srl;
};
```

## *Dependency Injection* Пример Interface Injection
!type is-default

```javascript
var Injectable = function ( ) { };
Injectable.prototype.inject = function (name, dep) { };

var Resource = function () { Injectable.apply(this); };
Resource.prototype.inject = function (name, dep) {
  this[name] = dep;
};
```

## *Dependency Injection* Другой пример Interface Injection
!type is-default

```javascript
Object.prototype.inject = function (name, dep) {
  this[name] = dep;
};

var resource = new Resource();
resource.inject(adapter, serializer);
```

## *Dependency Injection* Достоинства
!type is-default

- легкость внедрения даже в существующий код
- повышение переиспользуемости, тестируемости и сопровождаемости кода
- конфигурация системы при запуске
- сокрытие инфраструктурного кода для инициализации зависимостей
- независимая разработка стала еще проще

## *Dependency Injection* Недостатки
!type is-default

- сложнее читать код
- увеличивает количество кода
- выставляет требования к пользователю системы
- наложение ограничений в плане организации кода

## *Часть 5* IoC Container
!cover evilmartians.png

## *IoC Container* Описание
!type is-default

Программный каркас реализующий DI, и упрощающий его использование

Многие фреймворки являются реализацией IoC-container

## *IoC Container* Схема
!type is-default
!type is-scheme
!type is-container

!image container.png

## *IoC Container* Пример jQuery
!type is-default

```javascript


jQuery.fn.pluginName = function () {
  this; // jQuery объект с выборкой элементов
};
```

## *IoC Container* Пример Koa.js
!type is-default

```javascript

app.use(function * () {
  this;          // Koa Context
  this.request;  // Koa Request
  this.response; // Koa Response
});
```

## *Часть 6* IoC в Ember.js
!cover evilmartians.png

## Спасибо за внимание
!type with-em

* Презентация: [demiazz.github.io/ioc-slides](http://demiazz.github.io/ioc-slides/)
* [@demiazz](https://twitter.com/demiazz)

!image evilmartians.png
