# My English, My Choice (Vercel + GitHub 배포용)

Google Apps Script(`Code.gs` + `Index.html`)로 작성된 영어 작문 AI 피드백 웹앱을 **GitHub + Vercel** 환경에서 바로 배포할 수 있도록 변환한 프로젝트입니다.

## 1. 폴더 구조
```text
├── api/
│   └── index.js        # 서버리스 API (Gemini 호출 및 구글 시트 연동)
├── public/
│   └── index.html      # 프론트엔드 화면 (1~4단계 학습 및 선생님 관리)
├── package.json        # googleapis 의존성 정의
├── vercel.json         # Vercel 라우팅 및 함수 실행 시간(60초) 설정
└── .env.example        # 환경변수 예시
```

## 2. Vercel 환경변수 설정 (필수 및 선택)

Vercel 대시보드 > **Settings > Environment Variables**에 아래 변수를 등록합니다.

### 필수 환경변수
* `GEMINI_API_KEY`: Google AI Studio에서 발급받은 Gemini API 키
* `TEACHER_PIN`: 선생님 화면 로그인 비밀번호 (예: `1234`)

### 선택 환경변수
* `GEMINI_MODEL`: 사용할 모델명 (미입력 시 기본값 `gemini-3.5-flash-lite`)
* **구글 시트 연동용 (학생 제출 데이터 영구 저장 시 필요)**
  * `GOOGLE_SHEET_ID`: 데이터를 저장할 구글 스프레드시트 URL의 ID (`/d/`와 `/edit` 사이 문자열)
  * `GOOGLE_SERVICE_ACCOUNT_EMAIL`: Google Cloud 서비스 계정 이메일
  * `GOOGLE_PRIVATE_KEY`: 서비스 계정 JSON 키 파일 안의 `private_key` 전체 문자열 (`-----BEGIN PRIVATE KEY-----` 포함)
  * *(참고)* 구글 시트 환경변수를 비워 두어도 앱은 정상 작동하며, 예시 코드(`ENG-DEMO`)와 제출 내역이 서버 메모리에 임시 저장됩니다.

## 3. 배포 순서
1. 압축을 푼 폴더 안의 모든 파일을 GitHub 새 저장소(Repository)에 업로드합니다.
2. Vercel에서 **Add New > Project**를 누르고 해당 GitHub 저장소를 선택합니다.
3. **Environment Variables** 항목에 `GEMINI_API_KEY`와 `TEACHER_PIN`을 입력한 뒤 **Deploy**를 누릅니다.
