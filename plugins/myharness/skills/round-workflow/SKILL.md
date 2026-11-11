---
name: round-workflow
description: 라운드 단위로 개발을 진행할 때 사용한다. 라운드를 시작하거나, spec · plan · review 문서를 쓰거나, 라운드를 끝내기 전에 종료 조건을 점검할 때 따른다.
---

# 라운드 단위 개발

개발은 라운드 단위로 진행한다. 문서 위치나 테스트 · 린트 명령이 프로젝트의 CLAUDE.md에 따로 적혀 있으면 그것을 따른다.

## 문서 구조
- `docs/ROADMAP.md`: 개발 전에 정한 라운드 계획. 지금 어느 라운드인지는 여기서 확인한다.
- `docs/SSOT.md`: 진실의 원천. 지금 서비스의 API, 데이터 모델, 규칙.
- `docs/roundNN/`: 라운드마다 `spec.md` → `plan.md` → `review.md` 순서로 쓴다.

## 진행 순서
1. `docs/ROADMAP.md`에서 이번 라운드를 확인한다.
2. `spec.md`에 무엇을 만들지 적는다.
3. `plan.md`에 어떻게 만들지 적고 구현한다.
4. verifier 에이전트로 spec 기준 검증을 받는다.
5. cleaner 에이전트로 정리한다.
6. `review.md`에 결과를 적고 아래 종료 조건을 점검한다.

## Hook에 막혔을 때
- Hook에 막힌 작업은 다른 명령으로 우회하지 말고 멈춰서 사람에게 보고한다.

## 라운드 종료 조건
라운드를 끝내기 전에 아래를 모두 지킨다. 하나라도 안 되면 끝났다고 보고하지 않는다.
1. `docs/roundNN/spec.md` · `plan.md` · `review.md`가 지금 코드와 맞는다.
2. `docs/SSOT.md`를 지금 코드 기준으로 고쳤다. (현재 라운드, API 목록, 데이터 모델)
3. cleaner 에이전트로 죽은 코드를 정리했고, 결과를 `review.md`에 적었다.
4. 프로젝트의 테스트와 린트가 통과한다.
5. `docs/ROADMAP.md`에서 이번 라운드를 완료로 표시했다.
