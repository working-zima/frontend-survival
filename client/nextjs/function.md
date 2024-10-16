# Function

## usePathName

`usePathname`은 현재 URL의 경로명을 읽을 수 있게 해주는 클라이언트 컴포넌트 훅입니다.

```tsx
// app/example-client-component.tsx
'use client'

import { usePathname } from 'next/navigation'

export default function ExampleClientComponent() {
  const pathname = usePathname()
  return <p>Current pathname: {pathname}</p>
}
```

```js
// app/example-client-component.js
'use client'

import { usePathname } from 'next/navigation'

export default function ExampleClientComponent() {
  const pathname = usePathname()
  return <p>Current pathname: {pathname}</p>
}
```

`usePathname`은 의도적으로 클라이언트 컴포넌트에서 사용해야 합니다.\
클라이언트 컴포넌트는 서버 컴포넌트 아키텍처의 중요한 부분으로, 성능 저하 요소가 아닙니다.

예를 들어, `usePathname`을 사용하는 클라이언트 컴포넌트는 초기 페이지 로드 시 HTML로 렌더링됩니다.\
새로운 경로로 이동할 때, 이 컴포넌트는 다시 가져올 필요가 없습니다.\
대신, 컴포넌트는 한 번 다운로드(클라이언트 자바스크립트 번들)되고 현재 상태에 따라 다시 렌더링됩니다.

### 알아두면 좋은 점

- 서버 컴포넌트에서 현재 URL을 읽는 것은 지원되지 않습니다.\
이는 페이지 탐색 간 레이아웃 상태가 유지되도록 지원하기 위한 의도적인 설계입니다.

- 호환 모드:
  - 대체 경로가 렌더링되거나 Next.js에 의해 자동으로 정적으로 최적화된 pages 디렉토리 페이지일 때 usePathname이 null을 반환할 수 있습니다.
  - 프로젝트에 app 및 pages 디렉토리가 모두 있는 경우 Next.js가 자동으로 타입을 업데이트합니다.

## Parameters

```ts
const pathname = usePathname()
```

`usePathname`은 파라미터를 받지 않습니다.

## Returns

`usePathname`은 현재 URL의 경로명을 나타내는 문자열을 반환합니다.\

예를 들어

URL | 반환 값
:-: | :-:
`/` | `'/'`
`/dashboard` | `'/dashboard'`
`/dashboard?v=2` | `'/dashboard'`
`/blog/hello-world` | `'/blog/hello-world'`

## Examples

경로 변경에 반응하여 작업 수행

```tsx
// app/example-client-component.tsx
'use client'

import { usePathname, useSearchParams } from 'next/navigation'

function ExampleClientComponent() {
  const pathname = usePathname()
  const searchParams = useSearchParams()
  useEffect(() => {
    // 여기에서 작업 수행...
  }, [pathname, searchParams])
}
```

```js
app/example-client-component.js
'use client'

import { usePathname, useSearchParams } from 'next/navigation'

function ExampleClientComponent() {
  const pathname = usePathname()
  const searchParams = useSearchParams()
  useEffect(() => {
    // 여기에서 작업 수행...
  }, [pathname, searchParams])
}
```
