---
id: PERM-12
title: Consent & Purpose Matrix
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-12 — Consent & Purpose Matrix

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký purpose, consent/legal basis và allowed use cho data/action. Đây là lớp chặn consent misuse và purpose creep.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. Purpose registry

| Purpose Code | Purpose | Vietnamese name | Consent/legal basis required | Notes |
|---|---|---|---|---|
| PURP.AUTH | Authentication | Xác thực/đăng nhập | Legal/service basis | Identity/session |
| PURP.SERVICE | Service delivery | Cung cấp dịch vụ | Contract/service basis | Xem/tracking dịch vụ đang dùng |
| PURP.LOAN_APPLY | Loan application processing | Xử lý hồ sơ vay | Consent/legal basis | Lending journey |
| PURP.REPAYMENT | Repayment servicing | Thu nợ/thanh toán | Contract/service basis | Payment/repayment |
| PURP.INS_QUOTE | Insurance quote/advisory | Báo giá/tư vấn bảo hiểm | Consent if advisor/partner sharing | Insurance journey |
| PURP.CLAIM_SUPPORT | Claim support | Hỗ trợ bồi thường | Consent/legal basis | Claim evidence/docs |
| PURP.INVEST_DISCOVERY | Investment discovery | Khám phá đầu tư | Disclosure/consent if tracking | FInvest/partner-led |
| PURP.INVEST_HANDOFF | Investment partner handoff | Chuyển tiếp đối tác đầu tư | Explicit consent + suitability/disclosure | Partner-led regulated |
| PURP.BANKING_HANDOFF | Banking partner handoff | Chuyển tiếp ngân hàng | Explicit partner consent | MB/CIMB if applicable |
| PURP.SOCIAL_BANKING | Social Banking participation | Tham gia tài chính cộng đồng | Participation + group data consent | Group visibility |
| PURP.MARKETING | Marketing/campaign | Marketing/chiến dịch | Marketing opt-in/consent | Suppression/frequency applies |
| PURP.LIVE_INTENT | Live intent capture | Ghi nhận intent trong live | Interaction/intent consent | Shoppertainment |
| PURP.SUPPORT | Customer support | Hỗ trợ khách hàng | Service/legal basis | Case/workitem |
| PURP.OPS_PROCESSING | Operations processing | Xử lý vận hành | Work purpose + case assignment | Workforce only |
| PURP.COMPLIANCE_REVIEW | Compliance/risk review | Kiểm soát/tuân thủ | Legal basis + scope | Audit/access limited |
| PURP.PARTNER_RECON | Partner reconciliation | Đối soát đối tác | Partner contract | Partner Ops |
| PURP.ANALYTICS | Analytics/segmentation | Phân tích/phân khúc | Consent/legal basis + allowed use | Data governance |
| PURP.AUDIT | Audit | Kiểm toán/audit | Legal/internal basis | Audit Platform |


## 4. Consent-purpose matrix

| Journey / Use | Purpose | Consent/legal basis | Required reference in audit |
|---|---|---|---|
| Loan application | PURP.LOAN_APPLY | Consent/legal basis for loan processing | consent_ref/legal_basis_ref |
| eKYC for partner MB | PURP.BANKING_HANDOFF | Explicit partner consent + eKYC sharing consent | consent_ref, partner_contract_ref |
| Insurance quote | PURP.INS_QUOTE | Customer consent if advisor/partner data use | consent_ref/advisor_ref |
| Claim support | PURP.CLAIM_SUPPORT | Claim/legal basis + document consent if needed | case_ref/evidence_ref |
| Investment handoff | PURP.INVEST_HANDOFF | Explicit consent + suitability/disclosure | consent_ref, disclosure_ref |
| Social Banking group | PURP.SOCIAL_BANKING | Participation + group data sharing consent | group_consent_ref |
| Marketing campaign | PURP.MARKETING | Marketing opt-in/consent | consent_ref/suppression_result |
| Live intent capture | PURP.LIVE_INTENT | Interaction/intent capture consent | session_id, consent_ref |
| Support case | PURP.SUPPORT | Service/legal basis | case_ref |
| Analytics | PURP.ANALYTICS | Consent/legal basis + allowed use | data_product_ref |
| Compliance review | PURP.COMPLIANCE_REVIEW | Legal/internal basis | review_case_ref |
