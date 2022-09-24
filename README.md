# Lidemy HTTP Challenge writeup
[Here's the website](https://lidemy-http-challenge.herokuapp.com/start)

## Level 0
![](https://i.imgur.com/DkTV55a.png)

- The token is on the screen
<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv1?token={GOGOGO} -->

## Level 1
![](https://i.imgur.com/ZJuBE9X.png)

- Just pass the name you like as the token

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv1?token={GOGOGO}&name={User} -->

![](https://i.imgur.com/b1FaxiE.png)


<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv2?token={HellOWOrld} -->

## Level 2
![](https://i.imgur.com/3SA91Rs.png)

- try pass the URL as this format: `https://lidemy-http-challenge.herokuapp.com/lv2?token={HellOWOrld}&id=NUMBER` 
<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv2?token={HellOWOrld}&id=56 -->

![](https://i.imgur.com/pRzztbn.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv3?token={5566NO1} -->

## Level 3
![](https://i.imgur.com/mdeitPb.png)
![](https://i.imgur.com/HLEVew8.png)


- Write this code and run it by `node FILE_NAME.js` in the directory's terminal

```javascript=
const request = require('request');

request.post(
    'https://lidemy-http-challenge.herokuapp.com/api/books',// the request url
    // 因為 "POST 以及 PATCH 的 content type 為：application/x-www-form-urlencoded。"
    {form:{
        name: '《大腦喜歡這樣學》',
        ISBN: '9789863594475'
    }},
    (err, response, body) => {
        console.log(body)// get the result
    }
)
```

- After running it, you'll probably get a message and id(which is also the token)

- Get more `application/x-www-form-urlencoded` knowledge at [here](https://www.796t.com/content/1536302734.html)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv3?token={5566NO1}&id=1989 -->

![](https://i.imgur.com/NSCqsRs.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv4?token={LEarnHOWtoLeArn} -->

## Level 4
![](https://i.imgur.com/l3ESaOo.png)

- After reading this
![](https://i.imgur.com/HLEVew8.png)

- You'll probably know that `https://lidemy-http-challenge.herokuapp.com/api/books?q=世界` has the token

![](https://i.imgur.com/bEuNAEO.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv4?token={LEarnHOWtoLeArn}&id=79 -->

![](https://i.imgur.com/dRMXaNw.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv5?token={HarukiMurakami} -->

## Level 5
![](https://i.imgur.com/urAfRhv.png)

- Create a .js file with these codes
```javascript=
const request = require('request');

request.delete(
    'https://lidemy-http-challenge.herokuapp.com/api/books/23',
    (err, response, body) => {
        console.log(body)
    }
)
```
- After running it by `node FILE_NAME.js`, you'll see the token
<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv6?token={CHICKENCUTLET} -->

## Level 6
![](https://i.imgur.com/pcj62xo.png)

- Enter the URL you'll find this
![](https://i.imgur.com/IIBPXGE.png)

```python=
首先你必須準備好一組字串，內容為 base64(username:password)
舉例來說，如果 username 是 aaa，password 是 123 的話，就會是字串 aaa:123 拿去做 base64 編碼之後得到的結果
再把這個結果放到 Header 去，最後變成：Authorization: Basic YWFhOjEyMw==
只要帶上這個 Header 就可以驗證身份囉！
```

- Use [Online base64 encoder](https://www.base64encode.org/) to get the result of the 'Authorization'
![](https://i.imgur.com/XJWXhjS.png)

- Therefore, create a file with codes below
```javascript=
const request = require('request');

const option = {
    url: 'https://lidemy-http-challenge.herokuapp.com/api/v2/me',
    headers: {
        'Authorization': 'Basic YWRtaW46YWRtaW4xMjM='
    }
}

function callback (error, response, body) {
    console.log(body)
}

request(option, callback)
```
- And you'll get this: `{"username":"admin","email":"lib@lidemy.com"}`

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv6?token={CHICKENCUTLET}&email=lib@lidemy.com -->

![](https://i.imgur.com/Sie5u6V.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv7?token={SECurityIsImPORTant} -->

## Level 7

![](https://i.imgur.com/rBAaENs.png)

- Create a file and code this

```javascript
const request = require('request');

request.delete(
    {
        url: 'https://lidemy-http-challenge.herokuapp.com/api/v2/books/89',
        headers: {
            'Authorization': 'Basic YWRtaW46YWRtaW4xMjM='
        }
    }, 
    (error, response, body) => console.log(body)
)
```

- Run it to get the token

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv8?token={HsifnAerok} -->

## Level 8

![](https://i.imgur.com/NLBOgBS.png)
- Use [Online URI encoder](https://www.urlencoder.org/) to get the `q` value
![](https://i.imgur.com/7qES6Hm.png)


- Code a file that could find the book information (and the target is the book with id 72)
```javascript=
const request = require('request');

const option = {
    url: `https://lidemy-http-challenge.herokuapp.com/api/v2/books?q=%E6%88%91`,
    headers: {
        'Authorization': 'Basic YWRtaW46YWRtaW4xMjM='
    }
}

function callback (error, response, body) {
    const json = JSON.parse(body)
    console.log(json)
}

request.get(option, callback)

```

- Run these codes to get the token
```javascript=
const request = require('request');

const option = {
    url: 'https://lidemy-http-challenge.herokuapp.com/api/v2/books/72',
    headers: {
        'Authorization': 'Basic YWRtaW46YWRtaW4xMjM='
    },
    form: {
        ISBN: '9981835423',
    }
}

function callback (error, response, body) {
    console.log(body)
}

request.patch(option, callback)
```

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv9?token={NeuN} -->

## Level 9
![](https://i.imgur.com/VruetXq.png)

- Open DevTools to get the value of user agent
![](https://i.imgur.com/7AdbN2t.png)

- Run this file to get the token
```javascript=
const request = require('request');

const option = {
    url: 'https://lidemy-http-challenge.herokuapp.com/api/v2/sys_info',
    headers: {
        'Authorization': 'Basic YWRtaW46YWRtaW4xMjM=',
        'X-Library-Number': '20',
        'User-Agent': 'Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1)'
    },
}

function callback (error, response, body) {
    console.log(body)
}

request.get(option, callback)
```
- Pass the version value to get the token

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv9?token={NeuN}&version=1A4938Jl7 -->

![](https://i.imgur.com/iIDdcit.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv10?token={duZDsG3tvoA} -->

## Level 10
![](https://i.imgur.com/pbXbDEL.png)

- A "Guess the number game"

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv10?token={duZDsG3tvoA}&num=9613 -->

![](https://i.imgur.com/JW8j4dF.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv11?token={IhateCORS} -->

## Level 11
![](https://i.imgur.com/prQcKoX.png)

- You'll get this after accessing the website
![](https://i.imgur.com/x6bkhId.png)

- First, run the code similar to the files before
```javascript=
const request = require('request');

request.get(
    'https://lidemy-http-challenge.herokuapp.com/api/v3/hello',
    (error, response, body) => {
        console.log(body)
    }
)
```
- But get `您的 origin 不被允許存取此資源，請確認您是從 lidemy.com 送出 request。`
- So add the `origin` and it gave us the token
```javascript=
const request = require('request');

const option = {
    url: 'https://lidemy-http-challenge.herokuapp.com/api/v3/hello',
    headers: {
        'Origin': 'lidemy.com'
    },
}

function callback (error, response, body) {
    console.log(body)
}

request.get(option, callback)
```

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv12?token={r3d1r3c7} -->

## Level 12
![](https://i.imgur.com/fwi6aJN.png)

- After reading the file it provides, I decide to go to ` https://lidemy-http-challenge.herokuapp.com/api/v3/deliver_token`
- And open DevTools >>> Network and you'll find the token
![](https://i.imgur.com/HhmuUAH.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv13?token={qspyz} -->

## Level 13
![](https://i.imgur.com/QpKkjIs.png)

- Enter this [website](http://free-proxy.cz/zh/proxylist/country/PH/http/ping/all) and choose the one with HTTPS
- Change your proxy server to it
- Access `https://lidemy-http-challenge.herokuapp.com/api/v3/logs` to get the token
![](https://i.imgur.com/5HiJRWO.png)

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv14?token={SEOisHard} -->

## Level 14
![](https://i.imgur.com/mXMlBw9.png)

- Run `https://lidemy-http-challenge.herokuapp.com/lv14?token={SEOisHard}&hint=1` to get some clues
![](https://i.imgur.com/C1pApMK.png)

- Enter [this website](https://developers.whatismybrowser.com/useragents/explore/software_name/googlebot/) and grab one user agent
![](https://i.imgur.com/ZdvoQxF.png)

- Run this code to get the token
```javascript=
const request = require('request');

const option = {
    url: 'https://lidemy-http-challenge.herokuapp.com/api/v3/index',
    headers: {
        'User-Agent': 'Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)'
    },
}

function callback (error, response, body) {
    console.log(body)
}

request.get(option, callback)
```

<!-- ANSWER: https://lidemy-http-challenge.herokuapp.com/lv15?token={ILOVELIdemy!!!} -->

## Level 15
![](https://i.imgur.com/9wuNZKX.png)
