---
title: 主板诊断卡代码对照表
url: 28.html
id: 28
categories:
  - 'NULL'
  - 技术杂文
date: 2008-12-17 10:06:00
tags:
---

查表必读：  
1、特殊代码"00"和"ff"及其它起始码有三种情况出现：  
①已由一系列其它代码之后再出现："00"或"ff"，则主板ok。  
②如果将cmos中设置无错误，则不严重的故障不会影响bios自检的继续，而最终出现"00"或"ff"。  
③一开机就出现"00"或"ff"或其它起始代码并且不变化则为主板没有运行起来。  
2、本表是按代码值从小到大排序，卡中出码顺序不定。  
3、未定义的代码表中未列出。  
4、对于不同bios（常用ami、award、phoenix）用同一代码代表的意义不同，因此应弄清您所检测的电脑是属于哪一种类型的bios，您可查阅您的电脑使用手册，或从主板上的bios芯片上直接查看，也可以在启动屏幕时直接看到。  
5、有少数主板的pci槽只有一部分代码出现，但isa槽有完整自检代码输出。且目前已发现有极个别原装机主板的isa槽无代码输出，而pci槽则有完整代码输出，故建议您在查看代码不成功时，将本双槽卡换到另一种插槽试一下。另外，同一块主板的不同pci槽，有的槽有完整代码送出，如dell810主板只有靠近cpu的一个pci槽有完整代码显示，一直变化到"00"或"ff"，而其它pci槽走到"38"后则不继续变化。  
6、复位信号所需时间isa与pci不一定同步，故有可能isa开始出代码，但pci的复位灯还不熄，故pci代码停要起始代码上。  
代码对照表  
00 . 已显示系统的配置；即将控制INI19引导装入。  
01 处理器测试1，处理器状态核实,如果测试失败，循环是无限的。 处理器寄存器的测试即将开始，不可屏蔽中断即将停用。 CPU寄存器测试正在进行或者失败。  
02 确定诊断的类型（正常或者制造）。如果键盘缓冲器含有数据就会失效。 停用不可屏蔽中断；通过延迟开始。 CMOS写入／读出正在进行或者失灵。  
03 清除8042键盘控制器，发出TESTKBRD命令（AAH） 通电延迟已完成。 ROM BIOS检查部件正在进行或失灵。  
04 使8042键盘控制器复位，核实TESTKBRD。 键盘控制器软复位／通电测试。 可编程间隔计时器的测试正在进行或失灵。  
05 如果不断重复制造测试1至5，可获得8042控制状态。 已确定软复位／通电；即将启动ROM。 DMA初如准备正在进行或者失灵。  
06 使电路片作初始准备，停用视频、奇偶性、DMA电路片，以及清除DMA电路片，所有页面寄存器和CMOS停机字节。 已启动ROM计算ROM  
BIOS检查总和，以及检查键盘缓冲器是否清除。 DMA初始页面寄存器读／写测试正在进行或失灵。  
07 处理器测试2，核实CPU寄存器的工作。 ROM BIOS检查总和正常，键盘缓冲器已清除，向键盘发出BAT（基本保证测试）命令。 .  
08 使CMOS计时器作初始准备，正常的更新计时器的循环。 已向键盘发出BAT命令，即将写入BAT命令。 RAM更新检验正在进行或失灵。  
09 EPROM检查总和且必须等于零才通过。 核实键盘的基本保证测试，接着核实键盘命令字节。 第一个64K RAM测试正在进行。  
0A 使视频接口作初始准备。 发出键盘命令字节代码，即将写入命令字节数据。 第一个64K RAM芯片或数据线失灵，移位。  
0B 测试8254通道0。 写入键盘控制器命令字节，即将发出引脚23和24的封锁／解锁命令。 第一个64K RAM奇／偶逻辑失灵。  
0C 测试8254通道1。 键盘控制器引脚23、24已封锁／解锁；已发出NOP命令。 第一个64K RAN的地址线故障。  
0D 1、检查CPU速度是否与系统时钟相匹配。2、检查控制芯片已编程值是否符合初设置。3、视频通道测试，如果失败，则鸣喇叭。  
已处理NOP命令；接着测试CMOS停开寄存器。 第一个64K RAM的奇偶性失灵  
0E 测试CMOS停机字节。 CMOS停开寄存器读／写测试；将计算CMOS检查总和。 初始化输入／输出端口地址。  
0F 测试扩展的CMOS。 已计算CMOS检查总和写入诊断字节；CMOS开始初始准备。 .  
10 测试DMA通道0。 CMOS已作初始准备，CMOS状态寄存器即将为日期和时间作初始准备。 第一个64K RAM第0位故障。  
11 测试DMA通道1。 CMOS状态寄存器已作初始准备，即将停用DMA和中断控制器。 第一个64DK RAM第1位故障。  
12 测试DMA页面寄存器。 停用DMA控制器1以及中断控制器1和2；即将视频显示器并使端口B作初始准备。 第一个64DK RAM第2位故障。  
13 测试8741键盘控制器接口。 视频显示器已停用，端口B已作初始准备；即将开始电路片初始化／存储器自动检测。 第一个64DK RAM第3位故障。  
14 测试存储器更新触发电路。 电路片初始化／存储器处自动检测结束；8254计时器测试即将开始。 第一个64DK RAM第4位故障。  
15 测试开头64K的系统存储器。 第2通道计时器测试了一半；8254第2通道计时器即将完成测试。 第一个64DK RAM第5位故障。  
16 建立8259所用的中断矢量表。 第2通道计时器测试结束；8254第1通道计时器即将完成测试。 第一个64DK RAM第6位故障。  
17 调准视频输入／输出工作，若装有视频BIOS则启用。 第1通道计时器测试结束；8254第0通道计时器即将完成测试。 第一个64DK RAM第7位故障。  
18 测试视频存储器，如果安装选用的视频BIOS通过，由可绕过。 第0通道计时器测试结束；即将开始更新存储器。 第一个64DK RAM第8位故障。  
19 测试第1通道的中断控制器（8259）屏蔽位。 已开始更新存储器，接着将完成存储器的更新。 第一个64DK RAM第9位故障。  
1A 测试第2通道的中断控制器（8259）屏蔽位。 正在触发存储器更新线路，即将检查15微秒通／断时间。 第一个64DK RAM第10位故障。  
1B 测试CMOS电池电平。 完成存储器更新时间30微秒测试；即将开始基本的64K存储器测试。 第一个64DK RAM第11位故障。  
1C 测试CMOS检查总和。 . 第一个64DK RAM第12位故障。  
1D 调定CMOS配置。 . 第一个64DK RAM第13位故障。  
1E 测定系统存储器的大小，并且把它和CMOS值比较。 . 第一个64DK RAM第14位故障。  
1F 测试64K存储器至最高640K。 . 第一个64DK RAM第15位故障。  
20 测量固定的8259中断位。 开始基本的64K存储器测试；即将测试地址线。 从属DMA寄存器测试正在进行或失灵。  
21 维持不可屏蔽中断（NMI）位（奇偶性或输入／输出通道的检查）。 通过地址线测试；即将触发奇偶性。 主DMA寄存器测试正在进行或失灵。  
22 测试8259的中断功能。 结束触发奇偶性；将开始串行数据读／写测试。 主中断屏蔽寄存器测试正在进行或失灵。  
23 测试保护方式8086虚拟方式和8086页面方式。 基本的64K串行数据读／写测试正常；即将开始中断矢量初始化之前的任何调节。  
从属中断屏蔽存器测试正在进行或失灵。  
24 测定1MB以上的扩展存储器。 矢量初始化之前的任何调节完成，即将开始中断矢量的初始准备。 设置ES段地址寄存器注册表到内存高端。  
25 测试除头一个64K之后的所有存储器。 完成中断矢量初始准备；将为旋转式断续开始读出8042的输入／输出端口。 装入中断矢量正在进行或失灵。  
26 测试保护方式的例外情况。 读出8042的输入／输出端口；即将为旋转式断续开始使全局数据作初始准备。 开启A20地址线；使之参入寻址。  
27 确定超高速缓冲存储器的控制或屏蔽RAM。 全1数据初始准备结束；接着将进行中断矢量之后的任何初始准备。 键盘控制器测试正在进行或失灵。  
28 确定超高速缓冲存储器的控制或者特别的8042键盘控制器。 完成中断矢量之后的初始准备；即将调定单色方式。 CMOS电源故障／检查总和计算正在进行。  
29 . 已调定单色方式，即将调定彩色方式。 CMOS配置有效性的检查正在进行。  
2A 使键盘控制器作初始准备。 已调定彩色方式，即将进行ROM测试前的触发奇偶性。 置空64K基本内存。  
2B 使磁碟驱动器和控制器作初始准备。 触发奇偶性结束；即将控制任选的视频ROM检查前所需的任何调节。 屏幕存储器测试正在进行或失灵。  
2C 检查串行端口，并使之作初始准备。 完成视频ROM控制之前的处理；即将查看任选的视频ROM并加以控制。 屏幕初始准备正在进行或失灵。  
2D 检测并行端口，并使之作初始准备。 已完成任选的视频ROM控制，即将进行视频ROM回复控制之后任何其他处理的控制。 屏幕回扫测试正在进行或失灵。  
2E 使硬磁盘驱动器和控制器作初始准备。 从视频ROM控制之后的处理复原；如果没有发现EGA／VGA就要进行显示器存储器读／写测试。 检测视频ROM正在进行。  
2F 检测数学协处理器，并使之作初始准备。 没发现EGA／VGA；即将开始显示器存储器读／写测试。 .  
30 建立基本内存和扩展内存。 通过显示器存储器读／写测试；即将进行扫描检查。 认为屏幕是可以工作的。  
31 检测从C800：0至EFFF：0的选用ROM，并使之作初始准备。  
显示器存储器读／写测试或扫描检查失败，即将进行另一种显示器存储器读／写测试。 单色监视器是可以工作的。  
32 对主板上COM／LTP／FDD／声音设备等I／O芯片编程使之适合设置值。  
通过另一种显示器存储器读／写测试；却将进行另一种显示器扫描检查。 彩色监视器（40列）是可以工作的。  
33 . 视频显示器检查结束；将开始利用调节开关和实际插卡检验显示器的关型。 彩色监视器（80列）是可以工作的。  
34 . 已检验显示器适配器；接着将调定显示方式。 计时器滴答声中断测试正在进行或失灵。 35 . 完成调定显示方式；即将检查BIOS  
ROM的数据区。 停机测试正在进行或失灵。  
36 . 已检查BIOS ROM数据区；即将调定通电信息的游标。 门电路中A－20失灵。  
37 . 识别通电信息的游标调定已完成；即将显示通电信息。 保护方式中的意外中断。  
38 . 完成显示通电信息；即将读出新的游标位置。 RAM测试正在进行或者地址故障＞FFFFH。  
39 . 已读出保存游标位置，即将显示引用信息串。 .  
3A . 引用信息串显示结束；即将显示发现信息。 间隔计时器通道2测试或失灵。  
3B 用OPTI电路片（只是486）使辅助超高速缓冲存储器作初始准备。 已显示发现＜ESC＞信息；虚拟方式，存储器测试即将开始。  
按日计算的日历时钟测试正在进行或失灵。  
3C 建立允许进入CMOS设置的标志。 . 串行端口测试正在进行或失灵。  
3D 初始化键盘／PS2鼠标／PNP设备及总内存节点。 . 并行端口测试正在进行或失灵。  
3E 尝试打开L2高速缓存。 . 数学协处理器测试正在进行或失灵。  
40 . 已开始准备虚拟方式的测试；即将从视频存储器来检验。 调整CPU速度，使之与外围时钟精确匹配。  
41 中断已打开，将初始化数据以便于0：0检测内存变换（中断控制器或内存不良） 从视频存储器检验之后复原；即将准备描述符表。 系统插件板选择失灵。  
42 显示窗口进入SETUP。 描述符表已准备好；即将进行虚拟方式作存储器测试。 扩展CMOS RAM故障。  
43 若是即插即用BIOS，则串口、并口初始化。 进入虚拟方式；即将为诊断方式实现中断。 . 44 .  
已实现中断（如已接通诊断开关；即将使数据作初始准备以检查存储器在0：0返转。） BIOS中断进行初始化。  
45 初始化数学协处理器。 数据已作初始准备；即将检查存储器在0：0返转以及找出系统存储器的规模。 .  
46 . 测试存储器已返回；存储器大小计算完毕，即将写入页面来测试存储器。 检查只读存储器ROM版本。  
47 . 即将在扩展的存储器试写页面；即将基本640K存储器写入页面。  
48 . 已将基本存储器写入页面；即将确定1MB以上的存储器。 视频检查，CMOS重新配置。  
49 . 找出1BM以下的存储器并检验；即将确定1MB以上的存储器。 .  
4A . 找出1MB以上的存储器并检验；即将检查BIOS ROM数据区。 进行视频的初始化。  
4B . BIOS ROM数据区的检验结束，即将检查＜ESC＞和为软复位清除1MB以上的存储器。 . 4C .  
清除1MB以上的存储器(软复位)即将清除1MB以上的存储器. 屏蔽视频BIOS ROM。.  
4D。已清除1MB以上的存储器（软复位）；将保存存储器的大小。 .  
4E 若检测到有错误；在显示器上显示错误信息，并等待客户按＜F1＞键继续。 开始存储器的测试：（无软复位）；即将显示第一个64K存储器的测试。 显示版权信息。  
4F 读写软、硬盘数据，进行DOS引导。 开始显示存储器的大小，正在测试存储器将使之更新；将进行串行和随机的存储器测试。 .  
50 将当前BIOS监时区内的CMOS值存到CMOS中。 完成1MB以下的存储器测试；即将高速存储器的大小以便再定位和掩蔽。 将CPU类型和速度送到屏幕。  
51 . 测试1MB以上的存储器。 .  
52 所有ISA只读存储器ROM进行初始化，最终给PCI分配IRQ号等初始化工作。 已完成1MB以上的存储器测试；即将准备回到实址方式。 进入键盘检测。  
53 如果不是即插即用BIOS，则初始化串口、并口和设置时种值。 保存CPU寄存器和存储器的大小，将进入实址方式。 .  
54 . 成功地开启实址方式；即将复原准备停机时保存的寄存器。 扫描"打击键"  
55 . 寄存器已复原，将停用门电路A－20的地址线。 .  
56 . 成功地停用A－20的地址线；即将检查BIOS ROM数据区。 键盘测试结束。  
57 . BIOS ROM数据区检查了一半；继续进行。 .  
58 . BIOS ROM的数据区检查结束；将清除发现＜ESC＞信息。 非设置中断测试。  
59 . 已清除＜ESC＞信息；信息已显示；即将开始DMA和中断控制器的测试。 .  
5A . . 显示按"F2"键进行设置。  
5B . . 测试基本内存地址。  
5C . . 测试640K基本内存。  
60 设置硬盘引导扇区病毒保护功能。 通过DMA页面寄存器的测试；即将检验视频存储器。 测试扩展内存。  
61 显示系统配置表。 视频存储器检验结束；即将进行DMA＃1基本寄存器的测试。 .  
62 开始用中断19H进行系统引导。 通过DMA＃1基本寄存器的测试；即将进行DMA＃2寄存器的测试。 测试扩展内存地址线。  
63 . 通过DMA＃2基本寄存器的测试；即将检查BIOS ROM数据区。 .  
64 . BIOS ROM数据区检查了一半，继续进行。 .  
65 . BIOS ROM数据区检查结束；将把DMA装置1和2编程。 .  
66 . DMA装置1和2编程结束；即将使用59号中断控制器作初始准备。 Cache注册表进行优化配置。  
67 . 8259初始准备已结束；即将开始键盘测试。 .  
68 . . 使外部Cache和CPU内部Cache都工作。  
6A . . 测试并显示外部Cache值。  
6C . . 显示被屏蔽内容。  
6E . . 显示附属配置信息。  
70 . . 检测到的错误代码送到屏幕显示。  
72 . . 检测配置有否错误。  
74 . . 测试实时时钟。  
76 . . 扫查键盘错误。  
7A . . 锁键盘。  
7C . . 设置硬件中断矢量。  
7E . . 测试有否安装数学处理器。  
80 . 键盘测试开始，正在清除和检查有没有键卡住，即将使键盘复原。 关闭可编程输入／输出设备。  
81 . 找出键盘复原的错误卡住的键；即将发出键盘控制端口的测试命令。 .  
82 . 键盘控制器接口测试结束，即将写入命令字节和使循环缓冲器作初始准备。 检测和安装固定RS232接口（串口）。  
83 . 已写入命令字节，已完成全局数据的初始准备；即将检查有没有键锁住。 .  
84 . 已检查有没有锁住的键，即将检查存储器是否与CMOS失配。 检测和安装固定并行口。 85 . 已检查存储器的大小；即将显示软错误和口令或旁通安排。 .  
86 . 已检查口令；即将进行旁通安排前的编程。 重新打开可编程I／O设备和检测固定I／O是否有冲突。  
87 . 完成安排前的编程；将进行CMOS安排的编程。 .  
88 . 从CMOS安排程序复原清除屏幕；即将进行后面的编程。 初始化BIOS数据区。  
89 . 完成安排后的编程；即将显示通电屏幕信息。 .  
8A . 显示头一个屏幕信息。 进行扩展BIOS数据区初始化。  
8B . 显示了信息：即将屏蔽主要和视频BIOS。 .  
8C . 成功地屏蔽主要和视频BIOS，将开始CMOS后的安排任选项的编程。 进行软驱控制器初始化。  
8D . 已经安排任选项编程，接着检查滑了鼠和进行初始准备。 .  
8E . 检测了滑鼠以及完成初始准备；即将把硬、软磁盘复位。 .  
8F . 软磁盘已检查，该磁碟将作初始准备，随后配备软磁碟。 .  
90 . 软磁碟配置结束；将测试硬磁碟的存在。 硬盘控制器进行初始化。  
91 . 硬磁碟存在测试结束；随后配置硬磁碟。 局部总线硬盘控制器初始化。  
92 . 硬磁碟配置完成；即将检查BIOS ROM的数据区。 跳转到用户路径2。  
93 . BIOS ROM的数据区已检查一半；继续进行。 .  
94 . BIOS ROM的数据区检查完毕，即调定基本和扩展存储器的大小。 关闭A－20地址线。 95 .  
因应滑鼠和硬磁碟47型支持而调节好存储器的大小；即将检验显示存储器。 .  
96 . 检验显示存储器后复原；即将进行C800：0任选ROM控制之前的初始准备。 "ES段"注册表清除。  
97 . C800：0任选ROM控制之前的任何初始准备结束，接着进行任选ROM的检查及控制。 . 98 .  
任选ROM的控制完成；即将进行任选ROM回复控制之后所需的任何处理。 查找ROM选择。  
99 . 任选ROM测试之后所需的任何初始准备结束；即将建立计时器的数据区或打印机基本地址。 .  
9A . 调定计时器和打印机基本地址后的返回操作；即调定RS－232基本地址。 屏蔽ROM选择。  
9B . 在RS－232基本地址之后返回；即将进行协处理器测试之初始准备。 .  
9C . 协处理器测试之前所需初始准备结束；接着使协处理器作初始准备。 建立电源节能管理。  
9D . 协处理器作好初始准备，即将进行协处理器测试之后的任何初始准备。 .  
9E . 完成协处理器之后的初始准备，将检查扩展键盘，键盘识别符，以及数字锁定。 开放硬件中断。  
9F . 已检查扩展键盘，调定识别标志，数字锁接通或断开，将发出键盘识别命令。 .  
A0 . 发出键盘识别命令；即将使键盘识别标志复原。 设置时间和日期。  
A1 . 键盘识别标志复原；接着进行高速缓冲存储器的测试。 .  
A2 . 高速缓冲存储器测试结束；即将显示任何软错误。 检查键盘锁。  
A3 . 软错误显示完毕；即将调定键盘打击的速率。 .  
A4 . 调好键盘的打击速率，即将制订存储器的等待状态。 键盘重复输入速率的初始化。  
A5 . 存储器等候状态制定完毕；接着将清除屏幕。 .  
A6 . 屏幕已清除；即将启动奇偶性和不可屏蔽中断。 .  
A7 . 已启用不可屏蔽中断和奇偶性；即将进行控制任选的ROM在E000：0之所需的任何初始准备。 .  
A8 . 控制ROM在E000：0之前的初始准备结束，接着将控制E000：0之后所需的任何初始准备。 清除"F2"键提示。  
A9 . 从控制E000：0 ROM返回，即将进行控制E000：0任选ROM之后所需的任何初始准备。 .  
AA . 在E000：0控制任选ROM之后的初始准备结束；即将显示系统的配置。 扫描"F2"键打击。  
AC . . 进入设置.  
AE . . 清除通电自检标志。  
B0 . . 检查非关键性错误。  
B2 . . 通电自检完成准备进入操作系统引导。  
B4 . . 蜂鸣器响一声。  
B6 . . 检测密码设置（可选）。  
B8 . . 清除全部描述表。  
BC . . 清除校验检查值。  
BE 程序缺省值进入控制芯片，符合可调制二进制缺省值表。 . 清除屏幕（可选）。  
BF 测试CMOS建立值。 . 检测病毒，提示做资料备份。  
C0 初始化高速缓存。 . 用中断19试引导。  
C1 内存自检。 . 查找引导扇区中的"55""AA"标记。  
C3 第一个256K内存测试。 . .  
C5 从ROM内复制BIOS进行快速自检。 . .  
C6 高速缓存自检。 . .  
CA 检测Micronies超速缓冲存储器（如果存在），并使之作初始准备。 . .  
CC 关断不可屏蔽中断处理器。 . .  
EE 处理器意料不到的例外情况。 . .  
FF 给予INI19引导装入程序的控制，主板OK。

humen1 Tech![](https://blogger.googleusercontent.com/tracker/7269874978253342363-6819128970492068246?l=www.humen1.net)