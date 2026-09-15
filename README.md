# DocumentSetting

PC 간에 공유하는 문서 작성 규칙과 프로젝트별 참고 자료다. Codex 스킬로 사용하거나, 이 저장소를 작업 프로젝트로 열어 사용할 수 있다.

## 구성

```text
DocumentSetting/
├── SKILL.md                       스킬 진입점
├── AGENTS.md                      이 저장소에서 작업할 때 적용할 지침
├── default/
│   └── writing-rules.md           게임 무관 공통 문서 작성 규칙
└── references/
    └── make-drama/
        ├── README.md             메이크 드라마 프로젝트 안내
        ├── game-context.md       게임 정보
        ├── document-analysis.md  사용자가 지정한 기획서 분석
        └── sources.md            참고 문서 URL과 확인 상태
```

## 다른 PC에서 사용

Git과 이 저장소에 접근할 수 있는 GitHub 인증을 준비한다.

### 저장소를 작업 폴더로 사용

```sh
git clone https://github.com/YGseok/DocumentSetting.git
cd DocumentSetting
```

Codex에서 이 폴더를 프로젝트로 열고 문서 작업을 요청한다. `AGENTS.md`가 공통 규칙과 레퍼런스의 읽기 순서를 안내한다.

### 개인 스킬로 사용 (Windows PowerShell)

같은 이름의 스킬 폴더가 없을 때 아래 명령으로 설치한다.

```powershell
$documentSkillsRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $env:USERPROFILE '.codex\skills' }
New-Item -ItemType Directory -Force -Path $documentSkillsRoot | Out-Null
git clone https://github.com/YGseok/DocumentSetting.git (Join-Path $documentSkillsRoot 'document-writing')
```

설치 후 Codex의 스킬 목록에서 `document-writing`이 표시되는지 확인한다. 목록에 보이지 않으면 새 작업이나 앱 재시작 후 다시 확인한다. 호출 예:

```text
$document-writing 공통 작성 규칙으로 기획서를 정리해줘.
$document-writing 메이크 드라마 레퍼런스를 참고해 전투 콘텐츠 기획서를 작성해줘.
```

개인 스킬 설치는 이 PC의 파일시스템 권한과 설정에 따라 별도 허용이 필요할 수 있다. 저장소를 내려받는 것만으로 모든 기존 대화에 자동 반영되는 것은 아니다.

## PC 간 동기화

작업 전 해당 로컬 저장소에서 최신 내용을 받는다.

```sh
git pull --ff-only
```

변경 후 `git status`와 `git diff`로 확인하고, 반영할 파일만 추가해 커밋한 뒤 업로드한다.

```sh
git add <변경한-파일>
git commit -m "Update document writing rules"
git push origin main
```

다른 PC에서는 다시 `git pull --ff-only`를 실행한다. 동시 수정으로 분기되었다면 변경 내용을 검토하여 병합한다. 원격 변경을 강제로 덮어쓰지 않는다.

## 관리 원칙

- 게임과 무관한 작성 규칙은 `default/`에 둔다.
- 게임 정보·개별 문서 분석·참고 문서 경로는 `references/<프로젝트>/`에 둔다.
- 새 프로젝트를 추가할 때는 프로젝트 안내를 만들고 `SKILL.md`에서 연결한다.
- 모델의 대화 기억 대신 Git에 저장한 파일을 기준으로 유지한다.
- 노션 링크의 접근 권한과 원문은 GitHub 동기화와 별개다. 계정 인증 정보는 저장하지 않는다.
