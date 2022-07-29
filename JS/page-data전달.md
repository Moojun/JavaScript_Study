# page가 넘어갈 때, 넘어가기 이전 page의 data를 전달하기

Situation]

* 1.ejs -> 2.ejs -> 3.ejs -> 4.ejs -> **a.ejs**
* 1-1.ejs -> 2-1.ejs -> 3-1.ejs -> 4-1.ejs -> **a.ejs**

**a.ejs** 에서 button을 누르면 1.ejs or 1-1.ejs 로 이동해야 하는데, 이 때 4.ejs -> **a.ejs** 로 온 경우라면, button을 눌렀을 때 1.ejs로 이동해야 하고, 4-1.ejs -> **a.ejs** 로 온 경우라면, 1-1.ejs로 이동하도록 해야 한다.
x.ejs -> **a.ejs** 로 이동하는 function 혹은 button function은 javascript로 작성되어 있다.

-> `Html data attribute & Localstorage` 사용해서 해결함


### Html data attribute 

> reference link: [tistory](https://dololak.tistory.com/364), [delfstack](https://www.delftstack.com/ko/howto/javascript/get-attribute-values-in-javascript/), [velog](https://velog.io/@yunsungyang-omc/HTML-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%86%8D%EC%84%B1-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-data-attribute)

```html
<!-- 4.ejs -->
<input type="text" data-value="a-page" id="page">   
```

```html
<!-- 4-1.ejs -->
<input type="text" data-value="b-page" id="page">   
```

<br>

### Localstorage 

> reference link: [tistory](https://kgu0724.tistory.com/229)

localStorage is a property that allows JavaScript sites and apps to save key-value pairs in a web browser with no expiration date. This means the data stored in the browser will persist even after the browser window is closed.

```javascript
/* pageMove.js > moveTutorial() 과 연관됨 */
/* x.ejs -> a.ejs 로 이동하는 부분 */
let pageCheck = document.querySelector("#page").dataset.value;
localStorage.setItem("page", pageCheck);
```

```javascript
/* a.ejs -> x.ejs 로 이동하는 부분 */
async function moveTutorial() {
    if (localStorage.getItem("page") == "a-page")  {
        location.href = '/';
    }
    else if (localStorage.getItem("page") == "b-page"){
        location.href = 'b/';
    }
} 
```
