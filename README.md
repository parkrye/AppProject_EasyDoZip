# EasyDoZip

광고 · 데이터 수집 없는 안드로이드 파일 관리 · 압축 앱. 폴더 탐색 · 파일 작업, zip 압축 · 해제(암호 지원), 간단한 파일 미리보기를 한 앱에서. 파일은 기기 밖으로 나가지 않음. EasyDo 시리즈.

## 다운로드

최신 버전 0.2.1 — [Releases](https://github.com/parkrye/AppProject_EasyDoZip/releases)에서 `EasyDoZip-<버전>.apk`를 받아 설치. Android 8.0 이상.

- 처음 설치 시 "출처를 알 수 없는 앱" 설치 허용 필요. Play 프로텍트가 검사 화면을 띄울 수 있음
- 업데이트는 새 APK를 같은 방식으로 덮어 설치. 추가한 폴더 · 설정 유지. 앱 안 `설정 → 앱 정보 → 새 버전 받기`로 Releases 페이지를 열 수 있음
- 서명 인증서 SHA-256: `f16af4368ee3e278e5c4f8c9bc30e576fee9b92c13aad8124267e8b8a58b284f`
  (`apksigner verify --print-certs EasyDoZip-<버전>.apk`로 확인)
- 버그 · 제안은 [Issues](https://github.com/parkrye/AppProject_EasyDoZip/issues)에

## 기능

| 영역 | 내용 |
|---|---|
| 파일 탐색 | 전체 파일 접근 시 저장소 볼륨(내장 · SD카드 · USB) 바로 탐색, 그 밖에는 폴더 추가(시스템 폴더 선택 화면, 권한 유지), 폴더 이동, 이름 · 크기 · 수정한 날짜 정렬(오름 · 내림, 폴더 우선, 숫자 자연 정렬), 숨김 파일 보기 |
| 파일 작업 | 다중 선택(선택하면 하단 막대에 복사 · 이동 · 압축 · 삭제 · 이름 · 공유 버튼), 복사 · 이동(다른 폴더 · 다른 볼륨 · 추가 폴더로 붙여넣기), 이름 바꾸기, 삭제, 새 폴더, 공유 |
| 압축 | 여러 파일 · 폴더를 zip 하나로, 선택하면 AES-256 암호 |
| 해제 | 모두 풀기(압축 파일 이름의 새 폴더) · 선택 항목 풀기(선택하면 하단 막대에 여기에 풀기 · 골라서 풀기), 대상은 압축 파일이 있는 폴더 또는 직접 고른 폴더 |
| 압축 파일 보기 | 내부 폴더 탐색 · 정렬, 암호 항목 표시, 항목 하나 미리보기 · 외부 앱 열기, zip 안의 zip 열기 |
| 암호 zip | ZipCrypto · AES(128/192/256) 해제, AES-256 압축 |
| 미리보기 | 이미지(확대 · 이동), 텍스트(앞 1MB, UTF-8 · CP949 자동), PDF. 오디오 · 비디오 · 그 밖은 외부 앱으로 열기 |
| 진행률 | 압축 · 해제 · 복사 · 이동 진행률 표시 · 취소. 취소 · 실패 시 쓰던 파일 삭제 |
| 설정 | `화면`(배경화면 색 사용, 기본 꺼짐) · `데이터`(백업 만들기 · 백업에서 복원, 대상은 설정) · `앱 정보`(버전 · 개인정보 · 새 버전 받기 · 오픈소스 라이선스) |

### 지원 범위

- **zip만 지원.** 저장(Stored) · Deflate 방식, ZIP64(4GB 넘는 파일 · 65,535개 넘는 항목) 읽기
- **7z · rar · tar · gz 미지원.** 다른 압축 방식(bzip2 · LZMA · Deflate64)으로 된 zip 항목은 건너뛰고 개수를 알려줌
- 분할 zip(`.z01` …) 미지원
- 암호 zip에서도 파일 이름 목록은 암호 없이 보임(zip 형식 특성)
- 이름 인코딩: UTF-8 표시가 없는 zip은 UTF-8로 읽을 수 없으면 CP949(한국어 Windows)로 읽음
- 보안: `../` · 절대 경로 · 드라이브 문자 항목(zip slip)은 풀지 않고 건너뜀
- 작업은 앱이 실행 중일 때 진행. 앱을 강제 종료하거나 시스템이 앱을 끝내면 작업도 멈춤(쓰던 파일은 남을 수 있음)

## 개인정보

인터넷 권한 없음 · 광고 없음 · 수집 · 전송 없음

- **인터넷 권한 없음.** 네트워크 코드 · 라이브러리 없음. 계정 · 광고 · 사용 통계 · 오류 보고 없음
- 앱이 저장하는 것은 설정 · 추가한 폴더 목록뿐 (Android 클라우드 백업도 끔). 압축 파일 항목 미리보기는 앱 캐시에 잠시 풀었다가 다음 미리보기 때 지움

### 권한

| 권한 | Android | 용도 |
|---|---|---|
| 모든 파일 접근 (`MANAGE_EXTERNAL_STORAGE`) | 11 이상 | 내장 저장소 · SD카드 전체 탐색 · 압축 · 해제 · 복사 · 이동 |
| 저장소 읽기 · 쓰기 (`READ` · `WRITE_EXTERNAL_STORAGE`) | 10 이하 | 위와 같음 |
| 앱 설치 (`REQUEST_INSTALL_PACKAGES`) | 8 이상 | APK를 누르면 시스템 설치 화면 열기. 처음엔 '이 출처 허용' 화면으로 안내 |

- 파일 관리 앱은 사용자가 고르는 아무 폴더에나 파일을 읽고 써야 해서 모든 파일 접근을 사용. 인터넷 권한이 없어 접근한 파일이 기기 밖으로 나갈 경로 없음
- 선택 사항. 허용하지 않으면 시스템 폴더 선택 화면으로 고른 폴더만 사용
- `Android/data` · `Android/obb`는 Android 11부터 이 권한으로도 열 수 없음

## EasyDo 시리즈

| 앱 | 용도 | 플랫폼 |
|---|---|---|
| [EasyDoDraw](https://github.com/parkrye/MultiProject_EasyDoDraw) | 그림 · 애니메이션 | Android · Windows |
| [EasyDoWrite](https://github.com/parkrye/AppProject_EasyDoWrite) | 소설 · 글쓰기 | Android |
| [EasyDoRead](https://github.com/parkrye/AppProject_EasyDoRead) | 책 · 문서 읽기 | Android |
| [EasyDoShelve](https://github.com/parkrye/AppProject_EasyDoShelve) | 웹 소설 서재 | Android |
| [EasyDoPhoto](https://github.com/parkrye/AppProject_EasyDoPhoto) | 카메라 · 사진 편집 | Android |
| [EasyDoDiet](https://github.com/parkrye/AppProject_EasyDoDiet) | 식단 · 운동 기록 | Android |
| [EasyDoZip](https://github.com/parkrye/AppProject_EasyDoZip) | 파일 · 압축 관리 | Android |
| [EasyDoGame](https://github.com/parkrye/AppProject_EasyDoGame) | 미니 게임 모음 | Android |
| [EasyDoMix](https://github.com/parkrye/AppProject_EasyDoMix) | 영상 · 오디오 편집 | Android |
| [EasyDoRecord](https://github.com/parkrye/AppProject_EasyDoRecord) | 녹음 | Android |
| [EasyDoStudio](https://github.com/parkrye/DesktopProject_EasyDoStudio) | 화면 녹화 · 영상 편집 | Windows |

## 라이선스

MIT License · © parkrye. 포함된 서드파티 라이브러리 라이선스는 앱 안 `설정 → 앱 정보 → 오픈소스 라이선스`에서 확인.
