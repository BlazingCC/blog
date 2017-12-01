##flex实现div竖排并换列
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .box {
            width: 42px;
            height: 200px;
            display: flex;          /*flex*/
            flex-direction: column; /*竖排排列*/
            flex-wrap: wrap;        /*换行*/
        }
        .box>div {
            width: 19px;
            height: 19px;
            border: solid 1px lightblue;
        }
    </style>
</head>
<body>
    <!-- box高度限制显示10个 -->
    <div class="box">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
        <div>9</div>
        <div>10</div>
        <div>11</div>
        <div>12</div>
        <div>13</div>
    </div>
</body>
</html>
~~~