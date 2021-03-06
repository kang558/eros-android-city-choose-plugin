
![avatar](http://thyrsi.com/t6/617/1543290451x2728278835.gif)


**集成方式**

* 进入Android目录`工程目录/platforms/android/WeexFrameworkWrapper/` 目录下 clone 对应的插件。

``` java
git clone https://github.com/huanghaodong/eros-android-city-choose-plugin.git "citychooseplugin"
```



* 打开Android目录`工程目录/platforms/android/WeexFrameworkWrapper/`,编辑`settings.gradle`,添加引入。
在`settings.gradle` 中 添加如下代码。

``` java
//这里只需要在最后添加 , ':citychooseplugin'
include ':app',':sdk',':nexus', ':wxframework', ':citychooseplugin'  

// chooseCity
project(':citychooseplugin').projectDir = new File(settingsDir,'/citychooseplugin')

```

* 打开Android目录`工程目录/platforms/android/WeexFrameworkWrapper/app`,编辑app目录下`build.gradle` 文件 `dependencies` 下添对应 插件引用。

``` java
	dependencies {
		....
		compile project(':citychooseplugin')
	}
```
* 最后记得点击右上角sync now




## 使用

* 引用Module

	```js
	const choosecity = weex.requireModule('choosecity');
	```
	
* api
##### 参数说明

| name | type | required | Description |
| ------ | ------ | ------ | ------ |
| setSubmitText | String | false | 确定按钮文字 |
| setCancelText | String | false | 取消按钮文字 |
| setTitleText | String | false | 标题文字 |
| setSubCalSize | Number | false | 确定取消按钮文字大小 |
| setTitleSize | Number | false | 标题文字大小 |
| setTitleColor | String | false | 标题文字颜色 |
| setSubmitColor | String | false | 确定文字颜色 |
| setCancelColor | String | false | 取消文字颜色 |
| addressType | String | false | 'custom':自定义地区数据，在address中定义  'defalut':使用自带默认数据 |
| address | Array | false | 使用自定义的数据时，addressType必须为custom，且数据格式必须与该格式一致, |

##### 返回值说明
返回一个对象，属性如下

| name | type | Description |
| ------ | ------ | ------ |
| provinceStr | String | 一级文字 |
| provinceCode | String | 一级编码 |
| cityStr | String | 二级文字 |
| cityCode | String | 二级编码 |
| areaStr | String | 三级文字 |
| areaCode | String | 三级编码 |


```js
  choosecity.open({
        setSubmitText:'确定',//确定按钮文字
        setCancelText:'取消',//取消按钮文字
	setTitleText:'地区选择',//标题文字
	setSubCalSize:14,//确定取消按钮文字大小
	setTitleSize:14,//标题文字大小
	setTitleColor:'#000000',//标题文字颜色
	setSubmitColor:'#000000',//确定文字颜色
	setCancelColor:'#000000',//取消文字颜色
	addressType:'custom',//'custom':自定义地区数据，在如下address中定义  'defalut':使用自带默认数据
	address:[{
	    name:"重庆",
	    code:"12",
	    city:[
	      {
	        name:"重庆区县",
	        code:"13",
	        area:[
	          {
	            name:"彭水",
	            code:"14"
	          }
	        ]
	      }
	    ]
	    }],//自定义的数据，数据格式必须与该格式一致
	      },(place)=>{
	              
	      })
```
 * 返回值
```js
    {
      provinceStr:"湖北",
      provinceCode:"10000",
      cityStr:"武汉",
      cityCode:"10010",
      areaStr:"洪山区",
      areaCode:"10011"
    }
```
## 更新日志
 -   新增地区code编码；新增自定义地区数据。
 
 ## 如果觉得有用，请给个start，谢谢
