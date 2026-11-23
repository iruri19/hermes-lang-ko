# Hermes Agent 한국어 언어팩 (hermes-lang-ko)

[Hermes Agent](https://github.com/NousResearch/hermes-agent) **데스크톱 앱**을 한국어로 쓸 수 있게 해 주는 비공식 번역 팩입니다.

Hermes에는 CLI와 TUI용 한국어 번역이 기본으로 들어 있습니다. 하지만 **데스크톱 앱 번역은 들어 있지 않아서**, 언어를 한국어로 골라도 앱 화면은 영어로 나오고 언어 선택 메뉴에도 "한국어"가 보이지 않습니다. 이 팩이 그 빈자리를 채웁니다.

## 대상 버전

| 항목 | 버전 |
|---|---|
| Hermes Agent | **v0.23.3 (stable)**, commit `caafe53` |
| Hermes Desktop (Windows Store 패키지) | **2026.7749.2279.0** |

- 위 버전의 영어 원문을 기준으로 번역했습니다.
- 다른 버전에서도 대부분 동작합니다. 새로 생긴 문구만 영어로 보이고, 없어진 문구는 무시됩니다.

## 포함 내용

| 파일 | 대상 | 문구 수 |
|---|---|---|
| `locales/ko.desktop.yaml` | Hermes 데스크톱 앱 (메뉴, 설정, 안내, 설명 등) | 5,655 (전체 5,661개 중) |
| `locales/ko.yaml` | CLI와 메신저 게이트웨이 중 기본 번역에서 영어로 남아 있던 문구 | 37 |

- 번역하지 않은 6개는 목록이나 함수 형태라 언어팩 형식으로는 바꿀 수 없는 항목입니다. 입력창 예시 문구 묶음 등이 여기에 해당합니다.
- 브랜드 이름(OpenAI, Telegram 등), 명령어(`/model` 등), 단축키, 설정 키는 일부러 원문을 유지했습니다.
- 에이전트의 답변 언어는 이 팩과 관계없습니다. 답변 언어는 프롬프트로 정하세요.
- `hermes plugins validate`를 통과했습니다. 등록된 키 5,655개와 37개가 모두 영어 카탈로그와 일치하고, 보안 스캔도 safe입니다.

## 설치 방법

### 방법 1. 플러그인으로 설치 (권장)

```bash
hermes plugins install https://github.com/iruri19/hermes-lang-ko
hermes plugins enable hermes-lang-ko
hermes config set display.language ko
hermes gateway restart
```

그다음 Hermes 데스크톱 앱을 다시 실행하고 **설정 → 언어 → 한국어**를 선택합니다.

### 방법 2. 파일 직접 복사 (플러그인 없이)

`locales/` 폴더의 두 파일을 Hermes 홈의 `locales` 폴더에 복사합니다.

| 환경 | 복사할 위치 |
|---|---|
| 기본 | `~/.hermes/locales/` (Windows: `%USERPROFILE%\.hermes\locales\`) |
| `HERMES_HOME`을 따로 지정한 경우 | `$HERMES_HOME/locales/` |
| 프로필을 쓰는 경우 | `~/.hermes/profiles/<프로필>/locales/` |

```bash
mkdir -p ~/.hermes/locales
cp locales/ko.yaml locales/ko.desktop.yaml ~/.hermes/locales/
hermes config set display.language ko
hermes gateway restart
```

## 언어 메뉴에 "한국어"가 안 보일 때

- **원인:** 데스크톱 앱의 언어 목록은 백그라운드에서 도는 **Hermes 게이트웨이 프로세스**가 앱에 알려 줍니다. 게이트웨이는 켜질 때 목록을 한 번만 만들어 두고, 앱 창을 닫아도 꺼지지 않습니다. 그래서 설치 전에 켜져 있던 게이트웨이는 한국어 파일이 생긴 걸 모릅니다.
- **해결:** 아래 둘 중 하나를 하세요.
  - `hermes gateway restart`를 실행합니다.
  - 작업 관리자에서 `hermes_cli\main.py gateway run`으로 실행 중인 `python.exe`를 종료한 뒤 앱을 다시 실행합니다.

## 되돌리기

- **플러그인으로 설치한 경우:** `hermes plugins remove hermes-lang-ko`
- **직접 복사한 경우:** `locales/ko.yaml`, `locales/ko.desktop.yaml` 파일을 삭제
- **영어로 돌아가기:** `hermes config set display.language en`

## 번역 수정 및 기여

- 어색한 번역은 Issue나 PR로 알려 주세요.
- 파일은 `키: 값` 형식의 YAML입니다.
- `{0}`, `{1}`, `{name}` 같은 자리 표시자는 반드시 그대로 두세요. 위치는 바꿔도 됩니다.
- 수정한 뒤에는 `hermes plugins validate .`로 검사할 수 있습니다.

## 참고

- 이 팩은 Nous Research의 공식 배포물이 아닙니다.
- 언어팩 형식은 [Language Packs 문서](https://hermes-agent.nousresearch.com/docs/user-guide/features/language-packs)를 따릅니다.
- 라이선스: MIT
