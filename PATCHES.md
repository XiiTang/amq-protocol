# Runtime bounds

Base: amq-protocol v10.6.3, 68e9b68b68edbfb79bbcbffa99d4499ee1ae51ab.

- Bound recursive field tables/arrays to 16 containers inside the existing nom parsers. The synchronous, thread-local RAII guard is restored on success and failure. No parallel parser or transport implementation is introduced.
- Zero LongString storage on drop, including SASL response/challenge values. Frame buffers are separately cleared by the embedding lapin patch.

Validation: 60 amq-protocol-types unit tests and its integration test passed, including excessive mixed-container nesting and parsing again after rejection.
