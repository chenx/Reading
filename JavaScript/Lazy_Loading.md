# Lazy Loading

## <a href="https://www.xiaohongshu.com/explore/68d63ceb0000000013005f69?app_platform=ios&app_version=8.99.1&share_from_user_hidden=true&xsec_source=app_share&type=normal&xsec_token=CBtSUTi7L4R714z4Yz496ebjhk6U7AAUt4s1niWEb5IFA=&author_share=1&xhsshare=WeixinSession&shareRedId=N0o7QTc5Sjk2NzUyOTgwNjY0OTc2SUhB&apptime=1758895768&share_id=59e17a585f6d41d599258ac32d743604&code=081MYHkl2SDZmg4nIynl2vRvdb2MYHkL&state=wx_oauth">xiaohongshu: lazy loading</a>

Types:
- component lazy loading
- router
- image
- data

## React lazy loading

https://medium.com/@ignatovich.dm/optimizing-react-apps-with-code-splitting-and-lazy-loading-e8c8791006e3

Example: lazy loading a component

```
import React, { Suspense } from "react";

const LazyComponent = React.lazy(() => import("./LazyComponent"));

function App() {
  return (
    <div>
      <h1>Welcome to My App</h1>
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}

export default App;
```
