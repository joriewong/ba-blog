---
  layout: post
  title: 常用的JavaScript位操作(Bitwise)
  categories: [FE]
---

## 位操作

JavaScript中的数字都按照IEEE-754(Institute of Electrical and Electronics Engineers)标准以64位格式存储。在位操作中，数字被转换为有符号32位格式。每次运算符会直接操作该32位数以得到结果。虽然需要转换，但这个过程与JavaScript其他数学运算和布尔操作相比要快很多。

- Bitwise AND 按位与

两个操作数的对应位都是1时，则在该位置返回1。

- Bitwise OR 按位或

两个操作数的对应位只要一个为1时，则在该位返回1。

- Bitwise XOR 按位异或

两个操作数的对应位只有一个为1，则在该位返回1。

- Bitwise NOT 按位取反

遇0则返回1，反之亦然。

## 颜色交替

32位数字的二进制底层表示，偶数的最低位是0，奇数的最低位是1。如果此数为偶数，和1按位与的结果是0；如果此数为奇数，和1按位与的结果是1。可以使用该方法实现颜色交替，效率可能会比纯数学运算（如，取模）快50%。

``` javascript
    for (let i = Things.length - 1; i >= 0; i--) {
        if(i & 1) {
            className = 'oddColor';
        }else {
            className = 'evenColor';
        }
    }
```

## 位掩码

位掩码用于处理同时存在多个布尔选项的情形。使用单个数字的每一位来判定选项是否成立，从而有效地把数字转换为由布尔值标记组成的数组。**掩码中的每个选项的值都等于2的幂**。

``` javascript
const OPTION_A = 1;
const OPTION_B = 2;
const OPTION_C = 4;

const options  = OPTION_A | OPTION_B;

// 选项A是否在options中
if(options & OPTION_A) {
    // code here
}
// 选项A是否在options中
if(options & OPTION_B) {
    // code here
}
// 选项A是否在options中
if(options & OPTION_C) {
    // code here
}
```

