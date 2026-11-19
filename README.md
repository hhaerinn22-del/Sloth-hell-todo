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
- 가운데 원형 아레나와 3개 돌기둥이 **시계방향으로 실제로 돌아갑니다.**
  원본 일러스트를 원형으로 오려낸 회전 레이어(`assets/disc-*.webp`, 투명 PNG 폴백)를
  아래에 깔린 원본 위에 얹고, 아레나 중심을 축으로 `rotate()`만 매 프레임 갱신합니다.
  - 아레나 중심/반지름은 두 일러스트의 기둥 경계가 모이는 소실점을 측정해 잡았습니다
    (원본 941×1672 기준 중심 `(490, 777)`, 반지름 `380`).
    코드의 `ARENA_SRC` 값만 바꾸면 축과 크기를 조정할 수 있습니다.
  - 미완료가 많을수록 빨라지고(최대 약 15.6°/s), 하나만 남으면 천천히(약 4.5°/s),
    100% 완료하면 천국행 화면과 함께 부드럽게 멈춥니다.
  - `prefers-reduced-motion` 에서는 흔들림·파티클 없이 아주 느리게만 돕니다.
- 미완료가 많을수록 화면 흔들림·불티·먼지·땀방울·빨간 경고 펄스가 강해집니다.
- 모든 할 일을 체크하면 "오늘도 천국행! MISSION SUCCESS" 화면이 뜹니다.

## 회전 레이어 다시 만들기

원본 일러스트가 바뀌면 회전 레이어도 다시 구워야 합니다(원형 알파 마스크, 가장자리 12px 페더링).

```python
from PIL import Image
import numpy as np
CX, CY, R, F = 490, 777, 380, 12
def build(src, out_png, out_webp):
    im = Image.open(src).convert('RGBA'); w, h = im.size
    yy, xx = np.mgrid[0:h, 0:w]
    d = np.hypot(xx + .5 - CX, yy + .5 - CY)
    t = np.clip((R - d) / F, 0, 1); a = (t*t*(3-2*t)*255).round().astype(np.uint8)
    px = np.asarray(im).copy(); px[:, :, 3] = np.minimum(px[:, :, 3], a)
    Image.fromarray(px, 'RGBA').save(out_png, optimize=True)
    Image.fromarray(px, 'RGBA').save(out_webp, 'WEBP', lossless=True, quality=100, method=6)
```

## 수정 방법

GitHub Pages가 `gh-pages` 브랜치를 배포 소스로 사용합니다.
`index.html`(ver1)과 `v2/index.html`(ver2)을 고친 뒤 `gh-pages` 브랜치에 푸시하면 1~2분 안에 반영됩니다.
`main` 브랜치에는 원본 소스(`v2/index.html`, `assets/`)를 함께 둡니다.
