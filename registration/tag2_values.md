# prereg-tag2 values for every hand-check outcome

Analysis b1-analysis-2 (2026-11-08); rules b1-am5-rules-1 (2026-11-08).

Input labels (SHA-256 of labels.jsonl):
- labels_2b: `1e6a3f44d958f79ab4cd888c866751f1e957c9df0da8c171f039d4d745df2ea2`
- labels_3: `5dd0a0be583055c7c8a77598c6d50d06af5f1c45f71aa4da9992e24457555d7e`
- ow_labels_2b: `d5379722eb840659320ef0354cb86170c4932c2fac358f1fe994f4f2d4441cd1`
- ow_labels_3: `331e2baf70d782502091cea6ec2699ddbea4ea214c1a84332aa8f87b4640fa67`

Live answers for the poorly indexed approved journals, as the main run searches them:
- api_2b: 84 stored live-search rows merged (unresolved 84); 0 without a live answer; live labels `5188c845c17e08c4c987ba2b209da015f480f5ff2804cdbbeca15fe9e49c641b`
- api_3: 154 stored live-search rows merged (fabricated 2, unresolved 152); 0 without a live answer; live labels `db24d395355f7e910c3a5029e82a1304e6228f9d64e5f486ebaf18f575352e1d`

## Ceilings (stage-2b rehomed_rate)

| Switches | claude-haiku-5-5 | claude-sonnet-5-5 | deepseek-flash | deepseek-v4-pro |
|---|---|---|---|---|
| author=used, noauthor=used, title_only=joins | 0.194 (ceiling 0.353; 13/67) | 0.064 (ceiling 0.098; 23/362) | 0.203 (ceiling 0.304; 40/197) | 0.187 (ceiling 0.294; 50/268) |
| author=used, noauthor=used, title_only=does_not_join | 0.105 (ceiling 0.273; 4/38) | 0.023 (ceiling 0.034; 7/304) | 0.155 (ceiling 0.245; 22/142) | 0.133 (ceiling 0.237; 26/196) |
| author=used, noauthor=not_used, title_only=joins | 0.194 (ceiling 0.353; 13/67) | 0.064 (ceiling 0.098; 23/362) | 0.203 (ceiling 0.304; 40/197) | 0.187 (ceiling 0.294; 50/268) |
| author=used, noauthor=not_used, title_only=does_not_join | 0.105 (ceiling 0.273; 4/38) | 0.023 (ceiling 0.034; 7/304) | 0.155 (ceiling 0.245; 22/142) | 0.133 (ceiling 0.237; 26/196) |
| author=not_used, noauthor=used, title_only=joins | 0.203 (ceiling 0.368; 12/59) | 0.059 (ceiling 0.093; 20/337) | 0.184 (ceiling 0.288; 32/174) | 0.155 (ceiling 0.245; 35/226) |
| author=not_used, noauthor=used, title_only=does_not_join | 0.100 (ceiling 0.300; 3/30) | 0.014 (ceiling 0.025; 4/279) | 0.118 (ceiling 0.201; 14/119) | 0.071 (ceiling 0.146; 11/154) |
| author=not_used, noauthor=not_used, title_only=joins | 0.203 (ceiling 0.368; 12/59) | 0.059 (ceiling 0.093; 20/337) | 0.184 (ceiling 0.288; 32/174) | 0.155 (ceiling 0.245; 35/226) |
| author=not_used, noauthor=not_used, title_only=does_not_join | 0.100 (ceiling 0.300; 3/30) | 0.014 (ceiling 0.025; 4/279) | 0.118 (ceiling 0.201; 14/119) | 0.071 (ceiling 0.146; 11/154) |

## Tolerance, API-hosted drafts (stage 3 minus stage 2b; 2.5th to 97.5th percentile)

| Switches | Doer | compliant_count | fabrication_rate | year_mismatch_rate | misplacement_rate |
|---|---|---|---|---|---|
| author=used, noauthor=used, title_only=joins | claude-haiku-5-5 | [-0.194, 0.000] (n=10) | [-0.243, 0.092] (n=10) | [-0.540, 0.417] (n=10) | [-0.472, 0.193] (n=10) |
| author=used, noauthor=used, title_only=joins | claude-sonnet-5-5 | [-1.081, 0.694] (n=10) | [-0.217, 0.320] (n=10) | [-0.490, 0.191] (n=10) | [-0.280, 0.257] (n=10) |
| author=used, noauthor=used, title_only=joins | deepseek-flash | [-0.500, 0.775] (n=10) | [-0.058, 0.119] (n=10) | [-0.146, 0.489] (n=10) | [-0.181, 0.138] (n=10) |
| author=used, noauthor=used, title_only=joins | deepseek-v4-pro | [-0.250, 0.831] (n=10) | [-0.179, 0.075] (n=10) | [-0.216, 0.181] (n=10) | [-0.221, 0.100] (n=10) |
| author=used, noauthor=used, title_only=does_not_join | claude-haiku-5-5 | [-0.194, 0.000] (n=10) | [-0.282, 0.105] (n=10) | [-0.054, 0.500] (n=6) | [-0.646, 0.191] (n=6) |
| author=used, noauthor=used, title_only=does_not_join | claude-sonnet-5-5 | [-1.081, 0.694] (n=10) | [-0.177, 0.214] (n=10) | [-0.094, 0.080] (n=10) | [-0.802, 0.272] (n=10) |
| author=used, noauthor=used, title_only=does_not_join | deepseek-flash | [-0.500, 0.775] (n=10) | [-0.042, 0.109] (n=10) | [-0.162, 0.280] (n=8) | [-0.258, 0.380] (n=8) |
| author=used, noauthor=used, title_only=does_not_join | deepseek-v4-pro | [-0.250, 0.831] (n=10) | [-0.177, 0.066] (n=10) | [-0.167, 0.331] (n=10) | [-0.402, 0.226] (n=10) |
| author=used, noauthor=not_used, title_only=joins | claude-haiku-5-5 | [-0.194, 0.000] (n=10) | [-0.309, 0.093] (n=10) | [-0.540, 0.417] (n=10) | [-0.472, 0.193] (n=10) |
| author=used, noauthor=not_used, title_only=joins | claude-sonnet-5-5 | [-1.081, 0.694] (n=10) | [-0.229, 0.323] (n=10) | [-0.490, 0.191] (n=10) | [-0.280, 0.257] (n=10) |
| author=used, noauthor=not_used, title_only=joins | deepseek-flash | [-0.500, 0.775] (n=10) | [-0.055, 0.146] (n=10) | [-0.146, 0.489] (n=10) | [-0.181, 0.138] (n=10) |
| author=used, noauthor=not_used, title_only=joins | deepseek-v4-pro | [-0.250, 0.831] (n=10) | [-0.186, 0.072] (n=10) | [-0.216, 0.181] (n=10) | [-0.221, 0.100] (n=10) |
| author=used, noauthor=not_used, title_only=does_not_join | claude-haiku-5-5 | [-0.194, 0.000] (n=10) | [-0.348, 0.123] (n=10) | [-0.054, 0.500] (n=6) | [-0.646, 0.191] (n=6) |
| author=used, noauthor=not_used, title_only=does_not_join | claude-sonnet-5-5 | [-1.081, 0.694] (n=10) | [-0.277, 0.217] (n=10) | [-0.094, 0.080] (n=10) | [-0.802, 0.272] (n=10) |
| author=used, noauthor=not_used, title_only=does_not_join | deepseek-flash | [-0.500, 0.775] (n=10) | [-0.039, 0.133] (n=10) | [-0.162, 0.280] (n=8) | [-0.258, 0.380] (n=8) |
| author=used, noauthor=not_used, title_only=does_not_join | deepseek-v4-pro | [-0.250, 0.831] (n=10) | [-0.184, 0.061] (n=10) | [-0.167, 0.331] (n=10) | [-0.402, 0.226] (n=10) |
| author=not_used, noauthor=used, title_only=joins | claude-haiku-5-5 | [-0.194, 0.000] (n=10) | [-0.238, 0.090] (n=10) | [-0.629, 0.472] (n=10) | [-0.347, 0.157] (n=10) |
| author=not_used, noauthor=used, title_only=joins | claude-sonnet-5-5 | [-1.137, 1.138] (n=10) | [-0.222, 0.324] (n=10) | [-0.751, 0.177] (n=10) | [-0.068, 0.259] (n=10) |
| author=not_used, noauthor=used, title_only=joins | deepseek-flash | [-0.500, 0.775] (n=10) | [-0.058, 0.115] (n=10) | [-0.034, 0.575] (n=10) | [-0.211, 0.000] (n=10) |
| author=not_used, noauthor=used, title_only=joins | deepseek-v4-pro | [-0.250, 0.831] (n=10) | [-0.171, 0.078] (n=10) | [-0.343, 0.214] (n=10) | [-0.211, 0.196] (n=10) |
| author=not_used, noauthor=used, title_only=does_not_join | claude-haiku-5-5 | [-0.194, 0.000] (n=10) | [-0.275, 0.061] (n=10) | [-0.051, 0.500] (n=6) | [-0.615, 0.191] (n=6) |
| author=not_used, noauthor=used, title_only=does_not_join | claude-sonnet-5-5 | [-1.137, 1.138] (n=10) | [-0.281, 0.217] (n=10) | [-0.052, 0.041] (n=9) | [-0.084, 0.327] (n=9) |
| author=not_used, noauthor=used, title_only=does_not_join | deepseek-flash | [-0.500, 0.775] (n=10) | [-0.041, 0.101] (n=10) | [-0.076, 0.142] (n=7) | [-0.252, 0.206] (n=7) |
| author=not_used, noauthor=used, title_only=does_not_join | deepseek-v4-pro | [-0.250, 0.831] (n=10) | [-0.172, 0.070] (n=10) | [-0.250, 0.242] (n=10) | [-0.466, 0.259] (n=10) |
| author=not_used, noauthor=not_used, title_only=joins | claude-haiku-5-5 | [-0.194, 0.000] (n=10) | [-0.317, 0.090] (n=10) | [-0.629, 0.472] (n=10) | [-0.347, 0.157] (n=10) |
| author=not_used, noauthor=not_used, title_only=joins | claude-sonnet-5-5 | [-1.137, 1.138] (n=10) | [-0.302, 0.326] (n=10) | [-0.751, 0.177] (n=10) | [-0.068, 0.259] (n=10) |
| author=not_used, noauthor=not_used, title_only=joins | deepseek-flash | [-0.500, 0.775] (n=10) | [-0.050, 0.141] (n=10) | [-0.034, 0.575] (n=10) | [-0.211, 0.000] (n=10) |
| author=not_used, noauthor=not_used, title_only=joins | deepseek-v4-pro | [-0.250, 0.831] (n=10) | [-0.187, 0.073] (n=10) | [-0.343, 0.214] (n=10) | [-0.211, 0.196] (n=10) |
| author=not_used, noauthor=not_used, title_only=does_not_join | claude-haiku-5-5 | [-0.194, 0.000] (n=10) | [-0.356, 0.073] (n=10) | [-0.051, 0.500] (n=6) | [-0.615, 0.191] (n=6) |
| author=not_used, noauthor=not_used, title_only=does_not_join | claude-sonnet-5-5 | [-1.137, 1.138] (n=10) | [-0.380, 0.220] (n=10) | [-0.052, 0.041] (n=9) | [-0.084, 0.327] (n=9) |
| author=not_used, noauthor=not_used, title_only=does_not_join | deepseek-flash | [-0.500, 0.775] (n=10) | [-0.032, 0.128] (n=10) | [-0.076, 0.142] (n=7) | [-0.252, 0.206] (n=7) |
| author=not_used, noauthor=not_used, title_only=does_not_join | deepseek-v4-pro | [-0.250, 0.831] (n=10) | [-0.190, 0.065] (n=10) | [-0.250, 0.242] (n=10) | [-0.466, 0.259] (n=10) |

## Stage-3 API-hosted unresolved share

| Switches | Overall | Cell min | Cell max | Still pending, approved journal |
|---|---|---|---|---|
| author=used, noauthor=used, title_only=joins | 0.006 | 0.000 | 0.055 | 0 |
| author=used, noauthor=used, title_only=does_not_join | 0.048 | 0.000 | 0.114 | 0 |
| author=used, noauthor=not_used, title_only=joins | 0.073 | 0.000 | 0.151 | 0 |
| author=used, noauthor=not_used, title_only=does_not_join | 0.115 | 0.000 | 0.226 | 0 |
| author=not_used, noauthor=used, title_only=joins | 0.022 | 0.000 | 0.103 | 0 |
| author=not_used, noauthor=used, title_only=does_not_join | 0.064 | 0.000 | 0.136 | 0 |
| author=not_used, noauthor=not_used, title_only=joins | 0.089 | 0.000 | 0.162 | 0 |
| author=not_used, noauthor=not_used, title_only=does_not_join | 0.131 | 0.011 | 0.226 | 0 |

Still pending under an approved journal name: citations the verifier sends to OpenAlex (a journal in its thin or low-coverage set, or a name variant of one) and that have no live answer. They stay unresolved, as amendment no. 5 keeps poorly indexed journal misses.

## Open-weight arm, descriptive (amendment no. 5): draft tolerance (stage 3 minus stage 2b)

| Switches | Doer | compliant_count | fabrication_rate | year_mismatch_rate | misplacement_rate |
|---|---|---|---|---|---|
| author=used, noauthor=used, title_only=joins | qwen3-14b | [0.000, 0.000] (n=10) | [-0.006, 0.010] (n=10) | [0.000, 0.000] (n=7) | [0.000, 0.000] (n=7) |
| author=used, noauthor=used, title_only=joins | qwen3-32b | [0.000, 0.000] (n=10) | [-0.020, 0.022] (n=10) | [-0.463, 0.000] (n=6) | [0.000, 0.463] (n=6) |
| author=used, noauthor=used, title_only=joins | qwen38-27b | [0.000, 0.000] (n=10) | [-0.067, 0.119] (n=10) | [0.000, 0.399] (n=10) | [-0.393, 0.000] (n=10) |
| author=used, noauthor=used, title_only=does_not_join | qwen3-14b | [0.000, 0.000] (n=10) | [-0.017, 0.005] (n=10) | [—, —] (n=0) | [—, —] (n=0) |
| author=used, noauthor=used, title_only=does_not_join | qwen3-32b | [0.000, 0.000] (n=10) | [-0.015, 0.007] (n=10) | [-0.988, -0.512] (n=2) | [0.512, 0.988] (n=2) |
| author=used, noauthor=used, title_only=does_not_join | qwen38-27b | [0.000, 0.000] (n=10) | [-0.007, 0.103] (n=10) | [-0.492, -0.175] (n=2) | [0.169, 0.248] (n=2) |
| author=used, noauthor=not_used, title_only=joins | qwen3-14b | [0.000, 0.000] (n=10) | [-0.007, 0.012] (n=10) | [0.000, 0.000] (n=7) | [0.000, 0.000] (n=7) |
| author=used, noauthor=not_used, title_only=joins | qwen3-32b | [0.000, 0.000] (n=10) | [-0.022, 0.026] (n=10) | [-0.463, 0.000] (n=6) | [0.000, 0.463] (n=6) |
| author=used, noauthor=not_used, title_only=joins | qwen38-27b | [0.000, 0.000] (n=10) | [-0.102, 0.125] (n=10) | [0.000, 0.399] (n=10) | [-0.393, 0.000] (n=10) |
| author=used, noauthor=not_used, title_only=does_not_join | qwen3-14b | [0.000, 0.000] (n=10) | [-0.019, 0.005] (n=10) | [—, —] (n=0) | [—, —] (n=0) |
| author=used, noauthor=not_used, title_only=does_not_join | qwen3-32b | [0.000, 0.000] (n=10) | [-0.020, 0.008] (n=10) | [-0.988, -0.512] (n=2) | [0.512, 0.988] (n=2) |
| author=used, noauthor=not_used, title_only=does_not_join | qwen38-27b | [0.000, 0.000] (n=10) | [-0.012, 0.105] (n=10) | [-0.492, -0.175] (n=2) | [0.169, 0.248] (n=2) |
| author=not_used, noauthor=used, title_only=joins | qwen3-14b | [0.000, 0.000] (n=10) | [-0.004, 0.015] (n=10) | [0.000, 0.000] (n=6) | [0.000, 0.000] (n=6) |
| author=not_used, noauthor=used, title_only=joins | qwen3-32b | [0.000, 0.000] (n=10) | [-0.026, 0.027] (n=10) | [-0.900, 0.000] (n=5) | [0.000, 0.900] (n=5) |
| author=not_used, noauthor=used, title_only=joins | qwen38-27b | [0.000, 0.000] (n=10) | [-0.067, 0.018] (n=10) | [-0.111, 0.097] (n=10) | [-0.097, 0.111] (n=10) |
| author=not_used, noauthor=used, title_only=does_not_join | qwen3-14b | [0.000, 0.000] (n=10) | [0.000, 0.003] (n=10) | [—, —] (n=0) | [—, —] (n=0) |
| author=not_used, noauthor=used, title_only=does_not_join | qwen3-32b | [0.000, 0.000] (n=10) | [-0.014, 0.000] (n=10) | [—, —] (n=0) | [—, —] (n=0) |
| author=not_used, noauthor=used, title_only=does_not_join | qwen38-27b | [0.000, 0.000] (n=10) | [-0.008, 0.002] (n=10) | [0.000, 0.000] (n=1) | [-0.500, -0.500] (n=1) |
| author=not_used, noauthor=not_used, title_only=joins | qwen3-14b | [0.000, 0.000] (n=10) | [-0.005, 0.016] (n=10) | [0.000, 0.000] (n=6) | [0.000, 0.000] (n=6) |
| author=not_used, noauthor=not_used, title_only=joins | qwen3-32b | [0.000, 0.000] (n=10) | [-0.028, 0.031] (n=10) | [-0.900, 0.000] (n=5) | [0.000, 0.900] (n=5) |
| author=not_used, noauthor=not_used, title_only=joins | qwen38-27b | [0.000, 0.000] (n=10) | [-0.102, 0.025] (n=10) | [-0.111, 0.097] (n=10) | [-0.097, 0.111] (n=10) |
| author=not_used, noauthor=not_used, title_only=does_not_join | qwen3-14b | [0.000, 0.000] (n=10) | [0.000, 0.003] (n=10) | [—, —] (n=0) | [—, —] (n=0) |
| author=not_used, noauthor=not_used, title_only=does_not_join | qwen3-32b | [0.000, 0.000] (n=10) | [-0.018, 0.000] (n=10) | [—, —] (n=0) | [—, —] (n=0) |
| author=not_used, noauthor=not_used, title_only=does_not_join | qwen38-27b | [0.000, 0.000] (n=10) | [-0.010, 0.002] (n=10) | [0.000, 0.000] (n=1) | [-0.500, -0.500] (n=1) |

## Open-weight arm, descriptive: review tolerance (stage-3 repeat minus stage 3, all review levels)

| Switches | Doer | compliant_count | fabrication_rate | year_mismatch_rate | misplacement_rate |
|---|---|---|---|---|---|
| author=used, noauthor=used, title_only=joins | qwen3-14b | [0.000, 0.000] (n=10) | [-0.001, 0.002] (n=10) | [0.000, 0.000] (n=6) | [0.000, 0.000] (n=6) |
| author=used, noauthor=used, title_only=joins | qwen3-32b | [0.000, 0.000] (n=10) | [-0.005, 0.001] (n=10) | [-0.057, 0.050] (n=7) | [-0.115, 0.000] (n=7) |
| author=used, noauthor=used, title_only=joins | qwen38-27b | [0.000, 0.000] (n=10) | [-0.056, 0.066] (n=10) | [-0.245, 0.209] (n=10) | [-0.116, 0.139] (n=10) |
| author=used, noauthor=used, title_only=does_not_join | qwen3-14b | [0.000, 0.000] (n=10) | [-0.001, 0.000] (n=10) | [0.000, 0.000] (n=1) | [0.000, 0.000] (n=1) |
| author=used, noauthor=used, title_only=does_not_join | qwen3-32b | [0.000, 0.000] (n=10) | [-0.005, 0.002] (n=10) | [-0.063, 0.000] (n=3) | [-0.127, 0.190] (n=3) |
| author=used, noauthor=used, title_only=does_not_join | qwen38-27b | [0.000, 0.000] (n=10) | [-0.028, 0.069] (n=10) | [-0.244, -0.006] (n=3) | [-0.237, 0.364] (n=3) |
| author=used, noauthor=not_used, title_only=joins | qwen3-14b | [0.000, 0.000] (n=10) | [-0.001, 0.003] (n=10) | [0.000, 0.000] (n=6) | [0.000, 0.000] (n=6) |
| author=used, noauthor=not_used, title_only=joins | qwen3-32b | [0.000, 0.000] (n=10) | [-0.006, 0.002] (n=10) | [-0.057, 0.050] (n=7) | [-0.115, 0.000] (n=7) |
| author=used, noauthor=not_used, title_only=joins | qwen38-27b | [0.000, 0.000] (n=10) | [-0.061, 0.065] (n=10) | [-0.245, 0.209] (n=10) | [-0.116, 0.139] (n=10) |
| author=used, noauthor=not_used, title_only=does_not_join | qwen3-14b | [0.000, 0.000] (n=10) | [-0.001, 0.000] (n=10) | [0.000, 0.000] (n=1) | [0.000, 0.000] (n=1) |
| author=used, noauthor=not_used, title_only=does_not_join | qwen3-32b | [0.000, 0.000] (n=10) | [-0.005, 0.003] (n=10) | [-0.063, 0.000] (n=3) | [-0.127, 0.190] (n=3) |
| author=used, noauthor=not_used, title_only=does_not_join | qwen38-27b | [0.000, 0.000] (n=10) | [-0.031, 0.068] (n=10) | [-0.244, -0.006] (n=3) | [-0.237, 0.364] (n=3) |
| author=not_used, noauthor=used, title_only=joins | qwen3-14b | [0.000, 0.000] (n=10) | [-0.000, 0.002] (n=10) | [0.000, 0.000] (n=5) | [0.000, 0.000] (n=5) |
| author=not_used, noauthor=used, title_only=joins | qwen3-32b | [0.000, 0.000] (n=10) | [-0.002, 0.001] (n=10) | [0.000, 0.043] (n=7) | [-0.170, 0.000] (n=7) |
| author=not_used, noauthor=used, title_only=joins | qwen38-27b | [0.000, 0.000] (n=10) | [-0.047, 0.066] (n=10) | [-0.244, 0.215] (n=10) | [-0.155, 0.131] (n=10) |
| author=not_used, noauthor=used, title_only=does_not_join | qwen3-14b | [0.000, 0.000] (n=10) | [0.000, 0.000] (n=10) | — | — |
| author=not_used, noauthor=used, title_only=does_not_join | qwen3-32b | [0.000, 0.000] (n=10) | [-0.001, 0.002] (n=10) | [0.000, 0.000] (n=2) | [-0.195, -0.005] (n=2) |
| author=not_used, noauthor=used, title_only=does_not_join | qwen38-27b | [0.000, 0.000] (n=10) | [-0.016, 0.069] (n=10) | [-0.119, 0.000] (n=3) | [-0.475, 0.095] (n=3) |
| author=not_used, noauthor=not_used, title_only=joins | qwen3-14b | [0.000, 0.000] (n=10) | [-0.000, 0.003] (n=10) | [0.000, 0.000] (n=5) | [0.000, 0.000] (n=5) |
| author=not_used, noauthor=not_used, title_only=joins | qwen3-32b | [0.000, 0.000] (n=10) | [-0.003, 0.002] (n=10) | [0.000, 0.043] (n=7) | [-0.170, 0.000] (n=7) |
| author=not_used, noauthor=not_used, title_only=joins | qwen38-27b | [0.000, 0.000] (n=10) | [-0.050, 0.065] (n=10) | [-0.244, 0.215] (n=10) | [-0.155, 0.131] (n=10) |
| author=not_used, noauthor=not_used, title_only=does_not_join | qwen3-14b | [0.000, 0.000] (n=10) | [0.000, 0.000] (n=10) | — | — |
| author=not_used, noauthor=not_used, title_only=does_not_join | qwen3-32b | [0.000, 0.000] (n=10) | [-0.001, 0.003] (n=10) | [0.000, 0.000] (n=2) | [-0.195, -0.005] (n=2) |
| author=not_used, noauthor=not_used, title_only=does_not_join | qwen38-27b | [0.000, 0.000] (n=10) | [-0.016, 0.069] (n=10) | [-0.119, 0.000] (n=3) | [-0.475, 0.095] (n=3) |
