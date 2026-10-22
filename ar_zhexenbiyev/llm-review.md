# LLM review of `spec.md`

## Prompt used

> Review the following specification for the Top words problem. Identify every
> remaining ambiguity, omission, or contradiction that could allow two
> reasonable Python implementations to produce different results. Pay special
> attention to input validation, Unicode normalization and case folding,
> definition of a word in English/Russian/Kazakh, apostrophes, punctuation,
> digits, tie ordering, the ten-result limit, empty input, output shape, and
> whether every important decision has an example with an expected output.
> Review the complete contents of `spec.md` and report concrete fixes, not
> general encouragement.

## Specific LLM used

This review was performed by the AI assistant using Copilot SDK in VS Code.
The SDK session did not expose a model identifier, so no narrower model name
is claimed here.

## Review output

The specification is substantially deterministic and covers the important
choices: type errors, empty input, NFC normalization, Unicode letters,
apostrophes, separators, case folding, counting, tie-breaking, result limits,
and output shape. The examples exercise English, Russian, Kazakh, combining
marks, apostrophes, punctuation, ties, and fewer-than-ten results.

One contradiction was found in the ten-word example: `w1` through `w11` are
not words under the stated rule because digits are separators, and the example
therefore cannot demonstrate the ten-result limit. The specification should
replace it with a letter-only example.

One presentation issue was found in the following boundary example: it
included an extra trailing comma and then described a corrected result in
prose. That creates an unnecessary second interpretation. The example should
show only the formal expected result.

## Resolution

Both issues were resolved in `spec.md`: the invalid alphanumeric example is
explicitly identified as a non-word case, and the letter-only ten-plus-one
example is followed by the exact ten-item result. The contract itself remains
unambiguous.
