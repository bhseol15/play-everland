# 🎢 에버랜드 미니게임 제작 가이드 (참여자용 1페이지)

## 폴더 구조
```
everland/
├─ index.html          ← 지도(허브). 건드리지 않아도 됨
├─ games/              ← ★ 여기에 자기 파일 하나만 추가
│   ├─ _template.html  ← 복사해서 시작
│   ├─ texpress.html
│   ├─ bumper.html
│   └─ ...
└─ GAME-GUIDE.md       ← 이 문서
```

## 내 게임 만들기 — 3단계

### 1. 템플릿 복사
`games/_template.html` 을 복사해서 **담당 기구 id 로 이름을 바꿉니다.**

| 기구 | 파일명 | | 기구 | 파일명 |
|---|---|---|---|---|
| T익스프레스 | `texpress.html` | | 회전목마 | `carousel.html` |
| 사파리 월드 | `safari.html` | | 관람차 | `ferris.html` |
| 판다월드 | `panda.html` | | 범퍼카 | `bumper.html` |
| 아마존 익스프레스 | `amazon.html` | | 간식 코너 | `snack.html` |
| 로스트밸리 | `lostvalley.html` | | 굿즈 샵 | `shop.html` |
| 허리케인 | `hurricane.html` | | 퍼레이드 | `parade.html` |

파일명만 맞으면 허브가 **자동으로 연결**합니다. (허브 코드 수정 불필요)

### 2. 게임 작성
템플릿의 `↓↓↓ 여기부터 자유롭게 ↓↓↓` 아래를 전부 지우고 내 게임을 작성합니다.
HTML/CSS/JS 는 모두 **이 파일 하나 안에** 넣습니다.

### 3. 게임이 끝나면 이 한 줄
```js
EVERLAND.end(점수);            // 예: EVERLAND.end(1250);
EVERLAND.end(점수, '랭크');    // 예: EVERLAND.end(1250, 'S');  ← 랭크는 선택
```
템플릿 위쪽의 `EVERLAND` 블록은 지우지 마세요. 이 한 줄이 점수를 지도로 보내고,
지도는 결과 화면 · 최고 점수 저장 · "지도로 돌아가기" 를 알아서 처리합니다.

## 지켜주세요
- ✅ 파일 하나에 전부 (외부 CDN·라이브러리 링크 ❌, 인터넷 없이도 돌아가야 함)
- ✅ 화면 꽉 채우기 (`100vw × 100vh`), 세로 모바일에서도 깨지지 않게
- ✅ 마우스 **그리고** 터치 둘 다 동작 (`mousedown` + `touchstart`, 또는 `pointerdown`)
- ✅ 시작 화면 포함 (파일이 열리면 바로 게임이 시작되지 않고 "시작" 버튼이 먼저)
- ✅ 밝고 귀여운 한글 UI, 플랫/벡터 스타일 (SVG·Canvas·CSS 로 그리기)
- ❌ `alert()` / `confirm()` 사용 금지 (iframe 안에서 어색함)
- ❌ `localStorage` 키는 `everland.` 로 시작하지 않기 (허브가 사용 중)
- 이미지 파일이 꼭 필요하면 `games/<id>/` 하위 폴더에 넣고 상대경로로 참조

## 테스트 방법
- **혼자 테스트**: 내 html 파일을 브라우저로 그냥 열기 → 끝나면 자체 결과 화면이 뜸
- **허브에서 테스트**: `everland/` 폴더에서
  ```bash
  python -m http.server 8000
  ```
  → `http://localhost:8000` 열고 지도에서 내 기구 클릭 → 게임 시작
  (파일 더블클릭으로 index.html 을 열면 브라우저에 따라 iframe 이 막힐 수 있어요)

## 허브가 보내주는 것 (선택 사항)
게임이 로드되면 허브가 아래 메시지를 보냅니다. 필요하면 활용하세요.
```js
window.addEventListener('message', e => {
  if (e.data.type === 'EVERLAND_START') {
    e.data.ride   // 'texpress'
    e.data.name   // 'T익스프레스'
  }
});
```

## 제출
완성한 `games/<id>.html` 파일 하나만 공유 폴더(또는 GitHub `games/`)에 올리면 끝!
