# 双重检查加锁DCL

```java
public class SingleClassDCL {
    private static volatile SingleClassDCL sInstance = null;

    private SingleClassDCL() {

    }

    public static SingleClassDCL getInstance() {
        if (sInstance == null) {
            synchronized (SingleClassDCL.class) {
                if (sInstance == null) {
                    sInstance = new SingleClassDCL();
                }
            }
        }
        return sInstance;
    }
}
```

# 静态内部类

利用了java中`static`和`final`关键字，并且可以实现不同线程同时读取类。

```java
public class StaticInnerSingle {

    private StaticInnerSingle() {
    }

    public static StaticInnerSingle getInstance() {
        return SingleHolder.sInstance;
    }

    private static class SingleHolder {
        private static final StaticInnerSingle sInstance = new StaticInnerSingle();
    }

}
```



