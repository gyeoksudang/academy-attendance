# academy-attendance

# 결과 주소
[https://gyeoksudang.github.io/academy-attendance/]
[https://gyeoksudang.github.io/academy-attendance/attentance]

## 개발 가이드
[https://gyeoksudang.github.io/academy-attendance/development-guide.html]

## 데이터 교환 문제 해결 가이드
[https://gyeoksudang.github.io/academy-attendance/development-guide.html]

# 학원용 QR 코드 출석 체크 시스템 완전 구현 요청 (예시, claude)
학원용 QR 코드 출석 체크 시스템을 만들고 싶어. 요구사항은 다음과 같아:

## 📋 기본 기능 요구사항
1. 하루에 하나의 QR 코드만 출력해서 사용
2. 학생이 QR 스캔 후 본인 이름 선택으로 출석 체크  
3. 각 학생의 개별 수업 스케줄을 확인해서 15분 이상 지각시 부모에게 SMS 발송 (로그만 출력)
4. 학생 관리는 이름, 부모 전화번호, 수업 요일/시간만 간단하게
5. AI 시연용이라서 최대한 간단하게 구현하고 싶음
6. 웹 서비스 설치 없이 구글 시트 + GitHub Pages + Apps Script로 무료 구현
7. 관리자가 웹 접속하면 바로 당일 QR 코드가 표시되어 인쇄 가능하도록

## 🔧 데이터 입력 편의성 요구사항
- 구글 시트 설정시 헤더와 샘플 데이터를 한 번에 복사-붙여넣기할 수 있는 형태로 제공
- 일일이 셀별로 입력하지 않고 탭 구분자로 된 텍스트 블록을 제공하여 효율적인 초기 설정 가능
- 수업시간 데이터가 날짜 형식으로 잘못 변환되는 문제 해결 방법 포함

## 🚨 중요한 기술적 문제 해결 요구사항

### CORS 문제 완전 해결 필요:
- GitHub Pages에서 Apps Script로 요청시 발생하는 CORS 에러 해결 필요
- `Content-Type: application/json` 헤더 사용시 preflight 요청으로 인한 차단 문제
- **해결 방법**: 클라이언트에서 모든 fetch 옵션(headers, mode, cache 등) 완전 제거
- Apps Script는 단순한 JSON 응답만 사용하고 CORS 헤더 설정하지 않음
- 가장 단순한 `fetch(url)` 형태만 사용해서 preflight 요청 방지

### QR 코드 생성 문제 완전 해결 필요:
- `QRCode is not defined` 오류 해결
- CDN 라이브러리 로딩 실패 문제 해결
- **해결 방법**: `qrcodejs` 라이브러리 사용 (https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js)
- `QRCode.CorrectLevel.L` 옵션으로 에러 수정 레벨 최적화
- Apps Script 연결 실패시에도 기본 QR 코드 생성되도록 구현

### 기타 해결해야 할 문제들:
- 구글 시트에서 시간 데이터가 `1899-12-30T05:32:08.000Z` 형식으로 잘못 표시되는 문제
- 학생 명단을 구글 시트에서 동적으로 불러와서 HTML 수정 없이 관리 가능하도록
- 실제 작동 테스트를 통해 검증된 안정적인 코드만 제공

## 📤 제공해야 할 내용
- 구글 시트 설정 방법 (복사-붙여넣기 가능한 데이터 포함)
- Apps Script 완전한 코드 (CORS 문제 해결된 버전)
- HTML 파일 2개 (QR 생성 관리자 페이지, 학생용 출석 체크 페이지)
- GitHub Pages 설정 및 배포 방법
- Apps Script 웹앱 URL과 구글 시트 ID를 실제 코드에 적용하는 단계별 방법
- 위에서 언급한 모든 문제들의 해결 방법과 이유 설명
- 완전한 테스트 시나리오

## 💡 핵심 포인트
- **CORS 해결**: 모든 fetch 옵션 제거하여 단순한 요청만 사용
- **QR 생성**: qrcodejs 라이브러리로 안정적인 QR 코드 생성
- **데이터 형식**: 구글 시트 시간 열을 텍스트 형식으로 설정
- **실용성**: 실제 테스트를 거쳐 100% 작동하는 코드만 요청

실제로 작동하는 완전한 시스템의 구현 방법과 단계별 상세 가이드를 아티팩트로 만들어줘. 위의 모든 문제점들이 해결된 최종 완성 버전으로 만들어달라.
