# SEPA XML Validation Checklist

Common errors when creating ISO 20022 XML files, and how to fix them.

Use the free online validator: **[iso20022generator.com/validator](https://iso20022generator.com/en/validator)**

---

## 1. XML Structure Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Missing XML declaration | No `<?xml version="1.0"?>` | Add `<?xml version="1.0" encoding="UTF-8"?>` as the first line |
| Wrong namespace | Incorrect `xmlns` attribute | Use `urn:iso:std:iso:20022:tech:xsd:pain.001.001.03` for credit transfers |
| Wrong root element | Using `<CstmrCdtTrfInitn>` directly | Wrap in `<Document xmlns="...">` |

## 2. Group Header Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `NbOfTxs` mismatch | Count doesn't match actual transactions | Count all `<CdtTrfTxInf>` or `<DrctDbtTxInf>` elements |
| `CtrlSum` mismatch | Sum doesn't match transaction amounts | Sum all `<InstdAmt>` values (2 decimal places) |
| `MsgId` too long | Exceeds 35 characters | Shorten to max 35 ASCII characters |
| `MsgId` non-ASCII | Contains accents or special chars | Use only `[A-Za-z0-9+\-/().,':? ]` |

## 3. IBAN / BIC Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Invalid IBAN checksum | Typo in IBAN | Verify using the MOD-97 algorithm |
| IBAN wrong length | Country-specific length mismatch | FR=27, DE=22, ES=24, IT=27, NL=18, PL=28 |
| BIC wrong format | Not 8 or 11 characters | BIC must be exactly 8 or 11 alphanumeric chars |
| BIC doesn't match IBAN country | BIC from wrong country | Verify BIC corresponds to the IBAN's bank |

## 4. Amount Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Missing decimal places | `1500` instead of `1500.00` | Always use exactly 2 decimal places |
| Wrong currency | Non-EUR for SEPA | SEPA only supports EUR (use `Ccy="EUR"`) |
| Negative amount | Amount <= 0 | All amounts must be positive |
| Amount too large | Exceeds bank limit | Most banks limit single transfers to EUR 999,999,999.99 |

## 5. Date Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Wrong date format | Using DD/MM/YYYY | Use ISO format: `YYYY-MM-DD` |
| Date in the past | Execution date already passed | Use today or a future date |
| Weekend/holiday date | Bank can't process on non-business days | Use the next business day |
| SDD collection too soon | Not enough lead time | FRST/OOFF: 5 business days, RCUR: 2 business days |

## 6. Direct Debit Specific Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Missing `MndtId` | No mandate reference | Every SDD requires a unique mandate ID |
| Missing `DtOfSgntr` | No mandate signature date | Required: the date the customer signed the mandate |
| Missing `CdtrSchmeId` | No ICS/creditor identifier | Obtain your ICS from your central bank |
| Wrong `SeqTp` | Using FRST for recurring | Use FRST only for the first collection, then RCUR |

## 7. Character Encoding Errors

| Error | Cause | Fix |
|-------|-------|-----|
| XML special chars in names | Using `&`, `<`, `>`, `"`, `'` | Escape as `&amp;`, `&lt;`, `&gt;`, `&quot;`, `&apos;` |
| Non-Latin characters | Using Cyrillic, Chinese, etc. | SEPA allows only Latin characters (basic + extended) |
| Accented characters rejected | Some banks restrict charset | Transliterate: `é` → `e`, `ü` → `u`, `ñ` → `n` |

## 8. Remittance Information Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `Ustrd` too long | Exceeds 140 characters | Keep unstructured remittance info under 140 chars |
| Both structured and unstructured | Using `Strd` and `Ustrd` together | Choose one: either `<Strd>` or `<Ustrd>` |

---

## Quick Validation Steps

1. **Schema validation**: Validate against the official XSD schema
2. **Checksum verification**: Ensure `NbOfTxs` and `CtrlSum` match
3. **IBAN validation**: Verify all IBANs pass MOD-97
4. **BIC verification**: Confirm all BICs are valid and match IBAN countries
5. **Date check**: Ensure all dates are in the future and on business days
6. **Character check**: Verify no forbidden characters in names or references

**Free online validation**: [iso20022generator.com/validator](https://iso20022generator.com/en/validator)
