# 🛒 shopping-listapp

바닐라 HTML/CSS/JavaScript로 만든 간단한 쇼핑 리스트 웹 앱입니다. 데이터는 **Supabase** 데이터베이스에 저장됩니다.

## 기능

- 항목 추가 / 체크 / 삭제
- 체크된 항목 일괄 비우기
- Supabase(PostgreSQL)에 자동 저장 — 다른 기기·브라우저에서도 같은 목록이 보입니다
- 다크 모드 자동 대응 (`prefers-color-scheme`)
- 모바일 화면 대응

## 사용법

`index.html` 파일을 브라우저에서 열면 됩니다. 별도의 빌드가 필요 없습니다.

## 데이터베이스 스키마

`shopping_items` 테이블 (public 스키마):

| 컬럼 | 타입 | 설명 |
| --- | --- | --- |
| `id` | `uuid` | 기본키, `gen_random_uuid()` 자동 생성 |
| `text` | `text` | 항목 이름 (not null) |
| `checked` | `boolean` | 체크 여부, 기본값 `false` |
| `created_at` | `timestamptz` | 생성 시각, 기본값 `now()` |

RLS(Row Level Security)가 켜져 있으며, 로그인 없이 쓰는 학습용 앱이라 `anon` 역할에 조회/추가/수정/삭제를 모두 허용해 두었습니다. **누구나 목록을 읽고 지울 수 있으므로 민감한 정보는 넣지 마세요.** 실제 서비스로 만들 때는 Supabase Auth를 붙이고 `user_id` 기준으로 정책을 좁혀야 합니다.

## 설정

`index.html` 상단 스크립트의 값을 자신의 Supabase 프로젝트에 맞게 바꾸면 됩니다.

```js
const SUPABASE_URL = "https://<프로젝트-ref>.supabase.co";
const SUPABASE_PUBLISHABLE_KEY = "sb_publishable_...";
```

publishable(anon) 키는 브라우저에 노출되도록 설계된 공개 키라서 저장소에 커밋해도 괜찮습니다. `service_role` 키는 절대 커밋하면 안 됩니다.

## 라이브 데모 (GitHub Pages)

저장소 Settings → Pages 에서 배포하면 다음 주소로 접속할 수 있습니다:

```
https://ksh860811-rgb.github.io/shopping-listapp/
```
