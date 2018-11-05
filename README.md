## 30 seconds of code中所有函数解读 (慢慢补充中...)
## Array
#### all函数
>原文解释：
>Returns true if the provided predicate function returns true for all elements in a collection, false otherwise.Use Array.prototype.every() to test if all elements in the collection return true based on fn. Omit the second argument, fn, to use Boolean as a default.
>
>翻译结果：
>如果提供的谓词函数对集合中的所有元素返回true，则返回true，否则返回false。使用array .prototype. each()测试集合中的所有元素是否基于fn返回true。省略第二个参数fn，以使用布尔值作为默认值。
```
const all = (arr, fn = Boolean) => arr.every(fn);
all([4, 2, 3], x => x > 1); // true
all([1, 2, 3]); // true
```
以`all([4, 2, 3], x => x > 1);`为例进行解读：

 1. 使用every函数
 2. 这个函数传入了数组`[4, 2, 3]`，因为数组中的所有元素都满足`x => x > 1`，所以返回为true。

#### allEqual函数
>原文解释：
>Check if all elements in an array are equal.Use Array.prototype.every() to check if all the elements of the array are the same as the first one.
>
>翻译结果：
>检查数组中的所有元素是否相等。使用array .prototype.every()检查数组中的所有元素是否与第一个元素相同。
```
const allEqual = arr => arr.every(val => val === arr[0]);
allEqual([1, 2, 3, 4, 5, 6]); // false
allEqual([1, 1, 1, 1]); // true
```
以`allEqual([1, 2, 3, 4, 5, 6]);`为例进行解读：

 1. 使用了every函数，只有数组中所有元素都满足条件才返回true，否则返回false。
 2. 该函数出入了数组`[1, 2, 3, 4, 5, 6]`，如果所有数组元素的值和第一个数组元素的值相等的话代表数组中所有元素相等，将返回true，否则返回false。

#### any函数
>原文解释：
>Returns true if the provided predicate function returns true for at least one element in a collection, false otherwise.Use Array.prototype.some() to test if any elements in the collection return true based on fn. Omit the second argument, fn, to use Boolean as a default.
>
>翻译结果：
>如果提供的谓词函数对于集合中的至少一个元素返回true，则返回true，否则返回false。使用Array.prototype.some()测试集合中的元素是否基于fn返回true。省略第二个参数fn，以使用布尔值作为默认值。
```
const any = (arr, fn = Boolean) => arr.some(fn);
any([0, 1, 2, 0], x => x >= 2); // true
any([0, 0, 1, 0]); // true
```
以`any([0, 1, 2, 0], x => x >= 2);`为例进行解读：

 1. 使用了some函数
 2. 这个函数传入了数组`[0, 1, 2, 0]`和条件`x => x >= 2`，只要数组中存在大于等于2的值，那么这个函数就会返回true，如果不存在满足条件的元素，那么将返回false。

#### arrayToCSV函数
>原文解释：
>Converts a 2D array to a comma-separated values (CSV) string.Use Array.prototype.map() and Array.prototype.join(delimiter) to combine individual 1D arrays (rows) into strings. Use Array.prototype.join('\n') to combine all rows into a CSV string, separating each row with a newline. Omit the second argument, delimiter, to use a default delimiter of ,.
>
>翻译结果：
>将2D数组转换为逗号分隔值(CSV)字符串。使用Array.prototype.map()和Array.prototype.join(分隔符)将单个1D数组(行)组合成字符串。使用Array.prototype.join('\n')将所有行合并成CSV字符串，用换行符分隔每一行。省略第二个参数，分隔符，以使用默认的分隔符，。
```
const arrayToCSV = (arr, delimiter = ',') =>
  arr.map(v => v.map(x => `"${x}"`).join(delimiter)).join('\n');
arrayToCSV([['a', 'b'], ['c', 'd']]); // '"a","b"\n"c","d"'
arrayToCSV([['a', 'b'], ['c', 'd']], ';'); // '"a";"b"\n"c";"d"'
```
以`arrayToCSV([['a', 'b'], ['c', 'd']], ';');`为例进行解读：

 1. 这个函数使用了map函数格式化了数组中的元素和join函数将数组转换成了字符串。
 2. 首先看到了函数表达式`v.map(x => `"${x}"`).join(delimiter)`将数组中的数组里面的每个元素格式化成了带有双引号的字符串，然后使用join函数将数组转换成了使用`;`分割的字符串。最后使用`\n`回车符将字符串数组转换成了带有回车符的字符串。

#### bifurcate函数
>原文解释：
>Splits values into two groups. If an element in filter is truthy, the corresponding element in the collection belongs to the first group; otherwise, it belongs to the second group.Use Array.prototype.reduce() and Array.prototype.push() to add elements to groups, based on filter.
>
>翻译结果：
>将值分成两组。如果filter中的元素是真实的，集合中的相应元素属于第一组;否则，它属于第二组。使用Array.prototype.reduce()和Array.prototype.push()根据filter向组添加元素。
```
const bifurcate = (arr, filter) =>
  arr.reduce((acc, val, i) => (acc[filter[i] ? 0 : 1].push(val), acc), [[], []]);
bifurcate(['beep', 'boop', 'foo', 'bar'], [true, true, false, true]); // [ ['beep', 'boop', 'bar'], ['foo'] ]
```
以`bifurcate(['beep', 'boop', 'foo', 'bar'], [true, true, false, true]);`为例进行解读分析：

 1. 该函数中传入了原数组`['beep', 'boop', 'foo', 'bar']`、布尔值数组`[true, true, false, true]`和求和的初始化参数`[[], []]`，首先看到函数表达式`acc[filter[i] ? 0 : 1]`，意思是根据布尔值`filter[i]`来决定使用第一个空数组还是第二个空数组。
 2. 然后使用了push函数将数组中的元素进行push分组，也就是遇到布尔值为true时将字符串放到第一个空数组中，当布尔值为false时，将字符串放到第二个空数组中，最后返回对应的acc数组。

#### bifurcateBy函数
>原文解释：
>Splits values into two groups according to a predicate function, which specifies which group an element in the input collection belongs to. If the predicate function returns a truthy value, the collection element belongs to the first group; otherwise, it belongs to the second group.Use Array.prototype.reduce() and Array.prototype.push() to add elements to groups, based on the value returned by fn for each element.
>
>翻译结果：
>根据谓词函数将值分成两组，谓词函数指定输入集合中的元素属于哪个组。如果谓词函数返回一个真值，则集合元素属于第一组;否则，它属于第二组。根据fn为每个元素返回的值，使用Array.prototype.reduce()和Array.prototype.push()向组添加元素。
```
const bifurcateBy = (arr, fn) =>
  arr.reduce((acc, val, i) => (acc[fn(val, i) ? 0 : 1].push(val), acc), [[], []]);
bifurcateBy(['beep', 'boop', 'foo', 'bar'], x => x[0] === 'b'); // [ ['beep', 'boop', 'bar'], ['foo'] ]
```
以`bifurcateBy(['beep', 'boop', 'foo', 'bar'], x => x[0] === 'b');`为例进行解读：

 1. 这个杉树使用了reduce求和函数、三元表达式和push函数。
 2. 首先看到函数表达式`acc[fn(val, i) ? 0 : 1]`和`x => x[0] === 'b'`，两者结合的意思是如果字符串数组的第一个元素是b的话就返回0，否则返回1。然后b字母开头的的字符串在第一个空数组中集合，不是b开头的话就在第二个空数组中集合，求和函数的目的是每次返回的数组都是最新更新后所得的。

#### chunk函数
>原文解释：
>Chunks an array into smaller arrays of a specified size.Use Array.from() to create a new array, that fits the number of chunks that will be produced. Use Array.prototype.slice() to map each element of the new array to a chunk the length of size. If the original array can't be split evenly, the final chunk will contain the remaining elements.
>
>翻译结果：
>将数组分成指定大小的较小数组。使用array .from()来创建一个新的数组，它与将要生成的块数量相匹配。使用array .prototype.slice()将新数组的每个元素映射到大小为块的块。如果原始数组不能被平均分割，那么最后的块将包含其余的元素。
```
const chunk = (arr, size) =>
  Array.from({ length: Math.ceil(arr.length / size) }, (v, i) =>
    arr.slice(i * size, i * size + size)
  );
chunk([1, 2, 3, 4, 5], 2); // [[1,2],[3,4],[5]]
```
以`chunk([1, 2, 3, 4, 5], 2);`为例进行解读：

 1. 该函数使用了Array.from函数创建数组对象和slice截取函数。
 2. 首先看到Array.from中`{ length: Math.ceil(arr.length / size) }`表明了一个维数组对象，意思是要创建一个长度为3的数组，`arr.slice(i * size, i * size + size)`这句话其实是：将数组中的每个数组元素创建为，从原数组中每截取两个元素组成新数组，将这些新数组变为数组元素然后返回。

#### compact函数
>原文解释：
>Removes falsey values from an array.Use Array.prototype.filter() to filter out falsey values (false, null, 0, "", undefined, and NaN).
>
>翻译结果：
>从数组中删除falsey值。使用Array.prototype.filter()来过滤掉falsey值(false、null、0、""、undefined和NaN)。
```
const compact = arr => arr.filter(Boolean);
compact([0, 1, false, 2, '', 3, 'a', 'e' * 23, NaN, 's', 34]); // [ 1, 2, 3, 'a', 's', 34 ]
```
以`compact([0, 1, false, 2, '', 3, 'a', 'e' * 23, NaN, 's', 34]);`为例进行解读：

 1. 这个函数返回布尔值为true的元素，其中false、null、0、""、undefined和NaN的布尔值为false。

#### countBy函数
>原文解释：
>Groups the elements of an array based on the given function and returns the count of elements in each group.Use Array.prototype.map() to map the values of an array to a function or property name. Use Array.prototype.reduce() to create an object, where the keys are produced from the mapped results.
>
>翻译结果：
>根据给定的函数对数组的元素进行分组，并返回每组元素的计数。使用array .prototype.map()将数组的值映射到函数或属性名。使用Array.prototype.reduce()创建一个对象，其中键是根据映射的结果生成的。
```
const countBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val) => {
    acc[val] = (acc[val] || 0) + 1;
    return acc;
  }, {});
countBy([6.1, 4.2, 6.3], Math.floor); // {4: 1, 6: 2}
countBy(['one', 'two', 'three'], 'length'); // {3: 2, 5: 1}
```
以`countBy([6.1, 4.2, 6.3], Math.floor);`为例进行解读：

 1. 该函数使用了map函数进行格式化和reduce函数进行求和。
 2. 首先看到函数`typeof fn === 'function' ? fn : val => val[fn]`，因为传入的fn是Math.floor所以`arr.map`返回的是数组`[6, 4, 6]`。然后调用了reduce函数，函数的回调内容是`acc[val] = (acc[val] || 0) + 1`，它的意思是当初始化的空对象中如果不存在对应的键值对时就创建为0并加1，如果存在的话就在原先的基础上加一，这里的用法`(acc[val] || 0) + 1`使得语言更加自然，因为不存在的话就是0，不管存不存在都存在一个初始值，那就是0或者原先的值。

#### countOccurrences函数
>原文解释：
>Counts the occurrences of a value in an array.Use Array.prototype.reduce() to increment a counter each time you encounter the specific value inside the array.
>
>翻译结果：
>计数数组中出现的值。每次在数组中遇到特定值时，使用array. prototype.reduce()增加计数器的值。
```
const countOccurrences = (arr, val) => 
  arr.reduce((a, v) => (v === val ? a + 1 : a), 0);
countOccurrences([1, 1, 2, 1, 2, 3], 1); // 3
```
以`countOccurrences([1, 1, 2, 1, 2, 3], 1);`为例进行解读：

 1. 该函数使用了reduce函数进行求和三元表达式。
 2. 这里数组`[1, 1, 2, 1, 2, 3]`被传了进去，,因为reduce函数的最后传了0，所以该函数的求和初值是0。由于val的值是1，再加上判断表达式`v === val ? a + 1 : a`可得一旦检测到数组中有元素等于0，那么求和的值就会加1，所以最后统计出数组中共有3个1。

#### deepFlatten函数
>原文解释：
>Deep flattens an array.Use recursion. Use Array.prototype.concat() with an empty array ([]) and the spread operator (...) to flatten an array. Recursively flatten each element that is an array.
>
>翻译结果：
>深度压平阵列。使用递归。使用array([])和spread操作符(…)来压平一个数组。递归地将数组中的每个元素压平。
```
const deepFlatten = arr => 
  [].concat(...arr.map(v => (Array.isArray(v) ? deepFlatten(v) : v)));
deepFlatten([1, [2], [[3], 4], 5]); // [1,2,3,4,5]
```
以`deepFlatten([1, [2], [[3], 4], 5]);`为例进行解读：

 1. 使用map函数格式化数组中的元素和Array.isArray来判断是否是数组
 2. 这里传入了数组`[1, [2], [[3], 4], 5]`，首先准备了空数组，然后使用`Array.isArray`函数进行判断，如果是数组就进行回调操作，也就是将数组中的数组一层一层剥离出来并处理成数组元素，不是数组的话那就是数组元素直接返回，最终使用concat函数将数组全部合并。

#### difference函数
>原文解释：
>Returns the difference between two arrays.Create a Set from b, then use Array.prototype.filter() on a to only keep values not contained in b.
>
>翻译结果：
>返回两个数组之间的差异。从b创建一个集合，然后在a上使用Array.prototype.filter()来保存不包含在b中的值。
```
const difference = (a, b) => {
  const s = new Set(b);
  return a.filter(x => !s.has(x));
};
difference([1, 2, 3], [1, 2, 4]); // [3]
```
以`difference([1, 2, 3], [1, 2, 4]);`为例进行解读：

 1. 该函数使用了new Set函数和filter函数比较出了两数组不同的值，并将过滤的数组中不存在于比较函数中的元素都过滤出来。
 2. 首先使用new Set函数进行数组去重，由于数组`[1, 2, 4]`本就没有重复所以保持不变。然后使用filter函数将数组`[1, 2, 3]`过滤出了数组`[1, 2, 4]`中不存在的元素。

#### differenceBy函数
>原文解释：
>Returns the difference between two arrays, after applying the provided function to each array element of both.Create a Set by applying fn to each element in b, then use Array.prototype.filter() in combination with fn on a to only keep values not contained in the previously created set.
>
>翻译结果：
>将提供的函数应用于两个数组的每个数组元素后，返回两个数组之间的差异。通过将fn应用到b中的每个元素来创建一个集合，然后在a上使用Array.prototype.filter()和fn结合使用，以保持之前创建的集合中不包含的值。
```
const differenceBy = (a, b, fn) => {
  const s = new Set(b.map(fn));
  return a.filter(x => !s.has(fn(x)));
};
differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor); // [1.2]
differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], v => v.x); // [ { x: 2 } ]
```
以`differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], v => v.x);`为例进行解读：

 1. 这个函数使用了new Set函数和map函数进行数组重组和去重，然后使用了filter函数过滤不符合要求的值。
 2. 首先看到函数`new Set(b.map(fn))`，`b.map(fn)`是将数组`[{ x: 1 }]`格式化成`[1]`，然后使用使用new Set函数将数组进行去重处理。接着使用函数`a.filter(x =>!s.has(fn(x)))`将数组`[{ x: 2 }, { x: 1 }]`中存在和数组`[1]`中元素值相同的项给过滤了。

#### differenceWith函数
>原文解释：
>Filters out all values from an array for which the comparator function does not return true.Use Array.prototype.filter() and Array.prototype.findIndex() to find the appropriate values.
>
>翻译结果：
>将比较器函数不返回true的数组中的所有值过滤掉。使用Array.prototype.filter()和Array.prototype.findIndex()查找合适的值。
```
const differenceWith = (arr, val, comp) => 
  arr.filter(a => val.findIndex(b => comp(a, b)) === -1);
differenceWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0], (a, b) => Math.round(a) === Math.round(b)); // [1, 1.2]
```
以`differenceWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0], (a, b) => Math.round(a) === Math.round(b));`为例进行解读：

 1. 该函数使用了filter函数、findIndex函数和Math.round函数
 2. 首先看`val.findIndex(b => comp(a, b)) === -1`函数，将该函数进行分解，看到`comp(a, b)`函数也就是`Math.round(a) === Math.round(b)`，这里的a和b分别来自两个数组`[1, 1.2, 1.5, 3, 0]`和`[1.9, 3, 0]`，将这两个数组中的元素都进行Math.round函数的处理可以发现只有元素1和1.2的Math.round结果在数组`[1.9, 3, 0]`的结果中不存在，也就是数组`[1, 1.2, 1.5, 3, 0]`的findIndex结果在循环到数组元素为1和1.2时返回结果为-1。
 3. 所以最后留下了符合条件的数组元素，也就是A数组元素4舍5入后在B数组元素4舍5入后不存在的元素都留了下来。

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
