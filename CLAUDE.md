# 새 교육감에게 바란다 — 포춘 쿠키 게임

장애인의 날(4/20) 기념 이벤트 앱(4/20~24 진행). 포춘 쿠키를 깨서 교육감에게 바라는 메시지를 뽑고, Google Form으로 제출.

## 배포

- **GitHub Pages**: https://engccer.github.io/pledge-machine/
- **GitHub repo**: https://github.com/Engccer/pledge-machine
- 배포 방식: legacy mode (master 브랜치)

## 파일 구조

| 파일 | 용도 |
|------|------|
| `index.html` | 단일 HTML 앱 (CSS+JS 인라인) |
| `fortune_data.js` | 40개 포춘 메시지 + 17개 교육청 목록 |
| `sfx_data.js` | ElevenLabs 효과음 6종 base64 번들 (195KB) |
| `bg.png` | Gemini API 생성 배경 이미지 |
| `cookie.png` | Gemini API 생성 쿠키 이미지 (Pillow 투명 배경 처리) |
| `sfx/` | 원본 MP3 파일 (git 미추적) |

## Google Form

- **Form ID**: `1POKRNWdo4gsjuiAHQOQySDGEkRh8dPcEh0_lMZkxcLo`
- **응답자 URL**: `https://docs.google.com/forms/d/e/1FAIpQLScbltSg7xnYNCRK_5zmis44n2415T-T92osskdD5X2W0Zo8aw/viewform`
- **Pre-fill entry IDs**: 포춘 메시지 `entry.1952355422`, 나의 한마디 `entry.1029193054`
- **항목**: 포춘 메시지(필수), 나의 한마디(선택), 이름(필수), 소속 교육청(필수), 연락처(필수), 개인정보 동의(필수)
- **종료 화면 메시지**: 감사 인사 + 기프티콘 일괄 발송 안내(4월 24일 이후) + 슬로건. Forms API는 `confirmationMessage` 필드를 노출하지 않으므로 수정 시 브라우저 UI 필요.
- **응답자 접근 권한**: "Responder view: Anyone with the link" 필수. 기본값이 "Restricted"인 경우 Google 로그인이 강제되어 일반 이벤트 응답 수집이 불가하다. Forms API에도 노출되지 않으므로 확인·수정 시 상단 "Published" 버튼 → "Manage" → "Responder view"에서 설정. Editor view는 보안상 Restricted 유지.
- **관리**: `gws forms forms get --params '{"formId":"1POKRNWdo4gsjuiAHQOQySDGEkRh8dPcEh0_lMZkxcLo"}'`

## 블로그 게시물

- https://khudt.posthaven.com/jangaeinjugan-ibenteu-sae-gyoyuggamege-baranda-pocun-kuki

## 게임 플로우

1. 시작 화면 → "쿠키 뽑으러 가기"
2. 쿠키 7개 중 선택 → 중앙 이동 → 클릭하여 깨기
3. 쿠키 깨짐 + 종이 펼침 + 타자기 효과로 메시지 표시
4. "이 메시지로 참여하기" → 나의 한마디(선택) 추가
5. "나의 한마디 완성하기" → 클립보드 복사 + Google Form 이동

## 기술 스택

- 바닐라 HTML/CSS/JS (외부 라이브러리 없음, Google Fonts만)
- Web Audio API (SFX fallback)
- ElevenLabs MCP 효과음 (cookie_crack, paper_unfold, reveal_chime, ambient_shimmer, button_click, copy_success)
- Gemini API 이미지 생성
- CSS 애니메이션 (쿠키 떠다님, 깨짐, 종이 펼침, 타자기)

## 접근성

- 키보드 전체 조작 (Tab, Enter, Space, Escape)
- ARIA live region (`#sr-announce`) + announce() 패턴
- prefers-reduced-motion 지원
- 모바일 반응형 (600px breakpoint)
- 최소 터치 타겟 48px
- 뮤트 버튼 (SVG 아이콘, aria-label 동적 업데이트)

## 조합원 대상 이벤트

- 조합원 전용 (비조합원 참여 안내 없음)
- 참여자 전원 기프티콘 5천 원 (Form 연락처로 발송)
- 수집된 의견은 교육감 후보 면담 자료에 활용
