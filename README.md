## 30 seconds of code中所有函数解读 (慢慢补充中...)
#### drop函数
>原文解释：
>Returns a new array with n elements removed from the left.Use Array.prototype.slice() to slice the remove the specified number of elements from the left.
>
>翻译结果：
>返回一个从左边移除n个元素的新数组。使用Array.prototype.slice()将从左侧删除指定数量的元素。
```
const drop = (arr, n = 1) => arr.slice(n);
drop([1, 2, 3]); // [2,3]
drop([1, 2, 3], 2); // [3]
drop([1, 2, 3], 42); // []
```
以`drop([1, 2, 3], 2);`为例进行解读：

 1. 很容易明白数组`[1, 2, 3]`从索引为2开始截取得到数组`[3]`。

#### dropRight函数
>原文解释：
>Returns a new array with n elements removed from the right.Use Array.prototype.slice() to slice the remove the specified number of elements from the right.
>
>翻译结果：
>返回一个从右侧移除n个元素的新数组。使用Array.prototype.slice()从右侧删除指定的元素数量。
```
const dropRight = (arr, n = 1) => arr.slice(0, -n);
dropRight([1, 2, 3]); // [1,2]
dropRight([1, 2, 3], 2); // [1]
dropRight([1, 2, 3], 42); // []
```
以`dropRight([1, 2, 3], 2);`为例进行解读：

 1. 这个函数非常简单就是倒着截取函数，倒着从索引为-2开始截取数组`[1, 2, 3]`可以得到数组`[1]`。

#### dropRightWhile函数
>原文解释：
>Removes elements from the end of an array until the passed function returns true. Returns the remaining elements in the array.Loop through the array, using Array.prototype.slice() to drop the last element of the array until the returned value from the function is true. Returns the remaining elements.
>
>翻译结果：
>从数组末尾删除元素，直到传递的函数返回true为止。返回数组中的其余元素。循环遍历数组，使用array .prototype.slice()删除数组的最后一个元素，直到函数返回的值为true。返回其余元素。
```
const dropRightWhile = (arr, func) => {
  while (arr.length > 0 && !func(arr[arr.length - 1])) arr = arr.slice(0, -1);
  return arr;
};
dropRightWhile([1, 2, 3, 4], n => n < 3); // [1, 2]
```
以`dropRightWhile([1, 2, 3, 4], n => n < 3);`为例进行解读：

 1. 该函数使用了while循环和条件判断截取掉了不符合条件的数组元素。
 2. 首先看条件`n => n < 3`和`!func(arr[arr.length - 1])`，可以得出结论只要`n >= 3`就会返回true截取数组，所以最后截取掉了数组中的3和4。

#### dropWhile函数
>原文解释：
>Removes elements in an array until the passed function returns true. Returns the remaining elements in the array.Loop through the array, using Array.prototype.slice() to drop the first element of the array until the returned value from the function is true. Returns the remaining elements.
>翻译结果：
>删除数组中的元素，直到传递的函数返回true为止。返回数组中的其余元素。循环遍历数组，使用array .prototype.slice()删除数组的第一个元素，直到函数返回的值为true。返回其余元素。
```
const dropWhile = (arr, func) => {
  while (arr.length > 0 && !func(arr[0])) arr = arr.slice(1);
  return arr;
};
dropWhile([1, 2, 3, 4], n => n >= 3); // [3,4]
```
以`dropWhile([1, 2, 3, 4], n => n >= 3);`为例进行解读：

 1. 使用while循环和slice函数截取获得符合条件的数组元素，可以看到条件`n => n >= 3`和`!func(arr[0])`可以drop不符合条件的数组元素。显然1和2在`n => n >= 3`的条件下不成立，但是在`!func(arr[0])`的条件下成立，一旦条件成立就会执行slice函数进行截取，综上所述可知一共截取了两次数组，而且都是从第二个元素开始截取。

#### everyNth函数
>原文解释：
>Returns every nth element in an array.Use Array.prototype.filter() to create a new array that contains every nth element of a given array.
>翻译结果：
>返回数组中的第n个元素。使用array. prototype.filter()创建一个包含给定数组的第n个元素的新数组。
```
const everyNth = (arr, nth) => arr.filter((e, i) => i % nth === nth - 1);
everyNth([1, 2, 3, 4, 5, 6], 2); // [ 2, 4, 6 ]
```
以`everyNth([1, 2, 3, 4, 5, 6], 2);`为例进行解读：

 1. 使用条件回调方式过滤得到需要的数组元素，根据`i % nth === nth - 1`可知只有数组元素的索引值为奇数是才返回true，所以整个函数将返回数组索引的值为奇数的数组元素。

#### filterNonUnique函数
>原文解释：
>Filters out the non-unique values in an array.Use Array.prototype.filter() for an array containing only the unique values.
>
>翻译结果：
>过滤掉数组中的非唯一值。对于只包含唯一值的数组，使用array .prototype.filter()。
```
const filterNonUnique = arr => arr.filter(i => arr.indexOf(i) === arr.lastIndexOf(i));
filterNonUnique([1, 2, 2, 3, 4, 4, 5]); // [1, 3, 5]
```
以`filterNonUnique([1, 2, 2, 3, 4, 4, 5]);`为例进行解读：

 1. 该函数使用了三个函数，filter函数、indexOf函数、lastIndexOf函数。
 2. lastIndexOf() 方法可返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。
 3. 这个函数其实很好理解，只返回数组中不重复的值，可以看得到这样一个判`arr.indexOf(i) === arr.lastIndexOf(i)`，如果数组中存在两个相同的值i，那么该值肯定返回false，只有当数组中的值唯一不重复时才返回true，因为无论从前向后数还是从后向前数都是一致的索引值。

#### filterNonUniqueBy函数
>原文解释：
>Filters out the non-unique values in an array, based on a provided comparator function.Use Array.prototype.filter() and Array.prototype.every() for an array containing only the unique values, based on the comparator function, fn. The comparator function takes four arguments: the values of the two elements being compared and their indexes.
>
>翻译结果：
>根据提供的comparator函数，过滤掉数组中的非唯一值。使用array .prototype.filter()和array .prototype. each()来处理基于comparator函数fn的只包含唯一值的数组。comparator函数有四个参数:比较两个元素的值及其索引。
```
const filterNonUniqueBy = (arr, fn) =>
  arr.filter((v, i) => arr.every((x, j) => (i === j) === fn(v, x, i, j)));
filterNonUniqueBy(
  [
    { id: 0, value: 'a' },
    { id: 1, value: 'b' },
    { id: 2, value: 'c' },
    { id: 1, value: 'd' },
    { id: 0, value: 'e' }
  ],
  (a, b) => a.id == b.id
); // [ { id: 2, value: 'c' } ]
```
以`filterNonUniqueBy(
  [
    { id: 0, value: 'a' },
    { id: 1, value: 'b' },
    { id: 2, value: 'c' },
    { id: 1, value: 'd' },
    { id: 0, value: 'e' }
  ],
  (a, b) => a.id == b.id
);`为例进行解读：

 1. 该函数使用了两个函数，filter函数和every函数。
 2. 首先当`v = { id: 0, value: 'a' }, i = 0`时，表达式变为`arr.filter(({ id: 0, value: 'a' },0) => arr.every((x,j) => (0 === j) === fn({ id: 0, value: 'a' },x,0,j)))`，此时执行j = 0到j = 4的函数表达式`arr.every((x,j) => (0 === j) === fn({ id: 0, value: 'a' },x,0,j)))`,看它返回true还是false，因为fn中执行的函数回调，所以当j!=0时一定会出现`a.id = b.id`的情况，所以只要数组的对象中存在重复的id值，那么arr.eveny一定会返回false。因此排除了除`v = { id: 2, value: 'c' }`以外的所有情况。现在看当`v = { id: 2, value: 'c' }`时的情况，此时i的值为2，且表达式变为`arr.filter(({ id: 2, value: 'c' },2) => arr.every((x,j) => (i === j) === fn({ id: 2, value: 'c' },x,i,j)))`,来看表达式的这一部分`(2 === j) === fn({ id: 2, value: 'c' },x,2,j))`,当j从0-4发生变化时，该表达式返回的值肯定是true，所以最后只有当i = 2时，filter的回调函数才满足，其余情况下的对象都被过滤了，只剩下了不重复id的对象`{ id: 2, value: 'c' }`。

#### findLast函数
>原文解释：
>Returns the last element for which the provided function returns a truthy value.Use Array.prototype.filter() to remove elements for which fn returns falsey values, Array.prototype.pop() to get the last one.
>
>翻译结果：
>返回提供的函数为其返回一个真实值的最后一个元素。使用Array.prototype.filter()删除fn返回falsey值的元素。
```
const findLast = (arr, fn) => arr.filter(fn).pop();
findLast([1, 2, 3, 4], n => n % 2 === 1); // 3
```
以`findLast([1, 2, 3, 4], n => n % 2 === 1);`为例进行解读：

 1. 该函数只用到了两个函数，filter函数和pop函数。
 2. 首先使用filter函数过滤了不满足条件`n => n % 2 === 1`的数组元素得到数组`[1,3]`，然后使用pop函数提取出了末尾数组元素3。

#### findLastIndex函数
>原文解释：
>Returns the index of the last element for which the provided function returns a truthy value.Use Array.prototype.map() to map each element to an array with its index and value. Use Array.prototype.filter() to remove elements for which fn returns falsey values, Array.prototype.pop() to get the last one.
>
>翻译结果：
>返回最后一个元素的索引，提供的函数为该元素返回一个真实值。使用array .prototype.map()将每个元素映射到一个具有索引和值的数组。使用Array.prototype.filter()删除fn返回falsey值的元素。
```
const findLastIndex = (arr, fn) =>
  arr
    .map((val, i) => [i, val])
    .filter(([i, val]) => fn(val, i, arr))
    .pop()[0];
findLastIndex([1, 2, 3, 4], n => n % 2 === 1); // 2 (index of the value 3)
```
以`findLastIndex([1, 2, 3, 4], n => n % 2 === 1);`为例进行解读：

 1. 该函数用到了三个函数，map函数回调处理数组中的所有元素，并按照回调中的规则返回相应的键值对;filter函数利用回调函数过滤掉不符合要求的数据项;pop函数将删除原先数组的最后一个元素并返回。
 2. 首先利用map函数先把原先的数组格式化为`[[0,1],[1,2],[2,3],[3,4]]`意思是把原先的元素处理成`[元素的索引,元素]`的形式，然后使用filter函数中的回调函数`n => n % 2 === 1`过滤出`[[0,1],[2,3]]`，最后使用pop函数提取出数组[2,3]，并返回第一个元素值3对应的索引值2`(index of the value 3)`。

#### flatten函数
>原文解释：
>Flattens an array up to the specified depth.Use recursion, decrementing depth by 1 for each level of depth. Use Array.prototype.reduce() and Array.prototype.concat() to merge elements or arrays. Base case, for depth equal to 1 stops recursion. Omit the second argument, depth to flatten only to a depth of 1 (single flatten).
>
>翻译结果：
>将阵列压平至指定深度。使用递归，每层深度减1。使用Array.prototype.reduce()和Array.prototype.concat()合并元素或数组。基本情况，深度为1时停止递归。忽略第二个参数，深度要压平的深度仅为1(单个压平)。
```
const flatten = (arr, depth = 1) =>
  arr.reduce((a, v) => 
  a.concat(depth > 1 && Array.isArray(v) ? flatten(v, depth - 1) : v), []);
flatten([1, [2], 3, 4]); // [1, 2, 3, 4]
flatten([1, [2, [3, [4, 5], 6], 7], 8], 2); // [1, 2, 3, [4, 5], 6, 7, 8]
```
以`flatten([1, [2, [3, [4, 5], 6], 7], 8], 2);`为例进行解读：

 1. 这个函数整体使用了递归的思想，直到函数中的某些条件符合不再进行递归处理。
 2. 现在传入的arr值是`[1, [2, [3, [4, 5], 6], 7], 8]`，depth的值是2，此时条件`depth > 1 && Array.isArray(v) ? flatten(v, depth - 1) : v`执行到`v = [2, [3, [4, 5], 6], 7]`时结果是递归调用`depth > 1 && Array.isArray(v) ? flatten(v, depth - 1) : v`,当这里的`v = [3, [4, 5], 6]`时继续递归调用`depth > 1 && Array.isArray(v) ? flatten(v, depth - 1) : v`,当这里的`v = [4, 5]`时不再执行递归调用，而是返回该数组。因为此时的depth = 1，所以程序执行到这结束，除了数组`[4, 5]`没被处理即原样返回，其余的都被处理为单个数组元素。

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

3. `reduce((acc, val, i) => { acc[val] = (acc[val] || []).concat(arr[i]); return acc; }, {}); `这其实是一个求和函数，这里传入了一个起始的值`{}`是一个空对象，其实目的很简单就是为了给空的对象添加新的key，因为整个函数的本意是用来归类合并具有相同性质的数组元素，第一个调用示例`groupBy([6.1, 4.2, 6.3], Math.floor)`就是归类合并向下取整后的数组元素；第二个调用示例`groupBy(['one', 'two', 'three'], 'length')`就是归类合并具有相同字符长度的数组元素。`acc[val] = (acc[val] || []).concat(arr[i])`这句话的意思是给刚才传入的空`{}`在现有的基础上新建key并赋值`[]`或者覆盖已有的key所对应的数组。当遍历到的val是第一个元素6时`acc[6] = (acc[6] || []).concat(arr[0])`所得的结果是`{"6": [6.1]}`;当遍历到的val的第二个元素4时`acc[4] = (acc[4] || []).concat(arr[1])`所得的结果是`{"6": [6.1],"4": [4.2]}`;当传入的值是第三个元素6时`acc[6] = (acc[6] || []).concat(arr[2])`所得的结果是`{"4": [4.2],"6": [6.1,6.3]}`。