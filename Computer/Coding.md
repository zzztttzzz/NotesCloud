## string

* `to_string`可以返回一个`string`字符串.
* `iterator`使用`*`访问该元素，当作一个指针就好
* `s.begin()`指向第一个元素，`s.end()`指向最后一个往后的元素，均返回`iterator`.
* `string`的构造可以采用：
  `string reverseS(s.rbegin(), s.rend());`，实现了将`s`反向的操作。
  实际上`r.begin()`返回的是一个`reverse_iterator`
* 

