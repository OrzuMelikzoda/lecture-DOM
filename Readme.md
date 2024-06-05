## Хотя веб-браузером и вообще вебом область действия JavaScript не ограничивается, однако по прежнему одной из ключевых задач JavaScript является взаимодействие с пользователем и манипуляция элементами веб-страницы в браузере. Для JavaScript веб-страница доступна в виде объектной модели документа (document object model) или сокращенно DOM. DOM описывает структуру веб-станицы в виде древовидного представления и предоставляет разработчикe способ получить доступ к отдельным элементам веб-страницы.

## Важно не путать понятия BOM (Browser Object Model - объектная модель браузера) и DOM (объектная модель документа). Если BOM предоставляет доступ к браузеру и его свойствам в целом, то DOM предоставляет доступ к отдельной веб-странице или html-документу и его элементам.

### Например, рассмотрим простейшую страницу:

```
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
</head>
<body>
    <h2>Page Header</h2>
    <div>
        <h3>Block Header</h3>
        <p>Text</p>
    </div>
</body>
</html>
```

### Дерево DOM для этой страницы будет выглядеть следующим образом:

![image](https://github.com/OrzuMelikzoda/lecture-DOM/assets/167527624/33b20ca5-9ef8-46fd-af88-e17e5149c965)


### Таким образом, все компоненты упорядочены в DOM иерархическим образом, где каждый компонент представляет отдельный узел. То есть каждый элемент, например, элемент div, представляет собой узел. Но также и текст внутри элемента представляет отдельный узел

## Document: корневой узел html-документа, представляет весь документ в целом

### Для управления атрибутами элементов JavaScript предоставляет ряд методов:

### 1. getAttribute(attr): возвращает значение атрибута attr

### Для получения атрибута у элемента вызывается метод getAttribute(), в который передается имя атрибута. Например, пусть у нас на странице есть следующий элемент, который представляет ссылку:

```
<a id="home" class="link" href="index.html">Home</a>
```

### Получим атрибуты этого элемента:


```
// получаем элемент
const element = document.getElementById("home");
// получаем атрибуты элемента
console.log(element.getAttribute("id"));    // home
console.log(element.getAttribute("class")); // link
console.log(element.getAttribute("href"));  // index.html
```

### Стоит отметить, что атрибуты элементы также доступны через его свойства, которые называются аналогично атрибутам (за редким исключением):

```
// получаем элемент
const element = document.getElementById("home");
// получаем атрибуты элемента
console.log(element.id);    // home
console.log(element.className); // link
console.log(element.href);  // file:///Users/eugene/Documents/app/index.html
```

### Исключение касается в частности атрибута "class", который доступен через свойство className.

### Также свойства могут возвращать немного отличающиеся значения. Например, свойство href возвращает полную ссылку, а метод getAttribute("href") - непосредственное значение атрибута.

### То же самое касается и атрибута style:

```
<a id="home" style="color:red;" href="index.html">Home</a>
<script>
// получаем элемент
const element = document.getElementById("home");
// получаем атрибуты элемента
console.log(element.style);    // CSSStyleDeclaration
console.log(element.getAttribute("style")); // color:red;
</script>
```



### 2. setAttribute(attr, value): устанавливает для атрибута attr значение value. Если атрибута нет, то он добавляется


### Для установки значения атрибутов применяется метод setAttribute(attr, value), первый параметр которого - устанавливаемый атрибут, а второй - его значение:

```
<a id="home" href="index.html">Home</a>
<script>
// получаем элемент
const element = document.getElementById("home");
// устанавливаем атрибут href
element.setAttribute("href", "https://metanit.com");
// устанавливаем атрибут style
element.setAttribute("style", "color:navy;");
</script>
```

### Здесь изменяем атрибут "href" и устанавливаем атрибут "style". Поскольку атрибут "style" изначально отсутствует, то он будет добавлен. Но стоит отметить, что в реальности это приведет к тому, что будет создан узел Node, который представляет атрибут. У этого узла будет установлено соответствующее значение, и затем узел атрибута добавляется в коллекцию дочерних узлов элемента. То есть фактически это будет выглядеть следующим образом:

```
<a id="home" href="https://metanit.com">Home</a>
<script>
// получаем элемент
const element = document.getElementById("home");
// создаем узел-атрибут style
const attribute = document.createAttribute("style");
// устанавливаем значение узла-атрибута
attribute.value = "color:navy;";
// устанавливаем узел атрибута
element.setAttributeNode(attribute);
</script>
```

### 3. removeAttribute(attr): удаляет атрибут attr и его значение

### Для удаления атрибута применяется метод removeAttribute(), в который передается удаляемый атрибут:

```
<a id="home" href="https://metanit.com" style="color:navy;">Home</a>
<script>
// получаем элемент
const element = document.getElementById("home");
// удаляем атрибут style
element.removeAttribute("style");
</script>
```















