
RxJava 中的map与flatMap的区别

1、map和flatMap都是接受一个函数作为参数(Func1)
2、map函数只有一个参数，参数一般是Func1，Func1的<I,O>I,O模版分别为输入和输出值的类型，实现Func1的call方法对I类型进行处理后返回O类型数据
3、flatMap函数也只有一个参数，也是Func1,Func1的<I,O>I,O模版分别为输入和输出值的类型，实现Func1的call方法对I类型进行处理后返回O类型数据，不过这里O为Observable类型

背压的使用，onBackpressureBuffer()，关注三个参数的函数。第三个参数是OverflowStrategy类型的。
Introduce a new interface BackpressureOverflowStrategy that allows implementing different handlers for an overflow situation. This patch adds three implementations, reachable via OverflowStrategy:

static class OverflowStrategy {
    static final BackpressureOverflowStrategy DEFAULT = Error.INSTANCE;
    static final Error ERROR = Error.INSTANCE;
    static final DropOldest DROP_OLDEST = DropOldest.INSTANCE;
    static final DropLatest DROP_LATEST = DropLatest.INSTANCE;
}
The behavior for each is the following:

ERROR remains the default as the existing implementation.
DROP_LATEST will drop newly produced items after the buffer fills up.
DROP_OLDEST will drop the oldest elements in the buffer, making room for
newer ones.
