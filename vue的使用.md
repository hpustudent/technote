#### 属性

1、props，属性的书写方式是key:类型。

    export default {
        name: "HelloWorld",

        props:{
            msg: String,
            sec: String,
            age: {
                type: Number,
                validator: function(val){
                    //对数字进行校验
                    return [10, 20, 30].includes(val);
                }
            }
        }
    }

自定义属性props,原生属性attr，特殊属性style和class

#### 事件
1、普通事件，@click，@input，@change等事件，
2、修饰符事件，@input.trim, @click.stop等，一般用于原生html元素

#### 插槽
1、v-slot:****或者v-slot=***
带作用域的插槽
2、v-slot:***=“props” 或者slot-scope="props"
