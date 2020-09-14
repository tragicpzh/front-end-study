## 1.简介

属于 Web Components（可重用的定制元素）。
shadow DOM 可以将一个隐藏的独立的 DOM 附加到一个元素上。

## 2.使用

let shadow=element.attachShadow({mode:'open'||'closed'})
open:可以通过 element.shadowRoot(shadowHost、shadowTree、shadowBoundary)获得 shadowDOM 节点
closed:外部不能获取 shadowRoot

## 3.写为 React 组件（函数式）

不涉及 state props redux（静态）

```javascript
import React, { useEffect, useRef } from "react";
import ReactDOM from "react-dom";
const ShadowView = ({ children }: any) => {
  const shadowRef = useRef();
  useEffect(() => {
    const elm = shadowRef.current;
    const shadowRoot = elm.attachShadow({ mode: "open" });
    ReactDOM.render(children, shadowRoot);
  }, []);
  return <div ref={shadowRef}></div>;
};
export default ShadowView;
```

### 涉及 state props redux（动态）

```javascript
import React, { useEffect, useRef, useState } from "react";
import ReactDOM from "react-dom";
const ShadowContent = ({ root, children }) => {
  return ReactDOM.createPortal(children, root);
};
const ShadowView = ({ children }: any) => {
  const shadowRef = useRef();
  const [root, setRoot] = useState(null);
  useEffect(() => {
    const elm = shadowRef.current;
    // @ts-ignore
    const shadowRoot = elm.attachShadow({ mode: "open" });
    setRoot(shadowRoot);
  }, []);
  return (
    <div ref={shadowRef}>
      {root && <ShadowContent root={root}>{children}</ShadowContent>}
    </div>
  );
};
export default ShadowView;
```

### npm 包

npm i shadow-view --save
https://github.com/Houfeng/shadow-view
