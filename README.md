# Wortels

This is the design repo for Wortels - a novel design for a stateless WebAssembly-based consensus computer.

It is intended to build on learnings from Ethereum, an existing blockchain computer.

The goals are:
- To operate as a pegged chain, sidechain or independent chain
- Stateless chain
- No native token (aka "account abstraction")
- WebAssembly as an execution engine (this should focus on linking code)
- Not to focus on compatibility with Ethereum's EVM

The basic data structure for the tree is [explained here](./tree.md).

## Authors

Jake Lang, Martin Becze, Alex Beregszaszi
