# Gemini Project (gemini_proj)

이 프로젝트는 Gemini CLI를 기반으로 한 AI 에이전트 환경으로, 코드 생성, 문서 분석 및 OneNote MCP(Model Context Protocol)를 통한 생산성 도구 통합을 목표로 합니다.

## 🚀 주요 기능 및 구성 요소

- **Gemini CLI:** 터미널 우선의 AI 에이전트 환경.
- **OneNote MCP (`onenotemcp/`):** LLM(Gemini, Claude 등)과 Microsoft OneNote 계정을 연결하는 MCP 서버.
- **Crypto Analysis Reports (`crypto_reports/`):** 2024년 디지털 자산 및 암호화폐 흐름에 관한 주요 기관(BIS, ECB, FedNY) 보고서 포함.
- **Project Documentation:** `GEMINI.md`에 프로젝트의 상세한 컨텍스트와 개발 규칙이 명시되어 있습니다.

## 🛠️ 설치 및 실행

### 필수 요구 사항
- Node.js (>= 20.0.0)
- npm

### 설치 방법
```bash
npm install
```

### OneNote MCP 활성화 (필요 시)
1. `onenotemcp` 디렉토리로 이동:
   ```bash
   cd onenotemcp
   ```
2. 인증 절차 수행:
   - `authenticate` 도구 실행 후 브라우저에서 인증.
   - `saveAccessToken` 도구로 토큰 저장.

## 📂 프로젝트 구조

- `onenotemcp/`: OneNote 통합 서버 소스 코드.
- `crypto_reports/`: 암호화폐 관련 주요 PDF 보고서.
- `crypto_summary.md`: 암호화폐 보고서 분석 요약본.
- `presentation.qmd` / `presentation.html`: Quarto 기반 프레젠테이션 문서.
- `GEMINI.md`: AI 에이전트(Gemini)를 위한 프로젝트 가이드라인.

## 🤝 기여 방법

1. 브랜치를 생성하고 변경 사항을 커밋합니다.
2. [Conventional Commits](https://www.conventionalcommits.org/) 표준을 준수합니다.
3. Pull Request를 제출하기 전 `npm run lint`와 `npm run test`를 실행하여 무결성을 확인합니다.

---
Copyright 2026. All rights reserved.
