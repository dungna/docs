---
id: PERM-02
title: Actor Registry
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-02 — Actor Registry

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký các actor trong Customer World, Workforce World, Partner World và System Actor. Đây là nguồn dùng để evaluate permission.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. Actor registry

| Actor ID | Actor group | Actor name | Primary surface/interface | Authority/source | Notes |
|---|---|---|---|---|---|
| ACT-CUS-MYF88 | Customer | MyF88 Customer / Borrower | MyF88 | Identity + Party Foundation | Khách hàng vay / sử dụng money access |
| ACT-CUS-NNX | Customer | NNX Customer / Policyholder | NNX | Identity + Party Foundation | Khách hàng bảo hiểm |
| ACT-CUS-FINVEST | Customer | FInvest Customer / Saver / Investor | FInvest | Identity + Party Foundation | Khách hàng tích lũy/đầu tư |
| ACT-CUS-SB-MEMBER | Customer | Social Banking Member | MyF88/FInvest | Social Banking Domain + Party | Thành viên nhóm tài chính cộng đồng |
| ACT-WF-SALES | Workforce | Sales / Advisor | OpsF88 | Workforce/HXP + Distribution | Tư vấn bán hàng/hỗ trợ khách |
| ACT-WF-AGENT | Workforce | Insurance Agent | OpsF88 | Distribution/Agent Network + LMS/HXP | Agent phải có certification/eligibility |
| ACT-WF-LOANOPS | Workforce | Lending Ops Staff | OpsF88 | OpsF88 + Lending Domain | Xử lý hồ sơ, chứng từ, exception |
| ACT-WF-UNDERWRITER | Workforce | Underwriter / Credit Reviewer | OpsF88 | Lending Domain delegated authority | Review/phê duyệt theo delegated authority |
| ACT-WF-CLAIM-SUPPORT | Workforce | Claims Support | OpsF88 | OpsF88 + Claims Domain | Hỗ trợ claim/chứng từ |
| ACT-WF-CLAIM-ASSESSOR | Workforce | Claims Assessor | OpsF88 | Claims Domain delegated authority | Thẩm định/đề xuất/duyệt claim theo cấp |
| ACT-WF-SUPERVISOR | Workforce | Supervisor / Queue Owner | OpsF88 | OpsF88 | Gán việc, giám sát queue/SLA |
| ACT-WF-COMPLIANCE | Workforce | Compliance Officer | OpsF88 | Compliance/Risk | Review, audit, moderation, incident |
| ACT-WF-MODERATOR | Workforce | Live Moderator | OpsF88 | ExOS/CXP + OpsF88 | Moderation livestream/shoppertainment |
| ACT-WF-PARTNEROPS | Workforce | Partner Operations Staff | OpsF88 | Partner Exchange + OpsF88 | Xử lý callback/SLA/incident |
| ACT-PARTNER-MB | Partner | MB Bank | Partner API | MB Bank | Banking truth owner |
| ACT-PARTNER-CIMB | Partner | CIMB | Partner API | CIMB | Partner funding/banking/product flow nếu áp dụng |
| ACT-PARTNER-INS | Partner | Insurance Partner / Insurer | Partner API/Portal | Insurance Partner | Policy/claim truth nếu partner-owned |
| ACT-PARTNER-INVEST | Partner | Securities/Fund/Bond Partner | Partner API | Licensed Partner | Investment account/order/holding truth |
| ACT-PARTNER-PAYMENT | Partner | Payment/Wallet Partner | Partner API | Payment Partner | Payment execution/status |
| ACT-SYS-MYF88-BFF | System | MyF88 BFF / Channel Service | BFF | Channel Service owner | Compose/route/projection only |
| ACT-SYS-NNX-BFF | System | NNX BFF / Channel Service | BFF | Channel Service owner | Compose/route/projection only |
| ACT-SYS-FINVEST-BFF | System | FInvest BFF / Channel Service | BFF | Channel Service owner | Compose/route/projection only |
| ACT-SYS-OPSF88-BFF | System | OpsF88 BFF / Channel Service | BFF | OpsF88 Platform | Workforce/ops compose only |
| ACT-SYS-EXOS | System | ExOS/CXP | ExOS/CXP | ExOS/CXP | Campaign/NBA/NBO/engagement/attribution |
| ACT-SYS-PERMIT | System | Permit Service | Shared Foundation | Permit Foundation | Quyết định ALLOW/DENY/CONDITIONAL_ALLOW |
| ACT-SYS-NOTI | System | Notification/CCM Service | Shared Foundation | Notification/CCM | Delivery state/notification controls |
| ACT-SYS-AUDIT | System | Audit Platform | Shared Foundation | Audit Platform | Ghi audit trail |


## 4. Actor attribute registry

| Attribute | Applies to | Description | Example |
|---|---|---|---|
| actor_id | All | ID actor kỹ thuật | user_id, staff_id, partner_id, service_id |
| actor_type | All | Customer/Workforce/Partner/System | Customer |
| party_id | Customer | Party/customer reference | PTY-001 |
| workforce_id | Workforce | Staff/agent identifier | STF-001 |
| partner_id | Partner | Partner identifier | MB, CIMB |
| role_code | Workforce/System | Role nghiệp vụ/kỹ thuật | CLAIM_ASSESSOR |
| org_scope | Workforce | Chi nhánh/vùng/team | REGION_HN |
| product_scope | Workforce/Partner | Product allowed | INSURANCE, LENDING |
| certification_status | Agent/Workforce | Certification còn hiệu lực không | ACTIVE |
| assigned_case_id | Workforce | Case được giao | CASE-001 |
| device_trust_level | Customer/Workforce | Trust của thiết bị | TRUSTED/UNKNOWN |
