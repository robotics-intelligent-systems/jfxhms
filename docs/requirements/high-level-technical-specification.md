# High-level technical requirements specification — JFXHMS

Baseline: HMS-MBSE-001, 12 October 2026. Status: proposed requirements and design allocation; acceptance evidence pending. Source repository snapshot: `3240c065753701cf0b0c7ab8f461f58d6b02f958`.

## Purpose, system boundary and stakeholders

JFXHMS coordinates hospital clinical information, hospital operations, emergency dispatch, medical logistics and operational digital twins. Patients, practitioners, dispatchers, marine operators, facilities/logistics staff, interoperability engineers and verification owners have distinct responsibilities. External HIS/FHIR repositories, laboratory/imaging services, ERP providers, communications and physical control systems are interfaces rather than assumed installed dependencies.

The baseline adds ten system requirements to the existing 36 medical-fleet requirements without changing their IDs or acceptance text. The existing fleet CSV remains authoritative for MED-C/PAT/MOD/SHIP requirements; the combined register is a generated integration view. Changes to those requirements must update both registers and diagrams in the same review. All 46 requirements are proposed; no requirement is reported as verified.

## CAD concept allocation

| Concept and source | Selected design scope | Requirement allocation | Existing detailed specification |
| --- | --- | --- | --- |
| [Medical patrol boat](../../MBSE/CAD/medical-patrol-boat-concept.jpg) | Coastal/river hull, twin outboards, patient/stretcher area, modular deck, PV, local helm and separate water/waste | MED-C01–12 + PAT-01–07 | [Patrol boat](../../MBSE/CAS/Drawio/OpenTwin_Medical_Patrol_Boat_High_Level_Requirements.drawio) |
| [Modular medical vessel](../../MBSE/CAD/modular-medical-vessel-concept.jpg) | Replaceable medical modules, selected hybrid/PV, utilities, navigation, separately engineered helipad and boat handling | MED-C01–12 + MOD-01–08 | [Modular vessel](../../MBSE/CAS/Drawio/OpenTwin_Modular_Medical_Vessel_High_Level_Requirements.drawio) |
| [Large medical support ship](../../MBSE/CAD/large-medical-support-ship-concept.jpg) | Configured advanced-care modules, accommodation, command, cargo, energy variants, water/waste and independent aviation/boat interfaces | MED-C01–12 + SHIP-01–09 | [Support ship](../../MBSE/CAS/Drawio/OpenTwin_Large_Medical_Support_Ship_High_Level_Requirements.drawio) |

The JPEGs are illustrations, not dimensioned engineering geometry. Retain the [source manifest](cad-source-baseline.json) and [CAD interpretation](cad-concept-requirements.md). The patrol boat has no depicted helipad, ICU or operating theatre. Optional advanced clinical services and aviation operations require separately approved configurations. No numerical geometry, speed, occupancy or clinical performance is inferred from the images. This task preserves all CAD source assets.

## System requirements and proposed acceptance

I = inspection, A = analysis, D = demonstration, T = test. Criteria describe planned procedures, not completed tests. A proposed design allocation is a candidate means of satisfying a requirement, not proof of satisfaction.

| ID | Requirement | Allocated block | Method | Proposed acceptance criterion |
| --- | --- | --- | --- | --- |
| HMS-001 — Configuration and service scope | The system SHALL record approved facility, fleet, clinical-service and integration configurations with versioned identities and accountable roles. | `configuration` | I | Review one configuration and reject a module whose required interface or approval record is absent. |
| HMS-002 — Clinical workflow | The system SHALL support authorized registration, encounter, result review and handover with explicit responsible practitioners and workflow states. | `clinical` | T/D | Complete a synthetic encounter; reject invalid transitions and retain practitioner identity and reviewed result history. |
| HMS-003 — Clinical interoperability | The system SHALL declare selected FHIR versions, profiles, terminology and optional imaging adapters and validate incoming exchanges. | `clinical` | T | Accept selected-profile synthetic messages; reject invalid or unauthorized messages with traceable outcomes. |
| HMS-004 — Access and audit | The system SHALL enforce role and purpose scoped access at clinical APIs and audit authorized and denied access without copying clinical content into fleet telemetry. | `clinical` | T | Deny an unauthorized synthetic record request; log subject, action, outcome and time; inspect operational events for prohibited clinical fields. |
| HMS-005 — Hospital and supply operations | The system SHALL track bed, equipment, inventory and selected supply-chain transitions with revision checks and traceable lot/expiry records where applicable. | `operations` | T | Reject an outdated revision; reconcile synthetic reservation/release and lot/expiry events without duplicate stock movements. |
| HMS-006 — Supervised EMS coordination | The system SHALL coordinate incident, availability, assignment, transport and handover under qualified dispatch authority, with review before consequential assignment. | `dispatch` | T/D | Replay a synthetic incident through handover; reject an unreviewed assignment and detect an unavailable resource. |
| HMS-007 — Operational twin contract | The system SHALL expose versioned asset/configuration identity, timestamp, units, quality, readiness and fault state through a separate operational data contract. | `edge` | T | Replay valid, malformed and stale telemetry; validate provenance, mark stale state and preserve clinical-data isolation. |
| HMS-008 — Disconnected recovery | The system SHALL define local workflows, buffering, idempotent replay and conflict resolution for loss and restoration of selected external links. | `edge` | T | Replay duplicate and out-of-order events after simulated WAN loss; preserve identity and expose unresolved conflicts for authorized review. |
| HMS-009 — Governed decision support | The system SHALL label AI/CQL outputs as proposals with input/model/rule version and authorized human disposition; local helm and clinical authority SHALL remain independent of cloud availability. | `decision` | T/I | Reject an unreviewed consequential proposal; retrieve provenance and reviewer disposition; demonstrate continued local authority during AI/link loss. |
| HMS-010 — Verification and change control | The system SHALL link each requirement to configuration, proposed design allocation, verification procedure, result and change impact before release. | `configuration` | I/T | Inspect full requirement coverage; reject release when required evidence, critical budgets or approved dispositions are missing. |

## Inherited medical-fleet baseline

The table reproduces the complete requirement text from the fleet baseline. The [combined traceability register](high-level-requirements-traceability.csv) preserves each original criterion, owner role, evidence ID, CAD rationale and applicability. See the [original fleet register](cad-requirements-traceability.csv) for its canonical source.

| ID | Requirement | Design allocation | Verification method / planned evidence |
| --- | --- | --- | --- |
| MED-C01 | SHALL define displacement, draft, freeboard, mass/CG and stability for each approved occupancy and module loading case. | `hull` | A / `MED-C01-EV` |
| MED-C02 | SHALL define compartmentation, penetrations, structural load paths, module attachments, drainage and corrosion protection. | `hull` | A/I / `MED-C02-EV` |
| MED-C03 | SHALL define secure stretcher/equipment retention, boarding, handling, access and emergency egress for the approved occupancy. | `medical` | I/D / `MED-C03-EV` |
| MED-C04 | SHALL define protected power, reserve and degraded-load priorities for navigation, medical support, communications and alarms. | `energy` | A/T / `MED-C04-EV` |
| MED-C05 | SHALL define clean/dirty flows, ventilation, potable/process water, waste and equipment-service access for the selected medical mission. | `medical` | A/I / `MED-C05-EV` |
| MED-C06 | SHALL maintain versioned mounting, mass/CG, power/fluid, command/data and service contracts with compatibility and license records. | `configuration` | I / `MED-C06-EV` |
| MED-C07 | SHALL select clinical exchange versions/profiles and terminology; isolate HIS/FHIR and optional imaging adapters behind validated interfaces. | `clinical` | T/I / `MED-C07-EV` |
| MED-C08 | SHALL keep clinical records and access audit under dedicated governance; use authorized minimal links in ordinary asset/mission telemetry. | `clinical` | T / `MED-C08-EV` |
| MED-C09 | SHALL publish asset/configuration identity, mode, location, energy, equipment readiness, faults and maintenance with timestamps, units and quality. | `edge` | T / `MED-C09-EV` |
| MED-C10 | SHALL provide selected marine/local communications and authorized remote monitoring with buffering and defined disconnected workflows. | `edge` | T / `MED-C10-EV` |
| MED-C11 | SHALL retain validated local vessel control and qualified clinical/dispatch authority; record model, input provenance and human review for AI proposals. | `control` | T/I / `MED-C11-EV` |
| MED-C12 | SHALL approve mission/environment, device/calibration and recovery criteria; validate models and staged trials before envelope expansion. | `simulation` | A/T / `MED-C12-EV` |
| PAT-01 | SHALL define patrol, community access, supervised emergency transport and handover scenarios within a validated coastal/river envelope. | `control` | A/D / `PAT-01-EV` |
| PAT-02 | SHALL define the depicted twin-outboard propulsion arrangement and assess selected fuel/electric/hybrid alternatives without assuming simultaneous implementation. | `propulsion` | A/T / `PAT-02-EV` |
| PAT-03 | SHALL provide an arranged patient area for stretcher retention, selected monitoring and supervised telemedicine with accessible equipment. | `medical` | I/D / `PAT-03-EV` |
| PAT-04 | SHALL define deck equipment/rescue/cargo mounts, retention and clear working/boarding routes with controlled mass/CG. | `mission` | A/I / `PAT-04-EV` |
| PAT-05 | SHALL define roof PV and its protected conversion interface to the selected vessel energy system. | `energy` | A/T / `PAT-05-EV` |
| PAT-06 | SHALL integrate selected GPS/GNSS, AIS, radar/cameras, VHF and optional cellular/satellite communications with local helm indication. | `control` | T / `PAT-06-EV` |
| PAT-07 | SHALL provide separate fresh, grey and black water circuits/tanks with service access and approved capacities. | `medical` | I/T / `PAT-07-EV` |
| MOD-01 | SHALL define consultation, emergency support, laboratory, vaccination and telemedicine configurations with approved occupancy and crew roles. | `mission` | I/D / `MOD-01-EV` |
| MOD-02 | SHALL define replaceable medical-module installation, retention, utility connections and servicing without conflicting access/egress. | `medical` | A/I / `MOD-02-EV` |
| MOD-03 | SHALL treat the illustrated helipad as a separately engineered medevac/logistics interface with aircraft loads, clearances and operating limits. | `mission` | A/I / `MOD-03-EV` |
| MOD-04 | SHALL define stowage, handling, launching/recovery and safe patient-transfer interfaces for selected support boats. | `mission` | A/D / `MOD-04-EV` |
| MOD-05 | SHALL define the selected hybrid propulsion/energy arrangement and roof PV without inferring a fuel chemistry from the illustration. | `energy` | A/T / `MOD-05-EV` |
| MOD-06 | SHALL provide local navigation with selected GPS/GNSS, AIS and radar, plus reviewed AI assistance and mission status. | `control` | T / `MOD-06-EV` |
| MOD-07 | SHALL define fresh-water filtration and waste-treatment interfaces sized for selected clinical and accommodation loads. | `medical` | A/I / `MOD-07-EV` |
| MOD-08 | SHALL support authorized telemedicine and operational twin analytics through distinct clinical and asset data paths. | `clinical` | T / `MOD-08-EV` |
| SHIP-01 | SHALL define humanitarian, disaster-response and outreach configurations with passenger/patient/crew and logistics loading records. | `mission` | A/I / `SHIP-01-EV` |
| SHIP-02 | SHALL evaluate illustrated emergency, surgery, ICU, laboratory, pharmacy, maternity and telemedicine facilities as separately approved clinical modules. | `medical` | A/I / `SHIP-02-EV` |
| SHIP-03 | SHALL define configurable accommodation, transfers, accessibility and evacuation routes matched to approved occupancy and clinical scope. | `medical` | I/D / `SHIP-03-EV` |
| SHIP-04 | SHALL provide local navigation, communications and mission coordination under defined bridge and clinical responsibilities. | `control` | T/D / `SHIP-04-EV` |
| SHIP-05 | SHALL define modular cargo, supplies and vehicle/container interfaces with retention, loading records and cold-chain/expiry controls where applicable. | `mission` | A/I / `SHIP-05-EV` |
| SHIP-06 | SHALL engineer independent helipad and boat handling/transfer interfaces with approved loads, access, exclusion zones and operating limits. | `mission` | A/D / `SHIP-06-EV` |
| SHIP-07 | SHALL assess illustrated LNG/biofuel/electric-ready propulsion alternatives and PV against mission demand and essential reserves. | `energy` | A/T / `SHIP-07-EV` |
| SHIP-08 | SHALL define filtration/desalination/treatment candidates and separate potable, process and waste interfaces for mission/hotel/clinical demand. | `medical` | A/T / `SHIP-08-EV` |
| SHIP-09 | SHALL select authorized FHIR, optional DICOM imaging and mission/geospatial adapters with explicit versions, profiles and permissions. | `clinical` | T / `SHIP-09-EV` |

## High-level SysML design views

[Editable SysML views](../../MBSE/CAS/Drawio/JFXHMS_High_Level_SysML.drawio) contain a block definition diagram, internal block/data-boundary view, supervised mission state machine, release activity and eight requirements/allocation/verification pages covering all 46 IDs. The notation uses SysML 1.x-style stereotypes and directed dependencies in native Drawio cells; it is a conceptual model, not a compiled SysML repository or claim of formal tool conformance.

- `«satisfy»`: proposed design block → requirement. Labels explicitly mark allocation as proposed.
- `«verify»`: planned test case → requirement. No test case contains a passing result.
- BDD composition: filled diamond at the whole; parts are logical responsibilities, not proof of physical deployment.
- IBD connectors: typed information/service flows with explicit clinical versus operational boundaries. They are not complete electrical, hydraulic or network layouts.
- State guards: transition only after authorized readiness and mission review; recovery never automatically resumes a mission. Clinical encounter state and vessel control are separate state machines.

All ten HMS requirements and 36 inherited fleet requirements have a design block and planned verification link. Fleet-specific allocations apply together with all twelve common requirements for each configured vessel. Reusing evidence between vessels needs a recorded configuration-applicability decision.

## Interface contracts to refine

| Contract | Required contents | Boundary / rejection behavior |
| --- | --- | --- |
| Clinical exchange | Selected version/profiles, terminology, encounter identity, authorized purpose, provenance, audit | Validate at protected clinical adapter; reject invalid/unauthorized input; operational telemetry contains no clinical record payload |
| Asset event | Event/schema revision, unique event ID, asset/configuration/mission ID, time, units, quality, source and fault state | Deduplicate replay; mark stale/invalid data; retain unresolved conflicts |
| Reviewed operational request | Actor/role, approved action, target configuration/revision, expiry, acknowledgement | Local authority validates; reject unauthorized, expired or incompatible request |
| Medical module | Mounts, mass/CG, approved load cases, power/fluid interfaces, access/egress, maintenance and configuration | Block activation until applicable structural, utility and clinical approvals are recorded |
| Handover | Incident/mission linkage, sending/receiving responsible roles, time and acknowledgement | Exchange clinical detail through protected channel; record unresolved transfer state |

## Quantitative budgets and open decisions

| Decision record | Budget to approve | Proposed accountable role | Evidence needed before approval |
| --- | --- | --- | --- |
| HMS-DEC-01 | Vessel dimensions, loading, CG, stability, speed/endurance and environment | Naval architect / marine operations | Configuration-specific geometry, loading cases and selected analysis criteria |
| HMS-DEC-02 | Clinical service scope, occupancy, staff, equipment and hygiene/access | Clinical facilities / governance | Reviewed mission layout, service scope and equipment qualification |
| HMS-DEC-03 | Power/reserve, essential loads, ventilation and water/waste capacity/quality | Electrical / utilities leads | Approved mission demand budgets and source-loss cases |
| HMS-DEC-04 | API latency, event freshness, timing accuracy, recovery time and data-loss tolerance | Platform / interoperability leads | Mission-derived limits, traffic profile, failure/replay procedure |
| HMS-DEC-05 | Aircraft/boat compatibility, handling loads and exclusion/operating limits | Aviation / naval integration | Selected vehicle and separately approved interfaces; MOD/SHIP only |
| HMS-DEC-06 | Deployment jurisdiction, applicable rules and selected standards/releases | Systems / regulatory owner | Applicability register and approved verification plan |

All limits, named owners and due dates remain TBD. Each critical TBD requires a decision record before release; a placeholder cannot produce a verification pass. Requirements are engineering proposals, not clinical protocols or regulatory certification.

## Verification and maturity gates

1. Review mission and stakeholder needs; approve configuration/applicability and assign owners.
2. Fix critical budgets and acceptance thresholds; assess hazards and approve interfaces and local fault responses.
3. Validate synthetic platform contracts and negative cases for access, stale/duplicate events, invalid transitions and unreviewed AI proposals.
4. Validate models and bench/SIL/HIL evidence for the selected asset configuration; simulation alone does not establish physical or clinical acceptance.
5. Inspect installed subsystems and perform authorized controlled trials and supervised mission demonstration; clinical and aviation acceptance remain separate workstreams.
6. Release only with versioned evidence, resolved critical issues and approved residual dispositions; changes reopen affected requirements and evidence.

Evidence records must include requirement/procedure IDs, configuration and software/model revisions, input fixtures, expected outcome, observed result, reviewer and date. The repository presently contains proposed architecture, CAD illustrations and requirements artifacts, not a deployed hospital or validated vessel.

## Next AI-assisted work package

HMS-PILOT-002: implement an offline synthetic encounter-to-mission-handover contract harness. Use fictional data and mocked clinical/asset adapters; exercise authorization denial, invalid profile, unreviewed assignment, stale telemetry, duplicate replay, WAN recovery and recorded handover. Produce reproducible results linked to HMS-002/003/004/006/007/008/009 and applicable MED-C07–11. This task is proposed, not executed by this documentation update.

[Project overview](../../README.md) · [CAD-aligned requirements](cad-concept-requirements.md) · [Architecture sources](../architecture/README.md)
