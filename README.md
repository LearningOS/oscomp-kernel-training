# oscomp kernel training

## 训练邀请：OS kernel设计与实现
- [点击：创建自己的内核赛道训练repo](https://classroom.github.com/a/vk-D9SrL)
- [查看训练排行榜单](https://os-autograding.github.io/classroom-grading-template/)

**注：**
1. **基于Github Classroom，具有在线编程，在线自动评测，在线显示排行榜的特征**
2. **基于2022全国大学生OS比赛内核赛道，训练内容和难度超过全球99.9%的大学本科OS实验**
3. **没学过git/github使用、C/Rust语言、基本数据结构和算法、操作系统和与RISC-V相关的组成原理课程的同学，建议先补一下相关知识**

## 内核赛道OS训练repo说明

> 目前支持对2022全国大学生OS比赛内核赛道的Linux Apps测例的测试，采用形式与比赛大致相同，选手需要在根目录添加一个 Makefile 文件，使用 make all 命令在根目录生成 kernel-qemu 文件，由评测机自动执行。

- 一个基本的能运行的 `kernel demo`： [https://github.com/yfblock/oscomp-kernel-example](https://github.com/yfblock/oscomp-kernel-example)
- 一个能通过所有测例的 `complete kernel reference`：[暂不公布]()

目前已经支持 `musl libc-test`， `busybox`, `lua`, `lmbench` 相关Linux App测例，测试过程无人工干预，需要由内核自动运行，所有测例文件放在镜像中，内核需要支持 `fat32` 文件系统来读取文件。 [镜像文件](https://github.com/os-autograding/testsuits-in-one/raw/gh-pages/fat32.img)

## 本地测试

如你写好OS后，想在在本地测试，评测运行指令如下：

```shell
qemu-system-riscv64 \
    -machine virt \
    -bios default \
    -device loader,file=kernel-qemu,addr=0x80200000 \
    -drive file=fat32.img,if=none,format=raw,id=x0 \
    -device virtio-blk-device,drive=x0,bus=virtio-mmio-bus.0 \
    -kernel kernel-qemu \
    -nographic \
    -smp 4 -m 2G
```

## 在线测试
github的CI对内核进行测试的执行时间设置为 `300` 秒（`5`分钟），超时后程序会被终止，不再继续执行，所得分数为超时前完成的部分的分数。

github的CI执行完毕后，会在你的repo中的 gp-pages 分支下生成相关的 `log` 文件和 `README` 文件，在 `README` 文件中可以看到当前得到的分数，在 `log` 文件中能看到详细的得分情况。

## 注意事项
- `QEMU` 版本为 `7.0.0`
- `RUST ToolChain` 版本为 `nightly-2022-08-08`
- 编译目标架构为 `riscv64imac-unknown-none-elf`
- 内核执行时间为 `5` 分钟
- 内核可用内存大小为 `2G`
- 只有 `main` 分支的提交可以被Github 上的CI评测机处理
- Github 上的CI评测机在初次运行时需要编译 `qemu`，可能需要花费一些时间，请耐心等待
- 如果在实践中碰到问题，请在本repo的 `issues` 栏中发帖子
- 如果有进一步的改进，请给本repo提 `Pull requests`

## 学习资源
### 2022OS比赛内核实现赛道一等奖的仓库（包含从初赛到决赛全过程的文档/代码等）
- [北航：图漏图森破](https://gitlab.eduxiji.net/19373469/oskernel2022-x.git)
- [西工大：NPUcore](https://gitlab.eduxiji.net/2019301887/oskernel2022-npucore.git)
- [清华：Maturin](https://gitlab.eduxiji.net/scPointer/maturin.git)
- [哈工大深圳：FTL OS](https://gitlab.eduxiji.net/DarkAngelEX/oskernel2022-ftlos.git)
- [杭电：进击のOS](https://gitlab.eduxiji.net/YzTz/os.git)
- [哈工大深圳：OopS](https://gitlab.eduxiji.net/ZYF_2001/oskernel2022-oops.git)

### 训练与比赛信息（丰富的基础OS相关学习与训练资源）
- [与内核赛道相关的一些硬件/OS相关的实例/教程的参考信息](https://github.com/oscomp/os-competition-info/blob/main/ref-info.md)
- [2022暑期开源操作系统训练营](https://learningos.github.io/rust-based-os-comp2022/)
- [2022全国大学生操作系统比赛相关信息-技术报告/学习资料等](https://github.com/oscomp/os-competition-info)
- [全国大学生操作系统比赛官网](https://os.educg.net/)

## 致谢
- 杨金博：oscomp-kernel-training github classroom/CI/kernel demo
- 王明健：设计实现测试用例和评测方法等
- 闭浩扬：kernel demo&testing
