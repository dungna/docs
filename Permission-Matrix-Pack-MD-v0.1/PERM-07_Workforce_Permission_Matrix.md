---
id: PERM-07
title: Workforce Permission Matrix
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-07 — Workforce Permission Matrix

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký quyền workforce: sales, agent, ops, underwriter, claim support, supervisor, compliance. Trọng tâm là role + scope + purpose + case/workitem + audit, không cấp quyền rộng theo role.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. Workforce permission matrix

| Use Case ID | Actor | Object | Action | Purpose | Scope condition | Required controls | Decision |
|---|---|---|---|---|---|---|---|
| UC-WF-001 | Sales/Advisor | Customer/Lead | ACT.READ | PURP.OPS_PROCESSING | Assigned lead/customer | CTRL.AUTHN, CTRL.SCOPE, CTRL.PURPOSE, CTRL.AUDIT | ALLOW |
| UC-WF-002 | Sales/Advisor | OBJ.LOAN_APPLICATION | ACT.CREATE | PURP.LOAN_APPLY | Assisted journey | CTRL.CONSENT, CTRL.PERMIT, CTRL.AUDIT | CONDITIONAL_ALLOW |
| UC-WF-003 | Sales/Advisor | OBJ.LOAN_APPROVAL | ACT.DECIDE | PURP.LOAN_APPLY | N/A | N/A | DENY |
| UC-WF-004 | Loan Ops | OBJ.LOAN_APPLICATION | ACT.READ | PURP.OPS_PROCESSING | Assigned workitem/queue | CTRL.CASE, CTRL.SCOPE, CTRL.AUDIT | ALLOW |
| UC-WF-005 | Loan Ops | OBJ.DOCUMENT | ACT.UPDATE | PURP.OPS_PROCESSING | Assigned case | CTRL.CASE, CTRL.EVIDENCE, CTRL.AUDIT | ALLOW evidence update |
| UC-WF-006 | Underwriter | OBJ.LOAN_APPROVAL | ACT.DECIDE | PURP.LOAN_APPLY | Assigned queue + delegated authority | CTRL.CASE, CTRL.AUTHORITY, CTRL.PERMIT, CTRL.AUDIT | ALLOW/ESCALATE |
| UC-WF-007 | Agent | OBJ.INS_QUOTE | ACT.CREATE | PURP.INS_QUOTE | Assigned lead + certification | CTRL.CONSENT, CTRL.SCOPE, CTRL.PERMIT, CTRL.AUDIT | ALLOW |
| UC-WF-008 | Agent | OBJ.POLICY | ACT.READ | PURP.INS_QUOTE | Assigned customer/lead | CTRL.SCOPE, CTRL.PURPOSE, CTRL.AUDIT | CONDITIONAL_ALLOW limited |
| UC-WF-009 | Agent | OBJ.CLAIM_DECISION | ACT.DECIDE | PURP.CLAIM_SUPPORT | N/A | N/A | DENY |
| UC-WF-010 | Claim Support | OBJ.CLAIM_INTAKE | ACT.READ | PURP.CLAIM_SUPPORT | Assigned case | CTRL.CASE, CTRL.PURPOSE, CTRL.AUDIT | ALLOW |
| UC-WF-011 | Claim Support | OBJ.DOCUMENT | ACT.UPDATE | PURP.CLAIM_SUPPORT | Assigned case | CTRL.CASE, CTRL.EVIDENCE, CTRL.AUDIT | ALLOW |
| UC-WF-012 | Claim Assessor | OBJ.CLAIM_ASSESSMENT | ACT.UPDATE | PURP.CLAIM_SUPPORT | Assigned queue/case | CTRL.CASE, CTRL.AUTHORITY, CTRL.AUDIT | ALLOW |
| UC-WF-013 | Claim Assessor/Manager | OBJ.CLAIM_DECISION | ACT.DECIDE | PURP.CLAIM_SUPPORT | Delegated authority | CTRL.AUTHORITY, CTRL.PERMIT, CTRL.AUDIT, CTRL.DUAL if high value | ALLOW/ESCALATE |
| UC-WF-014 | Partner Ops | OBJ.MB_ACCOUNT_STATUS | ACT.READ | PURP.PARTNER_RECON | Assigned partner case | CTRL.CASE, CTRL.CONTRACT, CTRL.AUDIT | ALLOW |
| UC-WF-015 | Partner Ops | Partner callback issue | ACT.OPERATE | PURP.PARTNER_RECON | Assigned case | CTRL.CASE, CTRL.CONTRACT, CTRL.IDEMPOTENCY, CTRL.AUDIT | ALLOW |
| UC-WF-016 | Moderator | OBJ.SHOPPERTAINMENT | ACT.MODERATE | PURP.COMPLIANCE_REVIEW | Assigned live session | CTRL.CASE, CTRL.PURPOSE, CTRL.AUDIT | ALLOW |
| UC-WF-017 | Compliance Supervisor | OBJ.SHOPPERTAINMENT | ACT.KILL | PURP.COMPLIANCE_REVIEW | Kill authority | CTRL.PERMIT, CTRL.AUDIT, CTRL.KILL_SWITCH | ALLOW |
| UC-WF-018 | Ops Staff | OBJ.SB_LEDGER | ACT.UPDATE | PURP.SOCIAL_BANKING | N/A | N/A | DENY direct update |
| UC-WF-019 | Ops Staff | OBJ.DISPUTE | ACT.OPERATE | PURP.OPS_PROCESSING | Assigned case | CTRL.CASE, CTRL.AUDIT | ALLOW |
| UC-WF-020 | Supervisor | OBJ.WORKITEM | ACT.ASSIGN | PURP.OPS_PROCESSING | Queue owner | CTRL.SCOPE, CTRL.AUDIT | ALLOW |


## 4. Workforce access rules

| Rule | Description |
|---|---|
| Case-bound | Staff chỉ xem/làm trong case/workitem/queue được giao |
| Purpose-bound | Access phải có mục đích công việc hợp lệ |
| Delegated authority | DECIDE action cần authority được ủy quyền |
| Certification-bound | Agent chỉ bán/tư vấn sản phẩm khi certification/eligibility active |
| No universal customer access | Không actor workforce nào được xem toàn bộ customer data mặc định |
| Audit by default | Workforce access với customer/product object phải audit |
