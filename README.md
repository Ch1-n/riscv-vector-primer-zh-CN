# RISC-V Vector Primer 中文译本

**[开始阅读中文译本](zh-CN/README.md)** · [术语表](zh-CN/GLOSSARY.md) · [翻译与授权说明](zh-CN/TRANSLATION-NOTICE.md)

本仓库由 Ch'in 维护，收录经原作者邮件许可、用于非商业技术教育的非官方简体中文译本。原作者未审校中文译文，授权不代表对译文的背书。

原作作者为 **Thang Minh Tran、Paul Miller**，编辑为 **Jonah McLeod**，出版方为 **Simplex Micro**。译文基于[英文原仓库](https://github.com/simplex-micro/riscv-vector-primer)的 `fc66957a6458842beeabe9d85065ff334ccbd333`（2026-07-25）。保留原作 [CC BY-NC-ND 4.0 许可证](LICENSE)，翻译发布依据另行取得的邮件许可。

> **支持原作，向作者反馈**：原作者特别希望读者访问 [Simplex Micro 官网](https://www.simplexmicro.com)，并通过官网提供的联系渠道分享阅读反馈。欢迎用简短英文说明哪些章节对你有帮助、哪些概念还不够清楚，或希望增加哪些实例。中文翻译的措辞、错字及译注问题，请在本仓库提交 [Issue](https://github.com/Ch1-n/riscv-vector-primer-zh-CN/issues)，由译者跟进。

## 中文目录

- [第一章](zh-CN/chapter-01.md)
- [第二章](zh-CN/chapter-02.md)
- [第三章](zh-CN/chapter-03.md)
- [第四章](zh-CN/chapter-04.md)
- [第五章](zh-CN/chapter-05.md)
- [第六章](zh-CN/chapter-06.md)

以下保留英文原作 README，便于对照与引用。

---

# 📘 RISC-V Vector Primer

An implementation-focused guide to the RISC-V Vector Extension (RVV 1.0) and the emerging Matrix Extension — written for architects, compiler engineers, and embedded/edge AI developers.

➡️ **Read the chapters:** Browse the chapter files below or [start with Chapter 1](chapter-01.md)
⭐ **Star the repo if you’d like to follow updates**

---

Published by **Simplex Micro**

Welcome to the online edition of the **RISC-V Vector Primer**, a comprehensive guide to understanding, implementing, and applying the RISC-V Vector Extension (RVV). This site hosts the full book in chapter-based form, published openly for engineers, architects, students, and practitioners who want a clear and practical understanding of modern vector computation.

The primer explains RVV from first principles through real hardware design, performance analysis, and the architectural path toward matrix acceleration. It is grounded in decades of industry experience and written to be both accessible and technically rigorous.

---

## **Authors**

### **Dr. Thang Tran — Founder, CEO & CTO**
A microprocessor architect with over 40 years of experience across x86, Arm, PowerPC, ARC, and RISC‑V. Dr. Tran led the design of the AndesCore NX27V—the first commercial RISC‑V vector processor—and has held senior roles at AMD, Texas Instruments, Andes Technology, and Condor Computing.

### **Paul Miller — Senior Fellow of Architecture and Design**
A senior microprocessor designer with 35+ years of experience in RISC, x86, ARM, DSP, and GPU architectures. Paul has designed floating‑point units, SIMD engines, and AI accelerators, and now contributes to Simplex Micro’s RISC‑V Vector and Matrix processor development.

### **Jonah McLeod — Editor**
An award‑winning editor with 30+ years of Silicon Valley experience. Jonah has led major high‑tech publications and held senior communications roles at Virage Logic, Denali Software, Kilopass Technology, and Andes Technology.

---

## How to Cite This Book

If you reference this work in academic papers, technical articles, presentations, or documentation, please cite it as follows.

**Preferred citation (long form):**

Tran, Thang Minh; Miller, Paul; McLeod, Jonah.  
*RISC-V Vector Primer: An Implementation-Focused Guide to the RISC-V Vector Extension*.  
Simplex Micro, 2025.  
Available at: https://github.com/simplex-micro/riscv-vector-primer

**Short citation:**

T. M. Tran, P. Miller, and J. McLeod, *RISC-V Vector Primer*, Simplex Micro, 2025.

When citing a specific chapter, please include the chapter title and, if applicable, the version or commit date.

**BibTeX:**

```bibtex
@book{TranRiscVVectorPrimer2025,
  title        = {RISC-V Vector Primer: An Implementation-Focused Guide to the RISC-V Vector Extension},
  author       = {Tran, Thang Minh and Miller, Paul and McLeod, Jonah},
  year         = {2025},
  publisher    = {Simplex Micro},
  url          = https://github.com/simplex-micro/riscv-vector-primer
  note         = {Online edition}
}
---
```
## **Chapters**

- **Chapter 1 — RISC‑V Vector Extension Demystified**  
  A conceptual foundation: vector vs SIMD, time–space duality, chaining, strip mining, and the mental models needed to understand RVV.

- **Chapter 2 — From Concept to Core: A RISC‑V Vector Processor in Silicon**  
  How RVV maps into real hardware: lanes, VRF design, port pressure, micro‑ops, and a concrete 512‑bit implementation.

- **Chapter 3 — RISC‑V Vector Extension Fundamentals**  
  SEW, LMUL, VLEN, VLMAX, masking, vtype, vsetvl, register grouping, functional units, memory behavior, and CSR semantics.

- **Chapter 4 — Vector Instructions**  
  Memory operations, compute operations, widening/narrowing, fixed‑point and floating‑point arithmetic, reductions, masks, permutations, and register movement.

- **Chapter 5 — Matrix Computation and Performance Analysis**  
  Single‑precision GEMM, low‑precision MAC pipelines, chaining, memory bandwidth, tiling, and deterministic execution for AI workloads.

- **Chapter 6 — From Vectors to Matrices**  
  Why matrix workloads expose structural limits of 1‑D vectors, the architectural rationale for matrix tiles, PE arrays, tile geometry, and the emerging RISC‑V Matrix Extension.

---

## **About This Publication**

This primer is published by **Simplex Micro** as part of its mission to advance open, accessible technical education in RISC‑V vector and matrix processing. The content is released incrementally and updated as the book evolves.

**Source repository:**  
https://github.com/simplex-micro/riscv-vector-primer
---

## **License**

This work is licensed under the Creative Commons
Attribution-NonCommercial-NoDerivatives 4.0 International License (CC BY-NC-ND 4.0).
See the LICENSE file for details.
