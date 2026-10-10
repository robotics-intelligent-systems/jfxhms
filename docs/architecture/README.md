# Mermaid architecture and workflow sources

These files mirror the 14 Mermaid blocks in the root README. They replace ASCII flow sketches with explicit branches, stores, feedback and qualified review boundaries. The architecture remains proposed; diagrams are not a deployed-system description.

| Diagram | Source |
| --- | --- |
| Vision | [01-vision.mmd](01-vision.mmd) |
| Reference architecture | [02-reference-architecture.mmd](02-reference-architecture.mmd) |
| Digital twin | [03-healthcare-digital-twin-model.mmd](03-healthcare-digital-twin-model.mmd) |
| Clinical interoperability | [04-clinical-information-and-interoperability.mmd](04-clinical-information-and-interoperability.mmd) |
| Hospital workflow | [05-hospital-operations.mmd](05-hospital-operations.mmd) |
| Emergency workflow | [06-emergency-medical-services.mmd](06-emergency-medical-services.mmd) |
| Medical fleet and CAD-backed marine assets | [07-opentwin-medical-fleet.mmd](07-opentwin-medical-fleet.mmd) |
| Governed AI/CDS | [08-ai-and-clinical-decision-support.mmd](08-ai-and-clinical-decision-support.mmd) |
| Laboratory | [09-laboratory-and-diagnostics.mmd](09-laboratory-and-diagnostics.mmd) |
| Supply chain and financing | [10-healthcare-erp-supply-chain-and-financing.mmd](10-healthcare-erp-supply-chain-and-financing.mmd) |
| Data/events | [11-data-and-event-architecture.mmd](11-data-and-event-architecture.mmd) |
| MBSE/CAD/CAM/CAS | [12-mbse-and-simulation.mmd](12-mbse-and-simulation.mmd) |
| Minimal installation target | [13-installation-guide.mmd](13-installation-guide.mmd) |
| Operational MVP | [14-mvp.mmd](14-mvp.mmd) |

Solid edges show primary data/workflow relationships; dotted edges show constrained feedback, evidence or governance relationships. Clinical stores and ordinary operational stores are distinct logical responsibilities even if a deployment shares infrastructure. Reviewed actions still pass through the responsible authorized workflow. Technology/adapters remain replaceable candidates.

When changing a diagram, update both its `.mmd` and its README block, then parse and render it. Event-name examples, the API catalog and recommended directory tree remain reference text rather than being disguised as flowcharts. [CAD-aligned requirements](../requirements/cad-concept-requirements.md) define the separate proposed acceptance baseline.
