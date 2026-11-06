# 보안 최소 점검 결과

- 점검 도구: [dorms-check](https://github.com/shinnanchanguk/dorms-check) 0.3.1 (커밋 `91b40f6d0ea07d459ffce262ea2dc414a8adeb55`)
- 점검일: 2026년 11월 2일
- 점검 범위: `security` 트랙만 (edzip, protection은 선택하지 않음)
- 이 결과는 최소 점검이며 앱 전체의 안전을 보장하지 않습니다. 도름스 마크는 도름스 서버가 공개 주소를 다시 점검해 발급합니다.

## 요약

| 구분 | 내용 |
|---|---|
| 확인된 위험 | 없음 |
| 개선 권고 | 보안 헤더 설정 위치 (호스팅이 결정), 개인정보 처리방침과 이용 안내 (이번에 추가) |
| 미확인 | 공개 화면 점검, 도구 기준 앱 코드 비밀값 점검, 플랫폼 내부 동작 |

## 1. 확인된 위험

도구 결과에 실패 항목이 없습니다. 도구가 읽지 못한 `index.html`은 같은 기준으로 직접 확인했습니다.

| 항목 | 결과 |
|---|---|
| 비밀값, API 키 패턴 (`sk-`, `AIza`, `ghp_`, `xox`, secret/password/token 대입) | 0건 |
| `eval`, `new Function` (앱 코드) | 0건 |
| `innerHTML` 대입 33곳 | 모두 슬라이더나 숫자 입력값, 고정된 문장, KaTeX 출력만 넣음. 학생 글과 AI 답변은 텍스트 노드로 넣음 |
| 수식 안 `\href{javascript:...}` | MathJax와 KaTeX 모두 링크를 만들지 않음 |

## 2. 개선 권고와 이번 조치

| 권고 | 이번 조치 |
|---|---|
| 공개 HTML에서 개인정보 처리방침을 찾지 못함 | 앱 안에 ‘개인정보 처리방침’ 화면을 추가하고, HTML 원문 하단에 링크를 넣음. 같은 내용을 [PRIVACY.md](../PRIVACY.md)로 공개 |
| 이용약관 링크 없음 | 앱 안에 ‘이용 안내’ 화면과 하단 링크 추가 |
| AI로 전달되는 정보 안내 필요 | G-Man 멘토 대화창에 ‘보낸 내용은 Anthropic의 Claude로 전달’, ‘개인정보를 쓰지 말 것’ 안내 추가 |
| 학생 기록 삭제 수단 필요 | ‘이 기기의 내 기록 모두 지우기’ 버튼 추가 |
| 외부로 나가는 주소 정보 최소화 | `referrer` 정책을 `strict-origin-when-cross-origin`으로 지정 |
| 보안 헤더 설정 파일 없음 | 조치하지 않음. claude.ai와 GitHub Pages는 응답 헤더를 호스팅이 정하며, 이 점검만을 위해 호스팅을 바꾸지 않음 |
| 위험 코드 패턴 1건 | 게시 환경 설명 문서 사본(`artifacts/`)의 결과로 앱 코드가 아님. `.gitignore`로 저장소에서 제외 |

조치 뒤 dorms-check의 방침 찾기 기능(`checks/external/legal-pages.js`)에 앱 HTML 원문을 직접 넣어 확인했습니다.

| 항목 | 조치 전 | 조치 후 |
|---|---|---|
| `legal.privacy-policy` | 미확인 | 통과 (링크 발견) |
| `legal.terms` | 권고 | 통과 (링크 발견) |
| `legal.contact` | 통과 | 통과 |

## 이후 변경: 내 API 키로 G-Man 멘토 사용

claude.ai 밖에서 G-Man 멘토를 쓰도록 ‘내 API 키 넣기’ 기능을 추가했습니다. 점검 기준에서 달라진 점은 다음과 같습니다.

| 항목 | 처리 |
|---|---|
| 하드코딩 시크릿 | 앱 파일과 저장소에 API 키가 없음. 키는 사용자가 실행 중에 직접 입력 |
| 키 보관 | 기본은 탭 임시 저장소(`sessionStorage`), 사용자가 고를 때만 `localStorage`. 학습 기록 저장소와 PDF 보고서에는 들어가지 않음 (실행 시험으로 확인) |
| 키 표시 | 입력 칸은 비밀번호 형식, 저장 뒤에는 앞 10자와 끝 4자만 표시 |
| 전송 | 사용자가 넣은 키의 회사 API 주소로만 전송 (Anthropic, OpenAI, Google, OpenRouter, Groq, xAI, 또는 사용자가 입력한 https 주소). Anthropic은 `anthropic-dangerous-direct-browser-access: true` 헤더 사용 (사용자 본인 키 입력 방식에서만 적절). 직접 입력 주소는 `https://`만 허용 |
| 교체, 삭제 | 키 교체, 키 삭제, 연결 확인 버튼 제공. ‘내 기록 모두 지우기’도 키를 지움 |
| 남은 위험 | 같은 브라우저에서 실행되는 다른 코드나 확장 프로그램이 키를 읽을 수 있음. 공용 기기에서는 기억하기를 쓰지 않도록 안내 |

## 3. 미확인

| 항목 | 이유 | 확인 방법 |
|---|---|---|
| 공개 화면 (HTTPS 응답, 헤더, 본문) | 점검을 실행한 환경에서 claude.ai 주소로 접속할 수 없었음. 게시 화면은 공유 전까지 운영자만 볼 수 있음 | 앱을 공유하거나 GitHub Pages로 공개한 뒤 운영자 컴퓨터에서 `scan --url "<공개 주소>"` 실행 |
| 도구 기준 앱 코드 점검 | dorms-check 0.3.1의 코드 점검은 `.js` 등만 읽고 `.html`은 읽지 않음 | 위 1번의 직접 확인으로 보충. 도구 결과는 바꾸지 않음 |
| 플랫폼 내부 동작 | G-Man 멘토 요청 처리, 파일 저장 기능, 브라우저 저장소 격리는 claude.ai 쪽 기능 | Anthropic과 claude.ai의 공개 문서 확인 |
| 학교 심의 | 도구가 판단하지 않음 | 학교에서 별도 심의 |

## 다시 점검하기

```bash
npx -y https://github.com/shinnanchanguk/dorms-check/archive/91b40f6d0ea07d459ffce262ea2dc414a8adeb55.tar.gz detect
npx -y https://github.com/shinnanchanguk/dorms-check/archive/91b40f6d0ea07d459ffce262ea2dc414a8adeb55.tar.gz scan --url "<공개 주소>"
```

결과는 `.dorms-check/`에 저장되며, 이 폴더는 `.gitignore`로 저장소에 올리지 않습니다.
