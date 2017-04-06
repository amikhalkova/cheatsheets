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

### ES5 (2009)

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

### ES6 (2015)

```js
fetch('/article/fetch/user.json')
  .then(r => r.json())
  .then(user => alert(user.name))
  .catch(e => alert(e))
```

### ES2016 (ES7)

```js
(async() => {
  try {
    var response = await fetch('/article/fetch/user.json');
    var user = await response.json();
    alert(user.name);
  } catch (e) {
    alert(e)
  }
})(); // тут же вызываем
```

или в виде отдельной функции

```js
async function fetchAsync () {
  let response = await fetch('/article/fetch/user.json');
  let user = await response.json();
  return user;
}

fetchAsync()
    .then(user => alert(user.name))
    .catch(e => alert(e))
```

>См.  
[Ajax на javascript.ru](https://learn.javascript.ru/ajax),  
[Спецификация XMLHttpRequest](https://www.w3.org/TR/2012/NOTE-XMLHttpRequest1-20120117/),  
[jQuery.ajax](http://api.jquery.com/jquery.ajax/),  
[Спецификация fetch](https://fetch.spec.whatwg.org),  
[Fetch на javascript.ru](https://learn.javascript.ru/fetch),  
[Полифил fetch и много примеров, под капотом юзает xhr](https://github.com/github/fetch),  
[Проддержка fetch в браузерах](http://caniuse.com/#search=fetch)