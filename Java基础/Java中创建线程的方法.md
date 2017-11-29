## Java中创建线程的方法
#### Java中创建线程主要有三种方法

1. 从Thread继承，并实现run方法，通过调用start()方法启动线程的运行
2. 创建类并实现Runnable接口，实现run方法。使用时，创建一个Thread实例，并将实现了Runnable接口的类的实例传递给Thread构造函数，
```
class RunClass implements Runnalble {
	@Override 
    public void run() {...}
}
Thread newThread = new Thread(new RunClasss());
newThread.start();
```
当然，这里使用lambda表达式或者匿名类都是可以的，道理都一样
3. 利用Callable<T>接口和Future框架创建线程
刚学习Java的人对这种方法可能了解不多，其步骤如下：
		1. 创建新类实现Callable接口，并实现call()方法，该call方法将作位线程功能的执行代码（类似run，但run无返回值，call有返回值）
		2. 创建Callable实现类的实例，使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call方法的返回值
		3. 使用FutureTask对象的get()方法来获得子线程执行结束后的返回值
		
```
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

public class CallableDemo implements Callable<String> {
    private final String value;
    public CallableDemo(String value) {
        this.value = value;
    }

    @Override
    public String call() {
        return value;
    }

    static public void main(String[] args) {
        FutureTask<String> ft = new FutureTask<String>(new CallableDemo("Hello"));
        Thread t = new Thread(ft);
        t.start();
        try {
            System.out.println(ft.get());//get()将阻塞直至得到结果
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (ExecutionException e) {
            e.printStackTrace();
        }
    }
}
```
以上代码展示了Collable接口的使用，其与前两种方法的主要区别就是call()有返回值，调用Future的get()方法时，将产生阻塞，直至产生结果，这个特性可以用于后台计算等场景。