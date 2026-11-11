# Release Gate Licence Policy (v2.3)

Every model or dataset asset proposed for release must pass licence classification before publication.

## Licence classes

- `permissive`: apache-2.0, mit, bsd-2-clause, bsd-3-clause, cc-by-4.0, cc-by-sa-4.0, odc-by
- `restricted`: cc-by-nc-4.0, cc-by-nc-sa-4.0, llama3.1, llama3, gemma, bigcode-openrail-m,
  creativeml-openrail-m, bigscience-bloom-rail-1.0, openrail
- `unresolved`: no declared licence, or "unknown", "other", or any identifier not in the lists above

## Decision rules

Evaluate in order; the first matching rule wins.

1. Licence class is `unresolved` -> `BLOCKED`, reason code `license_unverifiable`
2. The upstream repository requires gated access approval -> `BLOCKED`, reason code `gated_access`
3. Release target is `public` and licence class is not `permissive` -> `BLOCKED`, reason code `non_permissive_public_release`
4. Release target is `internal` and licence class is `restricted` -> `RESTRICTED`, reason code `restricted_internal_only`
5. Otherwise -> `APPROVED`, reason code `permissive_ok`

## Follow-up requirements

- Every asset whose decision is not `APPROVED` requires a tracking issue in the release-gate repository,
  titled `[DECISION] asset-id - repo-id`, with the decision, licence and reason code in the body.
- The batch intake issue must receive a summary comment with the number of assets per decision.
