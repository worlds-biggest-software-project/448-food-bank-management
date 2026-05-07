# Standards & API Reference

> Project: Food Bank Management · Candidate #448 · Generated: 2026-05-07

---

## Industry Standards & Specifications

### US Federal Regulatory Frameworks

**7 CFR Part 251 — The Emergency Food Assistance Program (TEFAP)**
- Official URL: https://www.ecfr.gov/current/title-7/subtitle-B/chapter-II/subchapter-B/part-251
- The primary federal regulation governing TEFAP. Establishes household eligibility rules, record-keeping requirements (household name, size, eligibility basis), quarterly reporting obligations to state agencies, and 3-year record retention requirements. As of December 2024, prohibits requiring address or ID documents for eligibility. Any food bank management system serving TEFAP participants must satisfy these requirements.

**USDA FNS Form FNS-667 — TEFAP Quarterly Report**
- Official URL: https://www.fns.usda.gov/tefap/local-level-record-keeping-and-reporting-requirements
- The standardised federal reporting form used by state distributing agencies (SDAs) to report TEFAP participation to USDA Food and Nutrition Service. Data aggregated from local food banks rolls up into this form. Software must produce the underlying household count, pounds distributed, and commodity category breakdowns that feed the FNS-667.

**USDA TEFAP Income Eligibility Guidelines (annual)**
- Official URL: https://www.usda.gov/guidance-documents/food-distribution/fns/emergency-food-assistance-program-tefap-income-eligibility-guidelines-2026
- Annual income thresholds (updated each federal fiscal year) used to determine household eligibility for TEFAP benefits. Must be kept current in any eligibility-determination module.

**7 CFR Part 247 — Commodity Supplemental Food Program (CSFP)**
- Official URL: https://www.ecfr.gov/current/title-7/subtitle-B/chapter-II/subchapter-A/part-247
- Governs CSFP, which targets elderly participants. Adds participant-level tracking obligations (CSFP caseloads, monthly certification records) on top of the TEFAP framework. Systems serving food banks participating in both programs must track the two commodity streams separately.

---

### Human Services Data Standards

**Open Referral Human Services Data Specification (HSDS) v3.x**
- Official URL: https://docs.openreferral.org/en/latest/hsds/overview.html
- GitHub: https://github.com/openreferral/specification
- An open data exchange format for publishing machine-readable information about health, human, and social services — including food assistance programmes — their locations, and the organisations that provide them. Provides a minimal, canonical data model (Organisation, Service, Location, Contact) that enables interoperability among referral systems, 211 directories, and community resource databases. Food bank client-intake systems should be able to export service-directory data in HSDS format for integration with community resource networks.

**Open Referral Human Services Data API (HSDA)**
- Official URL: https://openreferral.github.io/api-specification/
- A family of OpenAPI specifications that define RESTful read/write access to HSDS-structured data. Relevant when a food bank management platform exposes its service catalogue to aggregators or referral platforms (e.g., 211 systems, hospital SDOH programmes).

**HL7 FHIR SDOH Clinical Care Implementation Guide (Gravity Project)**
- Official URL: https://build.fhir.org/ig/HL7/fhir-sdoh-clinicalcare/
- HL7 Blog: https://blog.hl7.org/gravity-project-completes-food-insecurity-and-housing-data-identification
- Defines FHIR profiles for capturing, exchanging, and using Social Determinants of Health data, including food insecurity (LOINC-coded screening questions, ICD-10-Z z-codes, SNOMED-CT intervention codes). Relevant where food banks participate in healthcare-adjacent referral loops — e.g., hospital social workers referring food-insecure patients — and need to exchange structured SDOH data with clinical systems.

---

### Product Identification & Traceability

**GS1 Global Trade Item Number (GTIN) and Barcode Standards**
- Official URL: https://www.gs1.org/standards/barcodes
- Traceability: https://www.gs1.org/standards/traceability
- GS1 standards govern barcode-based product identification used throughout food supply chains: GTIN uniquely identifies products; Global Location Number (GLN) identifies organisations and sites; batch/lot numbers and expiry dates encoded in GS1-128 and DataMatrix barcodes enable FIFO/FEFO rotation. Food banks receiving retail rescue and USDA commodity deliveries will encounter GS1 barcodes on incoming cartons. Any barcode-scanning receiving workflow should decode and store GTINs, lot numbers, and expiry dates per GS1 conventions.

**ISO 22000:2018 — Food Safety Management Systems**
- Official URL: https://www.iso.org/standard/65464.html
- Specifies requirements for a food safety management system along the food chain, incorporating HACCP principles and Codex Alimentarius prerequisites. Certification is not required for nonprofits, but the standard provides a framework for hazard identification, temperature-controlled storage, and product recall procedures that large food bank warehouses may voluntarily adopt or be audited against by insurers and funders.

**ISO 22005:2007 — Traceability in the Feed and Food Chain**
- Official URL: https://www.iso.org/standard/36297.html
- Provides general principles and basic requirements for traceability system design. Directly relevant to demand for supply-chain traceability features (donation → distribution → client) increasingly requested by major funders.

---

### Data API & Integration Standards

**OpenAPI Specification (OAS) 3.1**
- Official URL: https://spec.openapis.org/oas/v3.1.0.html
- Swagger: https://swagger.io/specification/
- The industry-standard language-agnostic format for describing REST APIs in YAML or JSON. Any food bank management system that exposes a public or partner API should publish an OpenAPI 3.1 document to enable automatic code generation, SDK production, and contract testing. Version 3.1 adds full JSON Schema alignment and webhook definitions.

**RFC 7519 — JSON Web Token (JWT)**
- Official URL: https://www.rfc-editor.org/rfc/rfc7519.html
- The standard for compact, URL-safe tokens used for stateless authentication in REST APIs. Widely adopted in SaaS platforms for passing identity and role claims between front-end clients and back-end services. Relevant for implementing the role-based access control required by TEFAP and client data privacy rules.

---

### Security & Compliance Standards

**OAuth 2.0 (RFC 6749) and OpenID Connect 1.0**
- OAuth URL: https://datatracker.ietf.org/doc/html/rfc6749
- OIDC URL: https://openid.net/developers/how-connect-works/
- The de-facto standard pair for delegated authorization (OAuth 2.0) and federated identity / single sign-on (OIDC). Required for enterprise food bank networks that need staff to authenticate via their organisation's identity provider (Microsoft Entra, Google Workspace). Also the standard mechanism for third-party integrations (donor CRMs, volunteer platforms) to access the food bank API on behalf of authorised users.

**NIST SP 800-53 Rev. 5 — Security and Privacy Controls**
- Official URL: https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final
- A comprehensive catalogue of security and privacy controls for information systems. While mandatory only for US federal agencies, state agencies administering TEFAP grants often impose NIST 800-53 control requirements on software vendors through their agreements. PlanStreet's FedRAMP certification is the most stringent implementation of these controls. Even non-FedRAMP platforms should align their security posture to NIST 800-53 families (Access Control, Audit and Accountability, Incident Response, System and Communications Protection) when pursuing government or large-foundation contracts.

**FedRAMP (Federal Risk and Authorisation Management Program)**
- Official URL: https://www.fedramp.gov/
- A US government programme standardising security assessment, authorisation, and monitoring for cloud services used by federal agencies. Required for cloud platforms accessed by federal or state government employees in their official capacity. PlanStreet holds FedRAMP authorisation (FR2101000225). New entrants targeting state TEFAP agencies or federal food assistance programmes should pursue FedRAMP Moderate authorisation.

**GDPR (EU General Data Protection Regulation) and CCPA (California Consumer Privacy Act)**
- GDPR: https://gdpr.info/
- CCPA: https://oag.ca.gov/privacy/ccpa
- Food banks collecting data on individuals located in the EU must comply with GDPR regardless of nonprofit status. CCPA applies to for-profit entities meeting California thresholds; however, food banks with California donors or online presences should implement comparable consent, data-subject-rights, and data-minimisation practices as a matter of best practice. Key requirements: lawful basis for processing, right to access/delete, data breach notification, and privacy-by-design architecture.

**HIPAA (Health Insurance Portability and Accountability Act)**
- Official URL: https://www.hhs.gov/hipaa/for-professionals/privacy/laws-regulations/index.html
- HIPAA applies to covered entities (health plans, healthcare providers, clearinghouses). Most food banks are not covered entities and their client records are PII rather than PHI. However, food banks that participate in healthcare-adjacent SDOH referral programmes, or that store health-related eligibility information (e.g., disability status for CSFP), should implement HIPAA-equivalent data segregation and access controls as a precaution and as required by healthcare partner agreements.

---

## Similar Products — Developer Documentation & APIs

### PantrySoft
- **Description:** The leading commercial SaaS platform for food pantries and food banks, covering client intake, USDA compliance (TEFAP, CSFP), inventory, distribution, and volunteer scheduling.
- **API Documentation:** https://www.pantrysoft.com/api-and-integration-services/
- **SDKs/Libraries:** Not publicly documented; contact sales for integration enquiries.
- **Developer Guide:** Contact PantrySoft account management.
- **Standards:** REST; OpenAPI documentation not publicly available.
- **Authentication:** Not publicly documented (likely API key or OAuth 2.0 for enterprise clients).

### Link2Feed
- **Description:** Cloud-based case management and food bank platform with mobile check-in, real-time inventory tracking, and automated USDA compliance reporting. First preferred technology provider for Feeding America's Service Insights initiative.
- **API Documentation:** https://link2feed.atlassian.net/wiki/spaces/LDM/ (Developer Manual — requires partner account)
- **RESTful Client and Appointment API:** https://link2feed.atlassian.net/wiki/spaces/LDM/pages/2223669293/Link2Feed+RESTful+Client+and+Appointment+API
- **Third-Party Data Access:** https://link2feed.atlassian.net/wiki/spaces/LDM/pages/1955725464/Third+Party+Data+Access+and+Analytics+Integration
- **SDKs/Libraries:** Database Access Suite (MySQL/MariaDB views over TLS/SSL); HTTP Export API for data warehouse sync.
- **Developer Guide:** Partner access required; API base URL format: `https://{{ HostName }}/api/v1/datatypes`
- **Standards:** REST/JSON; Database Access Suite uses standard MySQL/MariaDB connections.
- **Authentication:** TLS/SSL; specific token method not publicly documented.

### PlanStreet
- **Description:** HIPAA and FedRAMP-compliant case management platform for nonprofits and government social service agencies, with food pantry support, customisable intake, barcode scanning, and USDA compliance.
- **API Documentation:** https://www.planstreet.com/integration
- **SDKs/Libraries:** Not publicly documented.
- **Developer Guide:** Open API for integration with EHRs, CRMs, billing, and scheduling systems; automatic API generation for custom forms.
- **Standards:** REST; OpenAPI format not confirmed.
- **Authentication:** Not publicly documented; FedRAMP Moderate controls imply OAuth 2.0 / OIDC.

### Aplos
- **Description:** Nonprofit fund accounting and donation management SaaS. Relevant as a financial integration target for food banks needing donation-to-ledger data flows.
- **API Documentation:** https://www.aplos.com/api
- **Help Center:** https://help.aplos.com/hc/en-us/articles/34206320514573-API-Overview
- **SDKs/Libraries:** Third-party integrations via APIANT: https://apiant.com/connections/Aplos
- **Developer Guide:** Available via Aplos Help Center (account required for full docs).
- **Standards:** REST/JSON.
- **Authentication:** API key (confirmed via help documentation).

### MealConnect (Feeding America)
- **Description:** Feeding America's food rescue platform connecting food donors (retailers, restaurants) with local food banks and pantries. Has rescued over 7 billion pounds since 2014. Integration enables food banks to receive and log retail rescue donations automatically.
- **API Documentation (Food Bank):** https://faom.docs.apiary.io/
- **API Documentation (General):** https://mealconnect.docs.apiary.io/
- **Mobile Apps:** iOS (https://apps.apple.com/us/app/mealconnect/id1230097075), Android (https://play.google.com/store/apps/details?id=com.feedingamerica.mealconnect)
- **Standards:** REST; Apiary-hosted API Blueprint documentation.
- **Authentication:** Not publicly documented; Feeding America partner access required.

### Food Bank Manager
- **Description:** Cloud-based food bank and pantry management software trusted by 34,600+ volunteers processing 5+ million visits annually. Covers clients, donations, volunteers, inventory, and TEFAP compliance with electronic signatures.
- **API Documentation:** Not publicly documented. Contact https://www.foodbankmanager.com/ for integration enquiries.
- **SDKs/Libraries:** Not publicly available.
- **Standards:** Not publicly documented.
- **Authentication:** Not publicly documented.

### AidKit
- **Description:** A secure aid and benefits management platform used by government and nonprofit programmes to manage applications, eligibility verification, case management, and payment distribution. Relevant as an adjacent platform for broader emergency assistance programmes.
- **Platform:** https://www.aidkit.com/platform
- **IDKit API Reference (identity verification component):** https://docs.idkit.com/
- **Developer Guide:** Contact via https://www.aidkit.com/demo-request
- **Standards:** REST; full public API documentation not available.
- **Authentication:** Not publicly documented.

### StratusLIVE CRM (Microsoft Dynamics-based)
- **Description:** Nonprofit CRM for donor management, fundraising, and volunteer coordination. Built on Microsoft Dynamics 365. Relevant as a donor-management integration target for food banks with significant fundraising operations.
- **API Documentation:** Microsoft Dynamics 365 Web API: https://learn.microsoft.com/en-us/power-apps/developer/data-platform/webapi/overview
- **SDKs/Libraries:** Microsoft Power Platform SDK; Dataverse SDK for .NET, JavaScript.
- **Developer Guide:** https://learn.microsoft.com/en-us/dynamics365/
- **Standards:** OData v4 (REST-based); OpenAPI 2.0 (Swagger) support.
- **Authentication:** OAuth 2.0 / Microsoft Entra ID.

---

## Notes

**Data Standards Gap — Absence of a universal food bank API standard**
No sector-wide open API standard exists for food bank management (analogous to FHIR in healthcare or Open Banking PSD2 APIs in finance). Feeding America's Service Insights initiative is the closest effort to standardise data collection across its 200-member network, but it is proprietary and partner-only. The Open Referral HSDS/HSDA standards cover service-directory data but not operational data (inventory, distribution transactions, USDA commodity tracking). An open-source food bank platform has an opportunity to define a de-facto open API standard for this sector.

**Emerging Standard — USDA 2026 Reporting Rule**
The Food Distribution Programs: Improving Access and Parity Final Rule (89 FR 87228, effective 2026) revised reporting collection requirements across CSFP, TEFAP, FDPIR, and USDA Foods in Disasters programs, adding new data elements and modifying existing ones. Software vendors serving TEFAP-participating food banks should monitor FNS notices at https://www.fns.usda.gov/tefap/state-local-agency/policy for updated reporting requirements as implementing guidance is issued.

**SDOH Interoperability Opportunity**
The Gravity Project's FHIR-based SDOH implementation guide provides a clinical data exchange pathway for food banks operating in healthcare referral networks. As hospitals and health systems increasingly screen for food insecurity (driven by value-based care incentives), food banks that can receive structured FHIR-format referrals and return structured encounter data will have a meaningful interoperability advantage.

---

## Sources

- [USDA TEFAP Local-Level Record Keeping and Reporting Requirements](https://www.fns.usda.gov/tefap/local-level-record-keeping-and-reporting-requirements)
- [eCFR 7 CFR Part 251 — The Emergency Food Assistance Program](https://www.ecfr.gov/current/title-7/subtitle-B/chapter-II/subchapter-B/part-251)
- [USDA TEFAP Income Eligibility Guidelines 2026](https://www.usda.gov/guidance-documents/food-distribution/fns/emergency-food-assistance-program-tefap-income-eligibility-guidelines-2026)
- [Federal Register: Food Distribution Programs Improving Access and Parity Rule (2026)](https://www.federalregister.gov/documents/2026/03/19/2026-05442/agency-information-collection-activities-renewing-burden-number-0584-0293)
- [Open Referral HSDS Documentation](https://docs.openreferral.org/en/latest/hsds/overview.html)
- [Open Referral HSDA API Specification](https://openreferral.github.io/api-specification/)
- [HL7 FHIR SDOH Clinical Care IG (Gravity Project)](https://build.fhir.org/ig/HL7/fhir-sdoh-clinicalcare/)
- [Gravity Project Completes Food Insecurity Data Identification — HL7 Blog](https://blog.hl7.org/gravity-project-completes-food-insecurity-and-housing-data-identification)
- [GS1 Barcode Standards](https://www.gs1.org/standards/barcodes)
- [GS1 Traceability Standards](https://www.gs1.org/standards/traceability)
- [ISO 22000:2018 Food Safety Management](https://www.iso.org/standard/65464.html)
- [OpenAPI Specification 3.1](https://spec.openapis.org/oas/v3.1.0.html)
- [RFC 7519 JSON Web Token](https://www.rfc-editor.org/rfc/rfc7519.html)
- [OpenID Connect Overview — OpenID Foundation](https://openid.net/developers/how-connect-works/)
- [OAuth 2.0 RFC 6749](https://datatracker.ietf.org/doc/html/rfc6749)
- [NIST SP 800-53 Rev. 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final)
- [FedRAMP Marketplace — PlanStreet](https://www.fedramp.gov/marketplace/products/FR2101000225/)
- [GDPR Summary — HIPAA vs Nonprofits](https://www.hhs.gov/hipaa/for-professionals/privacy/laws-regulations/index.html)
- [PantrySoft API and Integration Services](https://www.pantrysoft.com/api-and-integration-services/)
- [Link2Feed Developer Manual (Confluence)](https://link2feed.atlassian.net/wiki/spaces/LDM/)
- [Link2Feed RESTful Client and Appointment API](https://link2feed.atlassian.net/wiki/spaces/LDM/pages/2223669293/Link2Feed+RESTful+Client+and+Appointment+API)
- [Link2Feed Third Party Data Access and Analytics Integration](https://link2feed.atlassian.net/wiki/spaces/LDM/pages/1955725464/Third+Party+Data+Access+and+Analytics+Integration)
- [PlanStreet Integrations](https://www.planstreet.com/integration)
- [Aplos API Overview](https://www.aplos.com/api)
- [MealConnect Food Bank API (Apiary)](https://faom.docs.apiary.io/)
- [MealConnect API (Apiary)](https://mealconnect.docs.apiary.io/)
- [MealConnect — Feeding America](https://www.feedingamerica.org/about-us/press-room/mealconnect)
- [Feeding America Data Standardisation Initiative — Dataversity](https://www.dataversity.net/case-studies/case-study-feeding-america-takes-project-standardize-data-improve-data-quality/)
- [Link2Feed Named Service Insights Partner for Feeding America](https://www.link2feed.com/link2feed-feedingamerica-partnership/)
- [Microsoft Dynamics 365 Web API](https://learn.microsoft.com/en-us/power-apps/developer/data-platform/webapi/overview)
