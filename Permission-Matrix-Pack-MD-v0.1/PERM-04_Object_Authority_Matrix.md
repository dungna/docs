---
id: PERM-04
title: Object Authority Matrix
pack: PERMISSION MATRIX PACK
version: v0.1
status: Draft for import/review
source_of_truth: F88 Ecosystem Architecture last.md
owners: Architecture, Security, Product, BA, DEV, OpsF88
---

# PERM-04 — Object Authority Matrix

> **Source of truth:** `F88 Ecosystem Architecture last.md`  
> **Nguyên tắc:** File MD gốc là nguồn chuẩn. Tài liệu này là registry/tài liệu vận hành được bóc tách từ master để import, đăng ký và quản trị permission.

## 1. Mục tiêu

Đăng ký object/truth và authority tương ứng. Đây là Domain Authority Registry được chuyển hóa thành permission source.

## 2. Source reference map

| Nhóm nội dung | Reference trong file MD gốc |
|---|---|
| Authority principle | `Domain Authority Registry`, `App surface is not authority`, `Domain owns truth` |
| Shared trust primitives | `Shared Trust & Foundation`, `Identity`, `Party`, `eKYC`, `Consent`, `Permit`, `Device Trust`, `Document/Evidence`, `Notification`, `Audit` |
| Trust worlds | `App Worlds & Trust Boundaries`, `Customer World`, `Workforce World`, `Partner World` |
| Channel/BFF boundary | `Channel Service / BFF Pattern`, `BFF composes experience; domain owns truth` |
| Control plane | `Control Plane & Governance`, `Build Stop Rules`, `No consent/permit, no action`, `No audit, no accountability` |


## 3. Object authority registry

| Object / Truth ID | Object / Truth | Authority | Domain group | Notes |
|---|---|---|---|---|
| OBJ.IDENTITY | Identity | Identity Foundation | Shared Trust & Foundation | Danh tính actor |
| OBJ.PARTY | Party / Customer Reference | Party Foundation | Shared Trust & Foundation | Chủ thể khách hàng thống nhất |
| OBJ.EKYC | eKYC Result / Evidence Package | Identity/eKYC Foundation | Shared Trust & Foundation | Kết quả/bằng chứng định danh |
| OBJ.CONSENT | Consent | Consent Foundation | Shared Trust & Foundation | Đồng ý theo purpose |
| OBJ.PERMIT | Permit / Access Decision | Permit Foundation | Shared Trust & Foundation | Quyết định quyền |
| OBJ.DEVICE_TRUST | Device Trust | Device Trust Foundation | Shared Trust & Foundation | Độ tin cậy thiết bị |
| OBJ.DOCUMENT | Document / Evidence | Document/Evidence Foundation | Shared Trust & Foundation | Hồ sơ, chứng từ, bằng chứng |
| OBJ.NOTIFICATION | Notification Delivery | Notification/CCM | Shared Trust & Foundation | Delivery state |
| OBJ.AUDIT | Audit Trail | Audit Platform | Shared Trust & Foundation | Nhật ký trách nhiệm |
| OBJ.LOAN_APPLICATION | Loan Application | Lending Domain | Lending | Hồ sơ vay |
| OBJ.LOAN_APPROVAL | Loan Approval | Lending Domain | Lending | Quyết định phê duyệt |
| OBJ.LOAN_CONTRACT | Loan Contract | Lending Domain | Lending | Hợp đồng vay |
| OBJ.REPAYMENT_OBLIGATION | Repayment Obligation | Lending Domain | Lending | Nghĩa vụ trả nợ |
| OBJ.PAYMENT_EXECUTION | Payment Execution | Payment Domain / Payment Partner | Payment | Thực thi thanh toán |
| OBJ.INS_PRODUCT | Insurance Product | Insurance Domain | Insurance | Sản phẩm bảo hiểm |
| OBJ.INS_QUOTE | Insurance Quote | Insurance Domain / NNX Insurance OS | Insurance | Báo phí/báo giá |
| OBJ.POLICY | Policy | Policy Admin Domain | Insurance | Hợp đồng bảo hiểm |
| OBJ.CLAIM_INTAKE | Claim Intake | Claims Domain | Claims | Tiếp nhận bồi thường |
| OBJ.CLAIM_ASSESSMENT | Claim Assessment | Claims Domain | Claims | Thẩm định claim |
| OBJ.CLAIM_DECISION | Claim Decision | Claims Domain | Claims | Duyệt/từ chối claim |
| OBJ.CLAIM_PAYOUT | Claim Payout | Claims Domain / Payment Partner | Claims/Payment | Chi trả bồi thường |
| OBJ.INVEST_ACCOUNT | Investment Account | Licensed Partner / Investment Domain | Investment | Tài khoản đầu tư |
| OBJ.INVEST_ORDER | Investment Order | Licensed Partner | Investment | Lệnh đầu tư |
| OBJ.PORTFOLIO | Holding / Portfolio | Licensed Partner / Investment Domain | Investment | Danh mục nắm giữ |
| OBJ.PORTFOLIO_PROJECTION | Portfolio Projection | Partner/domain projection | Investment | Bản chiếu, không phải app truth |
| OBJ.MB_ACCOUNT | MB Account | MB Bank | Banking Partner | Tài khoản MB |
| OBJ.MB_ACCOUNT_STATUS | MB Account Opening Status | MB callback/projection | Banking Partner | Trạng thái do MB trả về |
| OBJ.GOAL_SAVING | Goal Saving | Goal Savings Domain | Goal Savings | Mục tiêu tiết kiệm |
| OBJ.GOLD_PIGGY_VIS | Gold Piggy Bank Visualization | Goal Savings + Market Data | Gold/Goal | Mô phỏng vàng |
| OBJ.REAL_GOLD_OWNERSHIP | Real Gold Ownership | Gold partner if legal model allows | Gold Partner | Sở hữu vàng thật nếu có |
| OBJ.GOLD_COLLATERAL | Gold Collateral Asset | Gold & Collateral Domain | Gold/Collateral | Tài sản bảo đảm vàng |
| OBJ.COLLATERAL_VALUATION | Collateral Valuation | Valuation Service / Partner | Gold/Collateral | Định giá |
| OBJ.COLLATERAL_CUSTODY | Collateral Custody | Gold & Collateral / Custody Authority | Gold/Collateral | Lưu giữ/custody |
| OBJ.SB_GROUP | Social Banking Group | Social Banking Domain | Social Banking | Nhóm tài chính cộng đồng |
| OBJ.SB_MEMBER | Social Banking Member | Social Banking Domain | Social Banking | Thành viên nhóm |
| OBJ.SB_CONTRIBUTION | Contribution Obligation | Social Banking Domain | Social Banking | Nghĩa vụ góp |
| OBJ.SB_BID_AWARD | Bid / Award Result | Social Banking Domain | Social Banking | Kết quả bid/lượt nhận |
| OBJ.SB_LEDGER | Group Ledger | Social Banking Domain | Social Banking | Sổ cái nhóm |
| OBJ.DISPUTE | Dispute | Domain truth + OpsF88 case by nature | Domain + OpsF88 | Tranh chấp |
| OBJ.AGENT_PROFILE | Agent Profile | Distribution / Agent Network Domain | Distribution | Hồ sơ agent |
| OBJ.AGENT_CERT | Agent Certification | LMS/HXP | Workforce/HXP | Chứng nhận agent |
| OBJ.SELLING_ELIGIBILITY | Product Selling Eligibility | Distribution / Agent Network + Permit | Distribution | Điều kiện được bán/tư vấn |
| OBJ.COMMISSION_SCHEME | Commission Scheme | Incentive OS | Incentive | Chính sách hoa hồng |
| OBJ.COMMISSION_PAYABLE | Commission Payable | Incentive OS | Incentive | Hoa hồng được trả |
| OBJ.WORKITEM | WorkItem | OpsF88 | OpsF88 | Đầu việc |
| OBJ.QUEUE | Queue | OpsF88 | OpsF88 | Hàng đợi |
| OBJ.CASE | Case | OpsF88 | OpsF88 | Case vận hành |
| OBJ.SLA | SLA | OpsF88 | OpsF88 | Cam kết xử lý |
| OBJ.CAMPAIGN | Campaign State | ExOS/CXP | ExOS/CXP | Trạng thái chiến dịch |
| OBJ.NBA_NBO | NBA / NBO | ExOS/CXP | ExOS/CXP | Gợi ý hành động/offer |
| OBJ.SHOPPERTAINMENT | Shoppertainment Session | ExOS/CXP Shoppertainment Engine | ExOS/CXP | Phiên live/tương tác |
| OBJ.VOUCHER | Voucher Redemption | Loyalty / Voucher Domain | Loyalty | Dùng/nhận voucher |


## 4. Authority rules

| Rule | Meaning |
|---|---|
| Authority owns truth | Authority là nơi quyết định state chính thức |
| App reads projection | App chỉ đọc projection/summary đã được contract |
| Ops requests adjustment | OpsF88 không sửa truth trực tiếp, chỉ gửi request/command |
| Partner owns regulated truth | MB/investment/payment partner giữ regulated truth theo contract |
| Foundation owns trust primitives | Identity/Consent/Permit/Audit không bị copy vào app/domain |
