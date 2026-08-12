# nblog-guide

네이버 블로그 자동 포스팅 프로그램의 **사용 가이드 + 자동 업데이트 배포용** 저장소입니다.

## 구성

| 파일 | 용도 |
|---|---|
| `index.html` | 사용 가이드 (GitHub Pages 로 서빙) |
| `robots.txt` | 검색 엔진 수집 차단 |
| `latest.json` | 자동 업데이트 매니페스트 |

## 접근 정책

- 저장소는 **Public** 이지만 `robots.txt` 와 `<meta name="robots" content="noindex">` 로
  검색 노출을 차단합니다. **링크를 아는 사람만** 보는 문서입니다.
- 프로그램 소스 코드는 이 저장소에 들어가지 않습니다. 가이드와 배포 파일만 둡니다.

## latest.json 스키마

`updater.py` 가 읽는 형식입니다. 필드 이름을 바꾸면 업데이트가 동작하지 않습니다.

```json
{
  "latest_version": "1.0.1",
  "download_url": "https://github.com/am24311-netizen/nblog-guide/releases/download/v1.0.1/NaverAutomation_v1.0.1.zip",
  "sha256": "<ZIP 의 sha256 (소문자 hex 64자)>",
  "required": false,
  "release_notes": "변경 내용",
  "min_supported_version": ""
}
```

- `sha256` 이 실제 ZIP 과 다르면 업데이트가 **거부**됩니다 (검증됨).
- `download_url` 은 GitHub Releases 에 올린 ZIP 의 직접 다운로드 주소를 씁니다.
- `required: true` 로 두면 사용자가 건너뛸 수 없는 필수 업데이트가 됩니다.

## 배포 절차

1. 배포 ZIP 생성 (개인정보 스캔 통과 필수)
2. Releases 에 ZIP 업로드
3. ZIP 의 sha256 계산
4. `latest.json` 갱신 후 push
5. 실제 업데이트 왕복 1회 확인
