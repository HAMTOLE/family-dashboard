# 오늘의 체크리스트 (daily-todo)

은비 님의 개인 할 일 체크리스트 — 휴대폰에서 여는 웹앱입니다.
노션 데이터베이스 `✅ 은비 오늘 할 일` 과 Cloudflare Worker(`family-notion`)를 거쳐 연결됩니다.

- 앱: https://hamtole.github.io/daily-todo/
- 같은 주소 계열의 `세줄일기`(`/sejul-diary/`)와 **비밀키를 함께 씁니다.**
  브라우저 `localStorage` 의 `sejul.diaryKey` 를 그대로 읽고, 없으면 잠금 화면에서 한 번만 입력하면 됩니다.

## 이 저장소에 들어 있지 않은 것

공개 저장소이므로 다음은 코드에 넣지 않습니다.

- 노션 데이터베이스 ID, 통합 토큰
- Worker 비밀키 (`X-Diary-Key` 값)
- 실제 할 일 내용 (앱이 실행 중에 Worker에서 받아 옵니다)

앱은 Worker 주소(`https://family-notion.mynamebiya.workers.dev`)의 `/todos` 만 호출합니다.

## API (Worker `family-notion`)

| 요청 | 하는 일 |
| --- | --- |
| `GET /todos` | 미완료 전부 + 최근 7일 안에 완료한 항목 (기한 순) |
| `POST /todos` | 새 할 일 추가 `{title, category, due, source}` |
| `PATCH /todos/:id` | 완료 토글 `{done}` · 미루기 `{postpone:true}` · `{due}` · `{title}` · `{category}` |
| `DELETE /todos/:id` | 그 항목 보관(아카이브) |

모두 `X-Diary-Key` 헤더가 필요합니다.

## 아이폰에 앱처럼 붙이기

Safari 로 주소를 연 뒤 **공유 → 홈 화면에 추가**. 아이콘과 전체 화면으로 열립니다.
