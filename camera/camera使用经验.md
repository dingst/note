1、camera开发中，exifinterface中写入经纬度的时候不能包含小数，必须是整数。

2、camera api 1 中，拍照回调函数中的参数data中包含了exif信息，只需保存data到本地，然后通过exif类获取即可。

3、图片保存到本地，必须是全路径格式，包含扩展名。

