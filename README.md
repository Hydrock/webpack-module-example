# webpack-module-example
Простая сборка webpack для демонстрации как именно собираются модули

## Что делаем?

- Установи зависимости
- Запусти сборку командой `npm run build`
- Внимательно просмотри итоговый файл сборки `bundle.js` в папке `dist`

Ты увидишь несколько eval - это потому что webpack хранит весь твой код в виде строки (только в режиме разработки). Но если убрать все лишнее получится нечто вроде этого:


Условно, Webpack добавляет наш модуль в **modules scope** (не путать с областью видимости) в специальный массив `__webpack_exports__`

```js
__webpack_require__.r(__webpack_exports__);
__webpack_require__.d(__webpack_exports__, { "default": () => (action) });

function action() {return 'value';};
```

А вот тут Webpack успешно достает наш модуль из **modules scope** и присваивает переменной `_module__WEBPACK_IMPORTED_MODULE_0__` для дальнейшего использования.
```js
__webpack_require__.r(__webpack_exports__);
__webpack_require__.d(__webpack_exports__, {
       "default": () => (__WEBPACK_DEFAULT_EXPORT__)
});

var _module__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__("./src/module.js\");
         
const value = (0,_module__WEBPACK_IMPORTED_MODULE_0__["default"])();
         
const __WEBPACK_DEFAULT_EXPORT__ = (value);
```



