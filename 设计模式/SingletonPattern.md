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

使用java中`static`和`final`关键字，利用jvm的机制保证了线程安全性。

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



