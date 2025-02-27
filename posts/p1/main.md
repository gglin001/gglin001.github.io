# Add a New RISC-V Nop Instruction in LLVM

check full diff at

[github.com/produktivkraft/llvm-project][diff]

## notes

- add `xyz.nop` assembly instr

modify

```
llvm/lib/Target/RISCV/
llvm/lib/Target/RISCV/Disassembler/
```

- add `llvm.riscv.xyz.nop` llvm ir

- add clang builtin function `__builtin_riscv_xyz_nop()`

- In [llvm Dialect][llvm_Dialect], you can use `llvm.inline_asm` and `llvm.call_intrinsic`

eg:

```mlir
  // inline_asm
  llvm.inline_asm "xyz.nop", "" : () -> ()
  // call_intrinsic
  llvm.call_intrinsic "llvm.riscv.xyz.nop" () : () -> () {}
```

## refernce

- https://arxiv.org/abs/2310.18353
  Supporting Custom Instructions with the LLVM Compiler for RISC-V Processor

- https://sites.google.com/view/isca-2024-tutorial-riscv-instr/home
  Tutorial: Expedited Development of Novel RISC-V Instructions Through an Emulation-Simulation Framework(Co-located with ISCA 2024)

---

<!-- links -->

[diff]: https://github.com/produktivkraft/llvm-project/compare/xyz.nop.base...produktivkraft:llvm-project:xyz.nop
[llvm_Dialect]: https://mlir.llvm.org/docs/Dialects/LLVM/
