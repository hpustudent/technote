### rxjava核心
1.源头发数据  
2.响应者接数据  
3.数据变换  
4.线程调度  
5.可以看成两根水管之间水从上游到下游的流动，如果要进行线程调度，可以使用subscribeOn指定上游执行线程，observeOn指定下游执行线程