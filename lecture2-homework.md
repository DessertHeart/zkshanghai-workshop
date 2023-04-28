# 第2课 课后作业

> 题目链接：https://zkshanghai.xyz/notes/exercise2.html

## 第1题： 转换为bit位Num2Bits

```rust
pragma circom 2.1.4;

template Num2Bit (nBits) {
    signal input in;
    signal output b[nBits];

    var acc;
    for (var i = 0; i < nBits; i++) {
        b[i] <-- in \ (2 ** i) % 2;
        // 1st hint
        0 === b[i] * (1 - b[i]);
        // binary -> decimal
        acc += b[i] * (2 ** i);
    }
    
    // 2rd hint
    in === acc;
}

template Main () {
    signal input in;
    signal output o;

    component n2b = Num2Bit(4);
    n2b.in <== in;

    o <== n2b.b[0];
}

component main = Main();

/* INPUT = {
    "in": "11"
} */
```

## 第2题： 判零 IsZero

```rust
pragma circom 2.1.4;

template IsZero () {
    signal input in;
    signal output out;

    signal inv <-- in == 0? 0: 1/in;

    // 1st hint: 注意要先给out赋值，才能用第二个约束
    out <== -in * inv + 1;
    // 2st hint
    0 === in * out;
}

template Main () {
    signal input in;
    signal output o;

    component iz = IsZero();
    iz.in <== in;

    o <== iz.out;
}

component main = Main();

/* INPUT = {
    "in": "0"
} */
```

## 第3题： 相等 IsEqual

```rust
pragma circom 2.1.4;

template IsEqual () {
    signal input in[2];
    signal output out;

    component iz = IsZero();

    iz.in <== in[0] - in[1];

    out <== iz.out;
}

template Main () {
    signal input in[2];
    signal output o;

    component ie = IsEqual();
    (ie.in[0], ie.in[1])  <== (in[0], in[1]);

    o <== ie.out;
}

component main = Main();

/* INPUT = {
    "in": ["1", "2"]
} */
```

## 第4题： 少于 LessThan

```rust
pragma circom 2.1.4;

template LessThan (n) {
    signal input in[2];
    signal output out;

    // 输入信号最多为252, 2^k -1
    assert(n < 252);

    // 取n
    component n2b = Num2Bit(n+1);
    n2b.in <== in[0] + (1<<n) - in[1];

    // 二进制取最高位, 1-的目的为 < 比较，本身为 > 比较
    out <== 1 - n2b.b[n];
}

template Main () {
    signal input in[2];
    signal output o;

    component lt = LessThan(2);
    (lt.in[0], lt.in[1]) <== (in[0], in[1]);

    o <== lt.out;
}

component main = Main();

/* INPUT = {
    "in": ["0", "1"]
} */
```

## 第5题： 选择器 Selector

```rust
pragma circom 2.1.4;

// 求和
template Sum(n) {
    signal input in[n];
    signal output out;

    signal sums[n];

    sums[0] <== in[0];

    for (var i = 1; i < n; i++) {
        sums[i] <== sums[i-1] + in[i];
    }

    out <== sums[n-1];
}


template Select (nChoices) {
    signal input in[nChoices];
    signal input index;
    signal output out;

    // index 越界（不在 [0, nChoices) 中），out 应该是 0
    // 254 < 256 = 2^8
    component lt = LessThan(8);
    lt.in[0] <== index;
    lt.in[1] <== nChoices;
    lt.out === 1;

    component sm = Sum(nChoices);
    component ie[nChoices];

    for (var i = 0; i < nChoices; i++) {
        ie[i] = IsEqual();
        ie[i].in[0] <== i;
        ie[i].in[1] <== index;

        // 约束：对应index
        sm.in[i] <== ie[i].out * in[i];
    }

    // 输出out应该等于in[index]
    // 期望返回：0 + 0 ... + item
    out <== sm.out;
}

template Main () {
    signal input in[2];
    signal input index;
    signal output o;

    component st = Select(2);
    (st.in[0], st.in[1], st.index) <== (in[0], in[1], index);

    o <== st.out;
}

component main = Main();

/* INPUT = {
    "in": ["6", "7"],
    "index" : 0
} */
```
