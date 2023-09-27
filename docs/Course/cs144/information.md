# CS144 information

> 前5个Lab从byte_stream开始，一步一步地指导你实现出一个能真实使用的TCP，总得来说有趣而又有用，且难度也不算很大。
>
> Lab2和Lab3的test case不够多，导致错误或者是与Lab期望的设计不符的实现也能通过全部的test case。然后在Lab4里，这些问题会全部暴露出来......结果就是在做Lab4的时候完全不能信任自己在Lab2和Lab3里的相应实现，这样也大大增加了debug难度。
>
> Lab4里有两个test case即fsm_ack_rst和fsm_ack_rst_relaxed期待的行为是完全相反的。实际上在官方的FAQ页面上给出的状态机是与fsm_ack_rst期待的行为一致，但Lab4默认启用的却是fsm_ack_rst_relaxed......
>
> 官方提供的VirtualBox Image中的GDB是有bug的，在cmake_build_type=Debug生成的binary上不能正确地打断点。在Lab4之前我还能靠肉眼调试，但是Lab4实在是肉眼调不动了，不得不寻求解决方案。后来问了一位之前也做过这个Lab的清华大佬 [@RT Huang](https://www.zhihu.com/people/47ee4a7553348d5300b026fb4a3f4dc2)，他告诉我说他用的是LLDB。我就赶紧换了LLDB，这才能愉快的进行调试。顺带一提，这位大佬在GitHub上有自己[完成这门课程和Lab的笔记](https://link.zhihu.com/?target=https%3A//github.com/huangrt01/CS-Notes)，也是值得参考的Orz 我室友 [@Comzyh](https://www.zhihu.com/people/364960a3dd0d88cc9d22449badf0a456)后来怕我搞定不了又没人教我，就也来做这个Lab了，据他说开了-O0之后GDB就能正常工作了，但我自己之前尝试的时候这样还是不能正常工作。





​                   
