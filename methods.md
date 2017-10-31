# 情境範例

1. 如有各項input/output的範例可先舉例，供所有人快速了解，佳

2. 若輔以特定programming language的語法描述input/process/output，使表達更加清晰快速，可嘗試之

{% method %}
## 範例一

第一種方法，給予展示如何印出stdout

使用簡單例預設顯示在右側欄位

{% sample lang="js" %}
如何用JavaScript印出`stdout`
```js
console.log('My first method');
```

{% sample lang="C/C++" %}
如何用C/C++印出`stdout`
```c
printf("My first method");
```
or another way, 
```c
cout << "My first method";
```

{% common %}
螢幕輸出結果為：

```bash
$ My first method
```
{% endmethod %}

{% method %}
## 範例二

撰寫此頁面的語法如何使用，可參考[連結](https://gitbook.zhangjikai.com/themes.html)

{% sample lang="C/C++" %}
如何用C/C++相加兩個`string`
```c
string a = "hello";
string b = "world";
string c = a + " " + b;
cout << c << endl;  # hello world
```



{% endmethod %}

