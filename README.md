# deodeumi (더듬이) — substrate retrieval + path orchestration 함수의 자리

문턱(munteok) 시스템에서 *어떤 정보가 어디 있는지 더듬어 도달하고 · 무엇을 할지 · 어떤 순서로 · 언제 에스컬레이트할지* — 세션을 가로지르는 **substrate-내부 retrieval + 경로찾기 함수**가 사는 자리.

3-layer로 보면: kernel(`bedrock/sonmat/` — 어떻게 생각) / data(`hearth/` + `desk/` — 정체성·메모리·작업) / **management(deodeumi — 정보 도달 + 어디로 갈지 더듬기)**. 이름 = 곤충의 더듬이. 중앙 설계자 없이 환경을 *더듬어* 길을 찾는 기관.

## 정의 (2026-05-14)

> "정리된 데이터·정리되지 않은 데이터 모두에서 어떻게 하면 정보탐색을 잘 타고들어가서 원본의 내용을 정확하게 찾을 것인가."

→ load-bearing function = **substrate 내부 hybrid retrieval (정형/반정형/비정형 모두 내성) + path orchestration**.

두 면 결합:
- retrieval 없는 orchestration = *blind 경로찾기* (어디 갈지 결정할 자료 부족)
- orchestration 없는 retrieval = *맥락 없는 매칭* (찾아도 다음 행위와 연결 안 됨)

## 자리만, 구현은 아직 (v0.x TBD)

이 리포는 *함수 자리의 정의*만 둔다. 구현은 *통증이 누적된 후* 명세한다 (deflationary).

후보 카테고리 (commitment 아님):
- 정형 인덱스 강화 — frontmatter·인덱스·cross-link `[[name]]`
- 반정형 thread/heading 표준화
- **반복 쿼리 재구성 protocol** — agentic retrieval cycle (Letta filesystem 결: LoCoMo 74% > Mem0 graph 68.5%)
- hybrid index (BM25 + semantic + RRF; semble_rs 결) — *통증 누적 전 도구화 금지*
- graph traversal (ADR supersedes·`[[name]]` lineage)

## 채택 (instance 측 사연)

deodeumi는 *함수 자리*. 채택하는 instance(개인 안채·팀 substrate·company brain 등)는 자기 사연·자기 protocol·자기 자제선을 자기 instance에 박는다. 이 리포에는 *공통 함수 정의*만, 사연은 안채에 — 5/13 [`jun0-ds/munteok`](https://github.com/jun0-ds/munteok) framework/안채 분리 결과 적용.

레퍼런스 instance: `jun0-ds/munteok-anchae` (private, 작성자 본인) — domain memory의 deodeumi 항목에 외부 reference 1차 fact (semble_rs·ripgrep·ugrep `--fuzzy`·astgrep·mem0·letta·zep·cognee·graphiti·hermes·pi) + 3-tier 데이터 매핑 + 반복 쿼리 재구성 6단계 protocol + 우리 instance v0 practice/5-layer 부록 거주.

## 관련 자리

- [`jun0-ds/munteok`](https://github.com/jun0-ds/munteok) — 문턱(munteok) framework. 4-zone 정의 (bedrock·hearth·desk·madang)
- [`jun0-ds/sonmat`](https://github.com/jun0-ds/sonmat) — 손맛, thinking discipline (kernel 측)
- [`jun0-ds/bobusang`](https://github.com/jun0-ds/bobusang) — 보부상, 디바이스 싱크 (운영 도구)

## License

BSD 3-Clause
