# Suez Steel Co. — Enterprise PR & PO Procurement Follow-Up Dashboard
## Executive Architecture, Governance & Feature Guide

---

## 🏛️ Executive Summary

The **Suez Steel Enterprise PR & PO Follow-Up Dashboard** is a mission-critical, real-time procurement command center designed to monitor, track, and accelerate **3,800+ active purchase requisitions and purchase orders** across Suez Steel Company plants.

The dashboard integrates core ERP transaction data, stock consumption records, and supplier intelligence into a zero-scroll, high-performance command center. It bridges Plant Requisitioners, Procurement Leaders, Operational Buyers, Warehouse Teams, and Executive Management with a single source of truth.

---

## 📐 1. Command Center & Layout Architecture

### 1.1 Zero-Scroll Viewport Optimization (`100vh` Guaranteed Fit)
- **Universal Resolution Support:** Engineered with dynamic `clamp()` padding and ultra-compact component metrics to guarantee that **Stage 6 (On-Track Delivery)** and all bottom controls are 100% visible on any screen—from **1366×768** laptops up to **1920×1080** and 4K displays—with **zero vertical or horizontal scrolling**.
- **SLA Micro-Tracks:** Replaced bulky multi-row aging counters with sleek 5px inline progress and aging bars.
- **Reference Screenshot:**  
  `📁 01_Command_Center_Overview/01_Executive_Zero_Scroll_Grid.png`

### 1.2 Central Symmetrical Sunburst Donut Chart
- **Total Orders Tracked:** **3,677 Active Orders** (1,315 PRs / 2,362 POs).
- **Left Hemisphere (Requisition Pipeline - 1,315 PRs):**
  - Stage 1: TS Confirmed (Ready to Issue PO) — 245 PRs
  - Stage 2: Sourcing / RFQ (No Offers) — 930 PRs
  - Stage 3: Offers Under Plant Evaluation — 140 PRs
- **Right Hemisphere (Contracted PO Pipeline - 2,362 POs):**
  - Stage 4: PO Not Confirmed — 459 POs
  - Stage 5: Overdue Delivery — 1,045 POs
  - Stage 6: On-Track Delivery — 761 POs
- **Reference Screenshot:**  
  `📁 01_Command_Center_Overview/02_Sunburst_Donut_3677_Orders.png`

### 1.3 Option A Header Architecture (2-Tier Command Bar)
- **Tier 1 (Executive KPI & Action Utilities ~36px):**
  - Enterprise Title: `Suez Steel Co. — ENTERPRISE PR & PO FOLLOW-UP`
  - Zero-Stock Metric Badge (`10,760 Lines • 73.0% Zero-Stock`)
  - Instant Excel Export (`Export Zero`)
  - Stock Control Quick Access (`97 PRs • Pending L4 | 378 Zero-Stock`)
  - View Controls & Fullscreen toggle (`[F]` key)
- **Tier 2 (Unified Single-Row Multi-Dimensional Filter Toolbar ~32px):**
  - **Department Selector** (`[D]` key)
  - **Buyer & Team Routing** (`[/]` key)
  - **Origin Filter** (`Local PO` vs `Foreign Import` | `[O]` key)
  - **Priority Segment** (`P1 Critical`, `P2 Active`, `P3 Near-Zero`, `P4 Dormant`)
  - **Requisition Year Filter** (`2026`, `2025`, `2024`, `All Years`)
  - **More Filters Drawer** (Plant code, delivery status, value brackets)
- **Reference Screenshot:**  
  `📁 01_Command_Center_Overview/03_2Tier_OptionA_Header_Toolbar.png`

---

## 🔄 2. End-to-End Six-Stage Procurement Lifecycle

| Stage | Name | Metric | Business Definition & Action Trigger |
| :---: | :--- | :---: | :--- |
| **Stage 1** | **TS Confirmed (Ready to Issue PO)** | **245 PRs** | Technical specifications approved by Plant Engineers. Pricing & commercial terms finalized; pending Buyer formal PO issuance. |
| **Stage 2** | **Sourcing / RFQ (No Offers)** | **930 PRs** | Open requisitions actively being sourced in the market. RFQs issued to approved vendors; awaiting vendor quotations. |
| **Stage 3** | **Offers Under Plant Evaluation** | **140 PRs** | Vendor offers received by Procurement and submitted to Plant Engineering for technical review and compliance sign-off. |
| **Stage 4** | **PO Not Confirmed** | **459 POs** | Purchase Orders formally placed with vendors but awaiting formal order acknowledgment or Supply Chain SC Approval. |
| **Stage 5** | **Overdue Delivery** | **1,045 POs** | Purchase Orders exceeding Promised Delivery Date. Segmented into aging severity: 1–30d, 31–90d, and >90d late. |
| **Stage 6** | **On-Track Delivery** | **761 POs** | Active, healthy orders progressing within promised delivery lead times. Split into Foreign vs Local with pending delivery values. |

### Visual References:
- `📁 02_Six_Stage_Procurement_Flow/04_Stage1_TS_Confirmed.png`
- `📁 02_Six_Stage_Procurement_Flow/05_Stage2_Sourcing_RFQ.png`
- `📁 02_Six_Stage_Procurement_Flow/06_Stage3_Offers_Plant_Evaluation.png`
- `📁 02_Six_Stage_Procurement_Flow/07_Stage4_PO_Not_Confirmed.png`
- `📁 02_Six_Stage_Procurement_Flow/08_Stage5_Overdue_Delivery_Aging.png`
- `📁 02_Six_Stage_Procurement_Flow/09_Stage6_OnTrack_Delivery_Progress.png`

---

## ⚡ 3. Specialized Critical Operation Queues

### 3.1 Unassigned PRs (Pending Buyer Routing)
- **Count:** **84 Unassigned Requisitions**
- **Location:** Prominent top floating pill directly above the central Sunburst chart.
- **Function:** Identifies requisitions that have entered the ERP system without an assigned buyer or procurement group. Prevents requisitions from languishing unnoticed.
- **Reference Screenshot:**  
  `📁 03_Specialized_Operational_Pills/10_Unassigned_PRs_Buyer_Routing.png`

### 3.2 Technical Inspection Queue (In Warehouse • Decision Pending)
- **Count:** **98 Orders in Warehouse**
- **Location:** Prominent bottom floating pill directly beneath the central Sunburst chart.
- **The Golden Rule for Technical Inspection:**
  $$\mathbf{Qty\ Inspected > 0 \quad AND \quad Qty\ Accepted = 0 \quad AND \quad Qty\ Rejected = 0}$$
  - **Business Logic:** Goods have physically arrived at the Suez Steel central warehouse and been booked by warehouse receivers. They are currently awaiting formal Quality / Engineering Technical Validation.
  - If $\text{Qty Rejected} > 0$, inspection has concluded with a failure, triggering a vendor claim/replacement.
  - If $\text{Qty Accepted} > 0$, items have entered active plant stock.
- **Reference Screenshot:**  
  `📁 03_Specialized_Operational_Pills/11_Technical_Inspection_Warehouse_Rule.png`

---

## 📋 4. PR & PO Dossier Deep-Dive Modal

When clicking on any order or requisition across the dashboard, the **Interactive Dossier Modal** provides comprehensive end-to-end intelligence:

### 4.1 9-Step Procurement Journey Milestones
Tracks progress across all sequential lifecycle milestones:
1. `Plant Confirmed`
2. `SC Level 4 Confirmed`
3. `Leader Assignment`
4. `Sourcing & RFQ`
5. `Plant TS Technical Review`
6. `Issue PO`
7. `Draft PO Audit`
8. `Supplier Delivery (In Warehouse)`
9. `Technical Quality Inspection`

### 4.2 Intelligent Single-Pill Supplier Deduplication
- **The Enhancement:** In 95.4% of procurement lines, the plant engineer suggests the vendor who previously supplied the material. Previously, this displayed two identical stacked badges.
- **The Solution:** The system automatically cleans, matches, and deduplicates the supplier names, rendering **one sleek unified badge** (e.g. `🏷️ ISP For Industrial Service and General upplies (104716)`).
- **Price Cleared:** Removed cluttered inline price tags, as all pricing history and ERVs are available on demand in the Item Intelligence console.
- **Visual References:**
  - Full Dossier: `📁 04_Dossier_&_Item_Intelligence/12_PR_PO_Dossier_Lifecycle_Journey.png`
  - Deduplicated Row: `📁 04_Dossier_&_Item_Intelligence/13_Line_Items_Smart_Supplier_Deduplication.png`

---

## 📈 5. Analytical Intelligence & Stock Optimization

### 5.1 Item Intelligence Modal (3-Year Consumption & Trajectory)
Clicking on any underlined item code (e.g. `📈 S.5895.F000.0012`) opens deep historical intelligence:
- **3-Year Consumption Curve:** Monthly burn rate history (Sep 2023 – Sep 2026).
- **Weighted Moving Average (WMA):** Annualized consumption rate giving higher weight to recent quarters.
- **Lead Time Analytics:** Split into Internal Approval Lead Time vs External Supplier Delivery Lead Time.
- **Inventory Safety Parameters:** Re-Order Point (ROP), Minimum Stock, Maximum Stock, and Stock Cover in months.
- **Reference Screenshot:**  
  `📁 04_Dossier_&_Item_Intelligence/14_Item_Intelligence_3Year_Trajectory_WMA.png`

### 5.2 Zero-Stock Matrix & Priority Classification (P1 to P4)
- **P1 Critical (Red):** Zero stock in warehouse with surging/active demand. Requires immediate executive expediting.
- **P2 Active (Orange):** Zero stock in warehouse with steady historical consumption.
- **P3 Pre-Stockout (Yellow):** Current stock below Re-Order Point (ROP); stockout imminent if delivery is delayed.
- **P4 Dormant (Gray):** Zero stock, but zero consumption over the past 3 years. Low operational urgency.
- **Reference Screenshot:**  
  `📁 05_Enterprise_Controls_&_Exports/15_Zero_Stock_Matrix_P1_to_P4.png`

### 5.3 Level 4 Stock Control Console
- Provides dedicated review for **97 PRs (534 Lines)** awaiting Level 4 inventory authorization before entering active sourcing.
- **Reference Screenshot:**  
  `📁 05_Enterprise_Controls_&_Exports/16_Level_4_Stock_Control_Console.png`

### 5.4 Multi-Dimensional Arabic & Fuzzy Search Engine
- Real-time search indexing PR numbers, PO numbers, item codes, descriptions, plant names, and Arabic requisitioner names (`اسامة محمود محمد احمد`).
- **Reference Screenshot:**  
  `📁 05_Enterprise_Controls_&_Exports/17_MultiDimensional_Filtering_Arabic_Search.png`

---

## 🚨 6. P1 Critical Operational Showcase (Zero-Stock & Surging Consumption Gallery)

### 6.1 Purpose & Methodology
To support executive oversight on materials posing catastrophic operational risk to steelmaking and plant uptime, the **P1 Critical Showcase Gallery** aggregates items meeting the following criteria:
1. **Absolute Zero Stock Balance:** $\text{On-Hand Stock} = 0.0$ across all warehouses ($0.0\text{ Months Cover}$).
2. **High or Surging Burn Velocity:** High Weighted Moving Average ($\text{WMA} \ge 3.0$ units/yr) or positive Year-over-Year trajectory ($+52\%$ to $+108\%$ YoY).
3. **Active Open Requisition Demand:** Trapped in active PRs/POs requiring immediate executive unblocking.

### 6.2 Top 8 Critical Strategic Materials Master Table

| # | Item Code | Description | Key Plant | Stock | Annual Burn (WMA) | Contracted Vendor | Bottleneck Stage & Delay | Lead Buyer |
|---|---|---|---|---|---|---|---|---|
| **1** | `O0100100001` | **Liquid Oxygen (Bulk LOX)** | OP11 Oxygen Plant | **0 Liter** | **12,957,727 Liter/yr** | Abu Laila Factory | Sourcing / RFQ (1d) & PO Approval (136d) | Amr Adel |
| **2** | `M0100300001` | **Iron Ore Pellet Feed** | OP19 Pelletizing | **0 Ton** | **428,172 Ton/yr** | Cargill International | Supplier Overdue (+42d) | Amr Mossad |
| **3** | `O0400100332` | **Water Treatment Chemical N-WT-1009** | OP10 Utilities & OP19 | **0 KG** | **119,925 KG/yr** | Nalco Egypt (Sole Source) | Supplier Overdue (+623d, 4 POs) | Mabrouk Younis |
| **4** | `M0100100006` | **Scrap Steel Shredded** | OP02 SMP1 & OP05 SMP2 | **0 Ton** | **81,554 Ton/yr** | American Iron & Metal | Supplier Overdue (+538d) | Amr Mossad |
| **5** | `O.3200.5370.0009` | **Organic Binder Anionic Polyacrylamide** | OP19 Pelletizing | **0 KG** | **40,401 KG/yr** | Nalco Egypt | Supplier Overdue (+58d) | Mabrouk Younis |
| **6** | `M0200100002` | **Ferro Manganese High Carbon** | OP05 SMP2 & OP02 SMP1 | **0 Ton** | **7,425 Ton/yr** | Al Madina Steel Group | Supplier Overdue (+143d, 4 POs) | Ahmed Attef |
| **7** | `H0401603147` | **Grinding Ball Media 50mm CH14** | OP19 Pelletizing | **0 KG** | **3,302 KG/yr** | United Foundries | Sourcing / RFQ (+32d) | Amr Mossad |
| **8** | `S.3020.S204.0007` | **Rossi Gear Motor Mounting Kit** | OP05 SMP2 & IP22 | **0 Pcs** | **5.5 Pcs/yr** | Ashtechs | Unassigned PRs (+9d backlog) | Unassigned |

### 6.3 Triple Executive Presentation Architecture: Nano, Panorama & Flow
The dedicated showcase `P1_Critical_Showcase_Gallery.html` introduces three specialized executive presentation lenses:

1. **⚡ Nano Mode (Micro Grid):**
   - High-density micro metric cards showing item rank, stockout badge, monthly velocity, primary bottleneck, and responsible buyer.
   - Built-in **One-Click Markdown Copy** for rapid pasting into executive emails, Telegram, or WhatsApp briefings.
   - Direct modal trigger to inspect full-screen 1080p dossiers.
   - **Reference Screenshot:** `📁 06_P1_Critical_Zero_Stock_Gallery/00_Gallery_Mode_Nano.png`

2. **🖼️ Panorama (Pnana) Mode (Widescreen Analytical Banners):**
   - Dual-column panoramic executive cards featuring 1080p Item Intelligence dossier screenshots alongside interactive 3-Year Consumption Trajectory comparative bar charts.
   - Displays real-time financial valuation, sole-source commercial risks, plant consumption splits, and top active requisitions.
   - Includes specific **Executive Remediation Actions** tailored for leadership intervention.
   - **Reference Screenshot:** `📁 06_P1_Critical_Zero_Stock_Gallery/00_Gallery_Mode_Panorama.png`

3. **🔄 Process Flow Journey Mode (Bottleneck Radar):**
   - Visual 6-Stage end-to-end procurement lifecycle stepper (Stage 1: TS Confirmed $\to$ Stage 2: Sourcing $\to$ Stage 3: Plant Eval $\to$ Stage 4: PO Approval $\to$ Stage 5: Supplier Execution $\to$ Stage 6: Warehouse Receipt).
   - Identifies the exact blockage stage with pulsating alert halos, displaying supplier name, aging delays (up to $+623$ days), and assigned procurement officer.
   - **Reference Screenshot:** `📁 06_P1_Critical_Zero_Stock_Gallery/00_Gallery_Mode_Flow.png`

---

## ☁️ 7. Deployment & 24/7 Availability Architecture

The dashboard and executive showcase suite are delivered through a dual-channel deployment model:

1. **GitHub Pages Cloud (Permanent 24/7 Public Link — No VPN Required):**
   - **Main Command Center:** https://planner2317.github.io/suezsteel-buyer-dashboard/
   - **Architecture:** Lightweight 515 KB web shell + 14 modular data chunks with caching. Loads in under 2 seconds.
2. **Corporate OneDrive Cloud Folder:**
   - **Main Command Center:** `D:\OneDrive - Suez Steel Co\Buyer_Dashboard\buyer_dashboard.html`
   - **Executive Showcase Hub:** `D:\OneDrive - Suez Steel Co\Buyer_Dashboard\Executive_Showcase\Interactive_Feature_Showcase.html`
   - **P1 Critical Gallery:** `D:\OneDrive - Suez Steel Co\Buyer_Dashboard\Executive_Showcase\P1_Critical_Showcase_Gallery.html`
   - Real-time synchronization across corporate workstations.
3. **Local Standalone Artifacts:**
   - Standalone portable HTML and 1080p captures for board meetings and offline air-gapped executive presentations.

---
*Generated by Suez Steel Enterprise Procurement Intelligence Engine — September 2026*
