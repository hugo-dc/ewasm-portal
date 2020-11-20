---
layout: page
published: true
title: 'Projects'
date: '2020-11-18'
author: Ewasm Team
category: Main
toc: true
---

Below you may find a list of projects by the team.

## Ewasm 1.0

Ewasm 1.0 is an umbrella term for a collection of projects with the goal of bringing Wasm to the Eth1 mainnet. You may find the specs in the [design repo](https://github.com/ewasm/design).

* **[Hera (C++)](https://github.com/ewasm/hera) and [Hera.rs (Rust)](https://github.com/ewasm/hera.rs)**: The ewasm 1.0 virtual machine which
can be integrated in existing Ethereum client compatible with [EVMC](https://github.com/ethereum/evmc). Hera has support to different WebAssembly interpreters and compilers such as [Wabt](https://github.com/webassembly/wabt), [Binaryen](https://github.com/webassembly/binaryen), and [WAVM](https://github.com/WAVM/WAVM).
* [Ewasm Precompiles](https://github.com/ewasm/ewasm-precompiles): Wasm implementation of the Eth1 precompiled contracts
* [Sentinel Contract](https://github.com/ewasm/sentinel-rs): A system contract that validates and injects gas metering to contracts at deploy time. Written in Rust and targetting Wasm.
* [Ewasm Tests](https://github.com/ewasm/tests/tree/wasm-tests/src/GeneralStateTestsFiller/stEWASMTests): A suite of state tests for Wasm bytecodes adhereing to the [Ewasm interface](https://github.com/ewasm/design/blob/master/eth_interface.md), runnable by Ewasm-compatible clients.
* [Block Explorer (Etherchain Light](https://github.com/ewasm/etherchain-light): Fork of [Etherchain Light](https://github.com/gobitfly/etherchain-light) for visualizing blocks in the Ewasm testnet

### Ewasm API

The Ewasm API is an [interface](https://github.com/ewasm/design/blob/master/eth_interface.md) exposed to contracts written in Wasm to access Ethereum environment data. Clients integrating Ewasm must implement these functions to be compliant.

* [Rust Ewasm API](https://github.com/ewasm/ewasm-rust-api): Rust library which defines an Ewasm API that allows accessing Ewasm functions from contracts written in Rust.
* [Assemblyscript Ewasm API](https://github.com/ewasm/assemblyscript-ewasm-api): Ewasm API for AssemblyScript

### EVM to Ewasm

Ewasm could be introduced to Eth1 either as a replacement to EVM or as a second VM. Either way, these tools help reduce the burden on clients by enabling them to run EVM contracts through their Wasm engine so they don't have to maintain 2 VMs.

* [Runevm](https://github.com/axic/runevm): A Wasm contract that embeds an EVM [interpreter](https://github.com/paritytech/parity-ethereum/). It allows clients with only Wasm support to execute EVM bytecode.
* [Evm2wasm](https://github.com/ewasm/evm2wasm): Transcompiles EVM code to Ewasm
* [YEVM](https://github.com/axic/yevm): "Why EVM?" is an EVM compiler infrastructure, targetting Ewasm by utilising [Yul](https://solidity.readthedocs.io/en/develop/yul.html) as an intermediate step.

### Testnet

All these projects allowed to run an Ethereum 1.0 Testnet with Ewasm Support. This means you could create contracts in a language targetting EVM (i.e. Solidity), or you could write contracts using a language targetting WebAssembly (Rust, C, AssemblyScript, etc), and live in the same testnet. The testnet is not being actively maintained anymore. However you can play with a Ewasm 1.0 Testnet in a local environment using this [repository](https://github.com/jwasinger/ewasm-dev-env).

### Client integration

This section gives an overview of the efforts around integrating Ewasm into clients.

* **Geth+Wagon**: Integrating Wagon into Geth as Ewasm Engine.
* **Geth+Hera**: Integration of Hera in a fork of Geth.
* **PyEVM Integration**: Lane and Paul worked with the PyEVM team in order to integrate Ewasm
* [EthereumJS-VM integration](https://github.com/ethereumjs/ethereumjs-vm/pull/474)

### Wasm utilities

Some utilities developed for internal usage specific to Ewasm were extracted and published to benefit the wider Wasm ecosystem:

* [Wasm Chisel](https://github.com/wasmx/wasm-chisel): Some useful utilities to transform WebAssembly binaries, with feasures such as: `remapimports`, `trimexports`, `snip`, `deployer`, etc.
* [qimalloc](https://github.com/wasmx/qimalloc): Quick Incremental (Wasteful) Memory Allocator. This memory allocator will not release any memory. Its main use case is in short-lived environment, such as WebAssembly binaries.
* [Wasm Profiler](https://github.com/wasmx/wasm-profiler): Utilities for profiling WebAssembly binaries

### Metering

EVM comes with gas metering out-of-the-box to put a cap on the resources a node is expected to spend on a transaction. Wasm has no such notion by default. [Wasm-metering](https://github.com/ewasm/wasm-metering) was the first attempt at introducing metering to Wasm. Since then various alternatives have been explored and compared, including:

- Upperbound
- Symbolic metering
- Metering Injection
- Atomic Metering
    - Bounded Loop Finder?
    - Taint Analysis
- Wasm BluePrint
- Metering by counting cycles in [Boom](https://github.com/riscv-boom/riscv-boom)
  - https://github.com/poemm/assembles

To learn more about the design considerations for metering see [here](https://github.com/ewasm/design/blob/master/metering.md).

## EVM

- [evmone](https://github.com/ethereum/evmone): Fast Ethereum Virtual Machine implementation
- [EVMC](https://github.com/ethereum/EVMC): Ethereum Client-VM Connector API
  - evmc-geth integration
  - evmc-aleth integration
- [EVM384](https://notes.ethereum.org/@axic/evm384): An extension to the EVM which we hope will allow the implementation of fast BLS12-381 and potentially other cryptographic operations in EVM
  - [Discussion](https://ethereum-magicians.org/t/evm384-feedback-and-discussion/4533)
  - [EVMCurves](https://github.com/poemm/EVMcurves): An experiment to implement the BLS12-381 pairing operation in EVM with the proposed EVM384 extension
- [Daytona](https://github.com/axic/daytona): An EVMC compatible Ethereum VM kit. It aims to support a variety of VM implementations written in Rust, such as Parity's, CitaVM, SputnikVM, SputnikVM (fork), evm-rs (discontinued), evm-rs (fork) and rust-evm.

## Eth1x

- **Witness format**: Collaboration with other Eth1x teams with the goal of producing a well-specced witness format:
  - Formalization Review by Paul
  - Witness spec
  - Witness tests/Test Generation [Tool](https://github.com/poemm/eth_witness_experiments)
  - [multiproof-rs](https://github.com/gballet/multiproof-rs): A Rust implementation of Alexey Akhunov's multiproof algorithm
- **EVM Code Merkleization**: Experiments with the goal of reducing stateless block witness sizes by splitting contracts into chunks and merkleizing those chunks. These experiments have produced the following:
  - [EIP-2926](https://eips.ethereum.org/EIPS/eip-2926): Chunk-Based Code Merkleization
  - [JS implementation](https://github.com/ewasm/biturbo/pull/64)
  - [Python implementation](https://github.com/hugo-dc/code-chunks/)
  - [Geth integration](https://github.com/s1na/go-ethereum/tree/code-merkleization)
- **EVM Bytecode compression**: Experiments around compressing EVM bytecode
- **Light client sync**: An effort to improve the block header sync for light clients by employing techniques like FlyClient:
  - [Survey of existing work](https://ethresear.ch/t/state-of-block-header-sync-in-light-clients/8047)

## Eth 2.0

- [Deposit contract](https://github.com/axic/eth2-deposit-contract): A port of the Vyper Eth 2.0 deposit contract to Solidity which was deployed to [mainnet](https://etherscan.io/address/0x00000000219ab540356cbb839cbe05303d7705fa).
- **Eth1x64**: Exploration the idea of "putting eth1 on each shard" on Eth 2.0, with the goal of designing a cross-shard protocol between "Eth1 shards" with least invasive means to the EVM:
  - [The Eth1x64 experiment](https://ethresear.ch/t/the-eth1x64-experiment/7195)
  - [Eth1x64 Variant 1 "Apostille"](https://ethresear.ch/t/eth1x64-variant-1-apostille/7365)

### Phase 2

Phase 2 brings execution to the data shards introduced in phase 1. We explored various designs for state execution on the shards, communication between the shards, etc. A notable project is [Scout](https://github.com/ewasm/scout) which facilitated prototyping and testing Wasm-based Execution Environments (EEs). Scout was first implemented in Rust and later ported to various other languages such as [C++](https://github.com/poemm/scout_wabt.cpp) and [Typescript](https://github.com/ewasm/scout.ts).

#### Execution Environments (EEs)

Scout enabled us and other researchers to rapidly prototype and assess the feasiblity of various EEs:

- [Stateless KMM Token](https://github.com/poemm/stateless_kmm_token): Stateless merkle token with optimal witnesses in Wasm
- [Groth16 verifier](https://github.com/jwasinger/groth16-verify-wasm): Groth16 proof verifier written in Webassembly
- [Daiquiri](https://github.com/jwasinger/daiquiri): Eth2 Coin Mixer EE
- [Biturbo](https://github.com/ewasm/biturbo): Eth1 EE using Turboproofs
- [MiMC Merkle Tree](https://github.com/jwasinger/mimc-merkle-proof): Binary merkle tree using MiMC hash function, implemented in Assemblyscript
- [MiMC Wasm](https://github.com/jwasinger/mimc-wasm): Implementation of ZKSNARK-friendly MiMC-Feistel hash function in Assemblyscript
- [turbo-mpas](https://github.com/cdetrio/scout.ts/tree/turbo-mpas): Assemblyscript code to verify a Merkle branch
- [SMPT](https://github.com/ewasm/scout/pull/11): Stateless MPT token EE using Parity Ethereum's MPT Rust implementation
- [STARK Verifier](https://github.com/ewasm/scout/pull/22): STARK verification of a number of MIMC rounds expressed inside an EE
- [SMT](https://github.com/s1na/smt): Sparse merkle tree implementation in Typescript

## Wasm Interpreters

* [Fizzy](https://github.com/wasmx/fizzy): Fizzy aims to be a fast, deterministic, and pedantic WebAssembly interpreter written in C++
* [PyWebAssembly](https://github.com/poemm/pywebassembly): Implementation of the WebAssembly spec in Python
* **CppWebAssembly**: C++ implementation of the WebAssembly spec

## Misc

**Ewasm/Truffle Integration**: `<insert description>`

**Hera fuzzer**: `<insert description>`

**TurboEwasm/EwasmOS?**:  `<insert description>`

> Guillaume and Paul worked on this

**WebAssembly Blockchains Survey**: `<insert description>`

> I think it was an internal survey?, just in case we want to mention it

**Coda challenge/Wasmsnark?**: `<insert description>`

**Wag**: `<insert description>`

**WebAssembly Engines Benchmarking**: `<insert description>`

### 2020 - Benchmarks, Eth2Phase2 Execution Prototyping, Cross-shard, Metering, Eth1x, Eth1x64, EVM384

**Benchmark Report**:

- Added more engines: wasm3, wamr, fizzy, wamr-jit, wamr-aot, ssvm, asmble, eosvm
- Upgraded Docker images
- Included scout benchmarks

**Cross-shard research**:

- https://notes.ethereum.org/OS-kqaD3S-aGm6IEHTcfLQ
- Balance netting https://notes.ethereum.org/fkPBDSV_QiSePrrk5u-0Qg
- Atomic cross-shard via Lamport timestamps https://notes.ethereum.org/lOGzEL0YSD6R9F_IkZMsrQ
- Cross shard transfer https://notes.ethereum.org/Sd3pOEwrQSaYeXHdAmIEvw?view
- Minimal cross-shard communication
- Shard-aware host unctions
