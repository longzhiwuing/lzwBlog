---
title: Builder构建者模式 通用模板
date: 2017-02-12 19:17:04
tags: 构建者模式
categories:
---
能看到这篇文章的读者，我想应该或多或少了解Builder构建者模式。在Builder模式出现之前，构建对象会有如下两个问题：

1. 在属性过多的情况下，需要在构造函数中一次性传递所有需要初始化的参数，并且可能会根据需求override多个不同参数组合的构造函数。比较麻烦。

2. 如果是创建一个无参的空对象，通过setter方法，为每一个属性值赋值的话，有一个很大的问题就是会出现对象不一致的情况。也就是说由于setter方法可以在任何时间和地方可以为对象属性重新赋值，可能导致程序上下文对象的属性出现不一致的情况，这在序列化或者多线程的情境下会因为对象不一致而产生bug隐患。

<!--more-->

Builder构建者模式就可以很好的解决上述的两个问题。好了废话不多说，直接上CODE。下面我通过一个Config类，来实现一个构建者模式，其他情况可以参考这个进行相应修改。思路是一致的。

```
public class Config {
    private String protocol;
    private String ip;
    private String port;

    public String getProtocol() {
        return protocol;
    }

    public String getIp() {
        return ip;
    }

    public String getPort() {
        return port;
    }

    @Override
    public String toString() {
        return "Config{" +
                "protocol='" + protocol + '\'' +
                ", ip='" + ip + '\'' +
                ", port='" + port + '\'' +
                '}';
    }

    //新增Builder静态类并赋默认值
    public static class Builder {
        private String protocol = "http://";
        private String ip = "127.0.0.1";
        private String port = "80";

        //为每一个属性创建返回自身Builder对象的方法
        public Builder setProtocol(String protocol) {
            this.protocol = protocol;
            return this;
        }

        public Builder setIp(String ip) {
            this.ip = ip;
            return this;
        }

        public Builder setPort(String port) {
            this.port = port;
            return this;
        }

        //新建一个aplly方法，传一个父类引用，赋值构建的参数
        public void apply2Super(Config config) {
            config.protocol = this.protocol;
            config.ip = this.ip;
            config.port = this.port;
        }

        //新建一个build方法，创建一个父类对象，传递给apply方法为这个空对象赋构建出来的参数值，返回这个构建对象即可。
        public Config build(){
            Config config = new Config();
            apply2Super(config);
            return config;
        }

    }
}
```

调用方式：

```
        //使用默认值构建
        Config config1 = new Config.Builder().build();

        System.out.println(config1);

        //自定义构造参数
        Config config = new Config.Builder()
                .setProtocol("https://")
                .setIp("192.168.0.1.")
                .setPort("8080")
                .build();

        System.out.println(config);
```

总结

1、在需要构造的类中新增Builder静态类并赋默认值
2、为每一个属性创建返回自身Builder对象的方法
3、新建一个aplly方法，传一个父类引用，赋值构建的参数
 4、新建一个build方法，创建一个父类对象，传递给apply方法为这个空对象赋构建出来的参数值，返回这个构建对象即可。

P.S:
给大家安利一本书《大话设计模式》 作者是程杰的那个。这本书通俗易懂的讲解了所有的设计模式，是我看到过的所有讲设计模式中，最容易理解，最干净利索的。我现在正在根据书中讲的和我自身的理解，实现每一个设计模式。github地址：https://github.com/longzhiwuing/GOFDemos 欢迎拍砖和STAR