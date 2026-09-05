# RISC-V 向量入门

这是一份侧重工程实现的入门指南，系统介绍 RISC-V 向量扩展（RVV 1.0），并讨论仍在演进中的 RISC-V 矩阵扩展。适合处理器架构师、编译器工程师，以及从事嵌入式和边缘 AI 开发的读者。

> **经原作者邮件许可翻译，用于非商业技术教育。** 中文翻译：Ch'in。本译稿为非官方版本，未经原作者中文审校；授权摘要见[翻译说明](TRANSLATION-NOTICE.md)。

翻译术语见[术语表](GLOSSARY.md)，本轮技术纠正与审校范围见[修订记录](REVISION-NOTES.md)；平台署名与发布流程见[发布准备说明](PUBLISHING-GUIDE.md)。

> **支持原作：访问官网，把反馈带给作者。**
>
> 作者在授权交流中特别希望中文读者访问 [Simplex Micro 官网](https://www.simplexmicro.com)，并分享阅读感受或改进建议。如果这本教程对你有帮助，欢迎告诉作者：哪一章最有启发、还有哪些概念不够清楚、希望补充哪些算例。建议使用简短英文，并注明来自本书中文译本。

中文翻译的用词、错漏和排版问题，请在中文译稿仓库或译文评论区提出，由译者跟进。对原书内容的反馈与对译文的勘误，请尽量区分。

**阅读正文：**可以浏览下列章节，也可以从[第 1 章](chapter-01.md)开始顺序阅读。  
如需关注英文原作的后续更新，请收藏或关注[原仓库](https://github.com/simplex-micro/riscv-vector-primer)。

## 目录结构

- `chapter-01.md` 至 `chapter-06.md`：中文正文，本地图片统一引用 `images/`。
- `images/`：中文正文使用的全部图片。
- `zhihu/`：知乎导入版本，图片使用英文原仓库的公网地址，并移除了本地文档链接。
- `GLOSSARY.md`：中英文术语表。
- `REVISION-NOTES.md`：审校范围、重要技术纠正及规范依据。
- `TRANSLATION-NOTICE.md`：翻译与授权说明。
- `PUBLISHING-GUIDE.md`：发布和署名规范。

---

英文原作由 **Simplex Micro** 发布。

这是 *RISC-V Vector Primer* 的非官方简体中文译稿。原书以分章形式系统介绍 RISC-V 向量扩展（RVV），面向希望从工程角度理解现代向量计算的架构师、工程师、学生和相关从业者。

全书从基本概念出发，逐步深入到实际硬件设计、性能分析，以及从向量计算走向矩阵加速的架构思路。内容建立在作者团队数十年的产业经验之上，力求兼顾可读性与技术严谨性。

---

## 作者

### Thang Tran 博士：创始人、CEO 兼 CTO

微处理器架构师，在 x86、Arm、PowerPC、ARC 和 RISC-V 领域拥有 40 余年经验。Tran 博士曾领导 AndesCore NX27V 的设计，该产品是首款商用 RISC-V 向量处理器；他还曾在 AMD、Texas Instruments、Andes Technology 和 Condor Computing 担任高级职位。

### Paul Miller：架构与设计高级研究员

资深微处理器设计师，在 RISC、x86、Arm、DSP 和 GPU 架构方面拥有 35 年以上经验。Paul 设计过浮点单元、SIMD 引擎和 AI 加速器，目前参与 Simplex Micro 的 RISC-V 向量与矩阵处理器研发。

### Jonah McLeod：编辑

获奖编辑，在硅谷拥有 30 余年从业经验。Jonah 曾领导多家重要高科技出版物，并在 Virage Logic、Denali Software、Kilopass Technology 和 Andes Technology 担任高级传播职位。

---

## 如何引用原书

在论文、技术文章、演示文稿或文档中引用本书时，请引用英文原作，而不是把中文译稿列为原始来源。

**推荐的完整引用格式：**

Tran, Thang Minh; Miller, Paul; McLeod, Jonah.  
*RISC-V Vector Primer: An Implementation-Focused Guide to the RISC-V Vector Extension*.  
Simplex Micro, 2025.  
Available at: https://github.com/simplex-micro/riscv-vector-primer

**简短引用格式：**

T. M. Tran, P. Miller, and J. McLeod, *RISC-V Vector Primer*, Simplex Micro, 2025.

引用特定章节时，应补充章节标题，并在必要时注明版本或提交日期。

**BibTeX：**

```bibtex
@book{TranRiscVVectorPrimer2025,
  title        = {RISC-V Vector Primer: An Implementation-Focused Guide to the RISC-V Vector Extension},
  author       = {Tran, Thang Minh and Miller, Paul and McLeod, Jonah},
  year         = {2025},
  publisher    = {Simplex Micro},
  url          = {https://github.com/simplex-micro/riscv-vector-primer},
  note         = {Online edition}
}
```

## 章节

- **[第 1 章：揭开 RISC-V 向量扩展的面纱](chapter-01.md)**  
  建立概念基础：向量与 SIMD、时间-空间对偶、链式执行、分段处理，以及理解 RVV 所需的思维模型。

- **[第 2 章：从概念到芯片：RISC-V 向量处理器的实现](chapter-02.md)**  
  介绍 RVV 如何映射到真实硬件：通道、VRF 设计、端口压力、微操作，以及一个具体的 512 位实现。

- **[第 3 章：RISC-V 向量扩展基础](chapter-03.md)**  
  介绍 SEW、LMUL、VLEN、VLMAX、掩码、`vtype`、`vsetvl`、寄存器分组、功能单元、访存行为和 CSR 语义。

- **[第 4 章：向量指令](chapter-04.md)**  
  介绍访存、计算、加宽/窄化、定点与浮点运算、归约、掩码、置换和寄存器移动指令。

- **[第 5 章：RISC-V 向量扩展中的矩阵计算与性能分析](chapter-05.md)**  
  介绍单精度 GEMM、低精度 MAC 流水线、链式执行、存储带宽、分块，以及 AI 工作负载的确定性执行。

- **[第 6 章：从向量到矩阵：RISC-V 矩阵扩展的架构思路](chapter-06.md)**  
  说明矩阵工作负载为何会暴露一维向量表达的额外开销，并讨论矩阵块、PE 阵列、数据驻留，以及仍在演进的 RISC-V 矩阵扩展背后的架构动机。

---

## 关于英文原作

Simplex Micro 发布本书，旨在推动开放、易于获取的 RISC-V 向量与矩阵处理技术教育。英文内容采用增量方式发布，并随书稿演进持续更新。

原始仓库：https://github.com/simplex-micro/riscv-vector-primer

## 许可证与翻译状态

英文原作采用 [CC BY-NC-ND 4.0](../LICENSE) 许可证，原声明保持不变。本译稿已获得原作者针对非商业中文翻译申请的邮件许可，当前发布计划为 GitHub 和知乎；该许可不构成对原作的重新许可。具体记录与边界见[翻译说明](TRANSLATION-NOTICE.md)。
