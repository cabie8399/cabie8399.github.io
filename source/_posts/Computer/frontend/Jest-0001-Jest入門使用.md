---
title: "[Jset] Jset入門使用"
date: 2023-02-09 03:58:36
tags:
  - jest
categories:
  - frontend
cover: https://miro.medium.com/v2/resize:fit:828/format:webp/1*Lj98LRbO4tDyE9UCxPV58A.jpeg
feature: true
---


[Github程式範例](https://github.com/cabie8399/Study_Note/tree/main/Javascript/0001_jest_test)


# 為何要做測試 ?

為了在人工測試前先進行初步的除錯，發展出了自動化測試。

前端常見的自動化測試有兩大類別，此篇主要是講解「Unit Test」，以下為簡單的類別說明：

## **Unit Test**

單元測試，是以單一個行為進行測試，通常專案中最小的單位就是 funciton ，因此就是驗證 funciton 運行是否符合結果。

## **E2E Test**

直接模擬 User 在 Browser 的行為做測試。

# 如何使用Jest ?

- 安裝

```bash
cabie@cabie-ubuntu:~/workplace/01_study/0001_jest_test$ npm install -save-dev jest
```

- package.json : 加上scripts

```bash
{
  "devDependencies": {
    "jest": "^29.4.2"
  },
  "scripts": {
    "test": "jest",
    "start": "node index.js"
  }
}
```

- index.js

```bash
function sum(a, b) {
    return a + b;
};

module.exports = sum;
```

- index.test.js

```bash
const sum = require('./index');

// describe()
// 說明單元測試，類似群組的概念，將多個 test 包在一起，讓程式看起來更有結構性。
// describe('測試 sum function', function(){ test… })

// describe('僱員的行為測試', () => {
//     test('點餐內容與顧客需求相符', () => {});
//     test('結帳金額正確', () => {});
//     test('找零的金額正確', () => {});
// });

// test()
// 定義一個單元測試
test('a=1, b=2 加起來等於 3', () => {
    expect(sum(1,2)).toBe(3);
});
```

> ! 注意  :  在jest原生测试框架中，无法使用es6的import export语法，只能使用commonJS语法，本文解决了相关配置问题。
> 

可參考這篇了解在ES6中如何使用

[Jest使用ES6语法配置](https://juejin.cn/post/6990172738853797902)

- npm run test

```bash
cabie@cabie-ubuntu:~/workplace/01_study/0001_jest_test$ npm run test

> test
> jest

 PASS  ./index.test.js
  ✓ a=1, b=2 加起來等於 3 (2 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.23 s
Ran all test suites.
```

改成toBe(7), 再跑一次

```bash
cabie@cabie-ubuntu:~/workplace/01_study/0001_jest_test$ npm run test

> test
> jest

 FAIL  ./index.test.js
  ✕ a=1, b=2 加起來等於 3 (3 ms)

  ● a=1, b=2 加起來等於 3

    expect(received).toBe(expected) // Object.is equality

    Expected: 7
    Received: 3

      10 | // 定義一個單元測試
      11 | test('a=1, b=2 加起來等於 3', () => {
    > 12 |     expect(sum(1,2)).toBe(7);
         |                      ^
      13 | });

      at Object.toBe (index.test.js:12:22)

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 total
Snapshots:   0 total
Time:        0.305 s, estimated 1 s
Ran all test suites.
```

- 除了使用終端機外，Jest 與 VSCode 也能有很好的整合，不需要每次運行都輸入 `npm run test`，搭配套件使用即可在每次存檔後看到測試的結果。
    
    套件連結：[https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest)
    
- 新增jest.config.js(Jest 設定檔案)，此測試檔案預設僅需要匯出一個空的即可運作（全部使用官方預設即可）
    
    ```bash
    module.exports = {
    };
    ```
    

- 就可以看到test左邊就會顯示測試結果

![Untitled](https://i.imgur.com/CGxdp69.png)

### Jest總結

單元測試難的也並非是語法，更重要的是如何驗證函式的行為與產品邏輯一致。

1. 測試的目標為何？ -> `test('...', ()=>{})`
2. 導入要測試的函式 -> `sum()`
3. 測試的期望是什麼？ -> `expect(...).toBe(...);`

# 什麼是TDD ?

全名 Test-driven Development，中文為測試驅動開發，也就是我們先寫測試再做開發，好處就是寫完code時，測試也完成了。

測試驅動開發的「測試」，精髓在先定好想要的目標，強迫自己先想清楚最終目標，以終為始，避免自己走偏、迷惘、花時間在不必要的功能上。測試驅動開發的測試，不只是測試，更是一種需求的描述。

不過聽了那麼久TDD，好像蠻少遇到台灣公司是這樣開發的，畢竟大家第一個會覺得我都沒時間開發新功能了，還寫測試，不知道大家有沒有用TDD開發的經驗。

# 參考資料

[[第三週] JavaScript - 測試框架 Jest](https://miahsuwork.medium.com/%E7%AC%AC%E4%B8%89%E9%80%B1-javascript-%E6%B8%AC%E8%A9%A6%E6%A1%86%E6%9E%B6-jest-eccf0ff2cea2)