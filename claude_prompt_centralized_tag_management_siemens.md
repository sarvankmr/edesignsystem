# Claude Prompt — Centralized Tag Management App for Siemens Electrification X

Copy and paste this complete prompt into Claude. Attach the following files before running the prompt:

1. `centralized_tag_management_prd_with_example_tags_v2.md`
2. Siemens Design System / Element / iX style file

---

You are a senior product designer, UX architect, design systems expert, and frontend application engineer.

Your task is to create a **production-ready web application prototype** for **Centralized Tag Management** for a Siemens Electrification X SaaS platform.

Use the attached files as the primary source of truth:

1. `centralized_tag_management_prd_with_example_tags_v2.md`
   - Contains the PRD, use cases, tag examples, governance model, user roles, acceptance criteria, data model, and prototype requirements.

2. `Siemens Design System / Element / iX style file`
   - Use this file to strictly follow Siemens visual language, components, spacing, typography, colors, interaction behavior, accessibility patterns, and enterprise SaaS UI standards.

Do not create a generic SaaS interface. The output must feel like a real Siemens industrial SaaS application.

---

# 1. Product Context

The platform needs a centralized tagging capability that allows users to create, govern, assign, search, filter, visualize, and reuse tags across multiple Electrification X feature sets.

Today, tags may exist separately across modules or as free-text values, which creates inconsistency, duplication, poor searchability, and low trust.

The new application should introduce a **tenant-level centralized tag library** that works across supported object types.

Supported object types:

- Locations
- Assets
- Devices
- Documents
- Widgets
- Signals
- Dashboards
- Settings / configuration templates

The tagging capability should work as a platform capability, not as a feature hidden inside one module.

---

# 2. Product Goal

Create a scalable, enterprise-grade **Centralized Tag Management** app where tenant-level tags can be:

- Created
- Edited
- Archived
- Deleted only when unused
- Assigned to objects
- Removed from objects safely
- Searched
- Filtered
- Visualized
- Governed
- Audited
- Reused across modules

The application must be simple for operators, powerful for engineers, and controlled for administrators.

---

# 3. UX Vision

The UX should make tagging feel:

- Fast
- Simple
- Governed
- Reusable
- Safe
- Searchable
- Consistent
- Non-intrusive
- Scalable
- Enterprise-ready

Do not make tag management feel like a heavy admin tool. It should be easy to configure, but still production-grade.

---

# 4. Design System Requirements

Use the attached Siemens design system file strictly.

Follow the Siemens design system for:

- Typography
- Color tokens
- Spacing
- Layout grid
- Page structure
- Buttons
- Tables
- Inputs
- Search fields
- Filters
- Chips / badges
- Dialogs
- Side panels
- Dropdowns
- Tooltips
- Empty states
- Toast notifications
- Focus states
- Accessibility
- Responsive behavior

Do not invent a new visual style.  
Do not use random colors.  
Do not overuse gradients, decorative illustrations, or experimental UI.  
The design should look like a serious enterprise Siemens SaaS product.

If an exact Siemens component is not available, create the closest possible equivalent while staying visually consistent with the design system.

---

# 5. Required Application Screens

Create the following screens.

---

## Screen 1: Tag Management Overview

Purpose:  
A central place in Settings where tenant admins and engineers manage the tag library.

Route / area:

```text
Settings → Tag Management
```

Must include:

- Page title: `Tag Management`
- Short description explaining that tags are tenant-level reusable labels
- Primary CTA: `Create tag`
- Search field
- Filters for:
  - Category
  - Status
  - Object type
  - Usage
- Governance summary cards:
  - Total tags
  - Active tags
  - Archived tags
  - Duplicate candidates
  - Unused tags
- Tag table

Table columns:

- Tag
- Category
- Color
- Usage count
- Used in object types
- Created by
- Last updated
- Status
- Actions

Actions menu:

- View usage
- Edit
- Archive
- Delete, only if unused
- Merge, optional but recommended for governance screen

Tag row behavior:

- Tag should be displayed as a chip/badge
- Color should be visible but not the only indicator
- Usage count should be clickable or expandable
- Archived tags should be visually muted
- System-suggested tags should be clearly marked

---

## Screen 2: Create / Edit Tag Flow

Purpose:  
Allow safe creation and editing of tenant-level tags.

Use a modal or right-side panel based on Siemens design system best practice.

Fields:

- Tag name
- Category
- Description
- Color
- Synonyms / aliases
- Status
- Optional review date for temporary operational tags

Validation rules:

- Tag name is required
- Tag name must have a reasonable length limit
- Duplicate tag names are not allowed
- Duplicate detection must be case-insensitive
- Duplicate detection must ignore extra spaces
- Duplicate detection must detect similar variants
- User should be guided to use existing tags when possible

Example duplicate case:

If the user enters:

```text
cooling
```

and this tag already exists:

```text
Cooling
```

Show this message:

```text
A tag named “Cooling” already exists. Use the existing tag instead.
```

Similar tag warning example:

```text
Similar tags found: Cooling, Cooling-System. Review before creating a new tag.
```

Primary actions:

- Save tag
- Cancel

For edit mode:

- Show usage count
- Warn before changing name if tag is heavily used
- Do not allow destructive changes without clear warning

---

## Screen 3: Asset List with Tags

Purpose:  
Show how tags improve scanning, filtering, and operational context.

Must include:

- Asset list or asset table
- Search field
- Tag filters
- Object type filter
- Status filter
- Location filter
- Selected filter chips
- Tag chips on each asset row/card
- Add tag interaction
- Remove tag interaction
- Empty state when no result is found

Example assets:

- Transformer-01
- Cooler-07
- Meter-Bay-3
- Charger-Unit-EF04
- Feeder-Bay-11
- RMU-Station-02
- Protection-Relay-07

Example tag usage:

```text
Transformer-01 → Protection, Critical, 110kV
Cooler-07 → Cooling, Routine, Under-Maintenance
Meter-Bay-3 → Metering, Critical
Charger-Unit-EF04 → Recurrent-Fault, Watch-List, Vendor-X
```

---

## Screen 4: Object Detail View

Purpose:  
Show tags in context of one selected object.

Must include:

- Object title
- Object type
- Status
- Location
- Assigned tags
- Add tag CTA
- Remove tag action
- Tag overflow behavior
- Usage or metadata section
- Related documents or widgets, if useful

Required tag pattern:

```text
Tags
[Critical] [Cooling] [Vendor-X] [+ Add tag]
```

Remove tag confirmation:

```text
Remove tag “Critical” from Transformer-01?
This will only remove the tag from this object. It will not delete the tag from the central library.
```

Actions:

- Cancel
- Remove tag

---

## Screen 5: Cross-Object Search Results

Purpose:  
Show how users can search and filter across different object types using tags.

Must include:

- Search input
- Tag search syntax support or simulated support
- Selected tags as removable chips
- Result count
- Grouped results by object type
- Highlighted matching tags
- Empty state
- Clear filters action

Example search behavior:

```text
tag:critical
tag:"high voltage"
```

Example result summary:

```text
Showing 18 objects tagged with Critical + Cooling
```

Grouped result sections:

- Assets
- Devices
- Locations
- Documents
- Widgets
- Settings templates

Each result should show:

- Object name
- Object type
- Description or metadata
- Matching tag chips
- Location or module reference
- Open/view action

---

## Screen 6: Governance & Cleanup

Purpose:  
Help admins maintain a clean, high-quality tag library.

Must include sections for:

- Duplicate candidates
- Similar tag warnings
- Unused tags
- Archived tags
- High-usage tags
- Recently created tags
- Tags pending review
- Tags with no category
- Tags with inconsistent naming

Governance actions:

- Review duplicate
- Merge tags
- Archive unused tag
- Reassign usage
- View affected objects
- Keep separate

Example warning:

```text
This tag is used in 148 objects. It cannot be deleted. You can archive it or reassign objects to another tag.
```

Duplicate example:

```text
Cooling
cooling
COOLING
Cooling-System
```

Show recommendation:

```text
Recommended primary tag: Cooling
```

Merge behavior can be simulated in the prototype.

---

# 6. Tag Assignment Experience

Create a reusable tag assignment component.

It should work on:

- Asset rows/cards
- Object detail page
- Document rows/cards
- Widget cards
- Device rows/cards

Required behavior:

- Show assigned tags as chips
- Show maximum 3 visible tags initially
- Show `+N more` for overflow
- On hover/click, show all tags in tooltip/popover
- Use `+ Add tag` button or icon
- Open a typeahead tag selector
- Search existing tags first
- Support multi-select
- Show recently used tags
- Show suggested tags based on object type
- Prevent more than 5 tags per object in V1
- Show clear validation when limit is reached
- Allow safe tag removal
- Do not allow deletion of central tags from object-level UI

Validation message for max tag limit:

```text
Maximum 5 tags can be assigned to one object in this version.
```

---

# 7. Tag Visualization Rules

Use Siemens chip/badge styling.

Rules:

- Tags should be readable and compact
- Do not rely on color alone
- Always include text label
- Use accessible contrast
- Use consistent spacing
- Do not show too many chips in dense tables
- Use `+N more` overflow
- Tooltip/popover should reveal all hidden tags
- Color should support scanning, not dominate the UI

Recommended chip display:

```text
[Critical] [Cooling] [Vendor-X] +2
```

Color strategy:

- Priority / criticality: strong attention color
- Functional role: neutral or informational color
- Geography: calm location color
- Ownership: neutral color
- Operational state: status-related color
- System-suggested / AI-suggested: distinct but subtle style

Do not use random custom colors per user unless the PRD explicitly asks for it as nice-to-have. If custom colors are shown, keep them governed and accessible.

---

# 8. Search & Filtering Requirements

Tag filtering should be useful and visible.

Required capabilities:

- Search by tag name
- Filter by one tag
- Filter by multiple tags
- Combine tag filters with other filters:
  - Object type
  - Status
  - Location
  - Owner
  - Category
- Show selected filters as chips
- Clear one filter
- Clear all filters
- Highlight matching tags in result rows/cards
- Show no-result state

No-result state example:

```text
No objects found for Critical + Cooling.
Try removing one filter or search for another tag.
```

---

# 9. Role-Based Access Requirements

Support role-based behavior in the UI.

Roles:

| Role | Capabilities |
|---|---|
| Viewer | Can view tags only |
| Operator | Can assign existing tags to objects |
| Engineer | Can create, edit, assign, and archive tags |
| Admin | Full access including governance and deleting unused tags |

Add a role switcher in the prototype if useful to demonstrate permission behavior.

Permission rules:

- Viewer cannot assign tags
- Operator can assign existing tags but cannot create central tags
- Operator cannot edit, archive, or delete tags
- Engineer can create and edit tags
- Engineer can archive tags
- Admin can access all governance actions
- Delete is only available for unused tags
- Used tags should be archived or reassigned, not deleted

Operator message when restricted:

```text
You can assign existing tags, but only Engineers or Admins can create new tags.
```

---

# 10. Starter Tag Library

Use realistic Siemens Electrification X domain tags.

Include tags across these categories:

- Physical / geographic context
- Voltage / electrical level
- Functional role
- Priority / criticality
- Operational state
- Fault / health context
- Ownership / team
- Contract / DSO / partner
- Asset type / capacity
- Business segment / cohort
- Network / topology context
- Security / risk context
- Maintenance context
- Document classification
- Dashboard / widget context
- Settings / configuration context
- Lifecycle / maturity
- AI / automation-ready future tags

Use these starter tags in the app:

```text
Plant-A
Zone-3
Building-B
City-Centre
Highway
10kV
33kV
110kV
Medium-Voltage
High-Voltage
Cooling
Protection
Metering
Safety
Backup
Critical
High-Priority
Routine
Business-Critical
Watch-List
Known-Issue
Under-Maintenance
Decommissioned
Recurrent-Fault
Chronic-Issue
Under-Investigation
Escalated
Team-Alpha
Vendor-X
DSO-Amprion
Truck-Station
Car-Station
4-Charger
6-Charger
8-Charger
Cyber-Critical
Patch-Required
Hardening-Required
Inspection-Due
Service-Planned
Approved
Draft
Maintenance-Manual
IEC-Standard
Feeder-Alarms
Cyber-Overview
Maintenance-KPI
Protection-Template
Baseline
Deprecated
AI-Suggested
Anomaly-Detected
Needs-Validation
```

---

# 11. Example Tag Categories and Usage

Use this table as guidance for mock data and UI scenarios.

| Tag category | Example tags | Ideal object types | Usage scenario |
|---|---|---|---|
| Physical / geographic context | Plant-A, Zone-3, Building-B, Floor-2 | Locations, assets, devices | Group objects by real-world site structure |
| Voltage / electrical level | 10kV, 33kV, 110kV, High-Voltage | Locations, substations, feeders, widgets | Identify equipment and dashboards by voltage level |
| Functional role | Cooling, Protection, Metering, Safety | Assets, devices, signals, dashboards | Filter equipment by operational function |
| Priority / criticality | Critical, High-Priority, Routine | Assets, locations, devices | Highlight important operational objects |
| Operational state | Watch-List, Known-Issue, Under-Maintenance | Assets, devices, locations | Mark temporary operational context |
| Fault / health context | Recurrent-Fault, Chronic-Issue, Under-Investigation | Assets, devices, fault records | Track recurring problems or investigation status |
| Ownership / team | Team-Alpha, Vendor-X, Maintenance-Team | Assets, documents, tasks | Show responsible team or vendor context |
| Contract / DSO / partner | DSO-Amprion, Contract-2024 | Locations, EV sites, documents | Group sites by contract or DSO relationship |
| Asset type / capacity | Truck-Station, 4-Charger, 8-Charger | EV charging sites and assets | Support bulk operations by asset type |
| Business segment / cohort | Highway, City-Centre, Suburban | Locations, EV sites, dashboards | Analyze performance by site cohort |
| Security / risk context | Cyber-Critical, Patch-Required, Hardening-Required | Devices, assets, vulnerabilities | Provide cyber/OT operational context |
| Maintenance context | Inspection-Due, Service-Planned, Vendor-Visit | Assets, devices, tasks | Support maintenance planning |
| Document classification | Approved, Draft, Maintenance-Manual, IEC-Standard | Documents, templates | Standardize document tagging |
| Dashboard / widget context | Feeder-Alarms, Cyber-Overview, Maintenance-KPI | Dashboards, widgets | Clarify widget purpose and filtering |
| Lifecycle / maturity | Draft, Validated, Deprecated, Retired | Documents, settings, configurations | Show maturity of reusable objects |
| AI / automation-ready | AI-Suggested, Anomaly-Detected, Needs-Validation | Insights, assets, alarms | Prepare for AI-assisted tagging |

---

# 12. Data Model Expectations

Use clean mock data based on the PRD.

Recommended TypeScript-style entities:

```ts
type TagStatus = 'active' | 'archived' | 'system-suggested';

type ObjectType =
  | 'asset'
  | 'device'
  | 'location'
  | 'document'
  | 'widget'
  | 'signal'
  | 'setting';

interface Tag {
  id: string;
  name: string;
  normalizedName: string;
  category: string;
  color: string;
  description?: string;
  synonyms?: string[];
  status: TagStatus;
  usageCount: number;
  usedIn: ObjectType[];
  createdBy: string;
  updatedAt: string;
  reviewDate?: string;
}

interface ObjectItem {
  id: string;
  type: ObjectType;
  name: string;
  description?: string;
  status?: string;
  location?: string;
  owner?: string;
  tags: string[];
}
```

Normalization logic:

- Trim leading/trailing spaces
- Collapse multiple spaces
- Convert to lowercase for duplicate comparison
- Ignore case differences
- Detect similar variants

Example:

```text
" Cooling " → "cooling"
"COOLING" → "cooling"
"cooling" → "cooling"
```

---

# 13. Interaction Requirements

Implement realistic UI behavior.

Required interactions:

- Search tags in Tag Management
- Filter tags by category/status/object type
- Open Create Tag flow
- Validate duplicate tag names
- Show similar tag warning
- Save tag into mock state
- Edit existing tag
- Archive tag
- Prevent deleting used tags
- Delete unused tags
- View tag usage
- Assign tag to object
- Remove tag from object with confirmation
- Enforce maximum 5 tags per object
- Search/filter objects by selected tags
- Show grouped cross-object search results
- Show governance cleanup suggestions
- Show empty states
- Show loading states where relevant
- Show toast/notification after key actions

Toast examples:

```text
Tag created successfully.
Tag archived successfully.
Tag added to Transformer-01.
Tag removed from Transformer-01.
This tag cannot be deleted because it is currently used.
```

---

# 14. Production Quality Requirements

The output must be more than a visual demo.

It should include:

- Clean component structure
- Reusable components
- Centralized mock data
- Clear state management
- Accessible labels
- Keyboard-friendly interactions
- Responsive layout
- Empty states
- Error states
- Loading states
- Clear naming
- Maintainable code
- No hardcoded visual hacks
- No inconsistent spacing
- No random color usage
- No irrelevant decorative UI
- No incomplete flows

Recommended reusable components:

- `TagChip`
- `TagPicker`
- `TagManagementTable`
- `TagFormPanel`
- `ObjectTagSection`
- `ObjectList`
- `FilterBar`
- `GovernanceCard`
- `ConfirmationDialog`
- `EmptyState`
- `ToastNotification`
- `RoleSwitcher`

---

# 15. Accessibility Requirements

Ensure:

- Keyboard navigation
- Visible focus states
- ARIA labels where needed
- Accessible chip remove buttons
- Accessible dialog behavior
- Accessible combobox behavior
- Color contrast compliance
- Text label in addition to color
- Clear validation messages
- Screen-reader-friendly error messages
- No color-only meaning

Every remove button on a chip should have an accessible label such as:

```text
Remove Critical tag
```

---

# 16. Responsive Requirements

Desktop:

- Full table views
- Side filter panel or top filter bar
- Modal or side panel for forms
- Dense but readable enterprise layout

Tablet:

- Collapsible filters
- Responsive table/card hybrid
- Touch-friendly controls

Mobile:

- Card-first layout
- Full-screen or bottom-sheet tag picker
- Compact chips with overflow
- Clear primary actions

---

# 17. UX Copy Requirements

Use clear, professional enterprise copy.

Examples:

Create tag helper text:

```text
Create reusable tenant-level tags that can be assigned across assets, devices, documents, widgets, and settings.
```

Duplicate warning:

```text
A tag named “Cooling” already exists. Use the existing tag instead.
```

Max limit warning:

```text
Maximum 5 tags can be assigned to one object in this version.
```

Used tag delete warning:

```text
This tag is used in 148 objects. It cannot be deleted. You can archive it or reassign affected objects to another tag.
```

Empty tag library:

```text
No tags created yet.
Create your first tenant-level tag to standardize how teams organize and find objects.
```

No search results:

```text
No matching tags found.
Try a different search term or clear filters.
```

Restricted permission:

```text
You can assign existing tags, but only Engineers or Admins can create new tags.
```

---

# 18. Acceptance Criteria

The prototype is successful when:

1. A user can view all centralized tags.
2. A user can search and filter centralized tags.
3. A user can create a new tag.
4. Duplicate tag names are prevented.
5. Similar tag warnings are shown.
6. A user can edit a tag.
7. A user can archive a tag.
8. A user cannot delete a used tag.
9. A user can delete an unused tag.
10. A user can view where a tag is used.
11. A user can assign existing tags to assets, devices, documents, widgets, and settings.
12. A user cannot assign more than 5 tags to one object.
13. A user can remove a tag from an object safely.
14. Tags are visible as chips/badges across list and detail views.
15. Overflow tags show `+N more`.
16. Users can search/filter objects by tag.
17. Cross-object results are grouped by object type.
18. Admins can access governance and cleanup insights.
19. Operators cannot create/edit/delete central tags.
20. The UI follows the Siemens design system file.
21. The application is responsive.
22. The application is accessible.
23. The code is modular and maintainable.
24. The prototype feels production-ready and not like a rough demo.

---

# 19. Expected Output

Create a complete working app prototype.

Include:

- Source code
- Component structure
- Mock data
- All required screens
- Realistic interaction logic
- Styling based on Siemens design system
- Responsive behavior
- Accessibility behavior
- A short README explaining:
  - How to run the app
  - Project structure
  - Main components
  - Mock data model
  - How roles are simulated
  - How tag validation works

Before finalizing, review the attached PRD and Siemens design system file carefully and ensure no major requirement is missed.

The final app should be suitable for presenting to product owners, UX reviewers, engineering teams, and stakeholders as a production-grade concept for centralized tag management in Siemens Electrification X.
