# DOM 
觀念:  
1. 為 html 與 js 程式語言的溝通橋梁 (api)。
2. 在 javasript 中，物件的屬性 (properties) 可以為物件；例如 window 物件的 console 屬性及 document 屬性皆為另一個物件。

3. 所有 html 中的 element 皆為 window.document 以下的物件。
4. 最常使用 `document.querySelector()` 和 `document.querySelectorAll()`。

<br/>

<br/>


# Arrow function

與 ES5 宣告函數寫法不同地方:
1. 沒有 hoisting

    ```js
    // 可以呼叫
    hello()

    function hello() {
        console.log('hello');
    }
    ```
    ```js
    // 無法呼叫
    hello()

    let hello = () => {
        console.log('hello');
    }
    ```


2. 在 object 中，舊寫法的 `this` 為物件本身，但 arrow function 的 `this` 為 `window` 物件。

    ```js
    let obj = {
        name: 'apple',
        // 舊寫法 this
        hello(){
            console.log(this.name + ' hello');  // apple hello
        },


        // arrow 函數寫法
        arrow: () => {
             console.log(this.name + ' hello');  // undefined hello
        }
    }

    ```