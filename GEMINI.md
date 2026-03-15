# Gemini CLI Project Context

Gemini CLI는 Gemini 모델의 강력한 기능을 터미널에서 직접 활용할 수 있게 해주는 오픈 소스 AI 에이전트입니다. 개발자를 위해 터미널 우선(terminal-first), 확장성, 그리고 강력한 도구 통합을 목표로 설계되었습니다.

## Project Overview

- **Purpose:** 코드 이해, 생성, 자동화 및 MCP(Model Context Protocol)를 통한 도구 통합을 지원하는 원활한 터미널 인터페이스 제공.
- **Main Technologies:**
  - **Runtime:** Node.js (>=20.0.0, 개발 권장 ~20.19.0)
  - **Language:** TypeScript
  - **UI Framework:** React ([Ink](https://github.com/vadimdemedes/ink) 기반 CLI 렌더링)
  - **Testing:** Vitest
  - **Bundling:** esbuild
  - **Linting/Formatting:** ESLint, Prettier
- **Architecture:** npm workspace를 이용한 모노레포 구조.
  - `packages/cli`: 사용자 인터페이스, 입력 처리 및 렌더링.
  - `packages/core`: 백엔드 로직, Gemini API 오케스트레이션, 프롬프트 구성 및 도구 실행.
  - `packages/core/src/tools/`: 파일 시스템, 셸, 웹 작업을 위한 빌트인 도구.
  - `packages/a2a-server`: 실험적인 에이전트 간(Agent-to-Agent) 서버.
  - `packages/vscode-ide-companion`: CLI와 페어링되는 VS Code 확장 프로그램.

## Local Component: OneNote MCP Server (`onenotemcp`)

- **Purpose:** MCP 표준을 사용하여 사용자의 Microsoft OneNote 계정과 LLM 사이를 연결.
- **Key Files:**
  - `onenotemcp/onenote-mcp.mjs`: 서버 메인 엔트리 포인트.
  - `onenotemcp/.access-token.txt`: OAuth 2.0 액세스 토큰 저장소.
- **Authentication Workflow:**
  1. `authenticate` 도구 실행.
  2. 브라우저에서 `https://microsoft.com/devicelogin` 접속 및 인증.
  3. `saveAccessToken` 도구 실행.

## Building and Running

- **Install Dependencies:** `npm install`
- **Build All:** `npm run build:all` (패키지, 샌드박스, VS Code 컴패니언 빌드)
- **Build Packages:** `npm run build`
- **Run in Development:** `npm run start`
- **Run in Debug Mode:** `npm run debug` (Node.js 인스펙터 활성화)
- **Bundle Project:** `npm run bundle`
- **Clean Artifacts:** `npm run clean`

## Testing and Quality

- **Test Commands:**
  - **Unit (All):** `npm run test`
  - **Integration (E2E):** `npm run test:e2e`
  - **Workspace-Specific:** `npm test -w <pkg> -- <path>` (예: `-w @google/gemini-cli-core -- src/routing/modelRouterService.test.ts`)
- **Full Validation:** `npm run preflight`
  - 가장 엄격한 체크 도구 (clean, install, build, lint, type check, test 포함).
  - 실행 시간이 길므로 구현 작업의 마지막 단계에서만 실행 권장.
  - 실패 시 `npm run test` 등 빠른 도구로 수정 후 다시 시도. 단순 문서/프롬프트 수정 시에는 생략 가능.
- **Individual Checks:** `npm run lint` / `npm run format` / `npm run typecheck`

## Development Conventions

- **Legacy Snippets:** `packages/core/src/prompts/snippets.legacy.ts`는 과거의 시스템 프롬프트 스냅샷입니다. 역사적 동작 보존을 위해 문구 수정은 피하되, 컴파일 보장이나 코드 단순화를 위한 구조적 변경은 허용됩니다.
- **Contributions:** `CONTRIBUTING.md` 절차를 준수하며, Google CLA 서명이 필요합니다.
- **Pull Requests:** 작고 집중된 단위로 작성하며 관련 이슈를 연결합니다. PR 생성 시에는 항상 `pr-creator` 스킬을 활성화합니다.
- **Commit Messages:** [Conventional Commits](https://www.conventionalcommits.org/) 표준을 따릅니다.
- **Coding Style:** `packages/cli` (React/Ink) 및 `packages/core` (Backend)의 기존 패턴을 엄격히 준수합니다.
- **Imports:** 특정 모듈을 직접 임포트하며, ESLint에 의해 제한된 패키지 간 상대 경로 임포트는 피합니다.
- **License Headers:** 모든 새 소스 파일(`.ts`, `.tsx`, `.js`)에 현재 연도가 포함된 Apache-2.0 라이선스 헤더를 포함합니다 (예: `Copyright 2026 Google LLC`).

## Testing Conventions

- **Environment Variables:** 환경 변수 의존성 테스트 시 `vi.stubEnv('NAME', 'value')`를 `beforeEach`에서 사용하고, `afterEach`에서 `vi.unstubAllEnvs()`로 정리합니다. `process.env` 직접 수정은 지양합니다.

## Documentation

- 문서 작업(작성, 수정, 검토) 시에는 반드시 `docs-writer` 스킬을 사용합니다.
- 모든 문서는 `docs/` 디렉토리에 위치합니다.
- 코드 변경으로 인해 기존 문서가 유효하지 않게 될 경우 즉시 업데이트를 제안합니다.
