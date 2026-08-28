# ADR.md

## ADR-0001 - 설치 가능한 VS Code 테마 확장으로 제공

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

Ghostty의 `Ghostty Night` 색상 조합과 분위기를 VS Code에서 사용할 수 있는 결과물로 옮긴다.

### Decision

VS Code에서 개발 모드로 실행하고 패키징·설치할 수 있는 테마 확장 전체를 제작한다. 테마 JSON만 단독으로 제공하지 않고, 확장 매니페스트와 사용 문서를 포함한다.

### Consequences

- VS Code 테마 확장 매니페스트와 테마 기여점(contributes)을 설계해야 한다.
- 편집기, 워크벤치, 터미널, 상태 UI 등 VS Code 전용 색상 토큰을 Ghostty 팔레트에 매핑해야 한다.
- 패키징 가능 여부와 VS Code에서의 시각적 적용을 검증해야 한다.

### Evidence

- `~/.config/ghostty/themes/Ghostty Night`: 원본 배경·전경·커서·선택 영역·ANSI 팔레트
- 사용자 지시: “설치 가능한 VS Code 테마 확장 전체” 추천안 적용

## ADR-0002 - 다크 테마 단일 변형 제공

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

원본 `Ghostty Night`는 다크 터미널 테마이며, 목표는 그 색상 조합과 분위기를 VS Code로 옮기는 것이다.

### Decision

단일 다크 테마만 제공한다. 라이트 변형은 이번 범위에 포함하지 않는다.

### Consequences

- 원본의 배경 명도와 차가운 강조색 대비를 직접 보존하는 데 집중할 수 있다.
- 라이트 테마를 위한 별도의 의미 색상·대비 설계와 검증은 하지 않는다.

### Evidence

- `~/.config/ghostty/themes/Ghostty Night`: `#24283B` 배경 기반의 다크 팔레트
- 사용자 결정: 단일 다크 테마

## ADR-0003 - VS Code 테마 이름은 Night (MJY)로 지정

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

원본 파일명은 `Ghostty Night`지만 VS Code에서 제공할 테마에는 별도의 사용자-facing 이름이 필요하다.

### Decision

테마 표시 이름은 `Night (MJY)`로 지정한다. 확장 식별자는 `night-mjy`를 사용한다.

### Consequences

- VS Code 테마 선택기에서 `Night (MJY)`로 표시된다.
- 원본 Ghostty 테마와의 관계는 README와 테마 설명에 기록해야 한다.

### Evidence

- 사용자 결정: 테마 이름을 `Night (MJY)`로 설정

## ADR-0004 - 원본 팔레트 보존과 의미적 UI 매핑 병행

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

VS Code는 Ghostty 터미널보다 훨씬 많은 편집기·워크벤치·진단·소스 제어 색상 토큰을 제공한다.

### Decision

`Ghostty Night`의 핵심 색상값과 차가운 분위기는 최대한 보존하되, VS Code 토큰은 UI 역할에 맞게 의미적으로 매핑한다. 필요한 경우에만 같은 계열의 명도 단계를 소폭 보정한다.

### Consequences

- 터미널과 편집기 사이의 시각적 일관성을 유지할 수 있다.
- 모든 VS Code 토큰이 원본 팔레트의 일대일 대응을 갖지는 않는다.
- 토큰 매핑에는 가독성과 상태 구분에 대한 설계 판단이 필요하다.

### Evidence

- `~/.config/ghostty/themes/Ghostty Night`: 배경, 전경, 선택 영역, 커서 및 16색 ANSI 팔레트
- 사용자 결정: 추천 매핑안 적용

## ADR-0005 - VS Code 색상 토큰 포괄적 커버리지

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

테마가 실제 개발 환경에서 사용될 때 기본 토큰만 지정하면 특정 패널이나 상태 UI가 기본 테마 색으로 남을 수 있다.

### Decision

편집기·탭·사이드바·패널·터미널·검색·디버그·소스 제어·진단·Git 장식·Markdown·괄호 강조 등 주요 VS Code UI 영역을 포괄적으로 커버한다.

### Consequences

- 미지정 영역을 줄여 일관된 테마 경험을 제공한다.
- 테마 JSON이 커지고, 토큰 중복·충돌과 실제 UI 검증 부담이 증가한다.

### Evidence

- 사용자 결정: 색상 토큰을 포괄적으로 커버

## ADR-0006 - TextMate와 의미 토큰 강조를 함께 제공

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

VS Code의 문법 강조는 TextMate 문법 기반 토큰과 언어 서버가 제공하는 의미 토큰이라는 두 경로를 사용한다. 한 경로만 지정하면 언어·확장별 결과가 달라질 수 있다.

### Decision

`tokenColors`와 `semanticTokenColors`를 모두 정의한다. 두 계층 모두 시안·핑크·블루·퍼플 중심의 원본 팔레트와 역할별 명도 차를 사용한다.

### Consequences

- 기존 문법과 최신 언어 서버 기반 문법 강조의 호환성이 좋아진다.
- 두 토큰 계층 사이의 우선순위와 색상 충돌을 검증해야 한다.

### Evidence

- 사용자 결정: 추천안 적용

## ADR-0008 - 통합 터미널 ANSI 팔레트는 원본값 유지

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

VS Code 테마는 통합 터미널의 ANSI 16색을 별도로 지정할 수 있다. 이 값이 UI 매핑과 달라지면 같은 테마 안에서 터미널 출력의 인상이 달라진다.

### Decision

통합 터미널의 ANSI 16색은 `Ghostty Night`의 팔레트 값을 동일하게 사용한다. UI 색상 토큰에만 의미적 매핑과 필요한 대비 보정을 적용한다.

### Consequences

- Ghostty와 VS Code 통합 터미널의 출력 분위기가 일치한다.
- 터미널 ANSI 색상은 UI 가독성 기준에 맞춰 임의로 재설계하지 않는다.

### Evidence

- `~/.config/ghostty/themes/Ghostty Night`: ANSI 팔레트 0–15
- 사용자 결정: 통합 터미널 ANSI 16색 동일 지정

## ADR-0009 - 확장 publisher와 식별자 지정

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

VS Code 확장은 `publisher`와 확장 이름 조합으로 식별되며, 패키징 가능한 매니페스트가 필요하다.

### Decision

publisher는 `mjy`, 확장 이름은 `night-mjy`로 지정한다. 확장 식별자는 `mjy.night-mjy`가 된다.

### Consequences

- 로컬 개발·패키징·설치에 일관된 식별자를 사용할 수 있다.
- Marketplace 게시 시 실제 publisher 계정에 맞춰 변경할 수 있다.

### Evidence

- 사용자 결정: publisher를 `mjy`로 지정

## ADR-0010 - 패키징과 실제 UI 검증을 완료 조건으로 지정

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

테마 JSON이 문법적으로 유효한 것만으로는 VS Code의 실제 UI 토큰 적용과 시각적 일관성을 보장할 수 없다.

### Decision

완료 전에 매니페스트·테마 JSON 구조 검증, `.vsix` 패키징, VS Code 활성화 확인, 주요 UI 영역의 실제 화면 점검, 핵심 텍스트·상태 색상의 대비 점검을 수행한다.

### Consequences

- 구현 완료 판단이 파일 생성이 아니라 설치·활성화 가능한 동작 결과에 기반한다.
- VS Code가 설치되어 있지 않거나 화면 검증 환경이 제한되면 해당 범위를 명시적으로 보고해야 한다.

### Evidence

- 사용자 결정: 추천 검증 범위 적용

## ADR-0007 - 핵심 정보의 대비와 원본 분위기 균형

- 상태: accepted
- 날짜: 2026-08-28
- 근거 유형: explicit

### Context

원본 팔레트의 모든 색상을 그대로 사용하면 어두운 배경에서 비활성 텍스트나 일부 ANSI 색의 가독성이 낮아질 수 있다.

### Decision

본문 텍스트·코드·선택 영역·진단 메시지처럼 핵심 정보에는 충분한 대비를 우선한다. 장식적 요소에는 `Ghostty Night`의 차가운 색감과 개성을 유지하며, 필요한 색상만 소폭 보정한다.

### Consequences

- 장시간 사용 시 읽기 편한 테마가 된다.
- 일부 토큰은 원본 파일의 색상값과 정확히 일치하지 않을 수 있다.
- 대비 점검과 실제 화면 확인이 구현 검증에 포함된다.

### Evidence

- 사용자 결정: 추천안 적용
