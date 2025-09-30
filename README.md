# Init4 Github Actions README

## Repo Overview

```bash
| .github/
| | .workflows/ # the directory which holds all workflow files
| docs/
| | workflow-docs/ # each workflow must have its own documentation in here
| examples/ # each workflow must contain a fully complete example of usage here

```

## Init4 Github Actions Developer Getting Started Guide

This repository gives developers standard and secure building blocks to bootstrap CI in their repositories quickly and with minimal action configuration.

### Quickstart:

Simply download the quickstart workflow that matches your project type into the `.github/workflows/` directory in your repository:

For a rust binary:

```
$ curl -o .github/workflows/rust-bin.yml https://raw.githubusercontent.com/init4tech/actions/refs/heads/main/quickstart/rust-bin.yml
```

For a rust library:

```
$ curl -o .github/workflows/rust-lib.yml https://raw.githubusercontent.com/init4tech/actions/refs/heads/main/quickstart/rust-lib.yml
```

For a solidity project:

```
$ curl -o .github/workflows/solidity.yml https://raw.githubusercontent.com/init4tech/actions/refs/heads/main/quickstart/solidity.yml
```

### Workflows Overview

In Github Actions everything is built around workflows. When you configure a `workflow.yml` file in your repo you normally need to have many steps and need to know all the different CI actions you want. Annoyingly, this has to be done every time you set up a repo, and commonly results in lots of copy and pasting code all around. While manageable, it creates a lot of what I call "complexity creep" where CI steps get added and shared around without much intent. This creates CI bloat and can be a big time waster.

To fix this issue here at Init4 we can leverage the shared workflows contained in this repository, and creating your new repository with a robust CI workflow with as few as 10 lines of yaml. Each of the supplied workflows are designed to be as lightweight as possible without sacrificing baseline security. Workflows also have optional parameters that may be provided to give individual repositories further ability to configure the steps they need with simple booleans. Each workflow must also contain a `docs/<workflow_name>.md` file with all optional parameters documented.

### Repo Setup Steps

1. Create your new repository and add any code you have to get it structured how you'd like.
2. Create the directories `.github/workflows` at the root of your repository
3. Add a CODEOWNERS file at `.github/CODEOWNERS`
4. Create your CI workflow using one of our `*-base.yml` workflows to start

   `solidity-base.yml` example (see `examples` folder for others)

   ```yml
   name: CI
   # executes automatically on pull requests and pushes to main
   on:
     pull_request:
     push:
       branches:
         - main
     workflow_dispatch:

   # the only configuration needed for the solidity-base workflow
   jobs:
     solidity-base:
       uses: init4tech/actions/.github/workflows/solidity-base.yml@main
   ```

5. You now have a fully initialized repository, go code!

## Modifying an existing workflow

### Adding an optional external dependency

1. Find the workflow to modify in the directory `.github/workflows/`
2. Add a new `input:` parameter of type `boolean` to the workflow with the default set to `false`
3. Add a new step and include an `if:` block to check your new input parameter and optionally install your dependency

   - for an example, see the "Optional Foundry install Step" below:

   ```yml
         steps:
       - name: Checkout repository
         uses: actions/checkout@v3
       - name: Install Rust toolchain
         uses: dtolnay/rust-toolchain@stable
       - uses: Swatinem/rust-cache@v2
       - name: Optional Foundry Install
         if: ${{ github.event.inputs.install-foundry == 'true' }}
         uses: foundry-rs/foundry-toolchain@v1
         with:
           version: nightly
       - name: Run tests
         run: |
           cargo test --all-features --workspace
   ```
