# Issue reproduction

This is a repository for reproducing issues: https://github.com/spring-projects/spring-framework/issues/31819

Note: the issue has been fixed

# How to

Generate a project using r2dbc
via [Spring Initializer](https://start.spring.io/#!type=gradle-project&language=java&platformVersion=3.2.0&packaging=jar&jvmVersion=17&groupId=com.example&artifactId=demo&name=demo&description=Demo%20project%20for%20Spring%20Boot&packageName=com.example.demo&dependencies=webflux,native,data-r2dbc,postgresql)

Native compile using native command line or via docker:

```shell
./gradlew nativeCompile
```

Run it in shell or via docker:

```shell
./build/native/nativeCompile/demo
```

Press Ctrl+C to terminate the application, and you will see:

```
2023-12-12T16:13:03.627+08:00  WARN 43626 --- [ionShutdownHook] o.s.b.f.support.DisposableBeanAdapter    : Failed to invoke custom destroy method 'dispose' on bean with name 'connectionFactory'

org.graalvm.nativeimage.MissingReflectionRegistrationError: The program tried to reflectively invoke method public abstract void reactor.core.Disposable.dispose() without it being registered for runtime reflection. Add it to the reflection metadata to solve this problem. See https://www.graalvm.org/latest/reference-manual/native-image/metadata/#reflection for help.
        at org.graalvm.nativeimage.builder/com.oracle.svm.core.reflect.MissingReflectionRegistrationUtils.forQueriedOnlyExecutable(MissingReflectionRegistrationUtils.java:97) ~[na:na]
        at java.base@17.0.8/java.lang.reflect.Method.acquireMethodAccessor(Method.java:77) ~[demo:na]
        at java.base@17.0.8/java.lang.reflect.Method.invoke(Method.java:566) ~[demo:na]
        at org.springframework.beans.factory.support.DisposableBeanAdapter.invokeCustomDestroyMethod(DisposableBeanAdapter.java:316) ~[na:na]
        at org.springframework.beans.factory.support.DisposableBeanAdapter.destroy(DisposableBeanAdapter.java:249) ~[na:na]
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroyBean(DefaultSingletonBeanRegistry.java:587) ~[demo:6.1.1]
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroySingleton(DefaultSingletonBeanRegistry.java:559) ~[demo:6.1.1]
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.destroySingleton(DefaultListableBeanFactory.java:1200) ~[demo:6.1.1]
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroySingletons(DefaultSingletonBeanRegistry.java:520) ~[demo:6.1.1]
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.destroySingletons(DefaultListableBeanFactory.java:1193) ~[demo:6.1.1]
        at org.springframework.context.support.AbstractApplicationContext.destroyBeans(AbstractApplicationContext.java:1125) ~[demo:6.1.1]
        at org.springframework.context.support.AbstractApplicationContext.doClose(AbstractApplicationContext.java:1086) ~[demo:6.1.1]
        at org.springframework.boot.web.reactive.context.ReactiveWebServerApplicationContext.doClose(ReactiveWebServerApplicationContext.java:149) ~[demo:3.2.0]
        at org.springframework.context.support.AbstractApplicationContext.close(AbstractApplicationContext.java:1037) ~[demo:6.1.1]
        at org.springframework.boot.SpringApplicationShutdownHook.closeAndWait(SpringApplicationShutdownHook.java:145) ~[na:na]
        at java.base@17.0.8/java.lang.Iterable.forEach(Iterable.java:75) ~[demo:na]
        at org.springframework.boot.SpringApplicationShutdownHook.run(SpringApplicationShutdownHook.java:114) ~[na:na]
        at java.base@17.0.8/java.lang.Thread.run(Thread.java:833) ~[demo:na]
        at org.graalvm.nativeimage.builder/com.oracle.svm.core.thread.PlatformThreads.threadStartRoutine(PlatformThreads.java:807) ~[demo:na]
        at org.graalvm.nativeimage.builder/com.oracle.svm.core.posix.thread.PosixPlatformThreads.pthreadStartRoutine(PosixPlatformThreads.java:210) ~[na:na]
```
