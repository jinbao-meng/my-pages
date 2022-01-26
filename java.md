# java

Launches a Java application.

启动一个Java应用。

[原文地址](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html)

## Synopsis（概要）

**java** [*options*] *classname* [*args*]

**java** [*options*] **-jar** *filename* [*args*]

**javaw** [*options*] *classname* [*args*]

**javaw** [*options*] **-jar** *filename* [*args*]

*options*

Command-line options separated by spaces. See [Options](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html#CBBIJCHG).

命令行选项,多个选项之间以空格键分割。

*classname*

The name of the class to be launched.

要启动的类的全限定名称。

*filename*

The name of the Java Archive (JAR) file to be called. Used only with the `-jar` option.

要启动的jar包的名称，仅与`-jar`选项使用。

*args*

The arguments passed to the `main()` method separated by spaces.

启动后传递给`main()`的参数，多个参数之间以空格键分割。

## Description（简介）

The `java` command starts a Java application. It does this by starting the Java Runtime Environment (JRE), loading the specified class, and calling that class's `main()` method. The method must be declared *public* and *static*, it must not return any value, and it must accept a `String` array as a parameter. The method declaration has the following form:`public static void main(String[] args) `

`java`命令启动一个Java应用[^3]。`java`命令做了以下事情启动JRE，加载指定的类，然后调用其中的`main()`。`main()`必需被声明为*public*和*static*，并且不能有返回值，入参必需是`String`类型的数组。就像这样：`public static void main(String[] args) `

The `java` command can be used to launch a JavaFX application by loading a class that either has a `main()` method or that extends `javafx.application.Application`. In the latter case, the launcher constructs an instance of the `Application` class, calls its `init()` method, and then calls the `start(javafx.stage.Stage)` method.

`java`命令同样可以通过加载声明了`main()`或者继承了`javafx.application.Application`的类去启动一个JavaFX应用。在第二种情况下（继承`Application`），启动器构造一个`Application`的实例，调用`init()`,然后调用`start(javafx.stage.Stage)`。

By default, the first argument that is not an option of the `java` command is the fully qualified name of the class to be called. If the `-jar` option is specified, its argument is the name of the JAR file containing class and resource files for the application. The startup class must be indicated by the `Main-Class` manifest header in its source code.

通常情况下，`java`命令后第一个参数不是选项[^1]而是被调用类的全限定名称。如果在命令行中使用了`-jar`选项，它的参数是一个打包好包含了`.class`文件和资源文件的JAR包的名称。在元文件`MANIFEST.MF`中必需通过`Main-Class`参数明确指出启动类[^2]。

The JRE searches for the startup class (and other classes used by the application) in three sets of locations: the bootstrap class path, the installed extensions, and the user's class path.

JRE从以下三个位置寻找启动类[^3]：引导类的路径[^3.1]，已安装的扩展路径[^3.2]，用户的执行类路径[^3.3]。

Arguments after the class file name or the JAR file name are passed to the `main()` method.

`java`命令中在类的全限定名称或可执行JAR包文件名称之后的参数都将传递到`main()`。

The `javaw` command is identical to `java`, except that with `javaw` there is no associated console window. Use `javaw` when you do not want a command prompt window to appear. The `javaw` launcher will, however, display a dialog box with error information if a launch fails.

`javaw`启动的时侯不会关联一个控制台，除了以上不同之处与`java`执行结果完全一样。

[^1]: 参数：是用户输入的不可控的变量；选项：是命令预定义可解析的。
[^2]: 参考Springboot的可执行JAR包中的 `/META-INF/MANIFST.MF`
[^3]: [How the Java Launcher Finds Classes](https://docs.oracle.com/javase/8/docs/technotes/tools/findingclasses.html#javalauncher)
[^3.1]: Bootstrap classes : rt.jar和其他几个JAR包(jre/lib)
[^3.2]: Extensions classes : jre/lib/ext路径下的JAR包
[^3.3]: User classess : 开发者编写、第三方依赖的JAR包。在`java`命令中使用 `-classpath`选项指定，或在系统中的CLASSHPATH环境变量指定。

## Options（选项）

The `java` command supports a wide range of options that can be divided into the following categories:

`java`命令行支持多种类型的选项可分为以下种类：

- [Standard Options](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html#BABDJJFI)  标准选项
- [Non-Standard Options](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html#BABHDABI)  非标准选项
- [Advanced Runtime Options](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html#BABCBGHF)  高级选项-运行时行为选项
- [Advanced JIT Compiler Options](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html#BABDDFII)  高级选项-动态实时编译(JIT)选项
- [Advanced Serviceability Options](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html#BABFJDIC)  高级选项-系统运行与调试信息的选项
- [Advanced Garbage Collection Options](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html#BABFAFAE)  高级选项-垃圾回收执行选项

Standard options are guaranteed to be supported by all implementations of the Java Virtual Machine (JVM). They are used for common actions, such as checking the version of the JRE, setting the class path, enabling verbose output, and so on.

标准选项保证被所有的JVM支持。这被用来执行公共操作，像检查JRE的版本，设置`classpath`，启用详细输出等等。

Non-standard options are general purpose options that are specific to the Java HotSpot Virtual Machine, so they are not guaranteed to be supported by all JVM implementations, and are subject to change. These options start with `-X`.

非标准选项是特定的HotSpot的通用的选项，因此不能保证被所有的JVM支持，并根据实际情况做出变动。这类选项以`-X`开头。

Advanced options are not recommended for casual use. These are developer options used for tuning specific areas of the Java HotSpot Virtual Machine operation that often have specific system requirements and may require privileged access to system configuration parameters. They are also not guaranteed to be supported by all JVM implementations, and are subject to change. Advanced options start with `-XX`.

高级选项建议不要随便使用。这些都是开发人员选项用于调整*HotSpot*[^4]特定领域的操作，这些操作通常需要特定的系统访问权限。此类选项也不能保证被所有的JVM支持，并根据实际情况做出变动。这类选项以`-XX`开头。

[^4]: 高级选项参数都是特指HotSport这款虚拟机实现。
