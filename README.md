# Aras 12 REST Sample

### Aras REST API呼叫範例

### 示範Aras版本: Aras 12.0 SP9 (要Aras 12以上才有支援)

1. 裡面示範了用js以**REST**( `POST` )方式做身分驗證取得登入Token
   ```js
            //POST的Body參數
            let data = ["grant_type=password", 
                        "scope=Innovator", 
                        "client_id=IOMApp", 
                        "username=登入帳號", 
                        "password=登入密碼", 
                        "database=登入DB"];
            ...
            //這裡示範把Token塞到window以便後面取用(Production別這樣用...拜託...)
            window.arasToken = res.access_token;
   ```
2. 已經取得Token就可以使用Token存取資料啦~~~
   ```js
        //重點是要把Token在放Header的Authrization標籤中
        xhr.setRequestHeader('Authorization', `Bearer ${window.arasToken}`);
   ```


 > ⚠⚠⚠
 > 這裡有的問題要注意，就是用js會有**CORS**的問題要處理。基本上OAuth沒有問題，因為`OAuth.config`本身有CORS的配置...
 > 但是因為後段OData取資料呼叫的URL是`~\server\odata`，沒有設定CORS的地方就會呼叫失敗...
 > 如果是應用程式(Winform, WPF, 手機APP)就沒有這個問題囉~~

