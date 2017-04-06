# JS AJAX

## Классический вариант вызова

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

## JQuery вариант вызова

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


