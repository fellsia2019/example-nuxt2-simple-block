Был [такой](http://joxi.ru/a2XgvExtQ3Wp1m) макет блока.  
Блок разбит на две колонки, левая и правая  
В левой вначале расположено какое-то изображение, превью блока.  
Под ним расположены однотипные текстовые блоки  
В правой колонке расположены однотипные текстовые блоки, как в левой части, но без превью.  
Было принято решение разбить приходящий массив с обьектами для текстовых блоков на две части и выводить их таким образом:  
Если приходит четное кол-во текстовых блоков (объектов, далее айтемов), то выводим поровну слева и справа  
Если приходит нечетное кол-во айтемов, то выводим слева на 1 айтем меньше, чем справа  
Если приходит 1 айтем, выводим его справа.  
