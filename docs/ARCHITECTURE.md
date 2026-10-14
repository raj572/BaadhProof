# BaadhProof — Technical Architecture

**Project status:** Prototype in development  
**Version:** 0.1  
**Purpose:** Document the proposed architecture for a Hindi-first, mobile-friendly flood-damage record tool.

## 1. Overview

BaadhProof helps flood-affected families and farmers organize their own damage notes and supporting evidence, review a general document checklist, and find official relief resources. It is an information and record-organization tool—not a government portal and not an eligibility or compensation decision system.

## 2. Proposed system diagram

```text
┌───────────────────────────────────────┐
│ User: farmer / affected family        │
│ Mobile or desktop browser             │
└───────────────────┬───────────────────┘
                    │ HTTPS
                    ▼
┌───────────────────────────────────────┐
│ Frontend web application              │
│ React + TypeScript + Tailwind CSS     │
│ - Hindi-first responsive UI           │
│ - Damage record form                  │
│ - Evidence/photo selection (optional) │
│ - Checklist and official links        │
│ - Print / PDF summary                 │
└───────────────┬───────────────────────┘
                │
                ├──────────────► Browser print / PDF
                │
                ▼
┌───────────────────────────────────────┐
│ Optional backend (only if implemented)│
│ Supabase: database / object storage   │
│ Access control and validation         │
└───────────────────────────────────────┘

Official resource links are opened from a curated list maintained by the project.
They do not imply a live government integration.
```

## 3. Main components

### Frontend
- Responsive web interface usable on a mobile browser.
- Hindi-first labels and plain-language guidance.
- Form validation for required fields such as incident date, location, damage category, and description.
- A record summary view that can be printed or saved as PDF through browser print functionality, if implemented.

### Data layer
- **Local-only prototype:** records remain in the user's browser/session or are exported by the user; persistence must be clearly described by the UI.
- **Optional Supabase implementation:** store records only after configuring authentication, access policies, and any required consent. Do not store secrets in frontend code.
- Do not add photo upload or cloud storage unless it is implemented and access-controlled.

### Official resources
- A curated list of links to official government or disaster-management resources.
- Each link should include its title, URL, intended purpose, and last-checked date.
- If a link has not been checked, label it as unverified or omit it.

## 4. Typical data flow

1. User opens the web app.
2. User creates a damage record with date, location, category, and description.
3. The interface validates required fields and explains any errors.
4. User optionally attaches evidence if that capability is implemented.
5. User reviews and corrects the record.
6. User views the general checklist and curated official links.
7. User prints or exports a summary if this feature is implemented.
8. User decides whether and where to share the summary; BaadhProof does not submit a claim automatically.

## 5. Suggested record model

```ts
type DamageRecord = {
  id: string;
  incidentDate: string;       // YYYY-MM-DD
  district: string;
  villageOrLocality: string;
  category: "crop" | "home" | "livestock" | "documents" | "other";
  description: string;
  evidenceFiles?: string[];   // metadata/paths only; do not expose private files
  createdAt: string;          // ISO 8601
};
```

This is a suggested schema, not a claim that the current repository already implements it.

## 6. Security and privacy

- Collect only information needed for the user's record.
- Use fictional data in demos and tests; do not commit real names, phone numbers, identity documents, or precise household coordinates.
- Do not commit API keys, passwords, service-role keys, or `.env` files.
- If cloud storage is introduced, enforce per-user access controls and test unauthorized access.
- Explain where data is stored, how long it is retained, and how users can delete it.
- Do not promise encryption, deletion, or secure storage unless implemented and verified.

## 7. Error and offline considerations

- Show clear validation messages in simple Hindi.
- Avoid losing entered text when validation fails.
- If network features are added, show a clear error when saving or opening a resource fails.
- Do not describe the app as fully offline unless offline behavior has been implemented and tested.

## 8. Deployment (proposed)

- Frontend: Vercel or another static/web hosting provider.
- Optional data backend: Supabase with restrictive row-level security and storage policies.
- Use HTTPS for any deployed environment.
- Keep development, test, and production configuration separate.

## 9. Known limitations

- BaadhProof does not verify damage or determine eligibility.
- It does not guarantee relief, compensation, or approval.
- It does not automatically file claims or provide real-time claim status.
- Resource links and checklists are informational and must be checked against current official guidance.
- Features listed as proposed must be marked as “planned” until implemented.

## 10. Architecture decision log

| Decision | Rationale | Status |
|---|---|---|
| Mobile-friendly web app | Accessible from common phone browsers without app installation | Proposed |
| React + TypeScript + Tailwind | Familiar component-based UI and responsive styling | Proposed |
| Supabase | Optional managed database/storage if persistence is needed | Optional; not assumed implemented |
| Browser print to PDF | Low-complexity way to export a record summary | Proposed |
| Hindi-first interface | Supports the intended Bihar user group | Product goal |
