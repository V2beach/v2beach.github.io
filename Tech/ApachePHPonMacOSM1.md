# PHP

```
brew install php
php -v
PHP 8.2.12 (cli) (built: Oct 26 2023 18:20:46) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.2.12, Copyright (c) Zend Technologies with Zend OPcache v8.2.12, Copyright (c), by Zend Technologies
```

# Apache
macOS是自带apache的，但M1的macOS（或者是较新版的macOS）的apache不支持php。

## 方法1
```
sudo vim /etc/apache2/httpd.conf
#PHP was deprecated in macOS 11 and removed from macOS 12
LoadModule php_module /opt/homebrew/opt/php@8.2/lib/httpd/modules/libphp.so "V2beachRootCA"
```

需要加一行，加载php相关动态库。之后sudo apachectl restart即可。

## 方法2
如果还不行，在配置文件里再加入下面代码，针对php文件用application/x-httpd-php处理。

```
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>
 
<FilesMatch .php$>
  SetHandler application/x-httpd-php
</FilesMatch>
```

## 方法3
如果还不行，需要对libphp数字签名。

首先创建一个CA，一定要选择Code Signing。
![](/assets/Screen Shot 2023-11-08 at 16.00.51.png)
然后codesign，
```
(base) v2beach@V2beachs-mbp-m1 code % codesign --sign "V2beachRootCA" --force --keychain ~/Library/Keychains/login.keychain-db /opt/homebrew/opt/php@8.2/lib/httpd/modules/libphp.so
/opt/homebrew/opt/php@8.2/lib/httpd/modules/libphp.so: replacing existing signature

(base) v2beach@V2beachs-mbp-m1 Documents % apachectl -config
[Sun Nov 05 00:48:25.448876 2023] [so:notice] [pid 77976] AH06662: Allowing module loading process to continue for module at /opt/homebrew/opt/php@8.2/lib/httpd/modules/libphp.so because module signature matches authority "V2beachRootCA" specified in LoadModule directive
AH00526: Syntax error on line 1 of -c/-C directives:
Invalid command 'onfig', perhaps misspelled or defined by a module not included in the server configuration

(base) v2beach@V2beachs-mbp-m1 Documents % httpd -t
[Sun Nov 05 00:50:43.949190 2023] [so:notice] [pid 78112] AH06662: Allowing module loading process to continue for module at /opt/homebrew/opt/php@8.2/lib/httpd/modules/libphp.so because module signature matches authority "V2beachRootCA" specified in LoadModule directive
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using V2beachs-mbp-m1.local. Set the 'ServerName' directive globally to suppress this message
Syntax OK
```

现在应该就可以正确解析php了。
![](/assets/Screen Shot 2023-11-05 at 23.05.31.png)

改写了PHP音乐接口https://github.com/V2beach/meting-vercel 。还挺有趣的。