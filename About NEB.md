NewLand Enterprise Browser For NQuire-300
---

[TOC]

### 1. What is NEB
NEB is an acronym for NewLand Enterprise Browser.

You can install NEB on NQuire300, run it like an Android application, and use it instead of the original CIT application.NEB is based on the open source framework Cordova, so you can find what you need information on the [Cordova website](http://cordova.apache.org/).

### 2. What can NEB do

 - Boot automatically activated.
 - Full screen display.
 - Load the specified html file on server.
 - Scan Barcode
 - Read NFC Tag

### 3. How to use NEB

#### 3.1.Download&Import NEB code from GitHub


Unzip the [NlScanCordova.zip](https://github.com/feifly6666/NEB/blob/feifly6666-patch-1/NlScanCordova.zip) and import code into Android Studio.

※When you unzip the file you will need a password that provided by NewLand FAE.

Please select `NlScanCordova \ platforms \ android \ build.gradle` file to import the project.


#### 3.2.Copy the `www` folder to the server

After imported `NlScanCordova` into Android Studio, you can see a `www` folder under the path `NlScanCordova \ platforms \ android \ app \ src \ main \ assets`


 Copy the `www` folder to server.

**Examples:**

Copy the `www` folder to xampp (apache) server's htdocs directory and renamed it to NEBTest.


#### 3.3.Modify Config.xml

Config.xml is a global configuration file that controls many aspects of a cordova application's behavior. You can find more details in [cordova's homepage](http://cordova.axuer.com/docs/zh-cn/latest/config_ref/index.html).

Open the `NlScanCordova \ platforms \ android \ app \ src \ main \ res \ xml \ config.xml` file in Android Studio.

Before running NEB, you need to modify the `<content> `tag to set the URL to your own web page.

**Examples:**

```xml
<content src="http://192.168.27.152:80/NEBTest/index.html" />
```

Modify the `<preference>` tag to specify the error page's URL and local page's URL if you need.

`errorUrl` specifies the prompt page when the network is abnormal and the server is not connected.

`localUrl` specifies URL that the current network is normal, but you do not want to connect to the server and want to visit the local page of NQuire300.

**Examples:**

```xml
<preference name="errorUrl" value="file:///android_asset/www/errorPage.html" />
<preference name="localUrl" value="file:///android_asset/www/index.html" />
```
#### 3.4.Start NEB Application

Connect NQuire300 and computer via the USB cable and start NEB by Android Studio.


### 4.API

You can use the JS API provided by NEB to get the read results of  barcode or NFC Tag.

Methods:

- `nlscan.plugins.barcodescanner.scan`：Start to scan.
- `nlscan.plugins.barcodescanner.scanSetting`:Change the scan settings.
- `nlscan.plugins.barcodescanner.show`：Return the scan result.




#### nlscan.plugins.barcodescanner.scan

Start to scan a barcode.

**Method:**	

```
nlscan.plugins.barcodescanner.scan();
```

**Parameters**

​	**null**

**Example:**

```
var btnScan=document.getElementById("btnScan");
btnScan.onclick=function(){
 nlscan.plugins.barcodescanner.scan();
}
```



#### nlscan.plugins.barcodescanner.scanSetting

To change the scan settings

**Method:**	

```js
nlscan.plugins.barcodescanner.scanSetting([settingName,settingValue])
```

**Parameters**

- **settingName**:The name of setting which available value is `EXTRA_SCAN_POWER`,`EXTRA_TRIG_MODE` or `EXTRA_SCAN_NOTY_SND`.
- **settingValue**:The value to set.

Specific settings can refer to the following table.

| SettingName         | SettingValue | Note                       |
| ------------------- | ------------ | -------------------------- |
| EXTRA_SCAN_POWER    | 0            | Disable scanning           |
|                     | 1            | Enable scanning            |
| EXTRA_TRIG_MODE     | 0            | Normal trigger             |
|                     | 1            | Continuous trigger         |
|                     | 2            | Timeout trigger            |
| EXTRA_SCAN_NOTY_SND | 0            | Turn off the voice prompts |
|                     | 1            | Turn on the voice prompts  |

**Example:**

```
var btnScanSetting=document.getElementById("btnScanSetting");
btnScanSetting.onclick=function(){
 nlscan.plugins.barcodescanner.scanSetting(["EXTRA_SCAN_POWER",0]);
}
```



#### nlscan.plugins.barcodescanner.show

This API is also called by JAVA code and return the read result to Javascript.In Javascript code you can get the read result and display or modify it.

**Method:**	

```js
nlscan.plugins.barcodescanner.show(msg)
```

**Parameters**

​	**msg**:the read result

**Example:**

java:

```java
loadUrl("javascript:nlscan.plugins.barcodescanner.show('" + readResult + "')");
```

javascript:

```javascript
myFunc.prototype.show = function (msg) {
    document.getElementById("outputArea").value = document.getElementById("outputArea").value  + msg;
};
```

### 5.NEBConfig

NEBConfig is a config tool that you can use it to modify NEB's startup page URL.

You can install it to NQuire300 at the same time as NEB. 

#### 5.1.Download&Import NEB code from GitHub

Unzip the [NEBConfig.zip](https://github.com/feifly6666/NEB/blob/feifly6666-patch-1/NEBConfig.zip) and import code into Android Studio.

※When you unzip the file you will need a password that provided by NewLand FAE.

Please select `NEBConfig\ build.gradle` file to import NEBConfig project.

#### 5.2.Start NEBConfig Application

Connect NQuire300 and computer via the USB cable and start NEBConfig by Android Studio.


> Web Page

When you selected `Web Page` radio button the URL input area below will be enabled, you can enter your URL address that want to show in NEB.

> Local Page

When you selected `Local Page` radio button the URL input area below will be disabled,and NEB will show the page that  specified in the `Config.xml` file.
