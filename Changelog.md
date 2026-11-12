# Changelog

## Bug fixes

- **DZ blocks:** Validate compressed lengths against the platform size and declared block length, detect length overflow, and limit decompression to the declared output size. Correct inverse transposition for data whose final row is incomplete.
- **Range readers:** Check range-end arithmetic for overflow and convert requested lengths to `usize` safely in both file-backed and buffered readers.
- **Channel decoding:** Reject invalid integer widths, float widths, and bit offsets instead of risking invalid shifts. Use a wider intermediate when decoding unaligned 64-bit integers, apply bit offsets when decoding floats, and check byte-range arithmetic.
- **Streaming index construction:** Detect cycles in data-group, channel-group, channel, data-block, and fragment chains. Report unexpected data block types and unsupported nested conversions instead of silently stopping or skipping them.
- **Indexed channel reads:** Reject record-ID groups that the reader cannot correctly distinguish, validate record sizes and data-block ranges, and preserve records that span adjacent data blocks.

Regression tests cover malformed DZ lengths, bounded decompression, partial-row transposition, unaligned numeric decoding, cyclic data lists, range overflow, unsupported record IDs, and records split across blocks.
