# CAD-aligned medical fleet requirements

This proposed baseline connects the three marine JPEG concepts to high-level requirements, logical architecture, interfaces, operating contexts, verification criteria and planned evidence. The drawings are concept illustrations, not dimensioned production CAD or acceptance evidence. Clinical services, naval/aviation interfaces, energy sources and software integrations require separate configuration-specific engineering and approval.

| CAD concept | Editable requirements diagram | Illustrated scope |
| --- | --- | --- |
| [Medical patrol boat](../../MBSE/CAD/medical-patrol-boat-concept.jpg) | [Patrol boat specification](../../MBSE/CAS/Drawio/OpenTwin_Medical_Patrol_Boat_High_Level_Requirements.drawio) | Coastal/river craft, twin outboards, patient/stretcher area, modular equipment/rescue/cargo deck, PV, navigation/communications and fresh/grey/black water. No depicted helipad, operating theatre or ICU. |
| [Modular medical vessel](../../MBSE/CAD/modular-medical-vessel-concept.jpg) | [Modular vessel specification](../../MBSE/CAS/Drawio/OpenTwin_Modular_Medical_Vessel_High_Level_Requirements.drawio) | Configurable medical facilities, solar/hybrid energy, local navigation, helipad, rescue/support boat handling and utilities. |
| [Large medical support ship](../../MBSE/CAD/large-medical-support-ship-concept.jpg) | [Large support ship specification](../../MBSE/CAS/Drawio/OpenTwin_Large_Medical_Support_Ship_High_Level_Requirements.drawio) | Candidate advanced-care modules, accommodation, logistics/cargo, bridge/command, helipad/support boats, energy alternatives, water/desalination/waste candidates and clinical exchange examples. |
| All three concepts | [Common fleet requirements](../../MBSE/CAS/Drawio/OpenTwin_Medical_Fleet_Common_High_Level_Requirements.drawio) | Naval loading/structure, patient access, essential services, modular interfaces, protected clinical integration, asset telemetry, local authority, resilience and verification. |

## Allocation and acceptance

[The traceability register](cad-requirements-traceability.csv) contains 36 uniquely identified proposed requirements: 12 common, 7 patrol-boat, 8 modular-vessel and 9 large-ship requirements. Each records its CAD callout or architecture-derived rationale, design allocation, method, acceptance criterion, proposed owner role and planned evidence ID. Shared requirements MED-C01…MED-C12 apply alongside each asset specification; evidence reuse requires a documented applicability decision for the installed configuration.

The specifications cover scope/CAD interpretation, requirements with acceptance criteria, logical architecture, interfaces/operating contexts and verification/budget gates. Architecture arrows illustrate selected logical relations, not complete electrical/fluid layouts. Clinical work, dispatch and local vessel control retain distinct responsibilities. Acceptance evidence is planned, not produced; engineering roles are suggestions rather than assigned individuals.

Before baseline approval, assign named people/dates, approve mission/occupancy and configuration, fix measurable acceptance budgets and methods, and resolve critical interfaces, hazards and mode/fault responses. I = inspection; A = analysis; D = demonstration; T = test. Requirements with analysis/inspection criteria still need approved values and engineering evidence before they can pass.

## Decisions grounded in the illustrations

- Displayed speeds (28 kn, 12 kn and 18 kn), coordinates, temperatures, percentages and system-status labels are dashboard examples, not operational or acceptance limits.
- Helipad and support-boat interfaces apply to modular/large vessels only. Their appearance does not establish aircraft/boat compatibility, handling capability or authorization.
- The large ship's surgery, ICU, maternity and other advanced services are candidate modules. They do not become obligations for the smaller craft; each activated clinical service needs its own approved scope, staffing, equipment and qualification.
- Fuel/electric/hybrid, and the large ship's LNG/biofuel/electric-ready alternatives, require a recorded selection. The concepts do not prove that all alternatives are installed or achieve low-emission performance.
- Water/waste labels require separate potable, process and waste designs and quality/capacity criteria; a depicted desalination system is not potability evidence.
- Software/protocol logos and open-design labels are candidates/aspirations; they do not establish compatibility, deployed services, certification or freedom from third-party rights.
- Physical-asset twins use configuration, readiness and authorized minimal encounter links. Clinical records and access audit remain separately governed; ordinary fleet events must not become unrestricted clinical-data replicas.

The security boundary is consistent with [HL7's FHIR security guidance](https://www.hl7.org/fhir/security.html), which distinguishes FHIR exchange/content from the security systems that implement authentication, access control and audit. This proposal does not select a mandatory FHIR release: version, profiles, terminology and conformance tests must be selected per integration.

## Preserved Drawio reference

[MBSE/CAS/UML/D3Web.drawio](../../MBSE/CAS/UML/D3Web.drawio) contains d3web/Drools class sketches. It is unchanged and remains a research reference; it is not a predecessor naval requirements baseline. There were no corresponding technical-requirements diagrams to migrate in the inspected repository. The four new specifications therefore introduce requirement IDs without renaming existing class IDs or repurposing that file.

[The CAD source manifest](cad-source-baseline.json) records the input commit, SHA-256 hashes, Git blob identities and pinned links. All three source JPEGs remain unchanged.

## Relationship to Mermaid

The README's 14 Mermaid diagrams describe architecture/workflows; they are not verification evidence. [Editable sources and index](../architecture/README.md) mirror those blocks. The fleet architecture names the three CAD-backed vessel types and links their mission/asset state to EMS and healthcare coordination while preserving the clinical-data boundary.

## Integrated platform specification

[HMS-MBSE-001](high-level-technical-specification.md) adds ten platform requirements to this unchanged 36-requirement fleet baseline, with [combined traceability](high-level-requirements-traceability.csv) and [editable SysML views](../../MBSE/CAS/Drawio/JFXHMS_High_Level_SysML.drawio). The original fleet register remains authoritative for its IDs; the combined register reproduces those rows. Diagram satisfaction and verification links are proposed allocations and planned procedures, not acceptance results.
