## getElementsByTagName的一个以前没注意的点

在看knockout的源码时看到它检测IE版本的代码，觉得奇怪
~~~js
var ieVersion = document && (function() {
    var version = 3, div = document.createElement('div'), iElems = div.getElementsByTagName('i');

    // Keep constructing conditional HTML blocks until we hit one that resolves to an empty fragment
    while (
        div.innerHTML = '<!--[if gt IE ' + (++version) + ']><i></i><![endif]-->',
        iElems[0]
    ) {}
    return version > 4 ? version : undefined;
}());
~~~

然后自己试了一试

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div id="pp"></div>
</body>
<script>
    var cat = document && (function() {
        // getElementsByClassName,getElementsByTagName
        // 这两个方法为动态更新，它会随着DOM树的变化自动更新自身，所以，使用相同元素和相同参数时，没有必要多次的调用Element.getElementsByTagName()
        // chrome 和 IE 又有所不同
        var div = document.getElementsByTagName('div')[0],
        iElems = document.getElementsByTagName('i');
        iID = document.getElementById('cat');
        console.log(iElems);     // chrome下会自动更新，所以会看到，在插入innerHTML之前就显示了完整的对象。IE下则不会
        console.log(iElems[0]);                 // undefined
        console.log(iID);                       // null
        div.innerHTML = '<i id="cat">cat</i>',
        console.log(iElems[0]);                 // <i id="cat">cat</i>
        console.log(iID);                       // null
        iID = document.getElementById('cat');
        console.log(iID);                       // <i id="cat">cat</i>
        console.log(iElems[0] === iID);         // true
        return 'cat';
    }());
</script>
</html>

~~~
[参看MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getElementsByTagName)