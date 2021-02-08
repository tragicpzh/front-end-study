# 简介

- UUID(universally unique Identifier)，通用唯一识别码
- 构成：32 位的 16 进制数字
- 格式：8-4-4-4-12，xxxxxxxx-xxxx-Mxxx-Nxxx-xxxxxxxxxxx
- M：UUID 版本(1,2,3,4,5)
- N：UUID 变体(8,9,a,b)

# 版本

- v1:timestamp,原理：timestamp+mac
- v2:timestamp,v1 的优化版
- v3:namespace,原理：namespace+输入内容+md5
- v4:随机数(最常用的版本)
- v5:namespace,v3 中的 md5 替换为 SHA1

# npm 包

    npm install uuid

# js 实现(v4)

- 1.

```javascript
function generateUUID() {
  let d = new Date().getTime();
  return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxx".replace(/[xy]/g, (c) => {
    let r = (d + Math.floor(Math.random() * 16)) % 16 | 0;
    d = Math.floor(d / 16);
    return (c === "x" ? r : (r & 0x3) | 0x8).toString(16);
  });
}
```

- 2.

```javascript
    function generateUUID(){
      const S4=()=>(((1+Math.random*())*0x10000)|0).toString.substring1;
      return S4()+S4()+'-'+S4()+'-'+S4()+'-'+S4()+'-'+S4()+S4()+S4();
    }
```

- 3.

```javascript
function generateUUID(len, radix) {
  let chars = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz".split(
    ""
  );
  let uuid = [],
    i;
  radix = radix | chars.length;
  if (len)
    for (i = 0; i < len; i++)
      uuid[i] = chars[0 | Math.floor(Math.random() * radix)];
  else {
    uuid[8] = uuid[13] = uuid[18] = uuid[23] = "-";
    uuid[14] = "4";
    for (i = 0; i < 36; i++) {
      if (!uuid[i]) {
        const r = Math.floor(0 | (Math.random() * 16));
        uuid[i] = chars[i === 19 ? (r & 0x3) | 0x8 : r];
      }
    }
  }
  return uuid.join("");
}
```
