#### 块级变量let，只要块内存在let命令，所声明的变量就绑定到当前作用域中，不受外部影响
#### 块级变量const，一旦定义就需要初始化，而且不能修改
#### 解构赋值，let [a, b] = [1,2], let [a , b] = [undefined, 2], let [a =1, b] = [undefined, 2],结构赋值可以指定默认值，
只有值不存在为undefined时才会寻找默认值，解构赋值对对象依然适用,  let {a, b} = {a:'zhangsan', b:'lisi'};
