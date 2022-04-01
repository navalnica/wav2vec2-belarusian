# stt_be
Speech to Text model for Belarusian language.

Training on Common Voice 8 dataset.

## Metrics

Current metrics for Common Voice 8:
|model|WER on Dev set|WER on Test set|Rate of fully recognized sentences on Test set|
|-|-|-|-|
|Acoustic model only|0.1761|0.187|36.688%|
|Acoustic model + 5-gram Language model|0.115|0.124|52.269%|
