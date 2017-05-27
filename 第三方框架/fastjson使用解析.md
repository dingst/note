

源码地址：
https://github.com/alibaba/fastjson

android版本使用示例：
compile 'com.alibaba:fastjson:1.1.57.android'

Fastjson提供Android版本，和标准版本相比，Android版本去掉一些Android虚拟机dalvik不支持的功能，使得jar更小，同时针对dalvik做了很多性能优化，
包括减少方法调用等。parse为JSONObject/JSONArray时比原生org.json速度快，序列化反序列化JavaBean性能比jackson/gson性能更好。


使用方法：http://blog.csdn.net/zeuskingzb/article/details/17468079
