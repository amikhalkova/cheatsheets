# JS AJAX

## Классический вариант вызова (XHR)

```js
var xhr = new XMLHttpRequest();
xhr.open('GET', 'vote', true);
xhr.onreadystatechange = function() {
  if (xhr.readyState != 4) return;
  if (xhr.status != 200) {
    // обработать ошибку
    alert('Ошибка ' + xhr.status + ': ' + xhr.statusText);
    return;
  }  
  
  // обработать результат
  button.innerHTML = xhr.responseText;
}

xhr.send(null);
```

## JQuery вариант вызова (обертка XHR)

```js
$("#button").html(' ... ');
$.ajax({
  method: "GET",
  url: "vote",
  success: function(result) {
    $("#button").html(result);
  },
  fail: function(jqXHR, textStatus) {
    alert("Request failed: " + textStatus);
  }
});
```
## Метод fetch (замена XHR)

При вызове fetch возвращает промис, который, когда получен ответ, выполняет коллбэки с объектом Response или с ошибкой, если запрос не удался.

```js
fetch('/article/fetch/user.json')
  .then(function(response) {
    return response.json();
  })
  .then(function(user) {
    alert(user.name);
  })
  .catch(function(ex) {
    alert(ex)
  });
```

ES6

```js
fetch('/article/fetch/user.json')
  .then(r => r.json())
  .then(user => alert(user.name))
  .catch(e => alert(e))
```

ES7

```js
(async() => {
  try {
    var response = await fetch('/article/fetch/user.json');
    var user = await response.json();
    alert(user.name);
  } catch (e) {
    alert(e)
  }
})();
```

>См.  
[Стандарт](https://fetch.spec.whatwg.org),  
[javascript.ru](https://learn.javascript.ru/fetch),  
[habrahabr](https://habrahabr.ru/post/252941/),  
[Полифил и много примеров, под капотом юзает xhr](https://github.com/github/fetch),  
[Проддержка в браузерах](http://caniuse.com/#search=fetch)