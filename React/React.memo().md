# React.memo()

## React.memo()란?

- React는 먼저 컴포넌트를 렌더링한 뒤, 이전 렌더된 결과와 비교하여 DOM 업데이트를 결정한다. 만약 렌더 결과가 이전과 다르다면, React는 DOM을 업데이트한다.
- 다만, 부모 컴포넌트 A와 자식 컴포넌트 B가 있을 때 A 컴포넌트 값만 바뀌어도 B 컴포넌트가 재렌더링되는 이슈가 있다. 즉, 성능에 이슈가 생기는 것인데 React.memo를 사용하면 이를 해결할 수 있다.

```tsx
export function Movie({ title, releaseDate }) {
  return (
    <div>
      <div>Movie title: {title}</div>
      <div>Release date: {releaseDate}</div>
    </div>
  );
}

export const MemoizedMovie = React.memo(Movie);
```

- React.memo(Movie)는 새로 메모이징된 컴포넌트인 MemoizedMovie를 반환한다.
- MemoizedMovie의 렌더링 결과는 메모이징 되어있다. 만약 title이나 releaseData 같은 props가 변경되지 않는다면 다음 렌더링 때 메모이징 된 내용을 그대로 사용하게 된다.

```tsx
// 첫 렌더이다. React는 MemoizedMovie 함수를 호출한다.
<MemoizedMovie
  movieTitle="Heat"
  releaseDate="December 15, 1995"
/>

// 다시 렌더링 할 때 React는 MemoizedMovie 함수를 호출하지 않는다.
// 리렌더링을 막는다.
<MemoizedMovie
  movieTitle="Heat"
  releaseDate="December 15, 1995"
/>
```

- 메모이징 한 결과를 재사용 함으로써, React에서 리렌더링을 할 때 가상 DOM에서 달라진 부분을 확인하지 않아 성능상의 이점을 누릴 수 있다.

## 언제 React.memo()를 써야할까?

### 같은 props로 렌더링이 자주 일어나는 컴포넌트

- React.memo()를 사용하기 가장 좋은 케이스는 함수형 컴포넌트가 같은 props로 자주 렌더링 될거라 예상될 때이다.
- 일반적으로 부모 컴포넌트에 의해 하위 컴포넌트 같은 props로 리렌더링 될 때가 있다.

```tsx
function MovieViewsRealtime({ title, releaseDate, views }) {
  return (
    <div>
      <Movie title={title} releaseDate={releaseDate} />
      Movie views: {views}
    </div>
  );
}
```

- 이 어플리케이션은 주기적으로 서버에서 데이터를 폴링해서 MovieViewsRealTime 컴포넌트의 views를 업데이트한다.

```tsx
// Initial render
<MovieViewsRealtime
  views={0}
  title="Forrest Gump"
  releaseDate="June 23, 1994"
/>

// After 1 second, views is 10
<MovieViewsRealtime
  views={10}
  title="Forrest Gump"
  releaseDate="June 23, 1994"
/>

// After 2 seconds, views is 25
<MovieViewsRealtime
  views={25}
  title="Forrest Gump"
  releaseDate="June 23, 1994"
/>

// etc
```

- 이때 Movie 컴포넌트에 메모이제이션을 적용해보자.

```tsx
function MovieViewsRealtime({ title, releaseDate, views }) {
  return (
    <div>
      <MemoizedMovie title={title} releaseDate={releaseDate} />
      Movie views: {views}
    </div>
  );
}
```

- title 혹은 releaseDate props가 같다면, React는 MemoizedMovie를 리렌더링 하지 않을 것이다. 이렇게 MovieViewsRealtime 컴포넌트의 성능을 향상할 수 있다.
- 컴포넌트가 같은 props로 자주 렌더링되거나, 무겁고 비용이 큰 연산이 있는 경우, React.memo()로 컴포넌트를 래핑할 필요가 있다.

## 언제 React.memo()를 사용하지 말아야 할까?

- 쓸모없는 prop 비교
  - 이전 props와 다음 props의 동등 비교를 위해 비교 함수를 수행한다.
  - 비교 함수는 거의 항상 false를 반환하므로, React는 이전 렌더링 내용과 다음 렌더링 내요을 비교할 것이다.
  - 따라서 불필요한 작업이 진행되므로 성능에 오히려 좋지 않다.

## React.memo()와 콜백 함수

- 함수 객체는 '일반' 객체와 동일한 비교 원칙을 따른다.
- 함수 객체는 오직 자신에게만 동일하다.

```tsx
function sumFactory() {
  return (a, b) => a + b;
}

const sum1 = sumFactory();
const sum2 = sumFactory();

console.log(sum1 === sum2); // => false
console.log(sum1 === sum1); // => true
console.log(sum2 === sum2); // => true
```

- 함수 sum1과 sum2는 팩토리에 의해 생성된 함수다.
- 그러나 sum1과 sum2는 다른 함수 객체이다.
- 부모 컴포넌트가 자식 컴포넌트의 콜백 함수를 정의한다면, 새 함수가 암시적으로 생성될 수 있다. 이것이 어떻게 메모이제이션을 막는지 보고 수정해보자.

```tsx
function Logout({ username, onLogout }) {
  return <div onClick={onLogout}>Logout {username}</div>;
}

const MemoizedLogout = React.memo(Logout);

function MyApp({ store, cookies }) {
  return (
    <div className="main">
      <header>
        <MemoizedLogout
          username={store.username}
          onLogout={() => cookies.clear()}
        />
      </header>
      {store.content}
    </div>
  );
}
```

- 동일한 username 값이 전달되더라도, MemoizedLogout은 새로운 onLogout 콜백 때문에 리렌더링을 하게 된다. 즉, 메모이제이션이 중단되는 문제가 발생한다.
- 해당 문제를 해결하려면 onLogout prop의 값을 매번 동일한 콜백 인스턴스로 설정해야만 한다. useCallback()을 이용해서 콜백 인스턴스를 보존시켜보자.

```tsx
const MemoizedLogout = React.memo(Logout);

function MyApp({ store, cookies }) {
  const onLogout = useCallback(() => {
    cookies.clear();
  }, []);
  return (
    <div className="main">
      <header>
        <MemoizedLogout username={store.username} onLogout={onLogout} />
      </header>
      {store.content}
    </div>
  );
}
```

- useCallback은 메모이제이션된 콜백함수를 저장한다. 따라서 항상 같은 함수 인스턴스를 반환하기 때문에 MemoizedLogout의 메모이제이션이 정상적으로 동작하도록 수정될 수 있다.
