#  Next.js Server Action

> 매일메일 FE 2025년 4월 2주차 목요일 질문

### Server Action
- 서버에서 실행되며 브라우저에서 호출할 수 있는 비동기 함수
- 서버 로직을 직접 호출함으로써 클라이언트와 서버 간의 상호작용을 간소화
- 백엔드 서버와 API 통신을 하는 대신 Next 서버에서 데이터베이스에 직접 접근하는 식으로 활용 가능
- 애플리케이션에서 폼 제출 및 데이터 변조를 처리하기 위함

### 'use server'
- async 함수 안 또는 컴포넌트 상단에 `use server` 정의
- 함수가 서버에서만 실행되도록 지정
- 함수안에 있는 코드는 유저에게 노출되는 코드가 아니라 서버 코드가 됨

```js
export default function Page() {
  // Server Action
  async function handleSubmit(formData) {
    'use server'
    // 데이터 작업 또는 DB 처리
    const db = (await connectDB).db('forum')
    await db.collection('post_test').insertOne({title : formData.get('title')})
    revalidatePath('/write2') // "/write2"에 있는 캐시를 삭제하고 다시 생성 해줌 (새로고침)
  }
 
  return (
    // 컴포넌트에서 사용
    <form action={handleSubmit}>
        <textarea name="content" required />
        <button type="submit">Submit</button>
    </form>
  )
}
```

### 장점
- 클라이언트와 서버 간 상호작용을 간소화
    - 데이터베이스를 다루는 작업도 컴포넌트 안에서 모든 걸 해결할 수 있기 때문에 서버 API를 따로 만들지 않아도 서버 기능을 컴포넌트 안에서 개발 가능
    - 개발 생산성 향상 및 네트워크 통신을 줄여 성능 개선 가능
- 외부에 노출되면 안 되는 정보나 로직을 숨기는 데 활용
    - 민감한 정보를 노출하지 않아 보안에 도움이 됨
    - 번들 크기를 줄이는데도 기여할 수 있음
- JS가 로드되기 이전의 시점에도 서버와 상호작용
    - form의 action 속성을 이용하여 폼 데이터를 서버에 전송
    - ㅓS가 로드되지 않거나 비활성화되어도 서버와 통신이 가능