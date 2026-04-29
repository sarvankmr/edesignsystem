# Centralized Tag Management — PRD, Example Tag Library & Prototype Specification

**Domain:** Siemens Electrification X SaaS platform  
**Capability:** Universal and consistent tagging across feature sets  
**Target feature sets:** OTC, SEM, EVLM, OT Companion, dashboards, assets, locations, devices, documents, settings templates  
**Primary goal:** Create a production-grade centralized tag management concept that is easy to configure, simple to use, governed centrally, and scalable across modules.

---

## 1. Executive Summary

Electrification X needs a centralized tagging framework that lets customers organize assets, devices, locations, documents, dashboards, widgets, and configuration objects according to their own operational mental model.

A good tagging framework should solve three problems:

1. **Customer organization problem** — customers think in terms of plant, zone, voltage level, DSO, function, priority, contract, known issues, and operational cohorts, not only system hierarchy.
2. **Data consistency problem** — without a central tag library, users create duplicate variations such as `Cooling`, `cooling`, `COOLING`, `Cool`, and `Cooling System`.
3. **Cross-feature visibility problem** — a tag assigned in one feature set should be visible and searchable in another when the object is shared.

The recommended solution is a **tenant-level central tag registry** managed in **Settings → Tag Management**, combined with lightweight assignment controls across object views.

---

## 2. Product Vision

Create a tag system that feels:

- **Fast like Gmail labels**
- **Flexible like Notion multi-select properties**
- **Searchable like Jira / Azure DevOps labels**
- **Visual like Trello labels**
- **Governed like enterprise master data**
- **Future-ready for AI-assisted classification**

The experience should be powerful for engineers and admins, but simple for operators.

---

## 3. Goal 1 — Ideal Example Tags for Siemens Electrification X SaaS Platform

This section provides the missing **example tag library** for a Siemens Electrification X SaaS domain. These tags should be used as a realistic starter set for prototyping and as a best-practice reference for production taxonomy design.

### 3.1 Tag Strategy for Electrification X

Tags should help users answer practical operational questions:

- Which substations/assets belong to a specific voltage level?
- Which assets are cooling, protection, metering, or safety-related?
- Which devices or chargers are known issues, recurrent faults, or under investigation?
- Which locations are tied to a specific DSO, contract, vendor, or operations team?
- Which EV sites are highway, city-centre, suburban, truck station, or car station sites?
- Which documents are approved, draft, commissioning-related, maintenance-related, or superseded?
- Which widgets or dashboards are scoped to 10kV, feeder alarms, EV operations, or substation health?

### 3.2 Recommended Tag Categories and Examples

| Tag Category | Example Tags | Best Used On | Electrification X Scenario | UX / Business Value | Governance Guidance |
|---|---|---|---|---|---|
| Physical / geographic context | `Plant-A`, `Zone-3`, `Building-B`, `Floor-2`, `Yard-East`, `Substation-North` | Locations, assets, devices, dashboards | Filter assets by operational area or physical site zone | Matches how customers organize field operations | Define naming format once; avoid both `Plant A` and `Plant-A` |
| Voltage level / electrical context | `10kV`, `33kV`, `110kV`, `220kV`, `380kV`, `LV`, `MV`, `HV` | Locations, substations, feeders, assets, widgets | Identify substations, feeders, assets, or widgets by voltage class | Very strong fit for grid and electrification workflows | Standardize notation; use `10kV`, not mixed `10 KV`, `10kv`, `10-KV` |
| Functional role | `Cooling`, `Heating`, `Protection`, `Metering`, `Safety`, `Backup`, `Primary`, `Power-Quality` | Assets, devices, templates, widgets | Group equipment by engineering function | Helps new users understand asset purpose quickly | Use short functional nouns; avoid long phrases |
| Asset criticality | `Critical`, `High-Priority`, `Routine`, `Business-Critical`, `Safety-Critical` | Assets, locations, devices | Prioritize operations, inspection, alarm triage, and maintenance | Enables fast filtering of important equipment | Define difference between `Critical` and `High-Priority` clearly |
| Operational state | `Active`, `Under-Maintenance`, `Decommissioned`, `Commissioning`, `Temporary-Outage`, `Planned-Shutdown` | Assets, locations, devices | Add operational lifecycle or temporary context | Helps contextualize alarms and maintenance work | Do not duplicate official system status unless customer-specific context is needed |
| Investigation / fault handling | `Known-Issue`, `Watch-List`, `Recurrent-Fault`, `Chronic-Issue`, `Under-Investigation`, `Escalated`, `Analyzed`, `First-Fault` | Assets, devices, chargers, fault records | Mark repeated issues, known problems, and active investigations | Supports triage, vendor escalation, and maintenance planning | Add review/expiry date for temporary issue tags |
| Ownership / responsibility | `Team-Alpha`, `Team-North`, `Ops-Team-1`, `Maintenance-Team`, `Vendor-X`, `Vendor-Y`, `OEM-Siemens` | Assets, devices, locations, documents | Show responsible team or vendor | Helps route work and clarify accountability | Use structured owner fields for official ownership; use tags for flexible grouping |
| DSO / contract relationship | `DSO-Amprion`, `DSO-50Hertz`, `DSO-Tenant`, `Contract-2024`, `SLA-Premium`, `Grid-Connection-A` | Sites, locations, EV charging stations, documents | Group sites by DSO contract or load management relationship | Helps operators know whom to contact during DSO signal issues | Avoid sensitive contract identifiers unless permitted |
| EV charging site type | `Highway`, `City-Centre`, `Suburban`, `Motorway-Service`, `Fleet-Depot`, `Truck-Station`, `Car-Station` | EV sites, chargers, dashboards | Segment EV sites by demographic or business context | Useful for EV business performance and cohort monitoring | Keep site-type taxonomy limited and stable |
| Charger capacity / station model | `4-Charger`, `6-Charger`, `8-Charger`, `Fast-Charger`, `Depot-Charger`, `Public-Charger` | Chargers, EV sites, EV dashboards | Filter/bulk-operate by charger type or site capacity | Useful for firmware updates and rollout targeting | Treat as controlled configuration labels |
| Network / security segmentation | `OT-Network`, `IT-Network`, `DMZ`, `Segment-A`, `Purdue-Level-1`, `Purdue-Level-2`, `Purdue-Level-3` | Devices, assets, locations, cybersecurity views | Group devices by security/network architecture | Supports OT Companion and cyber workflows | Use approved cybersecurity terminology |
| Alarm / monitoring context | `Alarm-Heavy`, `Noise-Prone`, `Monitor-Only`, `Needs-Review`, `Ignore-During-Maintenance`, `Suppressed-Context` | Assets, devices, alarm widgets | Distinguish known alarm patterns from new incidents | Reduces repeated investigation effort | Avoid using tags to silently hide safety-critical issues |
| Sustainability / energy use | `High-Consumption`, `Peak-Load`, `Load-Shedding`, `Energy-Saving`, `Demand-Response`, `Carbon-Reporting` | Assets, sites, SEM dashboards | Group assets/sites for energy and load management use cases | Supports SEM views and energy optimization | Align with SEM terminology and reporting model |
| Document classification | `Commissioning`, `Maintenance-Manual`, `Approved`, `Draft`, `Superseded`, `IEC-Standard`, `Template`, `Inspection-Report` | Documents, manuals, templates | Classify documents consistently across modules | Prevents local free-text document tag chaos | Use central tags instead of document-only free text |
| Configuration / template type | `Protection-Settings`, `Baseline-Template`, `Relay-Config`, `Firmware-Update`, `Tested`, `Reusable`, `Customer-Specific` | Settings templates, configuration datasets, documents | Classify reusable configuration artifacts | Supports OTC template search and reuse | Avoid version numbers as tags unless truly required |
| Compliance / inspection | `Inspection-Due`, `Audit-Ready`, `Non-Compliant`, `Permit-Required`, `Regulatory`, `Safety-Check` | Assets, locations, documents | Track compliance and inspection context | Useful for audit preparation and safety workflows | Tags should complement, not replace, formal compliance workflow status |
| Business priority / customer segment | `Premium-Customer`, `Strategic-Site`, `Revenue-Critical`, `Pilot-Site`, `Demo-Site`, `Training-Site` | Sites, dashboards, reports | Segment sites by business importance | Supports rollout planning and executive views | Restrict sensitive business labels if required |
| Dashboard / widget scope | `Fleet-Overview`, `Substation-Health`, `Feeder-Alarms`, `10kV-View`, `EVLM-Operations`, `OTC-Templates` | Dashboards, widgets | Make dashboards and widgets searchable by scope | Useful when many dashboards/widgets exist | Keep widget tags descriptive but short |
| Migration / onboarding | `Imported`, `Needs-Validation`, `Validated`, `Legacy-System`, `New-Onboarding`, `Data-Cleanup` | Assets, locations, devices, documents | Track onboarding and data quality cleanup | Useful during migration and tenant setup | Archive after onboarding is complete |
| AI / automation readiness | `AI-Suggested`, `Auto-Classified`, `Rule-Based`, `Review-AI-Tag`, `Confidence-Low` | Future: assets, documents, insights | Identify tags created or suggested by automation | Builds transparency for future agentic workflows | Show source and confidence before auto-apply |

### 3.3 Recommended Starter Tag Library for Prototype

Use this starter set in the prototype so the concept feels realistic but not overloaded.

| Category | Starter Tags | Object Types to Demonstrate |
|---|---|---|
| Voltage Level | `10kV`, `33kV`, `110kV`, `380kV` | Locations, assets, widgets |
| Function | `Cooling`, `Protection`, `Metering`, `Safety` | Assets, devices |
| Criticality | `Critical`, `Routine`, `High-Priority` | Assets, locations |
| Operational Context | `Under-Maintenance`, `Known-Issue`, `Watch-List` | Assets, devices, chargers |
| EV Site Type | `Highway`, `City-Centre`, `Suburban`, `Truck-Station` | EV sites, chargers |
| Ownership | `Team-Alpha`, `Vendor-X`, `DSO-Amprion` | Locations, assets, documents |
| Investigation | `Recurrent-Fault`, `Under-Investigation`, `Escalated` | Chargers, fault records, assets |
| Document Type | `Maintenance-Manual`, `Approved`, `Draft`, `Superseded` | Documents, templates |
| Configuration | `Protection-Settings`, `Baseline-Template`, `Firmware-Update` | Settings templates, documents |
| Onboarding | `Imported`, `Needs-Validation`, `Validated` | Assets, locations, devices |

### 3.4 Good vs Poor Tag Examples

| Poor Tag | Better Tag | Reason |
|---|---|---|
| `cooling assets urgent` | `Cooling` + `High-Priority` | Use multiple reusable tags instead of one mixed tag |
| `10 KV`, `10kv`, `10-KV` | `10kV` | Normalize electrical notation |
| `team alpha responsible` | `Team-Alpha` | Keep tag short and scannable |
| `fault happens many times` | `Recurrent-Fault` | Use operational vocabulary |
| `vendor escalation needed` | `Escalated` + `Vendor-X` | Separate workflow state from ownership |
| `doc approved final latest` | `Approved` | Avoid ambiguous status combinations |
| `city`, `citycenter`, `City Center` | `City-Centre` | Choose one tenant-approved spelling |

### 3.5 Recommended Tag Color Strategy

Color should improve scanning, not become the only carrier of meaning.

| Category | Color Intent | Example Tags |
|---|---|---|
| Criticality | High attention | `Critical`, `High-Priority` |
| Operational / Investigation | Work-in-progress | `Under-Investigation`, `Watch-List`, `Known-Issue` |
| Function | Neutral classification | `Cooling`, `Protection`, `Metering` |
| Location / Geography | Spatial context | `Plant-A`, `Zone-3`, `Highway` |
| Ownership / Contract | Responsibility context | `Team-Alpha`, `Vendor-X`, `DSO-Amprion` |
| Document / Configuration | Knowledge artifact | `Approved`, `Draft`, `Protection-Settings` |

---

## 4. Product Requirements

### 4.1 Centralized Tag Management

Users with the right permission can manage tags centrally per tenant from:

```text
Settings → Tag Management
```

Required capabilities:

- Add tag
- Edit tag
- Archive tag
- Delete tag only when unused or after safe reassignment
- View usage count
- View where tag is used
- Search tags
- Filter tags by category/status
- Detect duplicates
- Manage color/category
- Manage description and governance metadata

### 4.2 Tag Assignment

Users can assign tags from the central library to supported objects.

Supported Step 1 objects:

- Locations
- Assets
- Devices
- Documents
- Settings templates

Optional/future objects:

- Widgets
- Dashboards
- Signals
- Datapoints
- Fault records
- Rules
- AI insights

Assignment behavior:

- User selects from predefined central tags.
- Typeahead search is supported.
- Maximum 5 tags per object in V1.
- Tag is applied instantly or with a clear save pattern depending on object edit mode.
- Removal should be safe but not over-confirmed.
- Operators can assign existing tags but cannot create/edit/delete the tag library.

### 4.3 Tag Searchability

Tags must be searchable and filterable where they create value:

- Asset tree
- Asset list
- Device list
- Location list
- Document library
- Dashboard/widget list
- Detail pages
- Cross-object search results

Search examples:

```text
tag:Critical
tag:10kV
tag:Recurrent-Fault
```

Filtering examples:

- `Critical` + `Cooling`
- `DSO-Amprion` + `Highway`
- `Known-Issue` + `Under-Maintenance`
- `10kV` + `Protection`

### 4.4 Tag Visualization

Tags should appear as consistent chips/badges across the application.

Display rules:

- Show max 3 visible tags in compact lists.
- Show `+N` overflow indicator.
- On hover/click, show remaining tags.
- On object detail pages, show full tag section.
- Tag chips should be searchable, keyboard accessible, and screen-reader friendly.

Example:

```text
[Critical] [Cooling] [10kV] +2
```

---

## 5. UX Best Practice Strategy

### 5.1 Core UX Principle

Tags should be **easy to assign at the point of use** and **centrally governed in Settings**.

Do not force users to leave their workflow just to tag an object.

### 5.2 Recommended Object Detail Pattern

```text
Asset: Transformer-01

Tags
[Protection] [Critical] [+ Add tag]
```

When the user clicks `+ Add tag`, open a combobox:

- Search existing tags
- Show recently used tags
- Show suggested tags
- Multi-select support
- Clear empty state
- No free-text creation for Operators

### 5.3 Recommended List / Table Pattern

| Asset | Type | Location | Tags | Status |
|---|---|---|---|---|
| Transformer-01 | Transformer | Plant-A | `Protection`, `Critical` | Active |
| Cooler-07 | Cooler | Zone-3 | `Cooling`, `Routine` | Active |
| Charger-EF04 | Charger | Highway-Site | `Recurrent-Fault`, `Watch-List` | Warning |

### 5.4 Safe Removal Pattern

For normal object-level tag removal:

```text
Remove tag “Critical” from Transformer-01?
[Cancel] [Remove]
```

For bulk removal:

```text
Remove tag “Critical” from 48 selected assets?
This will not delete the tag from the central library.
[Cancel] [Remove from selected]
```

### 5.5 Deletion vs Archive

Production systems should prefer **Archive** over hard delete.

| Action | Recommended Behavior |
|---|---|
| Delete unused tag | Allowed with confirmation |
| Delete used tag | Block or require reassignment |
| Archive tag | Allowed; hides from new assignment but keeps existing history |
| Merge duplicate tags | Admin workflow with preview |

---

## 6. Governance Model

### 6.1 Role Permissions

| Role | View Tags | Assign Tags | Create Tags | Edit Tags | Delete / Archive Tags | Merge Tags |
|---|---:|---:|---:|---:|---:|---:|
| Viewer | Yes | No | No | No | No | No |
| Operator | Yes | Yes | No | No | No | No |
| Engineer | Yes | Yes | Yes | Yes | Archive only | Suggest merge |
| Admin | Yes | Yes | Yes | Yes | Yes | Yes |

### 6.2 Duplicate Detection Rules

The system should detect duplicate or near-duplicate tags by normalizing:

- Case
- Extra spaces
- Leading/trailing spaces
- Hyphen differences
- Common punctuation variations
- Singular/plural similarity where possible

Examples:

| User Enters | Existing Tag | System Behavior |
|---|---|---|
| `cooling` | `Cooling` | Block duplicate; suggest existing tag |
| `10 KV` | `10kV` | Suggest existing normalized tag |
| `High priority` | `High-Priority` | Suggest match |
| `Known Issue` | `Known-Issue` | Suggest match |

### 6.3 Tag Health Dashboard

Admin view should show:

- Total tags
- Active tags
- Archived tags
- Unused tags
- Duplicate candidates
- Most used tags
- Recently created tags
- Tags without category
- Tags not used in last 12 months

---

## 7. Production-Grade Data Model

### 7.1 Tag Entity

| Field | Description |
|---|---|
| `tag_id` | Unique tag identifier |
| `tenant_id` | Tenant owning the tag |
| `display_name` | User-visible tag name |
| `normalized_name` | Used for duplicate checks |
| `description` | Optional governance description |
| `category` | Function, Criticality, Location, Ownership, etc. |
| `color_token` | Design-system color token |
| `status` | Active, Archived |
| `created_by` | User who created tag |
| `created_at` | Creation timestamp |
| `updated_by` | Last editor |
| `updated_at` | Last update timestamp |

### 7.2 Tag Assignment Entity

| Field | Description |
|---|---|
| `assignment_id` | Unique assignment identifier |
| `tenant_id` | Tenant scope |
| `tag_id` | Linked tag |
| `object_type` | Asset, Location, Device, Document, Template, etc. |
| `object_id` | Target object identifier |
| `assigned_by` | User who assigned tag |
| `assigned_at` | Assignment timestamp |
| `source` | Manual, Bulk, Import, API, AI-Suggested |

### 7.3 Audit Log Entity

| Field | Description |
|---|---|
| `event_id` | Unique event ID |
| `event_type` | Create, Edit, Archive, Delete, Assign, Remove, Merge |
| `tag_id` | Related tag |
| `object_id` | Related object when applicable |
| `before` | Previous value |
| `after` | New value |
| `performed_by` | User/system |
| `timestamp` | Event time |

---

## 8. API Requirements

### 8.1 Tag Library APIs

```http
GET    /api/tags
POST   /api/tags
GET    /api/tags/{tagId}
PATCH  /api/tags/{tagId}
DELETE /api/tags/{tagId}
POST   /api/tags/{tagId}/archive
POST   /api/tags/merge
```

### 8.2 Tag Assignment APIs

```http
GET    /api/objects/{objectType}/{objectId}/tags
POST   /api/objects/{objectType}/{objectId}/tags
DELETE /api/objects/{objectType}/{objectId}/tags/{tagId}
POST   /api/tags/bulk-assign
POST   /api/tags/bulk-remove
```

### 8.3 Search / Filter APIs

```http
GET /api/search?tag=Critical
GET /api/assets?tags=Critical,Cooling
GET /api/locations?tags=10kV
GET /api/devices?tags=Known-Issue
```

### 8.4 Future External API Requirement

External Locations and Assets APIs may include:

```json
{
  "id": "asset-123",
  "name": "Transformer-01",
  "type": "Transformer",
  "tags": [
    { "id": "tag-001", "name": "Protection" },
    { "id": "tag-002", "name": "Critical" }
  ]
}
```

---

## 9. Prototype Scenarios to Cover

### Scenario 1 — Create a Central Tag

**Persona:** Engineer/Admin  
**Goal:** Create reusable tenant tags.

Flow:

1. User opens `Settings → Tag Management`.
2. Clicks `Create tag`.
3. Enters `Cooling`.
4. Selects category `Function`.
5. Selects color token.
6. Saves tag.
7. Tag appears in central library.

Acceptance criteria:

- Duplicate `cooling` should be blocked.
- Tag must have a name.
- Category is recommended but optional in V1.
- Created tag is available in assignment picker.

### Scenario 2 — Assign Tags to an Asset

**Persona:** Operator/Engineer  
**Goal:** Assign existing tags to an asset.

Flow:

1. User opens `Transformer-01`.
2. Clicks `+ Add tag`.
3. Searches `Protection`.
4. Selects `Protection` and `Critical`.
5. Tags appear as chips on the asset.

Acceptance criteria:

- Operator can assign from existing tags.
- Operator cannot create a new tag.
- Max 5 tags per object.
- Tags appear in detail view and list view.

### Scenario 3 — Filter Asset Tree by Tags

**Persona:** Operator  
**Goal:** Find all high-priority cooling assets.

Flow:

1. User opens asset tree/list.
2. Opens filter panel.
3. Selects `Critical` and `Cooling`.
4. Asset list updates.
5. Matching tags are highlighted.

Acceptance criteria:

- Filter supports one or more tags.
- Results show active filters.
- User can clear all filters.
- Empty state explains no matching objects.

### Scenario 4 — Mark Recurrent Fault Chargers

**Persona:** EVLM Maintenance Engineer  
**Goal:** Identify chargers with repeated failures.

Flow:

1. Engineer opens charger `Charger-EF04`.
2. Adds `Recurrent-Fault` and `Watch-List`.
3. EVLM charger list displays these chips.
4. Operator filters by `Recurrent-Fault`.
5. All chronic issue chargers are shown.

Acceptance criteria:

- Same tag is visible in EVLM and shared asset views.
- Search returns all chargers/assets with this tag.
- User can remove tag after issue resolution.

### Scenario 5 — DSO Contract Grouping

**Persona:** Load Management Operator  
**Goal:** Find all sites related to a DSO.

Flow:

1. Admin creates tags `DSO-Amprion`, `DSO-50Hertz`.
2. Engineer assigns DSO tags to sites.
3. Operator filters site list by `DSO-Amprion`.
4. System displays all related sites.

Acceptance criteria:

- Tags can be assigned to locations/sites.
- Filter works across site list and related operational views.
- Tag is shown on site detail page.

### Scenario 6 — Document Classification

**Persona:** Engineer  
**Goal:** Standardize document tags.

Flow:

1. User uploads maintenance manual.
2. Selects tags `Maintenance-Manual` and `Approved`.
3. Tags are shown in document list.
4. User filters document library by `Approved`.

Acceptance criteria:

- Document tags come from central registry.
- Free-text duplicates are not allowed.
- Existing document tags can be migrated in future.

### Scenario 7 — Duplicate Prevention

**Persona:** Engineer  
**Goal:** Avoid bad tag quality.

Flow:

1. User enters `10 KV` in Create Tag.
2. System finds existing `10kV`.
3. System shows message: `A similar tag already exists: 10kV`.
4. User selects existing tag instead.

Acceptance criteria:

- Duplicate check is case-insensitive.
- Spacing and hyphen differences are detected.
- User can cancel or use existing tag.

### Scenario 8 — Archive Used Tag

**Persona:** Admin  
**Goal:** Retire a tag without breaking history.

Flow:

1. Admin opens tag `Legacy-System`.
2. Sees usage count: `42 objects`.
3. Clicks `Archive`.
4. Tag remains on existing objects but is hidden from new assignment picker by default.

Acceptance criteria:

- Used tag cannot be hard deleted directly.
- Archived tag remains searchable via admin filters.
- Existing assignments preserve historical context.

### Scenario 9 — Bulk Tag Assignment

**Persona:** Engineer/Admin  
**Goal:** Assign tags to many objects.

Flow:

1. User selects 100 assets.
2. Clicks `Assign tag`.
3. Selects `10kV`.
4. Confirms bulk assignment.
5. System shows success summary.

Acceptance criteria:

- Bulk action confirms object count.
- System prevents exceeding max tags per object.
- Failed items are reported clearly.

---

## 10. UX Copy

### Create Tag

```text
Create tag
Tags help users organize, search, and filter objects using your tenant vocabulary.
```

### Duplicate Tag

```text
A similar tag already exists: “10kV”.
Use the existing tag to keep your tenant vocabulary consistent.
```

### Max Tags

```text
You can assign up to 5 tags to this object.
Remove an existing tag before adding another one.
```

### Delete Used Tag

```text
This tag is used on 148 objects.
Archive it or reassign the objects before deleting it.
```

### Archive Tag

```text
Archived tags remain visible on existing objects but cannot be newly assigned by default.
```

---

## 11. Non-Functional Requirements

| Requirement | Target |
|---|---|
| Tag library load time | Under 300 ms for common tenant size |
| Assignment action | Under 500 ms perceived response |
| Search/filter | Server-side filtering with pagination |
| Accessibility | Keyboard navigation, screen reader labels, contrast-compliant chips |
| Auditability | All create/edit/delete/assign/remove actions logged |
| Scalability | Support thousands of tags and large object relationships |
| Security | Tenant isolation, role-based permissions |
| Localization | Tag UI supports localization; tenant-created tag names remain tenant-defined |

---

## 12. Design System Guidance

### Components Needed

| Component | Purpose |
|---|---|
| Tag chip | Display assigned tag |
| Tag overflow chip | Show `+N` hidden tags |
| Tag picker combobox | Assign existing tags |
| Tag management table | Admin management |
| Tag create/edit modal | Central tag creation/edit |
| Duplicate warning inline message | Prevent bad tag creation |
| Usage details drawer | Show where tag is used |
| Bulk assignment dialog | Apply/remove tags at scale |

### Chip Anatomy

```text
[Color indicator] Tag label [optional remove icon]
```

Rules:

- Remove icon only appears when user has permission.
- Tooltip shows full tag name and category.
- Overflow appears when space is limited.
- Chips should not dominate the object title.

---

## 13. Recommended Prototype Screens

1. **Settings → Tag Management list**
2. **Create/Edit tag modal**
3. **Duplicate detection state**
4. **Tag usage drawer**
5. **Asset detail with tag section**
6. **Device list with tags**
7. **Location/site list with tag filter**
8. **Document library with tag chips**
9. **EV charger list with recurrent fault tags**
10. **Bulk assign tags dialog**
11. **Archive/delete tag confirmation**
12. **Empty/no results state for tag filter**

---

## 14. Success Metrics

| Metric | Success Target |
|---|---|
| Duplicate tag creation attempts blocked | 100% of exact normalized duplicates |
| Tag reuse ratio | More reuse than new creation after first month |
| Search/filter adoption | Increasing usage in asset/device/location views |
| Time to find tagged assets | Reduced vs manual hierarchy navigation |
| Admin cleanup effort | Reduced duplicate/unused tags over time |
| Cross-feature consistency | Same tag appears consistently across OTC, SEM, EVLM |

---

## 15. MVP Scope Recommendation

### Must Have — V1

- Settings → Tag Management
- Create/edit/archive tags
- Duplicate prevention
- Assign tags to locations/assets/devices/documents
- Max 5 tags per object
- Visual chips/badges
- Search/filter by tag in supported views
- Role-based permissions
- Internal APIs for tag CRUD and assignment

### Should Have — V1.5

- Usage count and usage drawer
- Bulk assignment
- Recently used tags
- Tag categories
- Tag color tokens
- Empty states and governance guidance

### Could Have — V2

- Merge duplicate tags
- Suggested tags by object type
- Tag analytics dashboard
- Import/export tag library
- External API tags array

### Future — V3

- AI-suggested tags
- Rule-based auto-tagging
- Confidence and source metadata
- Temporary tags with expiry
- Cross-tenant starter templates

---

## 16. Final Recommendation

Treat centralized tagging as a **platform capability**, not as a feature-specific enhancement.

The best strategy is a hybrid model:

- **Central governance** for tag vocabulary
- **Simple assignment** at the point of use
- **Consistent visualization** across all object types
- **Powerful search/filter** wherever tags are shown
- **Safe admin controls** for archive, merge, duplicate detection, and audit
- **Future-ready architecture** for AI and rule-based automation

The prototype should clearly demonstrate that tags are not just visual labels. They are a lightweight operational metadata layer that improves navigation, search, filtering, onboarding, bulk operations, and cross-feature consistency.
