总结：
**①常用String 方法**
>- includes() 方法用于判断一个字符串是否包含在另一个字符串中，根据情况返回 true 或 false。
>- concat() 方法将一个或多个字符串与原字符串连接合并，形成一个新的字符串并返回。
>- toUpperCase() 将调用该方法的字符串值转换为大写形式，并返回。
>- toLowerCase() 会将调用该方法的字符串值转为小写形式，并返回。
>-  substr() 方法返回一个字符串中从指定位置开始到指定字符数的字符。
>- split()方法  使用指定的分隔符字符串将String对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。
>- slice() 方法提取一个字符串的一部分，并返回一新的字符串。
>- replace() 方法返回一个由替换值替换一些或所有匹配的模式后的新字符串。模式可以是一个字符串或者一个[正则表达式](替换值可以是一个字符串或者一个每次匹配都要调用的函数。
注意：原字符串不会改变
>- repeat() 构造并返回一个新字符串，该字符串包含被连接在一起的指定数量的字符串的副本。

**②常用数组方法**
- 修改器方法
下面的这些方法会改变调用它们的对象自身的值：

>Array.prototype.copyWithin() 
在数组内部，将一段元素序列拷贝到另一段元素序列上，覆盖原有的值。
>
>Array.prototype.fill() 
将数组中指定区间的所有元素的值，都替换成某个固定的值。
>
>Array.prototype.pop()
删除数组的最后一个元素，并返回这个元素。
>
>Array.prototype.push()
在数组的末尾增加一个或多个元素，并返回数组的新长度。
>
>Array.prototype.reverse()
颠倒数组中元素的排列顺序，即原先的第一个变为最后一个，原先的最后一个变为第一个。
>
>Array.prototype.shift()
删除数组的第一个元素，并返回这个元素。
>
>Array.prototype.sort()
对数组元素进行排序，并返回当前数组。
>
>Array.prototype.splice()
在任意的位置给数组添加或删除任意个元素。
>
>Array.prototype.unshift()
在数组的开头增加一个或多个元素，并返回数组的新长度。

- 访问方法
下面的这些方法绝对不会改变调用它们的对象的值，只会返回一个新的数组或者返回一个其它的期望值。

>Array.prototype.concat()
返回一个由当前数组和其它若干个数组或者若干个非数组值组合而成的新数组。
>
>Array.prototype.includes() 
判断当前数组是否包含某指定的值，如果是返回 true，否则返回 false。
>
>Array.prototype.join()
连接所有数组元素组成一个字符串。
>
>Array.prototype.slice()
抽取当前数组中的一段元素组合成一个新数组。
>
>Array.prototype.toSource() 
返回一个表示当前数组字面量的字符串。遮蔽了原型链上的 
Object.prototype.toSource() 方法。
>
>Array.prototype.toString()
返回一个由所有数组元素组合而成的字符串。遮蔽了原型链上的 
Object.prototype.toString() 方法。
>
>Array.prototype.toLocaleString()
返回一个由所有数组元素组合而成的本地化后的字符串。遮蔽了原型链上的 Object.prototype.toLocaleString() 方法。
>
>Array.prototype.indexOf()
返回数组中第一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1。
>
>Array.prototype.lastIndexOf()
返回数组中最后一个（从右边数第一个）与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1。


1：翻转字符串
要求：先把字符串转化成数组，再借助数组的reverse方法翻转数组顺序，最后把数组转化成字符串。
 方法：
String.split()   Array.reverse()    Array.join()
```
function reverseString(str) {
  // 请把你的代码写在这里
  var splArr = str.split('');
  
  splArr.reverse();
  var rString = splArr.join("");
  return rString;
}

```
2:计算阶乘
```
function factorialize(num) {
  var sum = 1,times= num;
  
  for(var i=0;i<times;i++){
    sum =sum * num;
    num -=1;
  }return sum;
}
```
曾犯错：循环里次数注意固定，开始直接用了num

3:检查字符串是回文
（去掉标点符号和空格）
String.replace()    String.toLowerCase()
```
function palindrome(str) {
  // 请把你的代码写在这里
  var str_cut = str.replace(/[^a-zA-Z0-9]/g,'').toLowerCase().split('');
  if (str_cut.join('') === str_cut.reverse().join('') ) return true;
  else return false;
  
}

```
4:找出最长的单词
```
function findLongestWord(str) {
  // 请把你的代码写在这里
  var arrStr = str.split(' ');
  var maxStr=arrStr[0].length;
  for(var i=0;i<arrStr.length-1 ;i++)
    {
      if(maxStr > arrStr[i+1].length) continue ;
      else maxStr = arrStr[i+1].length;
    }  
  return maxStr;
}
```
5：句子中每个首字母大写
```
function titleCase(str) {
  // 请把你的代码写在这里
  var newArr = str.toLowerCase().split(' ');
  var newArrA;
  for(var i = 0;i<newArr.length ;i++)
    {
      newArrA = newArr[i].split('');
        newArrA[0] = newArrA[0].toUpperCase();
      
      newArr[i] = newArrA.join('');
    }
  var newStr = newArr.join(' ');
  return newStr;
}
```
6:返回二维数组中的最大数组成一维数组
```
function largestOfFour(arr) {
  // 请把你的代码写在这里
  var newArr =[]; 
  var temp;
  for(var i=0 ;i<arr.length ; i++){
    temp = arr[i][0]; 
    for (var j=0 ;j<arr[i].length ; j++){
           if(temp<arr[i][j])  {
        temp = arr[i][j];
        newArr[i] = temp;
      }
      else newArr[i] = temp ; 
    }
  }
  return newArr;
 
}
```
7:检查字符串结尾
方法 str.substr(start[, length])
```
function confirmEnding(str, target) {
  // 请把你的代码写在这里
  var last = str.substr(-target.length);
  if (last === target) return true;
  else return false;
}
```
8:重复字符串
```
function repeat(str, num) {
  // 请把你的代码写在这里
  if(num<0) return"";
  else {
    var sum='' ;
    for(var i=0;i<num;i++)
      {
        sum+=str;
      }
  }
  return sum;
}
```
9:截断字符串
方法：String.slice()   str.slice(beginSlice[, endSlice])
```
function truncate(str, num) {
 // 请把你的代码写在这里
  if(num<str.length){
    if(num<=3) return str.slice(0,num)+'...';
    else return str.slice(0,num-3)+'...';
  }
  else return str;
}
```
10:分割数组
方法： Array.push()  Array.slice()
push() 方法将一个或多个元素添加到数组的末尾，并返回新数组的长度。
slice() 方法返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。且原始数组不会被修改。
```
function chunk(arr, size) {
  // 请把你的代码写在这里
  var x = Math.floor(arr.length / size) ;
  var nArr =[] ;
  for(var i=0;i<x;i++){
    nArr[i] = arr.slice(i*size,(i+1)*size);
  }
  if(arr.length % size!==0) nArr.push(arr.slice(i*size,arr.length));
             
  return nArr;  
}
```
11:截断数组
```
function slasher(arr, howMany) {
  // 请把你的代码写在这里
 var newArr = arr.slice(howMany);
  return newArr;
}
```
或
```
function slasher(arr, howMany) {
  // 请把你的代码写在这里
 arr.splice(0,howMany);
  return arr;
}
```
slice() 方法返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。且原始数组不会被修改。
splice() 方法通过删除现有元素和/或添加新元素来更改一个数组的内容。
12:比较字符串

（蛤蟆可以吃队友，也可以吃对手）

如果数组第一个字符串元素包含了第二个字符串元素的所有字符，函数返回true。
String.indexOf()

```
function mutation(arr) {
  // 请把你的代码写在这里
   var x =arr[1].toLowerCase().split('');
   var n =arr[0].toLowerCase();
   for(var i=0;i<x.length;i++)
     {
       var y = n.indexOf(x[i]); 
       
       if(y==-1) return false;
     }
  return true;
}
```
13:过滤数组假值

（真假美猴王）

删除数组中的所有假值。

在JavaScript中，假值有false、null、0、""、undefined 和 NaN。过滤数组假值

（真假美猴王）

删除数组中的所有假值。

在JavaScript中，假值有false、null、0、""、undefined 和 NaN。

方法：Boolean Objects
Array.filter()
```
function bouncer(arr) {
  // 请把你的代码写在这里

  var result = arr.filter(function(e){
    var falsy;
    return falsy=Boolean(e);
    
  });
  return result;
}
```
14:摧毁数组

金克斯的迫击炮！

实现一个摧毁(destroyer)函数，第一个参数是待摧毁的数组，其余的参数是待摧毁的值。

Arguments object
Array.filter()
```
function destroyer(arr) {
  // 请把你的代码写在这里 
  var arr_r = arguments; 
     for(var i =1;i<arr_r.length;i++){
            function isIt(element) {
               return  arr_r[i] !== element;        
      } 
         arr  = arr.filter(isIt);     
  }   return  arr;
}

```
15:数组排序并找出元素索引

我身在何处？

先给数组排序，然后找到指定的值在数组的位置，最后返回位置对应的索引。

Array.sort()
```
function where(arr, num) {
  // 请把你的代码写在这里 
  arr = arr.sort((a, b) => a - b);  
  for(var i=0;i<arr.length;i++)
   {
         if(arr[i]>=num) return i;
     
  }  
  return i;
}

```
16:写一个[ROT13](http://www.baike.com/wiki/ROT13&prd=so_1_doc)函数，实现输入加密字符串，输出解密字符串。

所有的字母都是大写，不要转化任何非字母形式的字符(例如：空格，标点符号)，遇到这些特殊字符，跳过它们。
String.charCodeAt()
String.fromCharCode()
```
function rot13(str) {
 var newarr=[];
  for(var i=0;i<str.length;i++){
    if(str.charCodeAt(i)<65||str.charCodeAt(i)>90){
      newarr.push(str.charAt(i));
    }else if(str.charCodeAt(i)>77){
      newarr.push(String.fromCharCode(str.charCodeAt(i)-13));
    }else{
      newarr.push(String.fromCharCode(str.charCodeAt(i)+13));
    }
  }
  return newarr.join("");
}
```
