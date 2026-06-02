---
id: PERM-14
title: Delegation & Dual Control Matrix
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-14 — Delegation & Dual Control Matrix

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký action nào có thể ủy quyền, action nào cần dual control và action nào không được delegate.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. Delegation matrix

| Authority / Action | Delegatable? | To whom | Required controls |
|---|---:|---|---|
| Loan application document review | Yes | Loan Ops | Role + case assignment + audit |
| Loan approval standard | Yes | Underwriter/Credit Reviewer | Delegated authority limit + audit |
| Loan policy override | Restricted | Senior authority | Dual control + waiver + audit |
| Claim document support | Yes | Claim Support | Case assignment + audit |
| Claim assessment | Yes | Claim Assessor | Queue/case + authority + audit |
| Claim decision high value | Restricted | Claim Manager/Senior | Dual control + audit |
| Investment order execution | No for F88 unless licensed | Licensed Partner | Partner authority |
| MB account creation | No | MB Bank | Partner authority |
| Social Banking ledger adjustment | Restricted | Social Banking Domain service | Dual control/evidence/reconciliation |
| WorkItem assignment | Yes | Supervisor/Queue Owner | Queue scope + audit |
| Live force stop | Restricted | Compliance Supervisor/Authorized kill role | Severity + audit |
| Data export | Restricted | Data Governance approved role | Approval + masking + audit |
