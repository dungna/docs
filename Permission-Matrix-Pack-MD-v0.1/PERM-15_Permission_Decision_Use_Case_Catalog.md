---
id: PERM-15
title: Permission Decision Use Case Catalog
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-15 — Permission Decision Use Case Catalog

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Catalog use case áp dụng mô hình permission cho từng action cần đánh giá. File này là nơi BA/DEV/QC thêm use case mới theo cùng format.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. Use case catalog template

| Field | Required | Description |
|---|---:|---|
| use_case_id | Yes | Stable ID, e.g. UC-LOAN-001 |
| actor_id | Yes | Link PERM-02 |
| surface/interface | Yes | MyF88/NNX/FInvest/OpsF88/Partner API/System |
| object_id | Yes | Link PERM-04 |
| action_code | Yes | Link PERM-03 |
| purpose_code | Yes | Link PERM-12 |
| authority | Yes | Derived from object registry |
| required_controls | Yes | Link control IDs |
| decision | Yes | ALLOW/DENY/CONDITIONAL_ALLOW/ESCALATE |
| audit_level | Yes | Link PERM-13 |
| notes | No | Special handling |

## 4. Customer use cases

| Use Case ID | Actor | Surface | Object | Action | Purpose | Required controls | Decision |
|---|---|---|---|---|---|---|---|
| UC-CUS-001 | Customer | MyF88/NNX/FInvest | OBJ.IDENTITY | ACT.READ | PURP.AUTH | CTRL.AUTHN, CTRL.SESSION | ALLOW self |
| UC-CUS-002 | Customer | MyF88 | OBJ.LOAN_APPLICATION | ACT.CREATE | PURP.LOAN_APPLY | CTRL.AUTHN, CTRL.IDENTITY, CTRL.CONSENT, CTRL.PERMIT, CTRL.AUDIT | ALLOW self |
| UC-CUS-003 | Customer | MyF88 | OBJ.LOAN_CONTRACT | ACT.READ | PURP.SERVICE | CTRL.AUTHN, CTRL.PARTY, CTRL.PERMIT, CTRL.FRESHNESS | ALLOW self |
| UC-CUS-004 | Customer | MyF88 | OBJ.LOAN_APPROVAL | ACT.DECIDE | PURP.LOAN_APPLY | N/A | DENY |
| UC-CUS-005 | Customer | MyF88 | OBJ.REPAYMENT_OBLIGATION | ACT.READ | PURP.REPAYMENT | CTRL.AUTHN, CTRL.PARTY, CTRL.FRESHNESS | ALLOW self |
| UC-CUS-006 | Customer | MyF88 | OBJ.PAYMENT_EXECUTION | ACT.EXECUTE | PURP.REPAYMENT | CTRL.AUTHN, CTRL.PERMIT, CTRL.IDEMPOTENCY, CTRL.AUDIT | CONDITIONAL_ALLOW via payment contract |
| UC-CUS-007 | Customer | NNX | OBJ.POLICY | ACT.READ | PURP.SERVICE | CTRL.AUTHN, CTRL.PARTY, CTRL.FRESHNESS | ALLOW self |
| UC-CUS-008 | Customer | NNX | OBJ.CLAIM_INTAKE | ACT.CREATE | PURP.CLAIM_SUPPORT | CTRL.AUTHN, CTRL.CONSENT, CTRL.EVIDENCE, CTRL.AUDIT | ALLOW self |
| UC-CUS-009 | Customer | NNX | OBJ.CLAIM_DECISION | ACT.DECIDE | PURP.CLAIM_SUPPORT | N/A | DENY |
| UC-CUS-010 | Customer | FInvest | OBJ.PORTFOLIO_PROJECTION | ACT.READ | PURP.INVEST_DISCOVERY | CTRL.AUTHN, CTRL.CONSENT, CTRL.FRESHNESS | ALLOW if consent/source valid |
| UC-CUS-011 | Customer | FInvest | OBJ.INVEST_ORDER | ACT.EXECUTE | PURP.INVEST_HANDOFF | CTRL.CONTRACT, CTRL.CONSENT | DENY in F88 app / handoff to partner |
| UC-CUS-012 | Customer | MyF88/FInvest | OBJ.SB_GROUP | ACT.READ | PURP.SOCIAL_BANKING | CTRL.AUTHN, CTRL.CONSENT, membership/scope | ALLOW member |
| UC-CUS-013 | Customer | MyF88/FInvest | OBJ.SB_LEDGER | ACT.UPDATE | PURP.SOCIAL_BANKING | N/A | DENY |
| UC-CUS-014 | Customer | MyF88 | OBJ.MB_ACCOUNT_STATUS | ACT.READ | PURP.BANKING_HANDOFF | CTRL.CONSENT, CTRL.CONTRACT, CTRL.FRESHNESS | ALLOW projection only |
| UC-CUS-015 | Customer | MyF88 | OBJ.MB_ACCOUNT | ACT.CREATE | PURP.BANKING_HANDOFF | CTRL.CONSENT, CTRL.CONTRACT, CTRL.EKYC if available | DENY in F88 / handoff to MB |
| UC-CUS-016 | Customer | App surfaces | OBJ.CAMPAIGN | ACT.READ | PURP.MARKETING | CTRL.CONSENT/suppression if marketing | ALLOW if eligible |
| UC-CUS-017 | Customer | App surfaces | OBJ.SHOPPERTAINMENT | ACT.READ | PURP.LIVE_INTENT | Consent if intent capture | ALLOW join/view |
| UC-CUS-018 | Customer | App surfaces | OBJ.SHOPPERTAINMENT | ACT.CREATE | PURP.LIVE_INTENT | CTRL.CONSENT, CTRL.AUDIT | ALLOW intent capture if consent |


## 5. Workforce use cases

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


## 6. Partner use cases

| Use Case ID | Partner | Object/Data | Action | Purpose | Required controls | Decision |
|---|---|---|---|---|---|---|
| UC-PART-001 | MB Bank | OBJ.EKYC | ACT.SHARE/receive | PURP.BANKING_HANDOFF | CTRL.CONSENT, CTRL.CONTRACT, payload schema, CTRL.AUDIT | ALLOW if contract valid |
| UC-PART-002 | MB Bank | OBJ.MB_ACCOUNT_STATUS | ACT.UPDATE/callback | PURP.BANKING_HANDOFF | CTRL.CONTRACT, signature, CTRL.IDEMPOTENCY, CTRL.AUDIT | ALLOW callback |
| UC-PART-003 | MB Bank | F88 internal case | ACT.READ | PURP.PARTNER_RECON | N/A | DENY unless explicit escalation contract |
| UC-PART-004 | Zalo/MoMo | Lead payload | ACT.SHARE/send | Referral/lead | Consent/disclosure, payload contract, attribution | ALLOW if contract valid |
| UC-PART-005 | Insurance Partner | OBJ.POLICY | ACT.UPDATE/callback | PURP.SERVICE | Partner contract, schema, audit | ALLOW if partner authority |
| UC-PART-006 | Insurance Partner | OBJ.CLAIM_DECISION | ACT.DECIDE/update | PURP.CLAIM_SUPPORT | Partner/domain contract, delegated model | ALLOW if authority |
| UC-PART-007 | Investment Partner | OBJ.INVEST_ORDER | ACT.EXECUTE | PURP.INVEST_HANDOFF | License/contract, suitability/disclosure, audit | ALLOW at partner |
| UC-PART-008 | Investment Partner | OBJ.PORTFOLIO_PROJECTION | ACT.SHARE/send | PURP.INVEST_DISCOVERY | Consent, contract, timestamp/freshness | ALLOW projection |
| UC-PART-009 | Payment Partner | OBJ.PAYMENT_EXECUTION | ACT.EXECUTE/callback | PURP.REPAYMENT | Payment contract, idempotency, reconciliation | ALLOW |
| UC-PART-010 | Partner | Other partner data | ACT.READ | Any | N/A | DENY |


## 7. System actor use cases

| Use Case ID | System Actor | Object | Action | Allowed | Forbidden | Required controls |
|---|---|---|---|---|---|---|
| UC-SYS-001 | MyF88 BFF | Domain projection | ACT.READ | Compose projection | Read DB directly | CTRL.CONTRACT, CTRL.FRESHNESS, correlation_id |
| UC-SYS-002 | MyF88 BFF | Domain command | ACT.CREATE/UPDATE route | Route command on behalf of customer | Decide/approve/execute truth | CTRL.PERMIT, CTRL.AUDIT, correlation_id |
| UC-SYS-003 | NNX BFF | Claim projection | ACT.READ | Display projection | Decide claim | CTRL.CONTRACT, CTRL.FRESHNESS |
| UC-SYS-004 | FInvest BFF | Portfolio projection | ACT.READ | Display with timestamp | Create holding/order truth | CTRL.CONTRACT, CTRL.FRESHNESS |
| UC-SYS-005 | OpsF88 BFF | WorkItem/Case | ACT.READ/OPERATE route | Compose ops views | Change product truth | CTRL.CASE, CTRL.SCOPE, CTRL.AUDIT |
| UC-SYS-006 | ExOS/CXP | OBJ.CAMPAIGN | ACT.CREATE/UPDATE | Campaign/NBA/NBO | Product approval/claim decision | CTRL.CONSENT, CTRL.AUDIT |
| UC-SYS-007 | ExOS/CXP | Lead/intent | ACT.CREATE | Capture/attribute intent | Execute regulated transaction | CTRL.CONSENT, CTRL.AUDIT |
| UC-SYS-008 | Notification/CCM | OBJ.NOTIFICATION | ACT.EXECUTE | Deliver notification | Override legal/critical suppression wrongfully | Consent/notification ownership/audit |
| UC-SYS-009 | Permit Service | OBJ.PERMIT | ACT.DECIDE | ALLOW/DENY | Mutate domain truth | Policy registry/audit |
| UC-SYS-010 | Audit Platform | OBJ.AUDIT | ACT.CREATE | Write audit | Delete audit | Append-only controls |


## 8. OpsF88 use cases

| Use Case ID | Actor | Object | Action | Conditions | Decision |
|---|---|---|---|---|---|
| UC-OPS-001 | Ops Staff | OBJ.WORKITEM | ACT.READ | Assigned workitem/queue | ALLOW |
| UC-OPS-002 | Ops Staff | OBJ.WORKITEM | ACT.UPDATE | Assigned workitem + allowed transition | ALLOW |
| UC-OPS-003 | Ops Staff | OBJ.WORKITEM | ACT.ASSIGN | Not queue owner | DENY |
| UC-OPS-004 | Supervisor | OBJ.WORKITEM | ACT.ASSIGN | Queue owner/team scope | ALLOW |
| UC-OPS-005 | Ops Staff | OBJ.CASE | ACT.OPERATE | Assigned case | ALLOW |
| UC-OPS-006 | Ops Staff | OBJ.CASE | ACT.DELETE | N/A | DENY |
| UC-OPS-007 | Supervisor | OBJ.SLA | ACT.READ | Team/queue scope | ALLOW |
| UC-OPS-008 | Supervisor | OBJ.CASE | ACT.ESCALATE | Severity/SLA breach | ALLOW |
| UC-OPS-009 | Partner Ops | Partner callback case | ACT.OPERATE | Assigned partner case | ALLOW |
| UC-OPS-010 | Social Banking Ops | OBJ.DISPUTE | ACT.OPERATE | Assigned dispute case | ALLOW |
| UC-OPS-011 | Social Banking Ops | OBJ.SB_LEDGER | ACT.UPDATE | N/A | DENY direct; request domain adjustment |
| UC-OPS-012 | Collateral Ops | OBJ.GOLD_COLLATERAL | ACT.UPDATE | Assigned case + evidence | CONDITIONAL_ALLOW |
| UC-OPS-013 | Compliance | OBJ.AUDIT | ACT.AUDIT_READ | Approved review scope | ALLOW |
| UC-OPS-014 | Moderator | OBJ.SHOPPERTAINMENT | ACT.MODERATE | Assigned live | ALLOW |
| UC-OPS-015 | Compliance Supervisor | OBJ.SHOPPERTAINMENT | ACT.KILL | Kill authority + incident severity | ALLOW |

