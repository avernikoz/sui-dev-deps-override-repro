# Sui `[dev-dependencies]` Build Bug Reproduction

This repository demonstrates a bug in `sui move build` where the command fails to compile a package if the `[dev-dependencies]` section is used.
This repository was created to support [Sui GitHub Issue #23173](https://github.com/MystenLabs/sui/issues/23173).

## The Bug

A standard `sui move build` (without the `--dev` flag) should ignore the `[dev-dependencies]` section. However, its presence currently causes the build to fail with address and module resolution errors, even when the project's configuration is otherwise valid.

## How to Reproduce

The repository is pre-configured in the failing state.

### 1. Run the Build (Fails)

From the `main_package` directory, run the build command.

```bash
sui move build
```

The command will fail with compilation errors related to an address with no value.

### 2. Apply the Workaround (Succeeds)

To prove the project is otherwise configured correctly, you can temporarily disable the problematic section.

1.  Open `main_package/Move.toml`.
2.  Comment out the `Pyth` and `deepbook` lines inside the `[dev-dependencies]` section.

Run the build command again:

```bash
sui move build
```

The build will now succeed, demonstrating that the failure is caused only by the presence of the `[dev-dependencies]` section in a standard build.

