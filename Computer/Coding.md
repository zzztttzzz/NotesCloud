## string

* `to_string`可以返回一个`string`字符串.
* `iterator`使用`*`访问该元素，当作一个指针就好
* `s.begin()`指向第一个元素，`s.end()`指向最后一个往后的元素，均返回`iterator`.
* `string`的构造可以采用：
  `string reverseS(s.rbegin(), s.rend());`，实现了将`s`反向的操作。
  实际上`r.begin()`返回的是一个`reverse_iterator`
* `A`的ascii为65，`'a'=='A'+32`，或者`'a'=='A'+0x20`;
* 





## c++ STL

> map

* 需要`#include <map>`。
* `map<int,string> mapName`构造一个map。使用时，按照数组的方式去访问元素。
  `map[2]="ok"`
* 使用一个迭代器遍历，`for (auto i=map.begin();i!=map.end();++i)`，`i->first``i->second`分别对应map中的`key`,`value`。
* 

> set

* 遇到计数排序相关问题，可以直接使用一个set



## c++输入

* 按行读int，每个结果都输出

  ```c++
  int n;
  while(cin>>n)
  {
  	cout << result << endl;
  }
  ```

* 按行读字符串，每个结果都输出

  ```c++
  string s;
  while(cin>>s)
  {
  	cout << result << endl;
  }
  ```

* 读num行，每行3个数值，存到变量里

  ```c++
  int num;
  int key,value; string s;
  while(num-- && cin>>key>>value>>s)
  {}
  ```

* 读一行存入一个`string`里

  ```c++
  string s;
  while(getline(cin,s))
  {
  	cout << s << endl;
  }
  ```

* 读入的char转为大写，小写，只能使用char类型

  ```c++
  char a='A';
  a=tolower(a);
  ```

  如果一次性转换`string`，可以使用transform容器：

  ```c++
  transform(source.begin(), source.end(),des.begin(),tolower);
  // 逐一对容器内元素实施tolower函数，并存储到des容器中。需要预定义。
  ```

  

