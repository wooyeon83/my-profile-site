---
description: '현재 브랜치를 원격 저장소에 안전하게 푸시합니다'
allowed-tools:
  [
    'Bash(git push:*)',
    'Bash(git status:*)',
    'Bash(git log:*)',
    'Bash(git branch:*)',
    'Bash(git remote:*)',
    'Bash(git diff:*)',
  ]
---

# Claude 명령어: Push

현재 브랜치를 원격 저장소에 안전하게 푸시합니다.

## 사용법

```
/git:push              # 현재 브랜치 푸시
/git:push --force      # 강제 푸시 (주의: 히스토리 덮어씀)
/git:push --dry-run    # 실제 푸시 없이 결과 미리 확인
```

## 프로세스

1. 현재 브랜치 및 원격 연결 상태 확인
2. 푸시할 커밋 목록 표시
3. main/master 브랜치 푸시 시 사용자 확인 요청
4. 업스트림 미설정 시 `-u` 옵션으로 자동 설정
5. 푸시 실행 및 결과 보고

## 안전 규칙

- **main/master 브랜치**: 반드시 사용자에게 확인 후 푸시
- **force push**: `--force-with-lease` 사용 (타인 커밋 보호)
- **미커밋 변경사항**: 푸시 전 경고 표시
- **원격 브랜치 앞선 경우**: pull 먼저 권장

## 푸시 전 점검 항목

1. **미커밋 변경사항 확인** — 작업 내용 누락 방지
2. **원격과의 차이 확인** — 충돌 가능성 사전 감지
3. **푸시 대상 커밋 목록** — 의도치 않은 커밋 포함 방지

## 출력 예시

```
🔍 푸시 전 점검 중...

브랜치: feature/user-auth → origin/feature/user-auth
푸시할 커밋 (2개):
  abc1234 ✨ feat: 로그인 폼 컴포넌트 추가
  def5678 🔧 chore: 인증 관련 설정 추가

✅ 푸시를 진행합니다...
✅ origin/feature/user-auth 업데이트 완료
```

## 참고사항

- 업스트림 브랜치가 없으면 `git push -u origin <브랜치명>` 자동 실행
- force push는 명시적으로 `--force` 인자를 전달한 경우에만 실행
- **main/master에 직접 force push는 절대 금지**
