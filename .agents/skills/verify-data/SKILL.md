---
name: verify-data
description: Verify a dataset column or aggregate against the data itself before relying on it — infer a field's meaning from its values, check fill rates, check that an intended key is unique, and cross-check aggregates with an independent computation. Use when interpreting an unfamiliar field, choosing a key, or trusting a count or sum.
---

# Verify data before relying on it

Do not infer a field's meaning, its key, or the value of an aggregate from the
name or the codebook alone. Check it against the data.

## 1. Infer a field's meaning from its values

- Sample the actual values and check the format (e.g. ISO 3166 alpha-2 vs alpha-3:
  two letters or three).
- Use the field's position in the schema and its pattern of missingness. A field
  that is never missing and takes only the values of the publication area is a
  property of the notice's own jurisdiction, not of a worldwide counterparty.

## 2. Check fill rates and overlap

- Count non-empty values per candidate field. A field with poor coverage may not
  support the construct you want (e.g. an identifier filled for only a third of
  rows).
- Compare related fields; when two fields fill at nearly the same rate, they
  likely describe the same set of rows.

## 3. Check that your key is unique

- Compare the row count against the distinct count of each candidate key and of
  the intended composite key. If they differ, explain why before aggregating.
- Watch for placeholder values that collapse distinct rows (e.g. an empty lot id
  turning every single-lot notice into the same key). Empty is not the same as
  missing, and must not be dropped or merged accidentally.

## 4. Cross-check aggregates independently

- Reproduce a small slice of any aggregate with a second tool (e.g. Python reading
  the raw CSV) and compare. A mismatch is a signal, not a rounding error.
- Prefer the simplest explanation. A wrong key or a formatting artefact is more
  likely than a surprising economic result.
