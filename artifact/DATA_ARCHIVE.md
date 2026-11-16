# Data archive: Study B1 replication data

The data behind Study B1's registered and post-registration results are archived on Zenodo.

| Field | Value |
| --- | --- |
| DOI (this version) | [10.5281/zenodo.24292422](https://doi.org/10.5281/zenodo.24292422) |
| Concept DOI (all versions) | [10.5281/zenodo.24292421](https://doi.org/10.5281/zenodo.24292421) |
| Record | https://zenodo.org/records/24292422 |
| Version | 1.0, published 2026-11-16 |
| Licence | CC BY 4.0 for the data and text; the analysis code is released separately under MIT |
| Files | 9, 1,534,955,303 bytes in all |

## Files and SHA-256

| File | Bytes | SHA-256 |
| --- | ---: | --- |
| `analysis.tar.gz` | 82,301,243 | `c3c3260d6ed3558195c29e09552fb88332639ee7c0949879fdffeddfc37e3b8e` |
| `documents.tar.gz` | 37,944,467 | `75be64a6e0b6aa829138c5aef15e5fc0a680f755d4ddaac7998d0eb4140f24a6` |
| `run_data_main.tar.gz` | 262,131,970 | `cc2875742aae6cd14ef74d02250c2ad4cb047b0c125802fea4db799b9b225f83` |
| `run_data_pilot.tar.gz` | 94,009,286 | `5d25a2243aafc568363be603a6fb24b586af5f94cd44ed86b9dd098938a9ff69` |
| `verification_caches.tar.gz` | 782,793,627 | `5125e72a7c6b0573c1cd5b087b61f866716775f65c017441761cffe1c54720e6` |
| `verification_labels.tar.gz` | 222,098,019 | `8b219f640cfd87370420fe1878cfe15f474808e182ef6c0f8fca9a96208a0ba1` |
| `SHA256SUMS` | 526 | `31db19e9aff5291e118fd337caacdf3288a14715bf22832bfcd000891ff3b8ab` |
| `MANIFEST.sha256` | 53,671,474 | `9cf7da48ec4e75b65d1a734f0d7e8d4509d93e49d7f8432e1d43dc326ce71600` |
| `README.md` | 4,691 | `0195357be40d14d1fe71b54416311c800e4cdf1ccf458b5334cd47d2af172d24` |

- `SHA256SUMS` lists the SHA-256 of the six archives, and `MANIFEST.sha256` lists the SHA-256 of every file inside
  them. Their own SHA-256 sums above tie both lists to this repository.
- The package's `README.md` says what each archive holds and what was replaced before release (local usernames,
  batch IDs, e-mail addresses in the stored bibliographic answers, and the two coders' names, now Author A and
  Author B). Its `SCRUB_LOG.tsv` gives each changed file's original and packaged SHA-256, so every changed file can be
  matched to the hashes registered at `prereg-tag2b`.
- The registered analysis outputs inside `analysis.tar.gz` carry the SHA-256 sums cited in the registration notes and
  in the Level 1 file.

## To check a download

Put the nine files in one folder and run this there (on a Mac, use `shasum -a 256 -c` in place of `sha256sum -c`):

```
sha256sum -c <<'EOF'
c3c3260d6ed3558195c29e09552fb88332639ee7c0949879fdffeddfc37e3b8e  analysis.tar.gz
75be64a6e0b6aa829138c5aef15e5fc0a680f755d4ddaac7998d0eb4140f24a6  documents.tar.gz
cc2875742aae6cd14ef74d02250c2ad4cb047b0c125802fea4db799b9b225f83  run_data_main.tar.gz
5d25a2243aafc568363be603a6fb24b586af5f94cd44ed86b9dd098938a9ff69  run_data_pilot.tar.gz
5125e72a7c6b0573c1cd5b087b61f866716775f65c017441761cffe1c54720e6  verification_caches.tar.gz
8b219f640cfd87370420fe1878cfe15f474808e182ef6c0f8fca9a96208a0ba1  verification_labels.tar.gz
31db19e9aff5291e118fd337caacdf3288a14715bf22832bfcd000891ff3b8ab  SHA256SUMS
9cf7da48ec4e75b65d1a734f0d7e8d4509d93e49d7f8432e1d43dc326ce71600  MANIFEST.sha256
0195357be40d14d1fe71b54416311c800e4cdf1ccf458b5334cd47d2af172d24  README.md
EOF
```

Then unpack the six archives in the same folder. Each unpacks into `Study_B1_replication/`. Run
`sha256sum -c MANIFEST.sha256` inside `Study_B1_replication/`, where `documents.tar.gz` also puts a copy of
`MANIFEST.sha256`.
