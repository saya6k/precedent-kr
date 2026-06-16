# AGENTS.md

이 저장소는 **대한민국 판례 데이터**다. 각 판례는 Markdown 파일이고, 각 판례의 선고일자가 Git commit date로 기록된다. 자세한 사용법은 스킬 [`precedent-kr`](.agents/skills/precedent-kr/SKILL.md)에 있다 — 판례 조회·검색·선고일자 조회 작업 전에 읽어라.

## 구조

```
{사건종류}/{법원등급}/{법원명}_{선고일자}_{사건번호}.md
```

- 사건종류: `민사` `형사` `일반행정` `세무` `가사` `특허` `선거·특별` `기타`
- 법원등급: `대법원` `하급심` `미분류`
- 각 파일 상단에 YAML frontmatter(`판례일련번호`, `사건번호`, `사건명`, `법원명`, `선고일자`, `출처` 등).

## 반드시 지킬 것

- **commit hash는 안정 식별자가 아니다.** 정규화 규칙 개선 시 저장소 전체가 재구성되고 **force-push**된다. 장기 참조는 hash가 아니라 **`판례일련번호` + `선고일자` + law.go.kr URL**로 하라. 동기화: `git fetch --all && git reset --hard origin/main`.
- **1970-01-01 이전 선고 판례**는 Git 한계로 commit 날짜가 1970-01-01로 고정된다. 실제 선고일은 frontmatter `선고일자`를 신뢰하라.
- **단기(檀紀)→서기 변환**: 일부 오래된 판례의 선고일자는 단기 연도를 `서기 = 단기 − 2333`으로 변환해 기록한다. 사건번호 속 단기 연도는 식별자라 보존된다.

## 이 포크에 대하여

`saya6k/precedent-kr`는 `legalize-kr/precedent-kr`의 포크이며, GitHub Actions(`.github/workflows/sync-upstream.yml`)가 **매일** 업스트림으로 **미러(hard-reset + force-push)**한다. 업스트림 콘텐츠를 통째로 덮어쓰므로 **데이터에 직접 커밋하지 마라 — 다음 동기화에 사라진다.** fork-local 파일(`AGENTS.md`, `.agents/`, sync 워크플로우)만 보존된다. 업스트림에는 어떤 쓰기도 하지 않는다(fetch 전용).
