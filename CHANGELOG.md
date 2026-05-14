# Changelog — deodeumi (더듬이)

All notable changes to deodeumi. Format loosely follows [Keep a Changelog](https://keepachangelog.com/).

**Versioning policy**: SemVer tag held back until external fork·breaking change·sustained API surface triggers it. Until then, changes accumulate under *Unreleased*.

**Scope**: substrate retrieval + path orchestration 함수의 *공통 자리* 정의. 채택 instance의 구현 사연(우리 사용자의 v0 practice·자제선)은 이 리포 밖 — instance README가 가리키는 자리.

---

## [Unreleased]

### Added (2026-05-14)
- `skills/requery/SKILL.md` — 첫 SKILL. agentic retrieval cycle (반복 쿼리 재구성) 6단계 protocol + 휴리스틱 4종(동의어·시점·추상↔구체·결) + 3-tier 데이터(정형/반정형/비정형) retrieval 매핑 + 손맛 vs 더듬이 경계 절. Letta filesystem 결(LoCoMo 74% > Mem0 graph 68.5%) 적용. 도구가 아닌 protocol 명시 (plugin 미등록 — 통증 누적 시 plugin화 검토)
- `skills/` 디렉토리 — 방법론 SKILL 자리

### Notes
- 후보 카테고리 (commitment 아님, README "v0.x TBD" 절 참조): 정형 인덱스 강화·반정형 thread/heading 표준화·hybrid index(BM25+semantic+RRF, semble_rs 결)·graph traversal(ADR supersedes·`[[name]]` lineage). 통증 누적 전 도구화 금지

---

## [2026-05-14 — initial public extraction]

### Added
- Repository initial commit (`8b11f8b`) — README + LICENSE (BSD 3-Clause) + .gitignore
- README: 함수 자리 정의 (substrate 내부 hybrid retrieval + path orchestration, 두 면 결합 — retrieval 없는 orchestration = blind, orchestration 없는 retrieval = 맥락 없는 매칭) + 3-layer 위치 + 이름 어원 + 채택 모델 + 관련 자리 (munteok·sonmat·bobusang)

### Context
- `munteok-anchae`에서 5/7 부트스트랩 시 `bedrock/deodeumi/` 디렉토리로 시작. 7일간 "함수 자리"는 박혀있었으나 load-bearing function 약함
- 2026-05-14 사용자 framing 격상으로 load-bearing function 명료화 — *정리/비정리 데이터 모두에서 정보탐색을 잘 타고들어가서 원본을 정확히 찾기*
- 같은 날 public 추출 결정 (5/13 framework/안채 분리 결의 4번째 컴포넌트, ADR-0007 submodule mount 패턴 적용 사례)
- minimal "자리만 만들기" 결로 진행 — instance 사연(v0 practice·자제선·external reference 1차 fact)은 채택 instance에 단일 SoT 유지

---

## Conventions

- **SKILL 추가/변경**은 *Added*/*Changed* 절. SKILL은 *protocol 명시*이지 *구현 강제* 아님
- **README 본문 의미 변화**(정의·자리·채택 모델)는 *Changed* 절
- **외부 reference 차용 추가**는 본문에 명시 + Changelog 한 줄
- 작은 typo·문구 조정은 기록 안 함 (`git log`만)

## Related repos

- 채택 instance (reference): `jun0-ds/munteok-anchae` (private) — `desk/memory/domain/deodeumi.md`가 외부 reference 1차 fact·3-tier 매핑·자제선·통증 측정 자리·v0 practice·5-layer 부록 거주
- 문턱 framework: [`jun0-ds/munteok`](https://github.com/jun0-ds/munteok)
- 손맛 (thinking discipline kernel): [`jun0-ds/sonmat`](https://github.com/jun0-ds/sonmat) — 손맛/더듬이 경계는 `skills/requery/SKILL.md` 안 절 참조
