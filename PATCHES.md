# Runtime bounds

Base: amq-protocol v10.6.3, 68e9b68b68edbfb79bbcbffa99d4499ee1ae51ab.

- Bound recursive field tables/arrays to 16 containers inside the existing nom parsers. The synchronous, thread-local RAII guard is restored on success and failure. No parallel parser or transport implementation is introduced.
- Zero LongString storage on drop, including SASL response/challenge values. Frame buffers are separately cleared by the embedding lapin patch.

Validation: 60 amq-protocol-types unit tests and its integration test passed, including excessive mixed-container nesting and parsing again after rejection.

## Fixed locked certificate verification (#312)

Update rustls-webpki 0.103.13 to 0.103.16 and webpki-root-certs 1.0.9 to
1.0.10 for RUSTSEC-2026-0382 and RUSTSEC-2026-0383. webpki now requires
aws-lc-rs 1.18; use its minimum 1.18.0 and aws-lc-sys 0.44.0. No protocol,
codec or public API code changes. Regression coverage: `cargo test
--workspace --locked` and Boundless's complete AMQP library tests.
