#单例设计模式

## 饿汉模式

缺点：无法对`sIntance`实例进行延迟加载

```java
public class HungrySingle {
	private static HungrySingle sIntance = new HungrySingle();
	
	public static HungrySingle getInstance(){
		return sIntance;
	}
}
```

## 懒汉模式

缺点：多线程并发无法保证实例唯一性

```java
public class LazySingle {
	private static LazySingle sInstance = null;
	
	public static LazySingle getInstance(){
		if(sInstance == null){
			sInstance = new LazySingle();
		}
		return sInstance;
	}
}

```

## 双重检查加锁DCL

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

## 静态内部类

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



