1：传递给你一个包含两个数字的数组。返回这两个数字和它们之间所有数字的和。
方法：Math.max()    Math.min()    Array.reduce()
```function sumAll(arr) {
  var x_max = arr.reduce(function(a,b){
    return Math.max(a,b);
  }) ;
  var x_min = arr.reduce(function(a,b){
    return Math.min(a,b);
  }) ;  
  var sum = 0;
  for(var i=x_min;i<x_max+1;i++)
    {
      sum+=i; 
    }
  return sum;
}

```

2
