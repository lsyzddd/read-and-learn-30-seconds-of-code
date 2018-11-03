## 30 seconds of code中所有函数解读 (慢慢补充中...)

#### forEachRight函数
>原文解释：
>Executes a provided function once for each array element, starting from the array's last element.Use Array.prototype.slice(0) to clone the given array, Array.prototype.reverse() to reverse it and Array.prototype.forEach() to iterate over the reversed array.
>
>翻译结果：
>对每个数组元素执行一次提供的函数，从数组的最后一个元素开始。使用array. prototype.slice(0)克隆给定的数组array. array. reverse()和array. prototype. foreach()迭代反向数组。
```
const forEachRight = (arr, callback) =>
  arr
    .slice(0)
    .reverse()
    .forEach(callback);
forEachRight([1, 2, 3, 4], val => console.log(val)); // '4', '3', '2', '1'
```
以`forEachRight([1, 2, 3, 4], val => console.log(val));`举例进行解读：

 1. 该函数用到了三个函数，slice()用作截取并返回一个新的数组并不会改变原来的数组；reverse()函数用作数组的反转；forEach()总所周知是遍历函数
 2. 首先slice(0)克隆并返回一个新的数组`[1, 2, 3, 4]`;然后将该数组`[1, 2, 3, 4]`反转reverse()得到`[4, 3, 2, 1]`;最后调用forEach(callback)函数倒序输出数组中的元素。

#### groupBy函数
>原文解释：
>Groups the elements of an array based on the given function.Use Array.prototype.map() to map the values of an array to a function or property name. Use Array.prototype.reduce() to create an object, where the keys are produced from the mapped results.
>
>翻译结果：
>根据给定的函数对数组元素进行分组。使用array .prototype.map()将数组的值映射到函数或属性名。使用Array.prototype.reduce()创建一个对象，其中键是根据映射的结果生成的。
```
const groupBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val, i) => {
    acc[val] = (acc[val] || []).concat(arr[i]);
    return acc;
  }, {});
groupBy([6.1, 4.2, 6.3], Math.floor); // {4: [4.2], 6: [6.1, 6.3]}
groupBy(['one', 'two', 'three'], 'length'); // {3: ['one', 'two'], 5: ['three']}
```

以 `groupBy([6.1, 4.2, 6.3], Math.floor); `举例进行解读：
1. 以上`reduce`函数中的acc代表求和的值，val代表遍历时的元素值，i代表遍历时的元素索引

2. `arr.map(typeof fn === 'function' ? fn : val => val[fn])`的map函数中传入的fn是`Math.floor`，因为`typeof fn === 'function'`的结果是true，所以`arr.map`的结果是`arr.map(Math.floor)`，这句话就是将原来的arr数据中的每个元素都`Math.floor`一遍然后所得的结果将是`[6, 4, 6]`。

3. `reduce((acc, val, i) => { acc[val] = (acc[val] || []).concat(arr[i]); return acc; }, {}); `这其实是一个求和函数，这里传入了一个起始的值`{}`是一个空对象，其实目的很简单就是为了给空的对象添加新的key，因为整个函数的本意是用来归类合并具有相同性质的数组元素，第一个调用示例`groupBy([6.1, 4.2, 6.3], Math.floor)`就是归类合并向下取整后的数组元素；第二个调用示例`groupBy(['one', 'two', 'three'], 'length')`就是归类合并具有相同字符长度的数组元素。`acc[val] = (acc[val] || []).concat(arr[i])`这句话的意思是给刚才传入的空`{}`在现有的基础上新建key并赋值`[]`或者覆盖已有的key所对应的数组。当遍历到的val是第一个元素6时`acc[6] = (acc[6] || []).concat(arr[0])`所得的结果是`{"6": [6.1]}`;当遍历到的val的第二个元素4时`acc[4] = (acc[4] || []).concat(arr[1])`所得的结果是`{"6": [6.1],"4": [4.2]}`;当传入的值是第三个元素6时`acc[6] = (acc[6] || []).concat(arr[2])`所得的结果是`{"4": [4.2],"6": [6.1,6.3]}`