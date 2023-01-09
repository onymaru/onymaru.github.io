---
title: Блиц на знание ООП в Java
layout: single-copy
classes: wide
author_profile: true
author: Pavel Shiryaev
---


## Вопрос 1. Что выведет на экран?

```java

class A{
    public static String txt="A";

    static public void myMethod(){
        System.out.println(txt);
    }
}


class B extends A{
    static public String txt="B";

    static public void myMethod(){
        System.out.println(txt);
    }
}


class Main {

    public static void main(String... args)  {

        A a = new A();
        a.myMethod();

        B b = new B();
        b.myMethod();


        A ab = new B();
        ab.myMethod();
    }
}

```

## Вопрос 2: Валидный код?

```java
abstract class A{
    protected int m1(){ return 0; }
}
class B extends A{
    int m1(){ return 1; }
}
```

## Вопрос 3: Что выведет на экран?

```java
class A{
    public int myVar=1;
}

class B extends A{
    {
        myVar = 2;
    }
}


class C extends B{
}

class Main {

    public static void main(String... args)  {

        A a = new A();
        B b = new B();
        C c = new C();

        A ab = new B();
        System.out.println(ab.myVar);

        A ac = new C();
        System.out.println(ac.myVar);

        System.out.println(a.myVar);
    }


}
```


## Вопрос 4:  Валидный код?

```java
interface Inter{
    void myInterMethod();
}


abstract class AB implements Inter{
    static public void myInterMethod(){

    }
}

```


## Вопрос 5:  Валидный код?

```java
class A{
    A(int a){ }
}

class B extends A{
    B(int a){super(a); }
}

```



## Вопрос 6:  Валидный код?

```java
interface Inter{
    static void myInterMethod();
}


```


## Вопрос 7:  Валидный код?

```java

class A {
      void myMethod(){
        System.out.println("hello from A");
    }

}

abstract class B extends A{
     abstract void myMethod();

}

```

