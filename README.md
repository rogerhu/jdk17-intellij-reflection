# Overview

Using an older IntelliJ SDK with JDK17 triggers this bug. See https://github.com/rogerhu/jdk17-intellij-reflection/commit/305aa8beabfc68b3a36814495c56ec71f7dd72f0

## Setup

1. Setup JAVA_HOME to point to JDK17

2. Run:

```bash
./gradlew run --no-daemon
```

The stack trace we see is:

```
> Task :app:run FAILED
Exception in thread "main" java.lang.ExceptionInInitializerError
        at tst.reflection.AppKt.main(App.kt:16)
        at tst.reflection.AppKt.main(App.kt)
Caused by: java.lang.reflect.InaccessibleObjectException: Unable to make protected void java.util.ResourceBundle.setParent(java.util.ResourceBundle) accessible: module java.base does not "opens java.util" to unnamed module @689349f1
        at java.base/java.lang.reflect.AccessibleObject.checkCanSetAccessible(AccessibleObject.java:354)
        at java.base/java.lang.reflect.AccessibleObject.checkCanSetAccessible(AccessibleObject.java:297)
        at java.base/java.lang.reflect.Method.checkCanSetAccessible(Method.java:199)
        at java.base/java.lang.reflect.Method.setAccessible(Method.java:193)
        at com.intellij.util.ReflectionUtil.makeAccessible(ReflectionUtil.java:252)
        at com.intellij.util.ReflectionUtil.getDeclaredMethod(ReflectionUtil.java:269)
        at com.intellij.DynamicBundle.<clinit>(DynamicBundle.java:22)
        ... 2 more

FAILURE: Build failed with an exception.
```