
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