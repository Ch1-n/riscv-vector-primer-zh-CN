# 术语表

译法按硬件架构语境统一。VL/VLEN、SEW/EEW 和 LMUL/EMUL 分别回答不同问题，不能互相替代；规范术语与作者采用的实现术语也分开说明。

| English | 中文译法 | 说明 |
|---|---|---|
| vector extension | 向量扩展 | 指 RISC-V V 扩展时也写作 RVV |
| vector-length-agnostic (VLA) | 向量长度无关 | 程序不写死实现的 VLEN，通过运行时 VL 分段处理数据 |
| hardware thread (hart) | 硬件线程（hart） | RISC-V 中独立取指并执行指令的硬件线程 |
| vector register file (VRF) | 向量寄存器文件 | 保留缩写 VRF |
| lane | 通道 | 指向量处理器中的并行执行通道 |
| chaining | 链式执行 | 上游部分结果就绪后，下游即可按元素或元素组开始处理；属于微架构机制，RVV 不强制要求 |
| strip mining | 分段处理（strip mining） | 把长循环拆成多轮，每轮根据实际返回的 VL 处理数据并更新指针 |
| element | 元素 | 向量寄存器中的数据单元 |
| element width | 元素位宽 | 通常由 SEW 指定 |
| selected element width (SEW) | 选定元素位宽 | 首次出现时保留英文缩写 |
| application vector length (AVL) | 应用请求向量长度 | 软件交给配置指令的请求长度，不一定等于实际 VL |
| vector length (VL) | 向量长度 | 普通逐元素操作的索引上界；`vstart=0` 且无掩码时等于处理元素数，CSR 名称为 `vl` |
| maximum vector length (VLMAX) | 最大向量长度 | 当前配置的元素容量，`VLMAX = LMUL × VLEN / SEW` |
| vector register length (VLEN) | 向量寄存器长度 | 单个架构向量寄存器的位数，是每个 hart 的实现参数 |
| datapath width (DLEN) | 数据通路宽度 | 原作使用的实现参数，不是 RVV ISA 参数；具体指单通道还是某单元的总宽度，应看实现文档 |
| register grouping | 寄存器分组 | 由 LMUL 控制 |
| vector register group multiplier (LMUL) | 向量寄存器组倍增系数 | 控制一个逻辑操作数占用的寄存器组大小 |
| effective element width (EEW) | 有效元素位宽 | 具体操作数的元素位宽；索引访存编码中的 EEW 指索引位宽，数据位宽仍为 SEW |
| effective LMUL (EMUL) | 有效 LMUL | 普通数据操作数满足 `EMUL = (EEW/SEW) × LMUL`；它描述有效分组，不由 DLEN 决定 |
| tail agnostic | 尾部不关心 | 对应 `vta=1` |
| tail undisturbed | 尾部保持 | 对应 `vta=0` |
| mask agnostic | 掩码关闭元素不关心 | 对应 `vma=1` |
| mask undisturbed | 掩码关闭元素保持 | 对应 `vma=0` |
| widening / narrowing | 加宽 / 窄化 | 指结果或操作数位宽变化 |
| reduction | 归约 | 将源向量活动元素与 `vs1[0]` 初始值合并，结果写入 `vd[0]`；不是直接写入标量寄存器 |
| indexed gather / scatter | 索引聚集加载 / 分散存储 | 按索引向量中的字节偏移访问内存 |
| register gather | 寄存器聚集 | 如 `vrgather`，按元素索引选择寄存器内数据，不访问数据内存 |
| fault-only-first load | 仅首元素故障加载 | 索引 0 的同步异常正常陷入；索引 i>0 的同步异常被抑制并将 VL 缩短到 i；“首”不是首个活动元素 |
| precise trap | 精确陷入 | 按规定维护指令顺序和可恢复状态；当前向量指令可部分完成，并由 `vstart` 指定恢复位置 |
| commit / retire | 提交 / 退休 | 许多文献近义使用；本书第 3.9.4 节特指作者的阶段划分，不能将“先提交”直接当作最终退休 |
| register renaming | 寄存器重命名 | 用物理寄存器消除伪相关 |
| architectural register | 体系结构寄存器 | 软件可见的寄存器名称及状态，如 `v0`～`v31`；不等于物理存储阵列的划分 |
| physical register | 物理寄存器 | 实现中保存数据的实际存储位置，常用于重命名语境 |
| bank | 存储体 | VRF bank 与缓存/本地存储器 bank 属于不同层级，冲突原因不能混用 |
| core / kernel | 处理器核 / 计算内核 | 硬件 core 与软件计算 kernel 分开译；操作系统 kernel 仍译“内核” |
| fire-and-forget | 发射后自主完成 | 本书用于描述提前安排依赖和资源的执行思路；不等于无需处理异常 |
| sticky flag | 粘滞标志 | 一旦置位就保持，直到软件清除；如 `fflags`、`vxsat` |
| NFIELDS / nf | 字段数 / 字段数编码 | 分段访存中 `NFIELDS = nf + 1` |
| functional unit | 功能单元 | 如 ALU、乘法、访存、置换单元 |
| processing element (PE) | 处理单元 | 矩阵阵列中的计算节点 |
| tile | 矩阵块（tile） | 矩阵架构或矩阵扩展提案中的二维数据对象 |
| output-stationary dataflow | 输出驻留数据流 | 让输出部分和留在本地，直到当前输出块完成 |
| operand-stationary dataflow | 操作数驻留数据流 | 让 A 或 B 等输入操作数的一部分留在本地并反复复用 |

## 容易混淆的边界

- **Agnostic 不等于任意位模式。**普通数据目的元素可以保留旧值或写成全 1；掩码结果的尾部另有规则。
- **LMUL 分组不等于物理拼接。**软件看到连续的寄存器组，内部仍可分通道、分存储体和分多拍执行。
- **分段处理与分段访存不同。**前者是 strip mining 循环模式，后者是 segment load/store，用于交错字段的搬运。
- **Tile 不等于 PE 阵列。**前者是软件操作的数据块，后者是物理计算资源；一个 tile 可以分多拍映射到阵列。
