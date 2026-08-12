> **Live Actor:** [Run ZUGFeRD to XRechnung Converter on Apify](https://apify.com/kamerozkan/zugferd-to-xrechnung-converter).

# ZUGFeRD to XRechnung Converter: JSON Examples and Schema

[![Apify Actor](https://img.shields.io/badge/Apify-Run%20Actor-00c7b7?logo=apify)](https://apify.com/kamerozkan/zugferd-to-xrechnung-converter)
![Build](https://img.shields.io/badge/build-0.0.1%20SUCCEEDED-2f855a)
![PPE](https://img.shields.io/badge/document--processed-%240.01-4c1)
![Samples](https://img.shields.io/badge/examples-3%20paired%20JSON-2f855a)
![License](https://img.shields.io/badge/license-MIT-blue)

Convert supported ZUGFeRD or Factur-X CII content toward XRechnung UBL with explicit missing-input and semantic evidence.

This repository is a flat, GitHub-friendly sample pack with three paired Actor
inputs, three Dataset result rows, and a standalone JSON Schema. It is useful
for ERP integration design, AP automation, e-invoice testing, and search-driven
technical discovery.

## Verified snapshot

| Field | Value |
|---|---|
| Actor | `zugferd-to-xrechnung-converter` |
| Actor ID | `fxxpdIbB0WYcyISTK` |
| Status | `PUBLIC STORE LISTING` |
| Successful build | `0.0.1` |
| Custom event | `document-processed` |
| Exact event price | `$0.01` |

The live pay-per-event price is $0.01 per evaluated conversion. An Actor-start charge can also apply; check the Store page for the current maximum charge before a production run.

Local contract examples ran the pinned Mustangproject 2.24.0, phax cii2ubl 3.1.7, and KoSIT XRechnung stack. They are not hosted or live Store results.

## What the Actor does

- current BASIC and EN16931 paths, plus EXTENDED only when transfer is proven
- fail-closed ZUGFeRD 1.0 BASIC, COMFORT, and EXTENDED upgrade attempt
- typed missingInputs and allowlisted add-only overrides

## Example matrix

| # | Scenario and input | Output | Result |
|---:|---|---|---|
| 01 | [BASIC source that needs target terms](01_needs_input_input.json) | [Dataset row](01_needs_input_output.json) | `SUCCEEDED` / `REJECTED` / `NEEDS_INPUT` |
| 02 | [EXTENDED source outside proven target transfer](02_extended_unsupported_input.json) | [Dataset row](02_extended_unsupported_output.json) | `SUCCEEDED` / `ACCEPTED` / `UNSUPPORTED` |
| 03 | [Legacy ZUGFeRD 1.0 upgrade boundary](03_legacy_upgrade_input.json) | [Dataset row](03_legacy_upgrade_output.json) | `SUCCEEDED` / `ACCEPTED` / `UNSUPPORTED` |

Example outputs are exact hosted field subsets or projections from real local
engine results. No omitted value was reconstructed. See
[`DATA_NOTICE.md`](DATA_NOTICE.md) for run IDs, fixture hashes, status, and the
hosted-versus-local evidence boundary.



## Dataset contract

[`dataset_record.schema.json`](dataset_record.schema.json) is adapted directly
from the production Dataset contract and narrowed to this Actor name. Money and
quantity values remain decimal strings. Raw XML, PDFs, and generated artifacts
belong in the run key-value store, not in Dataset rows.

Validate an output with any JSON Schema Draft 7 implementation:

```bash
python -m jsonschema -i 01_needs_input_output.json dataset_record.schema.json
```

## Interpretation boundary

The converter never invents missing business data. Legacy source-to-upgrade integrity is NOT_PROVEN, and unsupported semantic transfer does not produce a target artifact.

`ACCEPTED`, `CONFORMANT`, or `CONVERTED` describes only the evidence explicitly
recorded by the pinned processing pipeline. It does not prove legal validity,
tax treatment, authenticity, signature validity, transmission, payment,
archival compliance, or recipient or network acceptance.

## Privacy

Do not publish customer invoices, raw reports, extracted XML, bank details,
tax identifiers, personal data, access tokens, cookies, or private KVS links.
The examples reference public upstream fixtures. You remain responsible for
lawful processing, access control, retention, and deletion.

## Related e-invoice Actor samples

- [ZUGFeRD and Factur-X PDF to JSON](https://github.com/kamerozkan/zugferd-facturx-pdf-to-json-sample)
- [XRechnung XML to JSON](https://github.com/kamerozkan/xrechnung-to-json-parser-sample)
- [Peppol BIS UBL to JSON](https://github.com/kamerozkan/peppol-ubl-to-json-parser-sample)
- [ZUGFeRD to XRechnung](https://github.com/kamerozkan/zugferd-to-xrechnung-converter-sample) (this repository)
- [UBL and CII conversion](https://github.com/kamerozkan/ubl-cii-format-converter-sample)

## License

MIT applies to this repository's original documentation, JSON projections, and
schema adaptation. It does not relicense standards, validator engines, public
fixtures, upstream repositories, third-party marks, or source documents.
