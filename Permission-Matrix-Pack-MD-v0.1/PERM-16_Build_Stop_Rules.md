---
id: PERM-16
title: Permission Build Stop Rules
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-16 — Permission Build Stop Rules

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký các điều kiện bắt buộc dừng build/release nếu permission, consent, permit, authority, audit hoặc BFF/partner/Ops boundary chưa rõ.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. Stop build rules

| Rule ID | Stop condition | Why it matters |
|---|---|---|
| STOP-PERM-001 | Object không có authority | Không biết ai giữ truth |
| STOP-PERM-002 | Action không có taxonomy/risk level | Không evaluate được permit/audit |
| STOP-PERM-003 | Actor không có registry | Không resolve được identity/scope |
| STOP-PERM-004 | Purpose không rõ | Dễ data misuse |
| STOP-PERM-005 | Consent/legal basis không rõ | Rủi ro privacy/compliance |
| STOP-PERM-006 | Permit Foundation không được gọi cho restricted action | Bypass access control |
| STOP-PERM-007 | Workforce access không case/scope-bound | OpsF88 thành data portal |
| STOP-PERM-008 | Partner flow thiếu contract/payload/callback/idempotency | Federation không kiểm soát |
| STOP-PERM-009 | BFF tự tạo business truth hoặc đọc DB domain | Shadow domain |
| STOP-PERM-010 | App hiển thị projection không có source/timestamp | Sai truth/stale data |
| STOP-PERM-011 | High-risk action không audit | Không accountability |
| STOP-PERM-012 | Money/ledger/payment không có reconciliation | Lệch tiền/ledger |
| STOP-PERM-013 | Social Banking thiếu ledger/dispute/reconciliation permission | High customer harm |
| STOP-PERM-014 | Live/Shoppertainment thiếu moderation/kill permission | Compliance risk |
| STOP-PERM-015 | Data export thiếu approval/masking/audit | Data leakage |
| STOP-PERM-016 | Override không có dual control/waiver | Policy bypass |

## 4. Stop release rules

| Rule ID | Stop condition |
|---|---|
| REL-PERM-001 | Không có audit dashboard/log query cho high-risk actions |
| REL-PERM-002 | Không có contract test cho BFF/domain/partner permission path |
| REL-PERM-003 | Không có negative test cho DENY cases |
| REL-PERM-004 | Không có rollback/kill switch cho high-risk capability |
| REL-PERM-005 | Không có monitoring cho permission denied spikes |
| REL-PERM-006 | Không có access review process cho workforce/partner roles |
