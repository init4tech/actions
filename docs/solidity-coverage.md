# solidity-coverage.yml

## Base Usage

```yml
coverage:
  uses: init4tech/actions/.github/workflows/solidity-coverage.yml@main
```

## Description

This workflow checks code coverage for Solidity contracts using Foundry's coverage tools. It generates a coverage report and compares it against a committed `.coverage-report` file to ensure coverage doesn't regress.

The workflow:
- Generates a code coverage report using `forge coverage`
- Filters out test files, script files, and library files from the report
- Compares the generated report against the committed `.coverage-report` file
- Fails if there are differences, ensuring coverage is maintained

## Required Files

The repository must have a `.coverage-report` file committed that contains the expected coverage report. This file is used as a baseline for comparison.

## Environment Variables

The workflow uses `FOUNDRY_PROFILE: ci` for the coverage generation.

## Notes

- The workflow filters out coverage for test files (`test/`), script files (`script/`), and the `BytesLib` library
- Coverage is checked using the `--ir-minimum` flag for more accurate reporting
- The workflow will fail if the generated coverage differs from the committed `.coverage-report` file

