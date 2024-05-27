## 什么是JavaScript？

### 准备工作

- VSCODE
- Google浏览器



### 学习资源

[什么是 JavaScript？ - 学习 Web 开发 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/First_steps/What_is_JavaScript)

> JavaScript 是一种脚本语言，可以用来创建动态更新的内容，控制多媒体，制作图像动画，还有很多。（好吧，虽然它不是万能的，但可以通过简短的代码来实现神奇的功能。）

### 在页面中添加JavaScript

- 内部JavaScript：在</head>标签结束前添加 <script> </script> 标签在内部书写JavaScript代码。如果在</head>标签外部添加，可能造成无法加载脚本代码的问题。
- 外部JavaScript：在其他文件夹中创建script.js的文件，编写JavaScript代码，之后在script标签中使用src来引用。这样做更加有序，更易复用。
- 内联JavaScript：这样做污染了HTML，并不推荐。

```javascript
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>Apply JavaScript example</title>
    <!-- <script>
        // 在此编写 JavaScript 代码  内部JavaScript
        document.addEventListener("DOMContentLoaded", () => {
        function createParagraph() {
            const para = document.createElement("p");
            para.textContent = "你点击了按钮！";
            document.body.appendChild(para);
        }

        const buttons = document.querySelectorAll("button");

        for (const button of buttons) {
            button.addEventListener("click", createParagraph);
        }
        });

      </script> -->
	//外部JavaScript
      <script src="lib/script.js" defer></script>
      
  </head>
  <body>
    <button>Click me</button>
    <button>Click me</button>
    <button>Click me</button>

    <!-- 内联JavaScript <button onclick="createParagraph()">点我！</button> -->

  </body>
</html>
```

### 脚本调用策略

HTML 元素是按其在页面中出现的次序调用的，如果用 JavaScript 来管理页面上的元素（更精确的说法是使用文档对象模型DOM，若 JavaScript 加载于欲操作的 HTML 元素之前，则代码将出错。

旧方法：

把脚本元素放在文档体的底端（也就是 `</body>` 标签之前，与之相邻），这样脚本就可以在 HTML 解析完毕后加载了。此方案的问题是：只有在所有 HTML DOM 加载完成后才开始脚本的加载/解析过程。对于有大量 JavaScript 代码的大型网站，可能会带来显著的性能损耗。



脚本阻塞问题的两种解决方案：

> async：浏览器遇到 `async` 脚本时不会阻塞页面渲染，而是直接下载然后运行。但是，一旦下载完成，脚本就会执行，从而阻止页面渲染。脚本的运行次序无法控制。当页面的脚本之间彼此独立，且不依赖于本页面的其他任何脚本时，`async` 是最理想的选择。

> defer：使用 `defer` 属性加载的脚本将按照它们在页面上出现的顺序加载。在页面内容全部加载完毕之前，脚本不会运行，如果脚本依赖于 DOM 的存在（例如，脚本修改了页面上的一个或多个元素），这一点非常有用。

脚本调用策略小结：

- `async` 和 `defer` 都指示浏览器在一个单独的线程中下载脚本，而页面的其他部分（DOM 等）正在下载，因此在获取过程中页面加载不会被阻塞。
- `async` 属性的脚本将在下载完成后立即执行。这将阻塞页面，并不保证任何特定的执行顺序。
- 带有 `defer` 属性的脚本将按照它们的顺序加载，并且只有在所有脚本加载完毕后才会执行。
- 如果脚本无需等待页面解析，且无依赖独立运行，那么应使用 `async`。
- 如果脚本需要等待页面解析，且依赖于其他脚本，调用这些脚本时应使用 `defer`，将关联的脚本按所需顺序置于 HTML 的相应 `<script>` 元素中。

### 注释

```javascript
// 我是一条注释

// 我是一条注释
/*
  我也是
  一条注释
*/

```



### 猜数字游戏

```javascript
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8">

    <title>Number guessing game</title>

    <style>
      html {
        font-family: sans-serif;
      }

      body {
        width: 50%;
        max-width: 800px;
        min-width: 480px;
        margin: 0 auto;
      }
      
      .form input[type="number"] {
        width: 200px;
      }

      .lastResult {
        color: white;
        padding: 3px;
      }
    </style>
  </head>

  <body>
    <h1>Number guessing game</h1>

    <p>We have selected a random number between 1 and 100. See if you can guess it in 10 turns or fewer. We'll tell you if your guess was too high or too low.</p>

    <div class="form">
      <label for="guessField">Enter a guess: </label>
      <input type="number" min="1" max="100" required id="guessField" class="guessField">
      <input type="submit" value="Submit guess" class="guessSubmit">
    </div>

    <div class="resultParas">
      <p class="guesses"></p>
      <p class="lastResult"></p>
      <p class="lowOrHi"></p>
    </div>

    <script>

      // Your JavaScript goes here
        let randomNumber = Math.floor(Math.random() * 100) + 1;

        const guesses = document.querySelector(".guesses");
        const lastResult = document.querySelector(".lastResult");
        const lowOrHi = document.querySelector(".lowOrHi");

        const guessSubmit = document.querySelector(".guessSubmit");
        const guessField = document.querySelector(".guessField");

        let guessCount = 1;
        let resetButton;
        guessField.focus();
        function checkGuess() {
            const userGuess = Number(guessField.value);
            if (guessCount === 1) {
                guesses.textContent = "Previous guesses: ";
            }
            guesses.textContent += `${userGuess} `;

            if (userGuess === randomNumber) {
                lastResult.textContent = "Congratulations! You got it right!";
                lastResult.style.backgroundColor = "green";
                lowOrHi.textContent = "";
                setGameOver();
            } else if (guessCount === 10) {
                lastResult.textContent = "!!!GAME OVER!!!";
                lowOrHi.textContent = "";
                setGameOver();
            } else {
                lastResult.textContent = "Wrong!";
                lastResult.style.backgroundColor = "red";
                if (userGuess < randomNumber) {
                lowOrHi.textContent = "Last guess was too low!";
                } else if (userGuess > randomNumber) {
                lowOrHi.textContent = "Last guess was too high!";
                }
            }  
        }
        guessSubmit.addEventListener("click", checkGuess);

        guessCount++;
        guessField.value = "";
        guessField.focus();
        function setGameOver() {
            guessField.disabled = true;
            guessSubmit.disabled = true;
            resetButton = document.createElement("button");
            resetButton.textContent = "Start new game";
            document.body.append(resetButton);
            resetButton.addEventListener("click", resetGame);
        }
        function resetGame() {
            guessCount = 1;

            const resetParas = document.querySelectorAll(".resultParas p");
            for (const resetPara of resetParas) {
                resetPara.textContent = "";
            }

            resetButton.parentNode.removeChild(resetButton);

            guessField.disabled = false;
            guessSubmit.disabled = false;
            guessField.value = "";
            guessField.focus();

            lastResult.style.backgroundColor = "white";

            randomNumber = Math.floor(Math.random() * 100) + 1;
        }
    </script>
  </body>
</html>
```



### 声明变量

两个关键字：

- var：var  myname = "xiaoming"
- let：推荐使用  

变量类型

```javascript
Number类型： let myAge = 18
String类型： let dolphinGoodbye = "So long and thanks for all the fish";
Boolean类型： let iAmAlive = true;
Array类型： let myNameArray = ["Chris", "Bob", "Jim"];
			let myNumberArray = [10, 15, 40];
Object类型：let dog = { name: "Spot", breed: "Dalmatian" };

```



### 比较运算符

> 你可能会看到有些人在他们的代码中使用`==`和`!=`来判断相等和不相等，这些都是 JavaScript 中的有效运算符，但它们与`===`/`!==`不同，前者测试值是否相同，但是数据类型可能不同，而后者的严格版本测试值和数据类型是否相同。严格的版本往往导致更少的错误，所以我们建议你使用这些严格的版本。

