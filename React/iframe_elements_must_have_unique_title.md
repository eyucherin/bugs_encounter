## Problem Statement:
- iframe 사용해서 비디오 실행하고싶은데 비디오가 not available로 떳다. 
<img src="https://i.ibb.co/LRcqnyF/Screenshot-2023-10-20-at-8-33-33-PM.png" alt="Screenshot-2023-10-20-at-8-33-33-PM">

### Warning: elements must have a unique title property  jsx-a11y/iframe-has-title

## Code 
```js

<iframe
    id="player"
    type="text/html"
    width="100%"
    height="500"
    src={`http://www.youtube.com/embed/${videoInfo.id}`}
    frameBorder="0"
></iframe>

```

## Solution 
 - Title 을 꼭 넣어줘야한다.
```js
<iframe
    id="player"
    type="text/html"
    width="100%"
    height="500"
    title = {videoInfo.title}
    src={`http://www.youtube.com/embed/${videoInfo.id}`}
    frameBorder="0"
></iframe>
```