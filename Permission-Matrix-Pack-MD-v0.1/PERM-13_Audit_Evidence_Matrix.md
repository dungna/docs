---
id: PERM-13
title: Audit & Evidence Matrix
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-13 — Audit & Evidence Matrix

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký mức audit và bằng chứng bắt buộc cho các nhóm action/object. High-risk action không audit thì không được phép chạy.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. Audit levels

| Audit Level | Name | Applies to | Required fields |
|---|---|---|---|
| L0 | No audit / technical log only | Public/non-sensitive read | request_id, timestamp |
| L1 | Basic audit | Normal authenticated read | actor, action, object, timestamp |
| L2 | Sensitive read audit | Customer/partner/workforce sensitive data | actor, purpose, scope, object, correlation_id |
| L3 | Business action audit | Create/update/operate/partner handoff | actor, command, object, before/after if any, permit_decision, consent_ref |
| L4 | Critical decision/execute audit | Approve/override/payment/ledger/claim/partner PII sharing | actor, delegated authority, evidence, reason, before/after, dual_control, correlation_id |

## 4. Audit matrix

| Object/Action | Audit level | Evidence required |
|---|---|---|
| Loan application submit | L3 | consent_ref, eKYC/evidence if applicable, device/session, correlation_id |
| Loan approval/reject | L4 | delegated authority, rule trace, decision reason |
| Payment execution | L4 | idempotency key, payment partner response, reconciliation ref |
| Insurance quote create | L3 | consent/advisor ref |
| Claim submit | L3 | claim docs/evidence |
| Claim decision | L4 | assessment, decision reason, authority |
| Investment handoff | L3 | disclosure/suitability/partner contract |
| Investment order | L4 | partner authority, order ref |
| MB eKYC package sharing | L4 | explicit consent, payload ref, partner contract |
| Social Banking ledger adjustment | L4 | evidence, dual control, reconciliation |
| WorkItem/case operation | L3 | case_ref, action, result |
| Live moderation/kill | L4 | session_id, clip/transcript ref, reason, actor |
| Data export | L4 | approval, purpose, dataset, masking, recipient |
