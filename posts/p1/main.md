# Add a New RISC-V `Nop` Instruction in LLVM

check full diff at

https://github.com/produktivkraft/llvm-project/compare/xyz.nop.base...produktivkraft:llvm-project:xyz.nop

## notes

- add `xyz.nop` assembly instr
  modify `llvm/lib/Target/RISCV/`
  modify `llvm/lib/Target/RISCV/Disassembler/`

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

TODO: add ref

<!-- links -->

[llvm_Dialect]: https://mlir.llvm.org/docs/Dialects/LLVM/
