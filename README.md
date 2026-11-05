# gabrielmath.kr

**Gabriel Math · 수학과 함께하는 새로운 배움의 여정**

개념을 탐구하고 생각을 확장하는 수학 교육용 웹앱 사이트입니다. 값을 바꾸고 그래프를 움직이며 규칙을 직접 찾는 웹앱을 모았습니다. GitHub Pages로 배포합니다.

## 주소와 폴더

| 주소 | 폴더 | 내용 |
|---|---|---|
| [gabrielmath.kr](https://gabrielmath.kr) | `/` | 메인 페이지 (표지와 수학 웹앱 목록) |
| [gabrielmath.kr/math1](https://gabrielmath.kr/math1/) | `math1/` | 공통수학 개념 탐구 실험실 (공통수학1·2, 19차시) |
| [gabrielmath.kr/algebra](https://gabrielmath.kr/algebra/) | `algebra/` | 대수 개념 탐구 실험실 (대수, 21차시) |
| [gabrielmath.kr/calculus1](https://gabrielmath.kr/calculus1/) | `calculus1/` | 미적분Ⅰ 개념 탐구 실험실 (미적분Ⅰ, 21차시) |
| [gabrielmath.kr/calculus2](https://gabrielmath.kr/calculus2/) | `calculus2/` | 미적분Ⅱ 개념 탐구 실험실 (미적분Ⅱ, 27차시) |
| [gabrielmath.kr/prob-stats](https://gabrielmath.kr/prob-stats/) | `prob-stats/` | 확률과 통계 개념 탐구 실험실 (확률과 통계, 20차시, 실험 16차시) |

## 폴더 구조

```
index.html        메인 페이지 (로고와 그림이 파일 안에 들어 있음)
404.html          없는 주소로 들어왔을 때 보이는 페이지
CNAME             도메인 연결 (gabrielmath.kr) — 지우지 마세요
assets/style.css  404 페이지에서 쓰는 공통 스타일
math1/            공통수학 개념 탐구 실험실 (index.html, README.md, PRIVACY.md 등)
algebra/          대수 개념 탐구 실험실 (index.html, README.md, PRIVACY.md 등)
calculus1/        미적분Ⅰ 개념 탐구 실험실 (index.html, README.md, PRIVACY.md 등)
calculus2/        미적분Ⅱ 개념 탐구 실험실 (index.html, README.md, PRIVACY.md 등)
prob-stats/       확률과 통계 개념 탐구 실험실 (index.html, README.md, PRIVACY.md 등)
README.md         이 문서
```

## 메인 페이지 (`index.html`)

- **머리글:** 원형 로고, 메뉴(홈, 수학 웹앱), 웹앱 검색창
- **표지:** ‘수학, 더 깊이, 더 즐겁게!’, Gabriel Math, Gabriel 쌤과 G-Man 그림, ‘지금 바로 시작하기’ 단추
- **수학 웹앱:** 웹앱마다 배너 하나. 배너를 누르면 해당 폴더의 웹앱으로 이동. 배너 그림은 ‘Gabriel 쌤과 Gabriel Math’ 그림에서 잘라 낸 장면(미적분Ⅱ는 ‘AI와 함께 탐구하기’, 확률과 통계는 ‘학생과 함께 성장’)
- **검색:** 검색창에 낱말(예: 로그, 행렬, 미분, 확률, 신뢰구간)을 넣으면 맞는 배너만 남음
- 로고와 그림은 `index.html` 안에 이미지 데이터로 들어 있어 따로 올릴 이미지 파일이 없습니다. 외부에서는 Google Fonts 글꼴만 불러옵니다.

## 새 웹앱 추가하기

1. **웹앱 폴더 만들기:** 영문 소문자로 폴더를 만들고(예: `geometry`), 그 안에 웹앱 파일을 `index.html` 이름으로 저장합니다.
2. **메인 페이지에 배너 추가하기:** `index.html`에서 `<a class="app` 로 시작하는 배너 한 덩어리를 복사해 바로 아래에 붙여 넣고, 다음을 바꿉니다.
   - `href="/geometry/"` : 웹앱 주소
   - `data-k="..."` : 검색에 쓰일 낱말들 (단원명, 개념 등)
   - `chip`, `h3`, `p`, `meta` 안의 글자 : 과목, 제목, 소개, 차시 수
   - 배너 색: `class="app m1"`은 파란색, `class="app alg"`는 보라색, `class="app cal"`은 청록색, `class="app c2"`는 장밋빛 빨강, `class="app ps"`는 호박색
3. **이 문서 고치기:** 위 ‘주소와 폴더’ 표에 한 줄을 추가합니다.
4. **올리고 확인하기:** GitHub에 업로드(커밋)하고 1~2분 뒤 `gabrielmath.kr/geometry/`와 메인 페이지에서 확인합니다.

## 올리는 방법 (GitHub 웹)

- **파일 바꾸기:** 저장소에서 **Add file → Upload files**를 누르고 파일을 끌어다 놓은 뒤 **Commit changes**를 누릅니다. 같은 이름의 파일은 덮어씁니다.
- **폴더 올리기:** 폴더 **자체**를 끌어다 놓습니다. 업로드 목록에 `algebra/index.html`처럼 폴더 이름으로 시작하는 경로가 보여야 합니다.
- **배포 확인:** 저장소의 **Actions** 탭에서 초록색 체크가 되면 배포가 끝난 것입니다. 예전 화면이 보이면 Ctrl+Shift+R(맥은 Cmd+Shift+R)로 새로 고침합니다.
- **올리면 안 되는 것:** zip 파일은 그대로 올리지 말고, 압축을 푼 뒤 올립니다.

## 주의

- `CNAME` 파일은 지우지 마세요 (도메인 연결용).
- 폴더와 파일 이름은 영문 소문자, 숫자, 하이픈(-)만 사용합니다.
- 메인 페이지의 `index.html`과 웹앱의 `index.html`을 서로 바꿔 올리지 않도록 주의하세요. 맨 위 `index.html`이 웹앱으로 바뀌면 gabrielmath.kr에서 메인 페이지 대신 웹앱이 열립니다.
- **API 키를 어떤 파일에도 적지 마세요.** G-Man 멘토의 API 키는 사용자가 웹앱 화면에서 직접 넣고, 그 기기의 브라우저에만 저장됩니다.

## 개인정보

- 회원가입과 로그인이 없고, 운영자는 서버를 운영하지 않습니다.
- 학습 기록은 사용하는 기기의 브라우저에만 저장됩니다. math1, algebra, calculus1, calculus2, prob-stats의 기록은 따로 저장되고, G-Man 멘토 API 키 설정은 다섯 웹앱이 함께 씁니다.
- G-Man 멘토를 쓸 때만 보낸 말과 차시 정보가 Anthropic의 Claude로 전달됩니다.
- 웹앱별 처리방침: [math1/PRIVACY.md](./math1/PRIVACY.md), [algebra/PRIVACY.md](./algebra/PRIVACY.md), [calculus1/PRIVACY.md](./calculus1/PRIVACY.md), [calculus2/PRIVACY.md](./calculus2/PRIVACY.md), [prob-stats/PRIVACY.md](./prob-stats/PRIVACY.md)
- 개인정보 보호책임자: 전병제 (개인) · 문의: gabriel@gabrielmath.kr

## 문의

gabriel@gabrielmath.kr
