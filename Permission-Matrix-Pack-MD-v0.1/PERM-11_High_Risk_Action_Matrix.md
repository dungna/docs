---
id: PERM-11
title: High Risk Action Matrix
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-11 — High Risk Action Matrix

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký các action nhạy cảm cần kiểm soát cao: domain authority, dual control, waiver, audit, evidence, reconciliation hoặc kill switch.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. High-risk action registry

| High Risk ID | Object | Action | Risk | Required controls |
|---|---|---|---|---|
| HR-LOAN-001 | OBJ.LOAN_APPROVAL | ACT.DECIDE | Credit/regulatory/customer harm | CTRL.AUTHORITY, CTRL.PERMIT, CTRL.AUDIT, delegated authority |
| HR-LOAN-002 | OBJ.LOAN_APPROVAL | ACT.OVERRIDE | Policy bypass | CTRL.DUAL, CTRL.AUDIT, waiver |
| HR-PAY-001 | OBJ.PAYMENT_EXECUTION | ACT.EXECUTE | Money movement | CTRL.IDEMPOTENCY, CTRL.AUDIT, reconciliation |
| HR-CLAIM-001 | OBJ.CLAIM_DECISION | ACT.DECIDE | Claim/legal/customer harm | CTRL.AUTHORITY, CTRL.AUDIT, delegated authority |
| HR-CLAIM-002 | OBJ.CLAIM_PAYOUT | ACT.EXECUTE | Money payout | CTRL.IDEMPOTENCY, CTRL.AUDIT, payment reconciliation |
| HR-INV-001 | OBJ.INVEST_ORDER | ACT.EXECUTE | Regulated investment | Partner authority, suitability, disclosure, audit |
| HR-SB-001 | OBJ.SB_LEDGER | ACT.UPDATE/ACT.EXECUTE | Ledger integrity | Domain authority, CTRL.DUAL, evidence, reconciliation, audit |
| HR-PARTNER-001 | OBJ.EKYC | ACT.SHARE | PII/data sharing | Explicit consent, partner contract, audit |
| HR-BANK-001 | OBJ.MB_ACCOUNT_STATUS | ACT.UPDATE/callback | Regulated banking status | Signed callback, idempotency, source timestamp |
| HR-GOLD-001 | OBJ.COLLATERAL_VALUATION | ACT.UPDATE | Asset valuation risk | Valuation authority, evidence, audit |
| HR-GOLD-002 | OBJ.COLLATERAL_CUSTODY | ACT.UPDATE | Custody/legal risk | Custody authority, evidence, audit |
| HR-OPS-001 | OBJ.SHOPPERTAINMENT | ACT.KILL | Customer/compliance/business disruption | Kill authority, severity, audit |
| HR-DATA-001 | Customer data | ACT.EXPORT | Privacy/data leakage | DPO/data governance approval, masking, audit |
| HR-COMM-001 | Critical notification | ACT.EXECUTE/suppress | Customer harm/compliance | Notification ownership, legal review, audit |
| HR-COMM-002 | OBJ.COMMISSION_PAYABLE | ACT.UPDATE | Incentive payout risk | Incentive OS authority, audit, dual control if override |


## 4. High-risk decision rules

- High-risk action không được rely vào FE/BFF-only permission.
- High-risk write/execute/decide phải kiểm authority + permit + audit.
- Money/ledger/payment phải có idempotency và reconciliation.
- Partner data sharing phải có consent + contract + payload reference.
- Override/exception phải có waiver hoặc dual control.
