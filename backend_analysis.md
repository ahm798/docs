# Gov360 Backend API Analysis Report

## Executive Summary

This report provides a comprehensive analysis of existing backend endpoints and identifies missing endpoints required for complete Strategic Performance module functionality. The analysis covers all entities: Strategy, Perspective, Goal, Initiative, Indicator, and Vision components.

### Key Findings Summary

| Feature | Status | Impact | Module | Description |
|---------|--------|--------|--------|-------------|
| Team Members Management | ❌ Missing | HIGH | Strategy, Perspective, Goal, Initiative, Indicator | CRUD endpoints for team member assignment |
| Risk Management | ❌ Missing | HIGH | All Modules | Full risk entity and relationship endpoints |
| Perspective FAT Endpoint | ⚠️ Issue | HIGH | Perspective | Single endpoint returning all nested data needs splitting |
| Vision Goals | ❌ Missing | HIGH | Vision | Link/unlink goals to vision priorities |
| Vision Indicators | ❌ Missing | HIGH | Vision | Link/unlink indicators to vision priorities |
| Initiative Type | ❌ Missing | HIGH | Initiative | Lookup table for initiative types |
| Initiative Contributors | ❌ Missing | MEDIUM | Initiative | Team contributors separate from owners |
| Budget Source Lookup | ❌ Missing | HIGH | Cross-Cutting | Reference table for budget sources |
| Initiative Budget Sources | ❌ Missing | HIGH | Initiative | Track multiple budget sources per initiative |
| Initiative Payments | ❌ Missing | HIGH | Initiative | Payment tracking and management |
| Organization Unit Definition | ⚠️ Unclear | MEDIUM | Organization | Clarification needed on org unit structure |
| Owner Division (UI) | ⚠️ Unclear | MEDIUM | Organization | UI field mapping to backend unclear |

---

## 1. Strategy Module API Analysis

### 1.1 Existing Endpoints (Spring Data REST Auto-Generated)

#### ✅ List Strategies Page Endpoints

| Method | Endpoint | Status | UI Component |
|--------|----------|--------|--------------|
| GET | `/strategies` | ✅ Implemented | List all strategies with pagination (All Strategies - 3) |
| GET | `/strategies/{id}` | ✅ Implemented | Get strategy details for card display |

#### ✅ Basic CRUD Operations

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| POST | `/strategies` | ✅ Implemented | Create new strategy |
| PUT | `/strategies/{id}` | ✅ Implemented | Full update strategy |
| PATCH | `/strategies/{id}` | ✅ Implemented | Partial update strategy |
| DELETE | `/strategies/{id}` | ✅ Implemented | Soft delete strategy |

---

### 1.2 Missing Strategy Endpoints

#### 📋 List Strategies Page Endpoints

| Method | Endpoint | Priority | UI Component |
|--------|----------|----------|--------------|
| GET | `/strategies/filter` | HIGH | Filter strategies (Filters button) |
| GET | `/strategies?sort=...` | HIGH | Sort strategies (Sort button) |

**Filter Parameters for List Page:**
- `status` - Filter by status (Started, Paused, etc.)
- `startDate` - Filter by start date range
- `endDate` - Filter by end date range
- `teamMembers` - Filter by team members
- `search` - Search in strategy name/description

#### 📊 Dashboard Cards Endpoints

| Method | Endpoint | Priority | Dashboard Card |
|--------|----------|----------|----------------|
| GET | `/strategies/{id}/progress-overview` | HIGH | Overall Achievement (50% vs Target) |
| GET | `/strategies/{id}/kpis-summary` | HIGH | KPIs at Risk (18 total: 32 On Track, 15 At Risk, 3 Off Track) |
| GET | `/strategies/{id}/budget-consumption` | HIGH | Budget Consumption (35%: 25M Spent, 15M Left) |
| GET | `/strategies/{id}/milestones-summary` | HIGH | Milestones (4 total: 3 On Time, 2 Delayed) |


#### 👥 Team Management

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/strategies/{id}/team-members` | HIGH | Team Management |
| POST | `/strategies/{id}/team-members` | HIGH | Team Management |
| PUT | `/strategies/{id}/team-members/{userId}` | MEDIUM | Team Management |
| DELETE | `/strategies/{id}/team-members/{userId}` | MEDIUM | Team Management |

#### strategy details

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/strategies/{id}/perspectives` | HIGH | budget Management |
| GET | `/strategies/{id}/goals` | HIGH | goals Management |
| GET | `/strategies/{id}/indicators` | HIGH | indicators Management |
| GET | `/strategies/{id}/initiative` | HIGH | initiative Management |



---

## 2. Perspective Module API Analysis

### 2.1 Existing Endpoints

#### ✅ Basic CRUD Operations

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/perspectives` | ✅ Implemented | List all perspectives |
| GET | `/perspectives/{id}` | ✅ Implemented | Get perspective by ID |
| POST | `/perspectives` | ✅ Implemented | Create perspective (requires parent strategy) |
| PUT | `/perspectives/{id}` | ✅ Implemented | Update perspective |
| PATCH | `/perspectives/{id}` | ✅ Implemented | Partial update |
| DELETE | `/perspectives/{id}` | ✅ Implemented | Delete perspective |

#### ✅ Relationship Navigation

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/perspectives/{id}/goals` | ✅ Implemented | Get child goals |
| GET | `/perspectives/{id}/initiatives` | ✅ Implemented | Get child initiatives |
| GET | `/perspectives/{id}/parent` | ✅ Implemented | Get parent strategy |

---

### 2.2 Missing Perspective Endpoints

#### 🔵 Aggregation Endpoints

| Method | Endpoint | Status | Description | Priority |
|--------|----------|--------|-------------|----------|
| GET | `/perspectives/{id}` | ❌ Missing | List all goals, indecators, intiatives and risk  | HIGH |
| GET | `/perspectives/{id}/indicators` | ✅ Implemented | Get child indicators |
| GET | `/perspectives/{id}/risk` | ✅ Implemented | Get  risk |




## NOTE: pervious endpoint is bad design should be splited or paginated


#### 👥 Team Management

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/perspectives/{id}/team-members` | HIGH | Team Management |
| POST | `/perspectives/{id}/team-members` | HIGH | Team Management |
| PUT | `/perspectives/{id}/team-members/{userId}` | MEDIUM | Team Management |
| DELETE | `/perspectives/{id}/team-members/{userId}` | MEDIUM | Team Management |

---

## 3. Goal Module API Analysis

### 3.1 Existing Endpoints

#### ✅ Basic CRUD Operations

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/goals` | ✅ Implemented | List all goals |
| GET | `/goals/{id}` | ✅ Implemented | Get goal by ID (includes calculated health) |
| POST | `/goals` | ✅ Implemented | Create goal |
| PUT | `/goals/{id}` | ✅ Implemented | Update goal |
| PATCH | `/goals/{id}` | ✅ Implemented | Partial update |
| DELETE | `/goals/{id}` | ✅ Implemented | Delete goal |

#### ✅ Relationship Endpoints

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/goals/{id}/indicators` | ✅ Implemented | Get linked indicators (many-to-many) |
| PUT | `/goals/{id}/indicators` | ✅ Implemented | Replace all indicator links |
| POST | `/goals/{id}/indicators` | ⚠️ Partial | Add indicator link (text/uri-list format) |
| DELETE | `/goals/{id}/indicators/{indicatorId}` | ✅ Implemented | Remove indicator link |

#### ✅ Initiative Impact Endpoints

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/goals/{id}/impacts-by-initiatives` | ✅ Implemented | Get initiatives impacting this goal |
| POST | `/goals/{id}/impacts-by-initiatives` | ✅ Implemented | Add initiative impact |
| PUT | `/goals/{id}/impacts-by-initiatives` | ✅ Implemented | Replace all impacts |
| PATCH | `/goals/{id}/impacts-by-initiatives/{initiativeId}` | ✅ Implemented | Update impact level |
| DELETE | `/goals/{id}/impacts-by-initiatives/{initiativeId}` | ✅ Implemented | Remove impact link |

---

### 3.2 Missing Goal Endpoints

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/goals/search?strategyIds=uuid1,uuid2&perspectiveIds=uuid3,uuid4` | HIGH | List & Filter |
| GET | `/goals/summary` | HIGH | Dashboard Metrics |
| POST | `/goals/{id}/indicators/link` | HIGH | Indicator Linking (JSON format) |
| POST | `/goals/{id}/indicators/unlink` | HIGH | Indicator unLinking (JSON format) |
| POST | `/goals/{id}/indicators/new` | HIGH | Create & Link Indicator |
| GET | `/goals/{id}/health-trend` | MEDIUM | Health & Analytics |
| GET | `/goals/{id}/indicator-summary` | HIGH | Health & Analytics |
| GET | `/goals/{id}/risk-assessment` | HIGH | Health & Analytics |
| GET | `/goals/{id}/budget` | MEDIUM | Budget Management |
| GET | `/goals/{id}/team-members` | MEDIUM | Team Management |
| POST | `/goals/{id}/team-members` | MEDIUM | Team Management |
| DELETE | `/goals/{id}/team-members/{userId}` | LOW | Team Management |
| GET | `/goals/{id}/risks` | MEDIUM | Risk Management |
| POST | `/goals/{id}/risks` | MEDIUM | Risk Management |
| PUT | `/goals/{id}/risks/{riskId}` | MEDIUM | Risk Management |
| DELETE | `/goals/{id}/risks/{riskId}` | LOW | Risk Management |

---

## 4. Initiative Module API Analysis

### 4.1 Existing Endpoints

#### ✅ Basic CRUD Operations

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/initiatives` | ✅ Implemented | List all initiatives |
| GET | `/initiatives/{id}` | ✅ Implemented | Get initiative with milestones and progress |
| POST | `/initiatives` | ✅ Implemented | Create initiative |
| PUT | `/initiatives/{id}` | ✅ Implemented | Update initiative |
| PATCH | `/initiatives/{id}` | ✅ Implemented | Partial update (e.g., add progress entry) |
| DELETE | `/initiatives/{id}` | ✅ Implemented | Delete initiative |

#### ✅ Relationship Endpoints

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/initiatives/{id}/impacts-on-goals` | ✅ Implemented | Get goals this initiative impacts |
| GET | `/initiatives/{id}/parent` | ✅ Implemented | Get parent perspective |

---

### 4.2 Missing Initiative Endpoints

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/initiatives/search?strategyIds=uuid1&perspectiveIds=uuid2&goalIds=uuid3` | HIGH | List & Filter |
| GET | `/initiatives/summary` | HIGH | Dashboard Metrics |
| GET | `/initiatives/{id}/milestones` | HIGH | Milestone Management |
| POST | `/initiatives/{id}/milestones` | HIGH | Milestone Management |
| PUT | `/initiatives/{id}/milestones/{index}` | MEDIUM | Milestone Management |
| DELETE | `/initiatives/{id}/milestones/{index}` | MEDIUM | Milestone Management |
| POST | `/initiatives/{id}/progress-log` | HIGH | Progress Tracking |
| PUT | `/initiatives/{id}/progress-log/{index}` | MEDIUM | Progress Tracking |
| DELETE | `/initiatives/{id}/progress-log/{index}` | LOW | Progress Tracking |
| GET | `/initiatives/{id}/progress-analysis` | HIGH | Progress Analytics |
| GET | `/initiatives/{id}/completion-forecast` | MEDIUM | Progress Analytics |
| GET | `/initiatives/{id}/budget` | HIGH | Budget Management |
| PUT | `/initiatives/{id}/budget` | HIGH | Budget Management |
| GET | `/initiatives/{id}/budget-utilization` | HIGH | Budget Tracking |
| GET | `/initiatives/{id}/payments` | HIGH | Payment Management |
| POST | `/initiatives/{id}/payments` | HIGH | Payment Management |
| PUT | `/initiatives/{id}/payments/{paymentId}` | MEDIUM | Payment Management |
| DELETE | `/initiatives/{id}/payments/{paymentId}` | MEDIUM | Payment Management |
| GET | `/initiatives/{id}/team-members` | MEDIUM | Team Management |
| POST | `/initiatives/{id}/team-members` | MEDIUM | Team Management |
| PUT | `/initiatives/{id}/team-members/{userId}` | LOW | Team Management |
| DELETE | `/initiatives/{id}/team-members/{userId}` | LOW | Team Management |
| GET | `/initiatives/{id}/risks` | MEDIUM | Risk Management |
| POST | `/initiatives/{id}/risks` | MEDIUM | Risk Management |
| PUT | `/initiatives/{id}/risks/{riskId}` | MEDIUM | Risk Management |
| DELETE | `/initiatives/{id}/risks/{riskId}` | LOW | Risk Management |


## 5. Indicator Module API Analysis

### 5.1 Existing Endpoints

#### ✅ Basic CRUD Operations

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/indicators` | ✅ Implemented | List all indicators |
| GET | `/indicators/{id}` | ✅ Implemented | Get indicator with baseline/target/actual |
| POST | `/indicators` | ✅ Implemented | Create indicator |
| PUT | `/indicators/{id}` | ✅ Implemented | Update indicator |
| PATCH | `/indicators/{id}` | ✅ Implemented | Partial update (add actuals) |
| DELETE | `/indicators/{id}` | ✅ Implemented | Delete indicator |



---

### 5.2 Missing Indicator Endpoints

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/indicators/search` | MEDIUM | Search & Filter |
| GET | `/indicators/metric` | HIGH | Indicators Metric |
| PUT | `/indicators/{id}/yearly-targets/{year}` | HIGH | Yearly Targets Management |
| POST | `/indicators/{id}/yearly-targets/{year}` | HIGH | Yearly Targets Management |
| DELETE | `/indicators/{id}/yearly-targets/{year}` | MEDIUM | Yearly Targets Management |
| GET | `/indicators/{id}/quarterly-analysis` | MEDIUM | Quarterly Analysis |
| GET | `/indicators/{id}/team-members` | MEDIUM | Team Management |
| POST | `/indicators/{id}/team-members` | MEDIUM | Team Management |
| PUT | `/indicators/{id}/team-members/{userId}` | LOW | Team Management |
| DELETE | `/indicators/{id}/team-members/{userId}` | LOW | Team Management |

---

## 6. Vision Module API Analysis

### 6.1 Existing Endpoints

#### ✅ Vision Pillar

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/vision-pillars` | ✅ Implemented | List vision pillars |
| GET | `/vision-pillars/{id}` | ✅ Implemented | Get vision pillar |
| POST | `/vision-pillars` | ✅ Implemented | Create vision pillar |
| PUT/PATCH/DELETE | `/vision-pillars/{id}` | ✅ Implemented | Update/Delete |

#### ✅ Vision Priority

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/vision-priorities` | ✅ Implemented | List vision priorities |
| GET | `/vision-priorities/{id}` | ✅ Implemented | Get vision priority |
| POST | `/vision-priorities` | ✅ Implemented | Create vision priority |
| PUT/PATCH/DELETE | `/vision-priorities/{id}` | ✅ Implemented | Update/Delete |

---

### 6.2 Missing Vision Endpoints

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/vision-pillars/{id}/priorities` | HIGH | Pillar-Priority Relationship |
| GET | `/vision-pillars/{id}/full` | HIGH | Pillar Hierarchical View |
| GET | `/vision-priorities/{id}/goals` | HIGH | Priority-Goals Relationship |
| GET | `/vision-priorities/{id}/indicators` | HIGH | Priority-Indicators Relationship |
| POST | `/vision-priorities/{id}/goals` | HIGH | Link Goal to Priority |
| POST | `/vision-priorities/{id}/indicators` | HIGH | Link Indicator to Priority |
| DELETE | `/vision-priorities/{id}/goals/{goalId}` | MEDIUM | Unlink Goal from Priority |
| DELETE | `/vision-priorities/{id}/indicators/{indicatorId}` | MEDIUM | Unlink Indicator from Priority |

---

## 7. Cross-Cutting Endpoints

### 7.1 Existing

#### ✅ Permissions Management

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| POST | `/permissions/{kind}/{id}/{relation}` | ✅ Implemented | Grant permission |
| DELETE | `/permissions/{kind}/{id}/{relation}` | ✅ Implemented | Revoke permission |

Supported: strategies, perspectives, goals, initiatives (admins, writers, readers)

---


#### ❌ Risk Management Endpoints

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/risks` | HIGH | Risk CRUD |
| GET | `/risks/{id}` | HIGH | Risk CRUD |
| POST | `/risks` | HIGH | Risk CRUD |
| PUT | `/risks/{id}` | MEDIUM | Risk CRUD |
| DELETE | `/risks/{id}` | MEDIUM | Risk CRUD |

---

## 8. Organization & User Management Module

### 8.1 Existing Endpoints

#### ✅ User Management

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| POST | `/users` | ✅ Implemented | Create user (Keycloak) |
| DELETE | `/users/{sub}` | ✅ Implemented | Disable user |

#### ✅ Organizations

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/organizations` | ✅ Implemented | List organizations |
| GET | `/organizations/{id}` | ✅ Implemented | Get organization |
| POST | `/organizations` | ✅ Implemented | Create organization |
| PUT/PATCH | `/organizations/{id}` | ✅ Implemented | Update organization |
| DELETE | `/organizations/{id}` | ✅ Implemented | Delete organization |

#### ✅ Organization Groups

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/organization-groups` | ✅ Implemented | List groups |
| GET | `/organization-groups/{id}` | ✅ Implemented | Get group |
| POST | `/organization-groups` | ✅ Implemented | Create group |
| PUT/PATCH | `/organization-groups/{id}` | ✅ Implemented | Update group |
| DELETE | `/organization-groups/{id}` | ✅ Implemented | Delete group |

#### ✅ Organization Members

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/organization-members` | ✅ Implemented | List members |
| GET | `/organization-members/{id}` | ✅ Implemented | Get member |
| GET | `/organization-members/search/by-sub?sub={uuid}` | ✅ Implemented | Find by user sub |
| POST | `/organization-members` | ✅ Implemented | Create member |
| PUT/PATCH | `/organization-members/{id}` | ✅ Implemented | Update member |
| DELETE | `/organization-members/{id}` | ✅ Implemented | Delete member |

#### ✅ Organization Units (Neo4j)

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/organization-units` | ✅ Implemented | List units |
| GET | `/organization-units/{id}` | ✅ Implemented | Get unit |
| GET | `/organization-units/{id}/tree?depth={n}` | ✅ Implemented | Get unit tree |
| GET | `/organizations/{id}/organization-unit/tree?depth={n}` | ✅ Implemented | Get org tree |
| POST | `/organization-units` | ✅ Implemented | Create unit |
| PUT/PATCH | `/organization-units/{id}` | ✅ Implemented | Update unit |
| DELETE | `/organization-units/{id}` | ✅ Implemented | Delete unit |

#### ✅ Organization Permissions

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| POST | `/permissions/{kind}/{id}/{relation}` | ✅ Implemented | Grant permission |
| DELETE | `/permissions/{kind}/{id}/{relation}` | ✅ Implemented | Revoke permission |

Supported: organizations, organization-groups (writers, admins)

---

### 8.2 Missing Organization Endpoints

| Method | Endpoint | Priority | Category |
|--------|----------|----------|----------|
| GET | `/users/{sub}` | HIGH | User Details |
| GET | `/users/search?email={email}` | MEDIUM | User Search |
| PUT | `/users/{sub}` | MEDIUM | Update User |
| GET | `/organizations/{id}/members` | HIGH | Org Members List |
| GET | `/organizations/{id}/units` | HIGH | Org Units List |

---

**End of Gap Analysis Report**

