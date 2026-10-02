**Maintainer:** Frangel Raúl Crespo Barrera
**Last verified:** 2026-10-02
**Scope:** the audit framework, documentation, checklists, templates, and the current `tools/` directory.

| Field | Current record |
|---|---|
| Status | `tools/` classification is pending; GitHub did not detect a primary language. |
| Evidence | `tools/`, `docs/checklists/`, `docs/mitre-attack-ics-mapping.md`, `mkdocs.yml`, `.github/workflows/pages.yml`. |
| Standards | IEC 62443 and NIST SP 800-82 are assessment references. MITRE ATT&CK for ICS is a threat-technique mapping. No certification claim is made. |
| Verification | Classify every `tools/` item as documentation, auxiliary script, executable audit tool, or template; then run `mkdocs build --strict`. |
| Owner | Repository owner maintains the classification and nav entry. |
| Limitations | No test or packaging requirement is inferred until the classification is complete. |

The current CI publishes the MkDocs site. The `tools-classification.md` page is included in the `Resources` nav; the root README uses a GitHub URL so the same link remains valid when copied to `docs/index.md` by the Pages workflow.
