# 초급 프로젝트 SEVEN: 김수민 개발 리포트
[SEVEN](https://github.com/singnyeo/nb02-seven-team2)

## 📌 프로젝트 개요  
**진행 기간**: 2025.06.02 ~ 2025.06.20  
**주제**: 운동 인증 커뮤니티 서비스  
> 사용자가 그룹을 생성하고 원하는 그룹에 참여하여 운동 기록을 남길 수 있는 커뮤니티형 서비스  

**목표**: 프론트엔드 코드와 연동되는 백엔드 API 설계 및 구현

---

## 💻 기술 스택

| **분류** | **사용 도구** |
| --- | --- |
| Backend | Node.js 22.0.0 LTS (Express) |
| Database | Prisma, PostgreSQL |
| API 문서화 | Swagger |
| 협업 도구 | Discord, GitHub ([🔗 레포지토리](https://github.com/singnyeo/nb02-seven-team2)), Notion ([📚 세부 계획](https://www.notion.so/206fca01d5c980689666cc5d59fbef08?pvs=21)) |
| 일정 관리 | GitHub Issues, Notion |

---

## 👨‍💻 담당 작업  

- 운동 기록 목록 조회 API 설계
- 중간 발표
- 그룹 관련 API 및 태그 API Postman 테스트
- 그룹 관련 Swagger 문서화 테스트
- 프론트 연동 테스트

---

## 🛠️ 기능 구현

### 📁 `records-controller.js`

- **운동 기록 목록 조회 API 설계**
  - `superstruct`를 활용한 `params`, `query` 유효성 검사
  - 페이지네이션, 정렬 (`createdAt`, `duration`), 검색 (`닉네임`), 필터링 (`운동 종류`) 기능 구현
  - Prisma ORM의 `findMany()` 및 `include` 옵션으로 사용자 및 사진 데이터 포함 응답
  - 그룹 존재 여부 확인 및 사용자 필터링 처리
  - 전역 오류 핸들러 적용

### 📁 `records.js`

- Express 라우터 등록 (`GET /groups/:groupId/records`)

### 기술적 성과 
* 백엔드 API 테스트 정상 작동
* 프론트 연동 정상 작동

## 🎤 발표 및 공유

[📊 중간 발표 자료 보기](https://www.miricanvas.com/v/14qg1rp)

* 📢 발표 내용 

  중간 발표에서 현재 팀원들의 진행 상황과 프로젝트에서 발견된 문제점, 그리고 향후 계획에 대해 설명

---

## 🧪 그룹 API 테스트 보고서

- 프론트엔드 요청 스펙에 맞춘 Postman 테스트 수행  
- Swagger 문서 기준으로 API 동작 여부 일치 확인 

- [🔗 테스트 계획서](https://www.notion.so/seven-210a1c7d0d6a80269a25f5476a37c7a3?source=copy_link)  
- [🔗 테스터 보고서](https://www.notion.so/seven-217a1c7d0d6a80388cdbc33daf0f60da?source=copy_link)

---

## 🧩 문제점 및 해결과정

1. **커밋 히스토리 관리**  
   - PR 승인 전에 main 브랜치 수정 시 PR 충돌 및 커밋 히스토리 꼬임 현상 발생. 경험 부족으로 판단.  
   - 충돌 최소화를 위해 로컬에서 충분히 수정 후 push하는 방식으로 개선.

2. **로컬 main 최신화**  
   - 매일 작업 시작 전 main 브랜치를 pull하지 않아 충돌이 커진 경우 발생.  
   - 한 번 충돌 경험 후부터는 작업 전 로컬 main 브랜치를 최신화하는 습관을 들임.

3. **중복되는 코드 인지 미흡**  
   - 코드 리뷰를 통해 팀원 피드백을 받고 중복 코드를 줄여 가독성을 높일 수 있었음.

4. **스키마 설계 관련 협업 문제**  
   - 초기 스키마 설계를 한 사람이 진행했으나, 지속적으로 추가·변경이 생기면서 모든 팀원이 커밋과 푸시를 반복하는 비효율 발생.  
   - 앞으로는 각자 맡은 부분의 스키마 설계를 분담하여 진행하는 것이 효율적일 것으로 판단.

5. **함수명, 파일명 관련 초기 커뮤니케이션 부족**  
   - 구현 도중 코드 컨벤션이 맞지 않는 부분이 발견되어 수정하는 시간이 필요했음.  
   - 미리 함수명, 파일명 규칙을 정하고 진행하면 수정 시간을 줄일 수 있을 것으로 생각됨.


## 🧩 개선 사항 제안

1. **유효성 검사 강화**
   - `groupId`는 `string`으로 받고 있으나, 숫자 변환 로직이 따로 있어 개선 필요
   - 미들웨어에서 처리하도록 개선

2. **정렬 필드 유연성 향상**
   - 현재 `orderBy`: `createdAt`, `duration` → 추후 `distance` 등 확장 고려

3. **에러 메시지 개선**
   - 사용자 입장에서 명확하고 직관적인 에러 메시지 제공 필요

4. **테스트 범위 확대**
   - 현재 Postman 수동 테스트에서 → 추후 Jest + Supertest 기반 자동화 테스트로 고려

---

## 🔁 회고

1. **Git 협업 경험 부족**  
   - 충돌 걱정으로 조심스럽게 작업 진행  
   - rebase 활용으로 커밋 히스토리 관리 효율화 경험하고 싶음

2. **전체 시스템 이해의 중요성**  
   - 코드 작성뿐 아니라 팀원 코드와 흐름 파악이 중요하다는 점 체감

3. **기능 설계 역량 강화 필요**  
   - 이번 프로젝트 API 구현 범위 제한적  
   - 다음 프로젝트에서는 더 다양한 기능 직접 설계 희망

4. **프론트-백엔드 연동 경험**  
   - 프론트 연동 테스트를 통해 사용자 흐름 이해도 향상

5. **문서화 및 협업 이해도 증가**  
   - Swagger 문서화 및 연동 테스트로 백엔드-프론트 구조 이해 증진


---

## 📎 첨부 
- [🔗 팀 레포지토리](https://github.com/singnyeo/nb02-seven-team2)
- [📚 세부 계획](https://www.notion.so/206fca01d5c980689666cc5d59fbef08?pvs=21)
- [📊 중간 발표 자료](https://www.miricanvas.com/v/14qg1rp)
- [🔗 테스트 계획서](https://www.notion.so/seven-210a1c7d0d6a80269a25f5476a37c7a3?source=copy_link)  
- [🔗 테스터 보고서](https://www.notion.so/seven-217a1c7d0d6a80388cdbc33daf0f60da?source=copy_link)
