# 关键小信号参数

MOSFET 在模拟电路分析中最常用的几个参数：

- \(g_m\)
- \(r_o\)
- \(g_{mb}\)
- \(V_{TH}\)
- \(V_{OV}=V_{GS}-V_{TH}\)
- intrinsic gain \(=g_m r_o\)

---

## 1. \(g_m\)：跨导

### 定义

\[
g_m=\frac{\partial I_D}{\partial V_{GS}}
\]

意思是：

> 当 \(V_{GS}\) 发生一个很小变化时，漏极电流 \(I_D\) 会变化多少。

所以 \(g_m\) 描述的是 **gate 对 drain current 的控制能力**。

---

### 饱和区长沟道公式

在 saturation 区：

\[
I_D=\frac{1}{2}k_n V_{OV}^2
\]

其中：

\[
V_{OV}=V_{GS}-V_{TH}
\]

所以：

\[
g_m=\frac{\partial I_D}{\partial V_{GS}}
=k_n V_{OV}
\]

也可以写成：

\[
g_m=\frac{2I_D}{V_{OV}}
\]

或者：

\[
g_m=\sqrt{2k_n I_D}
\]

---

### 直观理解

\[g_m\]

越大，说明 MOS 管越容易把输入电压变化转换成输出电流变化。

在放大器中，\(g_m\) 越大，通常增益越大。

---

### 常见记忆

\[
\boxed{
g_m=\frac{2I_D}{V_{OV}}
}
\]

这条在模拟 IC 里非常常用。

---

## 2. \(r_o\)：输出电阻

### 定义

\[
r_o=\frac{1}{g_{ds}}
\]

其中：

\[
g_{ds}=\frac{\partial I_D}{\partial V_{DS}}
\]

意思是：

> 当 \(V_{DS}\) 变化时，\(I_D\) 也会因为 channel-length modulation 而变化。

---

### 公式

考虑 channel-length modulation：

\[
I_D=\frac{1}{2}k_n V_{OV}^2(1+\lambda V_{DS})
\]

所以输出电阻近似为：

\[
r_o \approx \frac{1}{\lambda I_D}
\]

---

### 直观理解

理想电流源的输出电阻是无穷大。

实际 MOS 在 saturation 区并不是完美电流源，因为 \(V_{DS}\) 变大时 \(I_D\) 也会略微变大。

所以 MOS 的输出端可以等效成一个有限电阻：

\[
r_o
\]

---

### 重要趋势

\[
r_o \approx \frac{1}{\lambda I_D}
\]

所以：

- \(I_D\) 越大，\(r_o\) 越小
- \(\lambda\) 越大，\(r_o\) 越小
- 沟道长度 \(L\) 越长，\(\lambda\) 越小，\(r_o\) 越大

---

### 常见记忆

\[
\boxed{
r_o=\frac{1}{\lambda I_D}
}
\]

在模拟放大器里， \(r_o\)越大越好，电压增益通常越高。
但是如果 MOS 被当作开关使用，看的是\(R_{on}\)，这时候希望\(R_{on}\)越小越好。

---

## 3. \(g_{mb}\)：体效应跨导

### 定义

\[
g_{mb}=\frac{\partial I_D}{\partial V_{BS}}
\]

或者有时候写成：

\[
g_{mb}=\frac{\partial I_D}{\partial V_{SB}}
\]

它描述的是：

> body/source 电压变化对漏极电流的影响。

---

### 为什么会有 \(g_{mb}\)？

MOS 的阈值电压 \(V_{TH}\) 会受到 source-body 电压影响。

当 \(V_{SB}\) 增大时，NMOS 的阈值电压会升高：

\[
V_{TH} \uparrow
\]

于是：

\[
V_{OV}=V_{GS}-V_{TH}
\]

会减小，导致：

\[
I_D \downarrow
\]

这就是 body effect。

---

### 小信号模型中的作用

在小信号模型里，除了 gate 控制电流：

\[
g_m v_{gs}
\]

body 也会控制电流：

\[
g_{mb} v_{bs}
\]

因此 MOS 小信号电流常写成：

\[
i_d = g_m v_{gs} + g_{mb} v_{bs} + g_{ds}v_{ds}
\]

---

### \(g_{mb}\) 和 \(g_m\) 的关系

通常：

\[
g_{mb}=\eta g_m
\]

其中：

\[
\eta \approx 0.1 \sim 0.3
\]

所以 \(g_{mb}\) 一般比 \(g_m\) 小。

---

### 直观理解

\(g_m\) 是 gate 控制电流的能力。

\(g_{mb}\) 是 body 控制电流的能力。

但是 body 控制能力通常比 gate 弱很多。

---

## 4. \(V_{TH}\)：阈值电压

### 定义

\[
V_{TH}
\]

是 MOSFET 开始形成强反型沟道所需要的栅源电压。

对于 NMOS：

\[
V_{GS}>V_{TH}
\]

MOS 进入强反型，开始明显导通。

---

### 直观理解

\(V_{TH}\) 可以理解为：

> MOS 管被打开所需要的最低 gate voltage。

---

### 需要注意

实际电路中 \(V_{TH}\) 不是固定不变的，它会受到很多因素影响：

- 工艺偏差
- 温度
- body effect
- channel length
- drain-induced barrier lowering，DIBL
- aging effect

---

### Body effect 公式

NMOS 的阈值电压可以写成：

\[
V_{TH}=V_{TH0}+\gamma
\left(
\sqrt{2\phi_F+V_{SB}}-\sqrt{2\phi_F}
\right)
\]

其中：

- \(V_{TH0}\)：当 \(V_{SB}=0\) 时的阈值电压
- \(\gamma\)：body effect coefficient
- \(2\phi_F\)：表面势相关参数
- \(V_{SB}\)：source 到 body 的电压

---

### 结论

对于 NMOS：

\[
V_{SB}\uparrow
\Rightarrow V_{TH}\uparrow
\Rightarrow V_{OV}\downarrow
\Rightarrow I_D\downarrow
\]

---

## 5. \(V_{OV}\)：过驱动电压

### 定义

\[
V_{OV}=V_{GS}-V_{TH}
\]

也叫：

\[
V_{eff}
\]

或者：

\[
V_{GT}
\]

---

### 直观理解

\(V_{OV}\) 表示：

> gate voltage 超过 threshold voltage 的那一部分。

也就是 MOS 真正用来增强沟道、产生强导通的有效电压。

---

### 和工作区判断的关系

对于 NMOS：

#### Triode / Linear 区

\[
V_{DS}<V_{OV}
\]

#### Saturation 区

\[
V_{DS}\ge V_{OV}
\]

所以判断 MOS 是否在 saturation，本质上就是比较：

\[
V_{DS}
\]

和：

\[
V_{OV}
\]

---

### 和电流的关系

饱和区：

\[
I_D=\frac{1}{2}k_n V_{OV}^2
\]

所以：

\[
I_D \propto V_{OV}^2
\]

---

### 和 \(g_m\) 的关系

\[
g_m=\frac{2I_D}{V_{OV}}
\]

所以在固定 \(I_D\) 下：

\[
V_{OV}\downarrow
\Rightarrow g_m\uparrow
\]

也就是说：

> 同样的偏置电流下，\(V_{OV}\) 越小，\(g_m\) 越大。

---

### 设计直觉

小 \(V_{OV}\)：

- \(g_m\) 大
- 增益可能更高
- 速度可能更慢
- headroom 更好
- 更接近弱反型/中等反型

大 \(V_{OV}\)：

- \(g_m\) 较小
- 速度可能更快
- 电压裕量要求更高
- 更强反型

---

## 6. Intrinsic Gain：本征增益

### 定义

\[
A_{v,int}=g_m r_o
\]

也叫：

\[
\text{intrinsic gain}
\]

它表示：

> 单个 MOS 管本身能提供的最大小信号电压增益能力。

---

### 为什么是 \(g_m r_o\)？

对于一个简单共源放大器，如果负载近似为 \(r_o\)，小信号增益为：

\[
A_v \approx -g_m r_o
\]

所以单管的本征增益大小为：

\[
|A_v| \approx g_m r_o
\]

---

### 代入公式

因为：

\[
g_m=\frac{2I_D}{V_{OV}}
\]

并且：

\[
r_o=\frac{1}{\lambda I_D}
\]

所以：

\[
g_m r_o
=\frac{2I_D}{V_{OV}}
\cdot
\frac{1}{\lambda I_D}
\]

化简：

\[
g_m r_o=
\frac{2}{\lambda V_{OV}}
\]

---

### 重要结论

\[
\boxed{
g_m r_o=\frac{2}{\lambda V_{OV}}
}
\]

所以 intrinsic gain 想变大，可以：

- 减小 \(V_{OV}\)
- 减小 \(\lambda\)
- 增大沟道长度 \(L\)

---

### 设计直觉

如果想要高增益：

\[
g_m r_o \uparrow
\]

通常可以：

- 用更长的 \(L\)
- 用更小的 \(V_{OV}\)
- 降低 \(I_D\)，提高 \(r_o\)
- 使用 cascode 结构提高输出电阻

---

## 7. 小信号参数总表

| 参数 | 名称 | 定义 | 常用公式 | 直观意义 |
|---|---|---|---|---|
| \(g_m\) | 跨导 | \(\frac{\partial I_D}{\partial V_{GS}}\) | \(\frac{2I_D}{V_{OV}}\) | gate 控制 drain current 的能力 |
| \(r_o\) | 输出电阻 | \(\frac{1}{g_{ds}}\) | \(\frac{1}{\lambda I_D}\) | MOS 作为电流源的理想程度 |
| \(g_{mb}\) | 体效应跨导 | \(\frac{\partial I_D}{\partial V_{BS}}\) | \(\eta g_m\) | body 控制 drain current 的能力 |
| \(V_{TH}\) | 阈值电压 | MOS 开始强反型的电压 | body effect 会改变它 | MOS 被打开的门槛 |
| \(V_{OV}\) | 过驱动电压 | \(V_{GS}-V_{TH}\) | \(\frac{2I_D}{g_m}\) | 超过阈值的有效 gate voltage |
| \(g_m r_o\) | 本征增益 | intrinsic gain | \(\frac{2}{\lambda V_{OV}}\) | 单个 MOS 的最大增益能力 |

---

## 8. 小信号模型中最常见的等效关系

MOS 在 saturation 区的小信号漏极电流可以写成：

\[
i_d = g_m v_{gs} + g_{mb} v_{bs} + g_{ds}v_{ds}
\]

其中：

\[
g_{ds}=\frac{1}{r_o}
\]

所以：

\[
i_d = g_m v_{gs} + g_{mb} v_{bs} + \frac{v_{ds}}{r_o}
\]

---

## 9. 最核心记忆

\[
\boxed{
g_m=\frac{2I_D}{V_{OV}}
}
\]

\[
\boxed{
r_o=\frac{1}{\lambda I_D}
}
\]

\[
\boxed{
g_{mb}\approx 0.1g_m \sim 0.3g_m
}
\]

\[
\boxed{
V_{OV}=V_{GS}-V_{TH}
}
\]

\[
\boxed{
A_{v,int}=g_m r_o
}
\]

\[
\boxed{
g_m r_o=\frac{2}{\lambda V_{OV}}
}
\]

---

## 10. 一句话总结

\(g_m\) 决定 MOS 把输入电压变成电流的能力。

\(r_o\) 决定 MOS 作为电流源的理想程度。

\(g_{mb}\) 是 body effect 造成的额外控制项。

\(V_{TH}\) 是打开 MOS 的门槛。

\(V_{OV}\) 是真正推动沟道导通的有效电压。

\[
g_m r_o
\]

决定单个 MOS 管天然能提供多大的电压增益。