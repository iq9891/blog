# 不能将类型“string”分配给类型“"default" | "small" | "large"”

## 报错

`TS2322: Type 'string' is not assignable to type '"default" | "small" | "large"'`

![image](https://user-images.githubusercontent.com/5716990/79195634-2f607700-7e61-11ea-9cae-e22b4f555eae.png)

## 依赖

- TypeScript 3.8.3
- andt 3.26.15

## 解决

因为属性中有没有用的属性混合在一起，整理一下 paginationConfig 属性即可。