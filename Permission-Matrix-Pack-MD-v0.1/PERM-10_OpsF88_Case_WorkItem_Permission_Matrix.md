---
id: PERM-10
title: OpsF88 Case & WorkItem Permission Matrix
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-10 — OpsF88 Case & WorkItem Permission Matrix

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký quyền vận hành của OpsF88 với WorkItem, Queue, Case, SLA, escalation, moderation, partner ops, dispute và reconciliation. OpsF88 vận hành work, không thay domain truth.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. OpsF88 permission matrix

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


## 4. OpsF88 operating rule

```text
OpsF88 can operate work.
OpsF88 must not mutate product truth directly.
```
