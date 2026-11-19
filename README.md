# 나태지옥 탈출 투두 (Sloth Hell To-do)

미루는 일이 쌓일수록 돌기둥이 빨라지는 잠금화면 콘셉트의 투두리스트 웹앱입니다.
할 일을 미루면 지옥 쪽으로, 해내면 천국 쪽으로 기울어집니다.

## 버전

| 버전 | 주소 | 내용 |
| --- | --- | --- |
| ver1 | https://hhaerinn22-del.github.io/Sloth-hell-todo/ | 캔버스로 그린 나태지옥 (초기 버전) |
| ver2 | https://hhaerinn22-del.github.io/Sloth-hell-todo/v2/ | 픽셀아트 2종 배경 + 장면 전환 + 파티클/경고 펄스 |

## 공통

- 단일 `index.html` (외부 의존성 없음)
- 할 일은 브라우저 `localStorage`에만 저장됩니다. 서버로 전송되지 않습니다.
- 아이폰 Safari에서 열고 "홈 화면에 추가"하면 앱처럼 전체 화면으로 실행됩니다.

## ver2 메모

- 배경 두 장(`assets/sloth-hell-pixel-push-120deg.png`, `assets/sloth-hell-pixel-run-120deg-left.png`)을
  오른쪽 위 버튼 또는 배경 탭으로 바꿔 볼 수 있습니다.
- 미완료가 많을수록 화면 흔들림·불티·먼지·땀방울·빨간 경고 펄스가 강해집니다.
- 모든 할 일을 체크하면 "오늘도 천국행! MISSION SUCCESS" 화면이 뜹니다.

## 수정 방법

GitHub Pages가 `gh-pages` 브랜치를 배포 소스로 사용합니다.
`index.html`(ver1)과 `v2/index.html`(ver2)을 고친 뒤 `gh-pages` 브랜치에 푸시하면 1~2분 안에 반영됩니다.
`main` 브랜치에는 원본 소스(`v2/index.html`, `assets/`)를 함께 둡니다.
