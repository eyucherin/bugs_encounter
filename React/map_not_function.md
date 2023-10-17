## Problem Statement:

- useEffect 통해 mock data를 fetch 하고 VideoSlice컴포넌트에 데이터 넘기기.
- data?.items는 분명 리스트 형태인데...map이 안됨.

### React Router caught the following error during render TypeError: search.map is not a function

<img src = "https://i.ibb.co/dQm9wQV/Screenshot-2023-10-17-at-4-32-54-PM.png">

## Code

```js
import React, { useEffect, useState } from "react";
import { useParams } from "react-router-dom";
import VideoSlice from "../components/VideoSlice";

export default function SearchVideo() {
  let { keyword } = useParams();
  let [search, setSearch] = useState("");

  useEffect(() => {
    let fetchData = async () => {
      let response = await fetch(
        `/data/${keyword ? "search" : "popular"}.json`
      );
      let data = await response.json();
      await setSearch(data?.items);
    };
    fetchData();
  }, [keyword]);

  return (
    <div>
      SearchVideo {keyword}
      {search.map((item) => {
        if (item?.id) {
          return (
            <VideoSlice
              key={item?.id?.videoId}
              thumbnails={item?.snippet?.thumbnails?.medium?.url}
            />
          );
        }
      })}
    </div>
  );
}
```

## Solution1

- isArray 함수를 통해 array가 넘겨지면 맵을 할 수 있게 설계.

```js
    {Array.isArray(search)?search.map((item)=>{
        if (item?.id) {
            return (
              <VideoSlice key={item?.id?.videoId}
                thumbnails={item?.snippet?.thumbnails?.medium?.url}
              />
            );
          }
    }):''}
```

## Solution2
 - data?.items는 분명 리스트 형태인데....
 - `let { keyword } = useParams();` 여기에 문제가 있었다. 
 - `useParams()` --> `useParams([])`.
 - 처음 랜더 될때 리스트를 넘기지 않아서, 애러가 생김..



