# claude_coder

픽셀 아트 버그-디펜스 로그라이트. 바닥의 **Clawd**(테라코타 게)가 5개 레인에서 떨어지는 버그를 막으며 LOC를 쌓는다. 한 판에 무기 1개, 공격은 자동. 죽거나 종료하면 ★로 무기·스탯·테마를 영구 강화하고 다시 출전한다. **5000 LOC = 배포 성공(승리)**.

바닐라 JS + Canvas 단일 `index.html` (픽셀 폰트 Galmuri만 jsDelivr CDN). 형제 스킨: [dino_coder](https://github.com/AItinkerer0/dino_coder), [duck_coder](https://github.com/AItinkerer0/duck_coder).

## Status

- **Last reviewed:** 2026-07-17 (base `79a03c3`)
- **Maturity:** 플레이 가능한 단일 HTML 프로토타입. 이 README 작성 시 게임을 실행·플레이하지는 않았다.
- **License:** 저장소에 라이선스 파일 없음 — 재사용 조건은 현재 명시되지 않음.

## 공유 코어 (dino / duck와 동일 계열)

소스상 공통 골격:

| 항목 | 내용 |
|---|---|
| 승리 | `loc >= 5000` → “5000 LOC 완성 — 배포 성공!” |
| 패배 UI | HP 고갈 시 “CONTEXT WINDOW EXCEEDED” |
| 무기 | 17종, 한 판에 1개 장착 (기본: 토큰 스트림) |
| 영구 스탯 | 추론력 · 출력속도 · 컨텍스트 (★ 상점) |
| 테마 | 자연 테마 5종 (숲/바다/사막/설원/화산, 상점 구매·장착) |
| 버그 | 7종 (splitter 분열체 runt 포함) |
| 레인 | 5 |
| 조작 | ←→ 또는 A/D 이동, 공격 자동 · `M` 음소거 · `Esc` 런 종료 · `1`/`2`/`3` 배속 · 터치 이동 지원 |
| 저장 | `localStorage` (키는 에디션별로 분리) |
| 네트워크 | 런타임 서버 없음. 페이지 로드 시 Galmuri 폰트 CDN 요청 가능 |

## 이 저장소만의 차이

- 주인공 스프라이트: `SPR.clawd` (Claude 마스코트 계열)
- 세이브 키: `claude_coder_v1`
- UI 액센트 컬러: 코랄 (`--coral:#cc7c5e`)
- 루트에 참조 이미지 `clawd_ref.png` (게임 HTML이 필수로 로드하지는 않음)

## 조작·기대 동작

1. **입력:** 키보드(레인 이동) 또는 캔버스 터치/드래그.
2. **실행:** 아래 Quick start 중 하나.
3. **기대 출력:** 메뉴(무기/스탯/테마 상점) → 출전 → 상단 LOC·HP HUD → 5000 LOC 승리 또는 컨텍스트 초과 패배 오버레이 → ★ 정산 후 메뉴 복귀.

## Quick start

저장소 루트에서 (이 리프레시 중에는 **실행하지 않음** — 소스·트리 기준 안내):

```sh
# 옵션 A: 로컬 정적 서버 (python3 가정)
python3 -m http.server 8080
# 브라우저에서 http://localhost:8080/ 열기

# 옵션 B: index.html을 브라우저로 직접 열기
open index.html   # macOS; 다른 OS는 파일 탐색기/브라우저로 동일 파일 오픈
```

게시된 GitHub Pages (소스 `main` 루트, API상 `built`):
https://aitinkerer0.github.io/claude_coder/

## 파일 맵

```
index.html      게임 전부 (HTML/CSS/JS + Canvas)
clawd_ref.png   Clawd 참조 이미지
README.md       이 문서
```

## 데이터 · 네트워크 · 안전

- **저장:** 브라우저 `localStorage` 키 `claude_coder_v1` (★, 최고 LOC, 스탯 레벨, 보유 무기/테마, 음소거·배속 등). 서버 업로드 없음.
- **네트워크:** 외부 API·계정 연동 없음. 폰트 CSS만 CDN(`cdn.jsdelivr.net/npm/galmuri@latest/...`). 오프라인만 쓰려면 폰트를 로컬로 두는 별도 조치가 필요하다(미구현).
- **오디오:** Web Audio API 비프/BGM (음소거 가능).
- **비밀·자격증명:** 없음.

## License

라이선스 파일 없음.
