Installing the php_imagick extension on Windows Azure Web App
===

Download the .dll
---

* Get the latest php_imagick.dll from here **https://mlocati.github.io/articles/php-windows-imagick.html**
* Make sure that the extensions are compatible with ***default version of PHP and are VC9 and non-thread-safe (nts) compatible***.
* Unzip the folder and Copy all `CORE_RL_*` files to `d:\home\site\ImageMagick\`
* Copy `php_imagick.dll` to `d:\home\site\ext\` 
* Create new `applicationHost.xdt` file inside the `d:\home\site` folder and copy the below configuration
	
```
<?xml version="1.0"?> 
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform"> 
  <system.webServer> 
    <runtime xdt:Transform="InsertIfMissing">
      <environmentVariables xdt:Transform="InsertIfMissing">
        <add name="PATH" value="%PATH%;d:\home\site\ImageMagick" xdt:Locator="Match(name)" xdt:Transform="InsertIfMissing" />
      </environmentVariables>
    </runtime> 
  </system.webServer> 
</configuration> 
```


* Also, attached the applicationHost.xdt in this repro

Application Settings
---

* Add an App Setting with the name `MAGICK_CODER_MODULE_PATH` and set value to `d:\home\site\ImageMagick`
* Add an App Setting with the name `MAGICK_HOME` and set the value to `d:\home\site\ImageMagick`
* Add an App Setting with the name `PHP_EXTENSIONS` and set the value to `d:\home\site\ext\php_imagick.dll`

**Restart the Web App and check the phpinfo page. It should return a imagick module section.**
	
Refrence
---
**https://blogs.msdn.microsoft.com/azureossds/2015/12/07/php-imagemagick-on-azure-web-apps/**
	