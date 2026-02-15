# PRD: 블로그 자동화 시스템 (Blog Automation System)

## 1. 프로젝트 목표
키워드 하나로 최신 정보를 수집하고, AI를 통해 고품질의 블로그 포스트를 생성하여 자동으로 배포하는 엔드 투 엔드 자동화 시스템 구축.

## 2. 상세 요구사항

### 2.1 정보 수집 (Search Module)
- **입력**: 특정 주제 키워드.
- **동작**: Google Search를 통해 관련성 높은 상위 웹페이지의 텍스트 데이터 추출.
- **출력**: `search.md` 파일에 요약된 참조 데이터 저장.

### 2.2 비주얼 생성 (Image Module)
- **동작**: Gemini Image Generation API를 호출하여 포스트 주제와 어울리는 썸네일 이미지 생성.
- **출력**: `image.jpg` 파일로 저장.

### 2.3 콘텐츠 제작 (Draft Module)
- **동작**: `search.md` 데이터를 컨텍스트로 사용하여 Gemini가 Markdown 형식의 블로그 글 작성.
- **조건**: SEO 최적화된 제목, 서론, 본문(소제목 구분), 결론, 해시태그 포함.
- **출력**: `draft.md` 파일 생성.

### 2.4 퍼블리싱 (Publish Module)
- **동작**: Quarto를 사용해 `draft.md`를 HTML로 변환.
- **배포**: GitHub Actions 또는 로컬 스크립트를 통해 GitHub Pages에 업로드.
- **출력**: `directory/index.html` 및 최종 웹 사이트 반영.

## 3. 기술 스택
- **Language**: Python (또는 Node.js)
- **AI**: Google Gemini Pro (Text & Image)
- **Static Site Generator**: Quarto
- **Hosting**: GitHub Pages
