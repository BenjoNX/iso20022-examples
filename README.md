# ISO 20022 XML Examples

Annotated examples of ISO 20022 payment files for SEPA Credit Transfers, Direct Debits, and SWIFT MT103 messages.

## Contents

| File | Format | Description |
|------|--------|-------------|
| [pain.001.001.03-credit-transfer.xml](examples/pain.001.001.03-credit-transfer.xml) | pain.001.001.03 | SEPA Credit Transfer (single payment) |
| [pain.001.001.03-batch.xml](examples/pain.001.001.03-batch.xml) | pain.001.001.03 | SEPA Credit Transfer (batch of 3 payments) |
| [pain.008.001.02-direct-debit.xml](examples/pain.008.001.02-direct-debit.xml) | pain.008.001.02 | SEPA Direct Debit (single collection) |
| [VALIDATION-CHECKLIST.md](VALIDATION-CHECKLIST.md) | — | Common errors and validation checklist |

## What is ISO 20022?

ISO 20022 is the international standard for financial messaging. It defines XML-based message formats used by banks and financial institutions worldwide for payment processing.

### Key message types

- **pain.001** — Customer Credit Transfer Initiation (SEPA wire transfers)
- **pain.002** — Customer Payment Status Report (bank acknowledgement)
- **pain.008** — Customer Direct Debit Initiation (SEPA direct debits)
- **camt.053** — Bank-to-Customer Statement

## Generate & Validate Online

You can generate and validate ISO 20022 XML files for free using:

- **Generator**: [iso20022generator.com](https://iso20022generator.com/en/sepa-xml-generator) — Generate pain.001, pain.008, and SWIFT MT103 files
- **Validator**: [iso20022generator.com/validator](https://iso20022generator.com/en/validator) — Validate any ISO 20022 XML file against XSD schemas

## Useful Resources

- [SEPA XML File Guide](https://iso20022generator.com/en/blog/sepa-xml-file-guide) — Complete guide to SEPA XML structure
- [pain.001 vs pain.002](https://iso20022generator.com/en/blog/pain-001-vs-pain-002) — Differences between initiation and status messages
- [ISO 20022 Migration Guide](https://iso20022generator.com/en/blog/iso-20022-migration-guide) — What you need to know for migration
- [ISO 20022 Official Catalog](https://www.iso20022.org/catalogue-messages) — Official message catalog

## License

These examples are provided under the [MIT License](LICENSE). Use them freely in your projects.
