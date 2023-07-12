# 第6课 课后作业

> https://zkshanghai.xyz/notes/exercise7.html

## 第1题 宽度为 3 的 AIR 框架 Fibonacci程序

|step|a|b|c|
|----|----|----|----|
|i=1|1|1|2|
|i=2|3|5|8|
|i=3|13|21|34|
|i=4|55|89|144|

转换程序：

 $f_1(X_1,X_2,X_3,X_1^{next},X_2^{next},X_3^{next}) = C - (A + B)$;
 
 $f_2(X_1,X_2,X_3,X_1^{next},X_2^{next},X_3^{next}) = A^{next} - (B + C)$;
 
 $f_3(X_1,X_2,X_3,X_1^{next},X_2^{next},X_3^{next}) = B^{next} - (C + A^{next})$.

## 第2题 构建仅在行 $i=1$ 上应用RAP的多重集合相等性检查的约束

> 大神解答：https://github.com/wenjin1997/zkshanghai-workshop/blob/main/lecture6-homework.md

<img width="1046" alt="image" src="https://github.com/DessertHeart/zkshanghai-workshop/assets/93460127/384ba7c9-c68f-4f11-a900-d1ec0364d0fa">
