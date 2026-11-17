# Metadata CSV schema

Required columns: `sample_id`, `district_id`, `image_path`, `label`, `split`, plus numeric environmental features.

Example placeholders in config:
- `sat_1`, `sat_2`: replace with actual verified satellite features.
- `clim_1`, `clim_2`: replace with actual verified climate variables.

`label` is an integer class index. `split` is train, val, or test. `sample_id` must be unique. This code requires complete numeric environmental feature values; it does not implement the manuscript's unknown missing-value policy or standardization. Implement preprocessing using training-subset statistics only and apply those unchanged to validation/test.
