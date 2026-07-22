# CMMC Compliance Tracker — User Guide

**Last updated:** 2026-07-22 (live checks added for AC.L1-b.1.i and SI.L1-b.1.xiii)
**Applies to:** `CMMC_Compliance_Tracker.html`, current build

This guide is also available inside the tool itself — click **📖 User Guide** in the toolbar. Both copies are kept in sync; when the tracker changes, this file and the in-app version are updated together.

---

## What this tool is (and isn't)

This is a self-assessment record-keeping tool for **CMMC Level 1** — 15 practices / 59 objectives, drawn directly from the DoD CMMC Assessment Guide – Level 1 (v2.13) and FAR 52.204-21.

It does **not** submit anything to SPRS, and it does not automatically decide whether a practice is Met — every finding is your judgment call, informed by the tool's built-in hints and live Microsoft 365 checks.

## 1. Start with Assessment Info

Click **⚙ Assessment Info** in the toolbar and fill in:
- Organization name
- Assessment date
- Assessor / preparer
- **CMMC Assessment Scope** (required — per 32 CFR §170.19, scope must be defined before a self-assessment is valid). The overall status banner stays locked on "Define scope to begin" until this is filled in.

## 2. Work through the practices

Practices are grouped into 6 domain cards:
- Access Control (AC)
- Identification & Authentication (IA)
- Media Protection (MP)
- Physical Protection (PE)
- System & Communications Protection (SC)
- System & Information Integrity (SI)

Click a practice to expand it and see its objectives. For each objective:
- Choose **Met**, **Not Met**, or **N/A**.
- Use the notes field to record your evidence — what you examined, interviewed, or tested, the same method real CMMC assessors use.
- Click **Show Azure/M365 configuration guidance** for suggested Microsoft 365/Entra ID settings mapped to that requirement (sourced from Microsoft's own CMMC Product Placemat and Technical Reference Guide).

A practice only shows **MET** once every one of its objectives is Met or N/A — one Not Met objective fails the whole practice (32 CFR §170.24 scoring rule).

## 3. Reading status at a glance

- **Colored chips** on each practice row: green = Met, red = Not Met, blue = N/A, gray = not assessed.
- **Domain rings** show percent complete per domain; the large ring in the summary bar shows overall progress.
- **Overall status banner:**
  - *Define scope to begin* — no scope set yet
  - *In Progress* — scope set, not all objectives assessed
  - *Compliant* — every practice shows Met
  - *Non-Compliant* — at least one practice shows Not Met

## 4. Live Microsoft 365 checks (optional)

Click **🔐 Connect to Microsoft 365** to sign in and let the tracker read real settings from your tenant via Microsoft Graph — Conditional Access policies, MFA registration, admin role counts, Intune device compliance. Results appear as advisory evidence with an **Insert into evidence notes** button. They are signals to review, never an automatic Met/Not Met.

Coverage: 8 of the 15 Level 1 practices have a live check so far (Access Control i/ii/iii, Identification & Authentication v/vi, Media Protection vii, System Integrity xii/xiii), and more are being added over time. The rest — especially Physical Protection — stay manual.

- **AC.L1-b.1.i (Authorized Access Control):** counts guest/external accounts (flagging any that are enabled, for you to confirm they're still authorized), reports the number of Intune-enrolled devices, and checks whether an enabled Conditional Access policy requires a compliant or hybrid-joined device before granting access.
- **SI.L1-b.1.xiii (Malicious Code Protection):** for each Intune-enrolled Windows device, reads its Microsoft Defender protection status and flags any device where real-time anti-malware protection is off or the device isn't reporting a clean state. Non-Windows devices aren't covered by this check and need a manual confirmation.

This requires a one-time Azure AD app registration by whoever has admin rights in your Microsoft 365 tenant. See `CMMC_Tracker_Live_Check_Setup.md` for that setup.

## 5. Saving and sharing progress

- **💾 Save Progress** / **📂 Load Progress** — download or load a local `.json` snapshot of your checklist.
- While connected to Microsoft 365, progress also auto-saves a few seconds after each change to a shared file at **Guardian / Shared Documents / CMMC / Current**, so the whole team sees (and continues) the same shared state, not separate per-browser copies. On connecting — including automatically on page load if the browser still has a session — it checks that file and offers to load it, asking first if it would overwrite unsaved local changes.
- **↺ Reset** only clears your local browser copy. It won't touch the shared SharePoint file unless you make another change afterward (which would then sync the blank state).

## 6. Exporting reports

- **📄 Export PDF** and **📝 Export Report (.txt)** both download a full report of findings, evidence, and FAR/NIST references.
- While connected to Microsoft 365, exports are also saved to **Guardian / Shared Documents / CMMC / Build**.

## Level 2

Level 2 (110 practices from NIST SP 800-171) stays locked until every Level 1 practice shows MET.

## Getting help

If something looks wrong or you want a feature changed, just tell Claude — this guide is updated alongside the tool itself.

---

## Related docs

- `CMMC_Tracker_Live_Check_Setup.md` — one-time Microsoft 365 admin setup for live checks and SharePoint sync
- `GS2_CMMC_L1_Azure_M365_Configuration_Guide.md` — full Azure/M365 configuration guidance per practice
- `CMMC_Official_Documentation_Sources.md` — index of official CMMC/DFARS/NIST sources

---

## Changelog

- **2026-07-22** — Added a live check for SI.L1-b.1.xiii (Malicious Code Protection): reads each Intune-enrolled Windows device's Defender protection status (`windowsProtectionState` — real-time protection enabled, malware protection enabled, device health state) and flags any device that's off or not reporting clean. Non-Windows devices stay manual.
- **2026-07-22** — Added a live check for AC.L1-b.1.i (Authorized Access Control): guest/external account count, Intune-enrolled device count, and whether a Conditional Access policy gates access on device compliance/hybrid-join. First practice being automated in an ongoing effort to extend live-check coverage beyond the original 6 practices.
- **2026-07-22** — Added this guide (standalone + in-app modal, accessible via the 📖 User Guide toolbar button). Tracker re-branded with Guardian/GS2 colors, fonts (Codec Pro / Montserrat), and logo.
