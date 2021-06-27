# 第十六周

## RISC-V 处理器

#### 概念表达
RISC-V（发音为“risk-five”）是一个基于精简指令集（RISC）原则的开源指令集架构（ISA）。

与大多数指令集相比，RISC-V指令集可以自由地用于任何目的，允许任何人设计、制造和销售RISC-V芯片和软件。虽然这不是第一个开源指令集，但它具有重要意义，因为其设计使其适用于现代计算设备（如仓库规模云计算机、高端移动电话和微小嵌入式系统）。设计者考虑到了这些用途中的性能与功率效率。该指令集还具有众多支持的软件，这解决了新指令集通常的弱点。
该项目2010年始于加州大学伯克利分校，但许多贡献者是该大学以外的志愿者和行业工作者。

RISC-V指令集的设计考虑了小型、快速、低功耗的现实情况来实做，但并没有对特定的微架构做过度的设计。

#### 定义
RISC-V(读作“RISC-FIVE”)是基于精简指令集计算(RISC)原理建立的开放指令集架构(ISA)，V表示为第五代RISC(精简指令集计算机),表示此前已经四代RISC处理器原型芯片。每一代RISC处理器都是在同一人带领下完成，那就是加州大学伯克利分校的David A. Patterson教授。与大多数ISA相反，RISC-V ISA可以免费地用于所有希望的设备中，允许任何人设计、制造和销售RISC-V芯片和软件。图1展示了此前的四代RISC处理器原型芯片。它虽然不是第一个开源的的指令集(ISA)，但它很重要，因为它第一个被设计成可以根据具体场景可以选择适合的指令集的指令集架构。基于RISC-V指令集架构可以设计服务器CPU，家用电器cpu，工控cpu和用在比指头小的传感器中的cpu。

#### 特色
* 完全开源
对指令集使用，RISC-V基金会不收取高额的授权费。开源采用宽松的BSD协议，企业完全自由免费使用，同时也容许企业添加自有指令集拓展而不必开放共享以实现差异化发展。
* 架构简单
RISC-V架构秉承简单的设计哲学。体现为：
在处理器领域，主流的架构为x86与ARM架构。x86与ARM架构的发展的过程也伴随了现代处理器架构技术的不断发展成熟，但作为商用的架构，为了能够保持架构的向后兼容性，其不得不保留许多过时的定义，导致其指令数目多，指令冗余严重，文档数量庞大，所以要在这些架构上开发新的操作系统或者直接开发应用门槛很高。而RISC-V架构则能完全抛弃包袱，借助计算机体系结构经过多年的发展已经成为比较成熟的技术的优势，从轻上路。RISC-V基础指令集则只有40多条，加上其他的模块化扩展指令总共几十条指令。 RISC-V的规范文档仅有145页，而“特权架构文档”的篇幅也仅为91页。
* 易于移植*nix
现代操作系统都做了特权级指令和用户级指令的分离，特权指令只能操作系统调用，而用户级指令才能在用户模式调用，保障操作系统的稳定。RISC-V提供了特权级指令和用户级指令，同时提供了详细的RISC-V特权级指令规范和RISC-V用户级指令规范的详细信息，使开发者能非常方便的移植linux和unix系统到RISC-V平台。
* 模块化设计
RISC-V架构不仅短小精悍，而且其不同的部分还能以模块化的方式组织在一起，从而试图通过一套统一的架构满足各种不同的应用场景。用户能够灵活选择不同的模块组合，来实现自己定制化设备的需要，比如针对于小面积低功耗嵌入式场景，用户可以选择RV32IC组合的指令集，仅使用Machine Mode（机器模式）；而高性能应用操作系统场景则可以选择譬如RV32IMFDC的指令集，使用Machine Mode（机器模式）与User Mode（用户模式）两种模式。
* 完整的工具链
对于设计CPU来说，工具链是软件开发人员和cpu交互的窗口，没有工具链，对软件开发人员开发软件要求很高，甚至软件开发者无法让cpu工作起来。在cpu设计中，工具链的开发是一个需要巨大工作量的工作。如果用RISC-V来设计芯片，芯片设计公司不再担心工具链问题，只需专注于芯片设计，RISC-V社区已经提供了完整的工具链，并且RISC-V基金会持续维护该工具链。当前RISC-V的支持已经合并到主要的工具中，比如编译工具链gcc, 仿真工具qemu等
###  什麽是[RISC-V](https://zh.wikipedia.org/wiki/RISC-V)
* RISC-V（发音为「risk-five」）是一个基于精简指令集（RISC）原则的开源指令集架构（ISA），简易解释为开源软体运动相对应的一种「开源硬体」。
* 该专案2010年始于加州大学柏克莱分校，但许多贡献者是该大学以外的志愿者和行业工作者。
* RISC-V指令集的设计考虑了小型、快速、低功耗的现实情况来实做，但并没有对特定的微架构做过度的设计。

#### 建立 RISC-V 架构的原因有很多，包括：
* 满足对开放原始码指令集架构 (ISA) 的需求，能在学术用途下，供学生用于大学专案中
* 藉此分享有关 ISA 开发的设计专业知识
* 藉此避免向目前的晶片公司支付权利金，并进而节省成本
* 保护某个架构 (某公司的 IP) 的设计细节，以维持商业可行性