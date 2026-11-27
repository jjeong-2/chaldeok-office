# Chaldeok Office

찰떡 본부 대시보드 — 단일 HTML 웹앱.

- 공개 주소: https://jjeong-2.github.io/chaldeok-office/
- 서빙 브랜치: `gh-pages` (루트) — GitHub Pages는 이 브랜치에서 배포됩니다.
- 파일을 고칠 때는 `main`과 `gh-pages` 두 브랜치에 같은 내용을 올려야 사이트에 반영됩니다.

## 실시간 상태 (`status.json`)

페이지는 `status.json?t=...` 을 **15초마다** 읽어 6명 요원의 위치·말풍선을 갱신합니다.

```json
{
  "mode": "working",                  // idle | meeting | working
  "task": "아침 경제 브리핑 1편 팩트체크 & 대표 이미지 생성 중",
  "agenda": "오늘 발행 3건 확정 회의",   // meeting 모드에서만 사용
  "updated_at": "2026-11-28T06:40:00+09:00",
  "expires_at": "2026-11-28T07:05:00+09:00",   // 지나면 자동으로 시간대별 기본 근무로 복귀
  "characters": {
    "chaldeok": { "room": "command", "bubble": "발행 3건 최종 점검 중!", "detail": "경제 브리핑·낮 유입글 발행 완료", "active": true }
  }
}
```

- 캐릭터 키 6명: `chaldeok`(본부장) · `muse`(팀장) · `bear`(차장) · `cat`(과장) · `fox`(대리) · `chick`(인턴)
- `mode=meeting` 이면 6명이 대회의실 원탁 의자로 모여 말풍선을 돌아가며 주고받고,
  `mode=working` 이면 각자 자리(지휘실·대회의실·작업실·라운지)에 앉아 `bubble`/`detail` 을 보여줍니다.
- **이 파일은 공개됩니다.** 실명·주소·직장·계정 같은 사적 정보는 절대 넣지 말고 업무 내용만 구체적으로 적으세요.
- 발행은 `set_status.py` 로 합니다(로컬 파일 갱신 + `main`·`gh-pages` 에 `status.json` 만 푸시, 보통 1~2초).
  GitHub Pages 빌드 때문에 라이브 반영까지는 20~30초 더 걸릴 수 있습니다.
