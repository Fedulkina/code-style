
  <a name="arrays--from"></a><a name="4.4"></a>
  - [4.4](#arrays--from) Для преобразования массиво-подобного объекта в массив используйте оператор расширения `...` вместо [`Array.from`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Array/from).

    ```javascript
    const foo = document.querySelectorAll('.foo');

    // хорошо
    const nodes = Array.from(foo);

    // отлично
    const nodes = [...foo];
    ```

  <a name="arrays--mapping"></a><a name="4.5"></a>
  - [4.5](#arrays--mapping) Используйте [Array.from](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Array/from) вместо оператора расширения `...` для маппинга итерируемых объектов, это позволяет избежать создания промежуточного массива.

    ```javascript
    // плохо
    const baz = [...foo].map(bar);

    // хорошо
    const baz = Array.from(foo, bar);
    ```


<a name="destructuring--object"></a><a name="5.1"></a>
  - [5.1](#destructuring--object) При обращении к нескольким свойствам объекта используйте деструктуризацию объекта. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > Почему? Деструктуризация избавляет вас от создания временных переменных для этих свойств.

    ```javascript
    // плохо
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // хорошо
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // отлично
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```


    <a name="destructuring--object-over-array"></a><a name="5.3"></a>
Используйте деструктуризацию объекта для множества возвращаемых значений, но не делайте тоже самое с массивами.

    > Почему? Вы cможете добавить новые свойства через некоторое время или изменить порядок без последствий.

    ```javascript
    // плохо
    function processInput(input) {
      // затем происходит чудо
      return [left, right, top, bottom];
    }

    // при вызове нужно подумать о порядке возвращаемых данных
    const [left, __, top] = processInput(input);

    // хорошо
    function processInput(input) {
      // затем происходит чудо
      return { left, right, top, bottom };
    }

    // при вызове выбираем только необходимые данные
    const { left, top } = processInput(input);
    ```

<a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) Отдавайте предпочтение использованию оператора расширения `...` при вызове вариативной функции. eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

    > Почему? Это чище, вам не нужно предоставлять контекст, и не так просто составить `new` с `apply`.

    ```javascript
    // плохо
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // хорошо
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // плохо
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // хорошо
    new Date(...[2016, 8, 5]);
    ```


 <a name="es2016-properties--exponentiation-operator"></a><a name="12.3"></a>
  - [12.3](#es2016-properties--exponentiation-operator) Используйте оператор `**` для возведения в степень. eslint: [`no-restricted-properties`](https://eslint.org/docs/rules/no-restricted-properties).

    ```javascript
    // плохо
    const binary = Math.pow(2, 10);

    // хорошо
    const binary = 2 ** 10;
    ```
