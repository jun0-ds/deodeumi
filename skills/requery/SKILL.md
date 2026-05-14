---
name: requery
description: Agentic retrieval cycle — 원래 질문이 한 번에 hit 안 되면 변환·시점·결을 바꿔 재질문하는 protocol. substrate 내부 정형/반정형/비정형 자료를 가로지른다. Letta filesystem 결(LoCoMo 74% > Mem0 graph 68.5%)의 적용. 도구가 아닌 규율.
user-invocable: true
---

# Requery — Agentic Retrieval Cycle

`requery`는 *반복 쿼리 재구성*. 원래 질문 한 번으로 답을 못 찾았을 때 *질문을 변환해 다시 검색*하는 protocol. 도구 추가가 아닌 **규율 명시**다.

근거: Letta blog *Is a Filesystem All You Need?* (LoCoMo QA) — filesystem 기반 단순 도구(grep + search_files) + agent 자율성이 graph 기반(Mem0) 68.5%를 74%로 능가. **정확도의 핵심은 retrieval 메커니즘 정교화가 아닌 *반복 쿼리 재구성*.**

---

## 발동 시점

다음 신호가 잡힐 때:

1. **첫 질문 hit miss** — 인덱스·헤더·grep 한 번에 못 잡음
2. **carry forward 누락 의심** — bridge-note·agenda에 "그거 어디 박았지" 발생
3. **stale 의심** — 이름·경로·framing이 *변했을 수 있는* 정보
4. **추상↔구체 갭** — 사용자가 추상으로 요청 / 본문은 구체 표현 (또는 역)

발동 *안 하는* 자리: 첫 질문 hit이면 즉시 종료. 사이클 강제 X.

---

## 3-tier 데이터 결과 retrieval 결

| tier | 예시 | 1차 메커니즘 |
|------|------|------------|
| 정형 | MEMORY·인덱스, frontmatter, ADR supersedes, agenda 체크박스 | grep + index Read |
| 반정형 | thread 헤더(`## ⎯ ...⎯`), devlog 파일명(`{date}_{slug}.md`), journal 헤더(`## YYYY-MM-DD [hostname]`) | head/grep + 본문 Read |
| 비정형 | journal body, notes inbox, scribe bridge-note body, devlog narrative | `rg` + 반복 쿼리 재구성 |

정형이 정합도 높으면 *cycle 한 번에 종료*. 반정형으로 떨어지면 cycle 한두 번. 비정형은 사이클 여러 번 자연.

---

## 6단계 protocol

```
1. 질문 받음 (사용자 / self-surface)
2. 정형 hit 시도 — MEMORY → domain → ADR supersedes
3. miss → 반정형 — bridge-note thread 헤더, devlog 날짜, journal 헤더
4. miss → 비정형 — rg + 본문 Read
5. 여전히 miss → 질문 재구성 → 2부터 다시 (휴리스틱 4종 적용)
6. n번 사이클 후 miss → external surface — 사용자에게 명시
```

### 단계 5의 휴리스틱 4종

| 휴리스틱 | 적용 자리 | 예시 |
|---------|---------|------|
| **동의어** | 이름·호칭 stale | "준선생" → "류선생" / "언선생" → "김이박" |
| **시점 변경** | 날짜·thread 분기 | "5/14 작업" → "다섯 번째 thread" / "어제" → "전 세션 carry forward" |
| **추상↔구체** | 라벨 vs 항목 | "agenda" → "[ ] 더듬이 v0.x 첫 단위" |
| **결 변경** | 정책·구현·운영 | "더듬이 정의" → "load-bearing function" → "retrieval cycle" |

각 휴리스틱은 *질문을 다른 표현으로 변환*해 매칭 재시도. 사이클 횟수 명시 limit 없음 — 통증 인지 시 cycle 길이를 stale 신호로 사용.

---

## 자제선 (deflationary)

1. **도구 추가 안 함** — embedding·BM25·graph index는 통증 누적 *후* 결정. 본 SKILL은 *규율 명시*이지 *인덱스 빌드*가 아님
2. **사이클 자동화 안 함** — agent가 단계마다 *판단*하는 자리. 자동 retrieval pipeline X
3. **정확도 metric 명시 측정 안 함** — Letta blog 결: "메모리는 *도구를 잘 쓰는 능력*". 측정 강박이 정확도 자체보다 큰 자리 — 통증 *인지*가 메트릭

---

## 손맛 vs 더듬이 경계

| 측면 | 손맛 (sonmat) | 더듬이 (deodeumi) |
|------|--------------|-----------------|
| 결 | thinking discipline | retrieval discipline |
| 대상 | 사고 흐름·검증·기록 | 정보 도달·원본 추적 |
| 발동 | System 1 신호 (inspect), 결정 직전 (devil), 마무리 (punch) | 질문 hit miss, carry forward 누락, stale 의심 |
| SKILL 예 | `devil`·`inspect`·`punch`·`autoloop`·`scribe`·`guard` | `requery` (첫 SKILL) |

두 컴포넌트는 *별도 자리*. 결합 시: 손맛이 *답이 맞는지 검증* / 더듬이가 *답에 도달하는 경로 추적*.

---

## 예시 (시연 — 안채 instance 패턴)

**질문**: "더듬이 5/14에 뭐 결정했지?"

```
1. 정형 hit — desk/memory/MEMORY.md 인덱스에서 "더듬이" grep
   → domain/deodeumi.md 발견. 정의 가설 1차 박힘 + public 추출 결정 확인
2. (필요 시) 반정형 — bridge-note 5/14 thread "여섯 번째" head 5줄
3. (사이클 종료) 정형 hit 충분

총 cycle = 1 (정형). 종료.
```

**질문**: "더듬이 함수 정의가 *원래 어떻게* 박혀 있었지?"

```
1. 정형 — domain/deodeumi.md 인덱스에 hit. 단 *original* 정의는 *현재 박힘 정의* 아님
2. 휴리스틱 시점 변경 → "원래 / 부트스트랩 / 5/7" 재질문
3. devlog 2026-05-07_experiment-and-bootstrap.md head — 원본 framing 발견
4. (또는) bedrock/deodeumi 리포 git log — initial commit 시점 본문

총 cycle = 2~3 (시점 휴리스틱). 종료.
```

---

## 채택 (instance 측)

이 SKILL은 *함수 자리*의 첫 본문. 채택하는 instance는 자기 substrate 구조(memory 경로·devlog cadence·bridge-note thread 형식)에 맞춰 *3-tier 매핑*과 *6단계 protocol*을 자기 결로 변형한다.

레퍼런스 instance: `jun0-ds/munteok-anchae` (private) — `desk/memory/domain/deodeumi.md`에 우리 적용 사연·외부 reference 1차 fact·통증 측정 자리 거주.
