# Application Definition
- Name: EcoVendor - ESG & Supplier Risk Hub
- Application Type: Enterprise
- Description: Enterprise application for monitoring supplier risk, Scope 1-3 carbon emissions, regulatory audit compliance, and real-time anomaly alerts.
- Theme: Redwood Light
- Authentication Scheme: Database Accounts
- Access Control:
  - Role: Administrator
    - Description: Full administrative access to all application settings, users, and data management.
  - Role: Sustainability Manager
    - Description: Manages ESG audits, carbon accounting baselines, and environmental rating assignments.
  - Role: Procurement Officer
    - Description: Manages supplier directory, contract values, operational contacts, and audit requests.
  - Role: Auditor
    - Description: Creates and updates audit reports, inspection outcomes, and compliance findings.
  - Role: Executive Viewer
    - Description: Read-only access to executive dashboards, supplier analytics, and risk feeds.
- Application Settings:
  - Setting
    - Name: APP_COMPANY_NAME
    - Value: EcoVendor Global Enterprises
  - Setting
    - Name: DEFAULT_PAGE_MODE
    - Value: STANDARD
  - Setting
    - Name: ALERT_REFRESH_INTERVAL_SECONDS
    - Value: 300
- Lists of Values:
  - LOV
    - Name: LOV_SUPPLIERS_ESG_RATING
    - Type: Static
    - Entries:
      - Entry:
        - Display: Tier A (Leader)
        - Return: A
      - Entry:
        - Display: Tier B (Compliant)
        - Return: B
      - Entry:
        - Display: Tier C (Needs Attention)
        - Return: C
      - Entry:
        - Display: Tier D (High Risk)
        - Return: D
      - Entry:
        - Display: Tier F (Non-Compliant)
        - Return: F
  - LOV
    - Name: LOV_SUPPLIERS_FINANCIAL_RISK_INDEX
    - Type: Static
    - Entries:
      - Entry:
        - Display: Low Risk
        - Return: LOW
      - Entry:
        - Display: Medium Risk
        - Return: MEDIUM
      - Entry:
        - Display: High Risk
        - Return: HIGH
      - Entry:
        - Display: Critical
        - Return: CRITICAL
  - LOV
    - Name: LOV_SUPPLIERS_AUDIT_STATUS
    - Type: Static
    - Entries:
      - Entry:
        - Display: Compliant
        - Return: COMPLIANT
      - Entry:
        - Display: Pending Audit
        - Return: PENDING_AUDIT
      - Entry:
        - Display: Under Review
        - Return: UNDER_REVIEW
      - Entry:
        - Display: Non-Compliant
        - Return: NON_COMPLIANT
  - LOV
    - Name: LOV_SUPPLIER_AUDITS_AUDIT_TYPE
    - Type: Static
    - Entries:
      - Entry:
        - Display: Annual Comprehensive
        - Return: ANNUAL_COMPREHENSIVE
      - Entry:
        - Display: Scope 3 Carbon Verification
        - Return: SCOPE3_CARBON
      - Entry:
        - Display: Labor & Human Rights
        - Return: LABOR_RIGHTS
      - Entry:
        - Display: Waste & Circularity
        - Return: WASTE_CIRCULARITY
      - Entry:
        - Display: Ad-hoc Risk Review
        - Return: AD_HOC_REVIEW
  - LOV
    - Name: LOV_SUPPLIER_AUDITS_AUDIT_OUTCOME
    - Type: Static
    - Entries:
      - Entry:
        - Display: Passed
        - Return: PASSED
      - Entry:
        - Display: Conditional Pass
        - Return: CONDITIONAL_PASS
      - Entry:
        - Display: Action Plan Required
        - Return: ACTION_REQUIRED
      - Entry:
        - Display: Failed
        - Return: FAILED
  - LOV
    - Name: LOV_RISK_ALERTS_ALERT_SEVERITY
    - Type: Static
    - Entries:
      - Entry:
        - Display: Critical
        - Return: CRITICAL
      - Entry:
        - Display: High
        - Return: HIGH
      - Entry:
        - Display: Medium
        - Return: MEDIUM
      - Entry:
        - Display: Low
        - Return: LOW
  - LOV
    - Name: LOV_RISK_ALERTS_RESOLUTION_STATUS
    - Type: Static
    - Entries:
      - Entry:
        - Display: Open
        - Return: OPEN
      - Entry:
        - Display: Under Investigation
        - Return: INVESTIGATING
      - Entry:
        - Display: Remediation In Progress
        - Return: REMEDIATING
      - Entry:
        - Display: Resolved
        - Return: RESOLVED
      - Entry:
        - Display: Dismissed
        - Return: DISMISSED
- Page Groups:
  - Page Group
    - Name: Home
    - Description: Executive summary dashboards and high-level KPI overviews.
  - Page Group
    - Name: Supplier Risk & Directory
    - Description: Supplier master registry, multi-attribute faceted search, and profile management.
  - Page Group
    - Name: ESG & Carbon Accounting
    - Description: Scope 1-3 greenhouse gas emissions, renewable energy share, and audit history.
  - Page Group
    - Name: Risk & Compliance Feed
    - Description: Real-time supply chain disruption, financial risk, and ESG exception alert streams.
  - Page Group
    - Name: Administration
    - Description: User access control, application configuration, and system lookup management.
- Menu:
  - Menu Name: Navigation Menu
  - Entries:
    - Entry
      - Label: Executive Dashboard
      - Icon: fa-dashboard
      - Action: Navigate
      - Target: Page 1
      - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer, Auditor, Executive Viewer
    - Entry
      - Label: Supplier Directory
      - Icon: fa-building
      - Action: Navigate
      - Target: Page 2
      - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer, Auditor, Executive Viewer
    - Entry
      - Label: ESG & Carbon Audits
      - Icon: fa-leaf
      - Action: Navigate
      - Target: Page 4
      - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer, Auditor, Executive Viewer
    - Entry
      - Label: Risk Alerts Feed
      - Icon: fa-exclamation-triangle
      - Action: Navigate
      - Target: Page 6
      - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer, Auditor, Executive Viewer
    - Entry
      - Label: System Administration
      - Icon: fa-cogs
      - Action: Navigate
      - Target: Page 9
      - Authorized Roles: Administrator

## Pages
### Page 1: Executive Dashboard
- Description: Executive ESG & Supplier Risk command center displaying high-level metrics, risk distribution, and urgent alert activity.
- Comments: Executive landing page for CPO, CSO, and procurement leadership.
- Pattern: metric-chart-two-up
- Page Mode: standard
- Menu: true
- Page Group: Home
- Security Requirements:
  - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer, Auditor, Executive Viewer
#### Regions
##### Region: Total Active Suppliers KPI
- Position: body
- Colstart: 1
- Colspan: 3
- Component:
  - Component Type: Metric Card
- Metric Subtitle: Total monitored suppliers
- Metric Icon: fa-building
- Metric Icon Style: subtle
- Data Source:
  - Type: SQL
  - SQL:
```sql
select count(*) as value
  from ECO_SUPPLIERS
 where AUDIT_STATUS != 'NON_COMPLIANT'
```
##### Region: High Risk Suppliers KPI
- Position: body
- Colstart: 4
- Colspan: 3
- Component:
  - Component Type: Metric Card
- Metric Subtitle: Financial & ESG risk tier D/F
- Metric Icon: fa-warning
- Metric Icon Style: danger
- Data Source:
  - Type: SQL
  - SQL:
```sql
select count(*) as value
  from ECO_SUPPLIERS
 where FINANCIAL_RISK_INDEX in ('HIGH', 'CRITICAL')
    or ESG_RATING in ('D', 'F')
```
##### Region: Avg Carbon Intensity KPI
- Position: body
- Colstart: 7
- Colspan: 3
- Component:
  - Component Type: Metric Card
- Metric Subtitle: Benchmark score (0-100 scale)
- Metric Icon: fa-leaf
- Metric Icon Style: success
- Data Source:
  - Type: SQL
  - SQL:
```sql
select round(avg(CARBON_INTENSITY_SCORE), 1) as value
  from ECO_SUPPLIERS
```
##### Region: Open Critical Alerts KPI
- Position: body
- Colstart: 10
- Colspan: 3
- Component:
  - Component Type: Metric Card
- Metric Subtitle: Requiring immediate mitigation
- Metric Icon: fa-bolt
- Metric Icon Style: warning
- Data Source:
  - Type: SQL
  - SQL:
```sql
select count(*) as value
  from ECO_RISK_ALERTS
 where RESOLUTION_STATUS in ('OPEN', 'INVESTIGATING')
   and ALERT_SEVERITY in ('HIGH', 'CRITICAL')
```
##### Region: Suppliers by ESG Rating
- Position: body
- Colstart: 1
- Colspan: 6
- Component:
  - Component Type: Donut Chart
- Chart Title: Distribution by ESG Rating Tier
- Data Source:
  - Type: SQL
  - SQL:
```sql
select ESG_RATING, count(*) as SUPPLIER_COUNT
  from ECO_SUPPLIERS
 group by ESG_RATING
 order by ESG_RATING
```
##### Region: Average Carbon Score by Country
- Position: body
- Colstart: 7
- Colspan: 6
- Component:
  - Component Type: Bar Chart
- Chart Title: Carbon Intensity Benchmark by Country
- Data Source:
  - Type: SQL
  - SQL:
```sql
select COUNTRY, round(avg(CARBON_INTENSITY_SCORE), 1) as AVG_CARBON_SCORE
  from ECO_SUPPLIERS
 group by COUNTRY
 order by AVG_CARBON_SCORE desc
```

### Page 2: Supplier Directory & Risk Scoring
- Description: Multi-faceted directory allowing procurement teams to filter suppliers by country, ESG tier, risk index, and audit status.
- Pattern: faceted-search-report
- Page Mode: standard
- Menu: true
- Page Group: Supplier Risk & Directory
- Security Requirements:
  - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer, Auditor, Executive Viewer
#### Regions
##### Region: Supplier Facets
- Position: left
- Colstart: 1
- Colspan: 3
- Component:
  - Component Type: Facet Filter
- Facets:
  - Facet: Country
    - Type: Checkbox Group
    - Source Column: COUNTRY
  - Facet: ESG Rating
    - Type: Checkbox Group
    - Source Column: ESG_RATING
  - Facet: Financial Risk
    - Type: Radio Group
    - Source Column: FINANCIAL_RISK_INDEX
  - Facet: Audit Status
    - Type: Checkbox Group
    - Source Column: AUDIT_STATUS
##### Region: Suppliers Search Results
- Position: body
- Colstart: 4
- Colspan: 9
- Component:
  - Component Type: Interactive Report
- Data Source:
  - Type: Table
  - Table: ECO_SUPPLIERS
- Actions:
  - Action: Create Supplier
    - Target: Page 3
    - Mode: Create
  - Action: Edit Row Link
    - Target: Page 3
    - Parameter Mapping:
      - P3_ID: ID

### Page 3: Supplier Profile & Remediation
- Description: Drawer modal for inspecting supplier details, modifying risk parameters, and managing audit remediation plans.
- Pattern: slide-out-drawer-form
- Page Mode: drawerModal
- Page Group: Supplier Risk & Directory
- Security Requirements:
  - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer
#### Regions
##### Region: Supplier Form
- Position: body
- Colstart: 1
- Colspan: 12
- Component:
  - Component Type: Form
- Target Table: ECO_SUPPLIERS
- Primary Key: ID
- Items:
  - Item: P3_ID (hidden)
  - Item: P3_SUPPLIER_NAME (text, required)
  - Item: P3_SUPPLIER_CODE (text, required)
  - Item: P3_COUNTRY (selectList, LOV: LOV_COUNTRIES)
  - Item: P3_ESG_RATING (selectList, LOV: LOV_SUPPLIERS_ESG_RATING)
  - Item: P3_CARBON_INTENSITY_SCORE (number)
  - Item: P3_FINANCIAL_RISK_INDEX (selectList, LOV: LOV_SUPPLIERS_FINANCIAL_RISK_INDEX)
  - Item: P3_AUDIT_STATUS (selectList, LOV: LOV_SUPPLIERS_AUDIT_STATUS)
  - Item: P3_PRIMARY_CONTACT_EMAIL (text)
  - Item: P3_CONTRACT_VALUE (number, format: FML999G999G999D00)
  - Item: P3_MITIGATION_PLAN (textarea, dynamic visibility when ESG_RATING in ('D', 'F'))

### Page 4: ESG & Carbon Audits Hub
- Description: Multi-year greenhouse gas carbon accounting (Scope 1, 2, and 3) and regulatory audit verification records.
- Pattern: interactive-report
- Page Mode: standard
- Menu: true
- Page Group: ESG & Carbon Accounting
- Security Requirements:
  - Authorized Roles: Administrator, Sustainability Manager, Auditor, Executive Viewer
#### Regions
##### Region: Carbon Audits Report
- Position: body
- Colstart: 1
- Colspan: 12
- Component:
  - Component Type: Interactive Report
- Data Source:
  - Type: SQL
  - SQL:
```sql
select a.ID,
       s.SUPPLIER_NAME,
       a.AUDIT_YEAR,
       a.AUDIT_TYPE,
       a.SCOPE1_CO2_TONNES,
       a.SCOPE2_CO2_TONNES,
       a.SCOPE3_CO2_TONNES,
       (a.SCOPE1_CO2_TONNES + a.SCOPE2_CO2_TONNES + a.SCOPE3_CO2_TONNES) as TOTAL_CO2_TONNES,
       a.RENEWABLE_ENERGY_PCT,
       a.AUDIT_OUTCOME,
       a.AUDIT_DATE,
       a.AUDITOR_NAME
  from ECO_SUPPLIER_AUDITS a
  join ECO_SUPPLIERS s on s.ID = a.SUPPLIER_ID
 order by a.AUDIT_YEAR desc, a.AUDIT_DATE desc
```
- Actions:
  - Action: Log New Audit
    - Target: Page 5
    - Mode: Create

### Page 5: ESG Audit Record Detail
- Description: Standard modal form to submit annual emissions disclosures, environmental verifications, and compliance findings.
- Pattern: modal-dialog-form
- Page Mode: modalDialog
- Page Group: ESG & Carbon Accounting
- Security Requirements:
  - Authorized Roles: Administrator, Sustainability Manager, Auditor

### Page 6: Risk Alerts & Exception Stream
- Description: Real-time supply chain disruption, financial risk anomaly, and environmental non-compliance alert feed.
- Pattern: interactive-report-with-badges
- Page Mode: standard
- Menu: true
- Page Group: Risk & Compliance Feed
- Security Requirements:
  - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer, Auditor, Executive Viewer
#### Regions
##### Region: Anomaly Alerts Feed
- Position: body
- Colstart: 1
- Colspan: 12
- Component:
  - Component Type: Interactive Report
- Data Source:
  - Type: SQL
  - SQL:
```sql
select r.ID,
       s.SUPPLIER_NAME,
       r.ALERT_TYPE,
       r.ALERT_SEVERITY,
       r.ALERT_TITLE,
       r.ALERT_DESCRIPTION,
       r.RESOLUTION_STATUS,
       r.DETECTED_DATE,
       r.AI_CONFIDENCE_SCORE
  from ECO_RISK_ALERTS r
  join ECO_SUPPLIERS s on s.ID = r.SUPPLIER_ID
 order by r.DETECTED_DATE desc
```

### Page 7: Risk Alert Remediation
- Description: Modal dialog for acknowledging alerts, escalating investigations, and closing risk anomalies with root-cause notes.
- Pattern: modal-dialog-form
- Page Mode: modalDialog
- Page Group: Risk & Compliance Feed
- Security Requirements:
  - Authorized Roles: Administrator, Sustainability Manager, Procurement Officer

### Page 8: Sustainability & ESG Analytics Hub
- Description: Deep-dive charts for multi-year Scope 3 carbon trajectories, renewable energy adoption, and ESG rating transitions.
- Pattern: chart-analytics-grid
- Page Mode: standard
- Menu: true
- Page Group: ESG & Carbon Accounting
- Security Requirements:
  - Authorized Roles: Administrator, Sustainability Manager, Executive Viewer

### Page 9: Administration & Settings Hub
- Description: System settings, user role assignments, audit thresholds, and controlled lookup lists.
- Pattern: admin-dashboard
- Page Mode: standard
- Menu: true
- Page Group: Administration
- Security Requirements:
  - Authorized Roles: Administrator
