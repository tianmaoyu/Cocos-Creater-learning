# 使用 async await 让程序变得简单优美

## 1.1 先看看 能带动一帮兄弟就业的写法，能带动整个软件行业走向繁荣哦

```ts
  
    private createAuthorize() {
        let self=this;
        tt.login({
            success(res) {
                tt.getSetting({
                    success(res) {
                        tt.getUserInfo({
                            withCredentials: true,
                            success(res) {
                               //console.log(`getUserInfo调用成功${res}`);
                                tt.request({
                                            url: "*******",
                                            data: {},
                                            method: 'GET',
                                            success: function(res){
                                                //console.log(`getUserInfo调用成功${res}`);
                                             },
                                             fail(res){

                                       }
                                });
                            },
                            fail(res) {
                                //console.log(`getUserInfo调用失败${res}`);
                            }
                        })
                    }
                })
            },
            fail(res) {
                //console.log(`login调用失败`);
            }
        });

    }
```

##  1.2 改进后的效果

```ts
    /**TT的 openid */
    public static async createAuthorize() :Promise<string>{
        let login = await TTAsync.loginAsync();
        let seting = await TTAsync.getgetSettingAsync();
        let userInfo = await TTAsync.getUserInfoAsync();
        let session = await TTAsync.getSession(userInfo);
    }
```
## 1.3 如果报错怎么办？再改进一下
```ts
    /**TT的 openid */
    public static async createAuthorize() :Promise<string>{
        var  [err,login] = await asyncWrap(TTAsync.loginAsync());
        if(err){ /*报错了*/ }

        var  [err,seting] = await  asyncWrap(TTAsync.getgetSettingAsync());
        if(err){ /*报错了*/}

        var  [err,userInfo] = await  asyncWrap(TTAsync.getUserInfoAsync());
        if(err){ /*报错了*/}

        var  [err,session] = await  asyncWrap(TTAsync.getSession(userInfo));
         if(err){ /*报错了*/}
    }
```

## 1.4  对 tt 中 api 异步的封装
```js
declare let tt:any;

export function asyncWrap<T, U = any>(promise: Promise<T>): Promise<[U | null, T | null]> {
    return promise
        .then<[null, T]>((data: T) => [null, data])
        .catch<[U, null]>(err => [err, null])
}


export class TTAsync{

    public static loginAsync():Promise<any>{
        return new Promise<any>((resolve,reject)=>{
            tt.login({
                success(res) {
                    resolve(res);
                },
                fail(res){
                    reject(res)
                }
            });
        });
    }
   
    public static getgetSettingAsync():Promise<any>{
        return new Promise<any>((resolve,reject)=>{
            tt.getSetting({
                success(res) {
                    resolve(res);
                },
                fail(res){
                    reject(res)
                }
            })
        });
    }

    public static getUserInfoAsync():Promise<any>{
        return new Promise<any>((resolve,reject)=>{
            tt.getUserInfo({
                withCredentials: true,
                success(res) {
                    resolve(res);
                },
                fail(res){
                    reject(res)
                }
            })
        });
    }


    public static getSession(clientInfo:any):Promise<any>{
        return new Promise<any>((resolve,reject)=>{
            var url='https://developer.toutiao.com/api/apps/jscode2session?appid='+clientInfo.appid+'&secret='+clientInfo.secret+'&js_code='+clientInfo.code+'&grant_type=authorization_code';  
            tt.request({  
                url: url,  
                data: {},  
                method: 'GET', 
                success: function(res){ 
                    resolve(res);
                },
                fail(res){
                    reject(res)
                } 
            });
        });
    }

}

```

## 少年我知道你早晚都回超越我的，你会了吗》 来下在远程MP3 试试
```js

let audio= await CCAsync.loadMp3("https://www.baidu.com/bgm.mp3");


export class CCAsync {

    public static loadMp3(url): Promise<cc.AudioClip> {
        return new Promise<cc.AudioClip>((resolve, reject) => {
            cc.loader.load({url: url , type: 'mp3'}, function (err, texture) {
                if (err) {
                    reject(err);
                } else {
                    resolve(texture);
                }
            });
        });
    }

}
```

