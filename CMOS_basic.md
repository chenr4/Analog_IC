# MOS 工作区

---

## 1.Cutoff 区：截止区

对于 NMOS：

\[
V_{GS}<V_{TH}
\]

但是实际上仍然有很小的漏电流，尤其在先进工艺里不能完全忽略。

---

## 2. Triode / Linear 区：线性区 / 三极管区

NMOS 已经打开：

\[
V_{GS}>V_{TH}
\]

同时漏源电压较小：

\[
V_{DS}<V_{GS}-V_{TH}
\]

线性区条件也可以写成：


\[
V_{DS}<V_{OV}
\]

电流公式

\[
I_D=\mu_n C_{ox}\frac{W}{L}
\left[
(V_{GS}-V_{TH})V_{DS}-\frac{V_{DS}^2}{2}
\right]
=k_n\left[V_{OV}V_{DS}-\frac{V_{DS}^2}{2}\right]
\]

小 \(V_{DS}\) 时

如果 \(V_{DS}\) 很小，二次项可以忽略：

\[
I_D \approx k_n V_{OV}V_{DS}
\]

这时候 MOS 像一个电阻：
\[
R_{on}\approx \frac{1}{k_n V_{OV}}
\]

直观理解

MOS 已经导通，但 \(V_{DS}\) 不大，沟道从 source 到 drain 都存在。

所以它像一个 **电压控制电阻**。

Gate 电压越高，\(V_{OV}\) 越大，沟道越强，等效电阻越小。

---

## 3. Saturation 区：饱和区

NMOS 已经打开：

\[
V_{GS}>V_{TH}
\]

同时：

\[
V_{DS}\ge V_{GS}-V_{TH}
\]

也就是：

\[
V_{DS}\ge V_{OV}
\]

- 电流公式，忽略 channel-length modulation

\[
I_D=\frac{1}{2}\mu_n C_{ox}\frac{W}{L}(V_{GS}-V_{TH})^2
=\frac{1}{2}k_n V_{OV}^2
\]
- 电流公式，考虑 channel-length modulation

实际中饱和区电流会随 \(V_{DS}\) 略微增加：

\[
I_D=\frac{1}{2}k_n V_{OV}^2(1+\lambda V_{DS})
\]

对应输出电阻：

\[
r_o \approx \frac{1}{\lambda I_D}
\]

直观理解

当 \(V_{DS}\) 增大到一定程度，靠近 drain 端的沟道被 pinch-off。

这不是电流停止，而是电流主要由 \(V_{GS}\) 控制，\(V_{DS}\) 影响变小。

所以饱和区 MOS 像一个 **电压控制电流源**。

这是模拟电路里最常用的工作区，例如共源放大器、电流镜、差分对等。

---

## 4. Subthreshold 区：亚阈值区

\[
V_{GS}<V_{TH}
\]

但不是完全没有电流。更准确地说，当 \(V_{GS}\) 略低于 \(V_{TH}\) 时，MOS 仍然会有扩散电流。

电流特性

亚阈值区电流近似呈指数关系：

\[
I_D \propto e^{\frac{V_{GS}}{nV_T}}
\]

其中：

\[
V_T=\frac{kT}{q}\approx 26mV
\]

\(n\) 是 subthreshold slope factor，一般大于 1。

更完整地写：

\[
I_D \approx I_0 e^{\frac{V_{GS}-V_{TH}}{nV_T}}
\]

直观理解

虽然 \(V_{GS}<V_{TH}\)，强反型沟道还没有完全形成，但仍然存在弱反型电流。

这个区域叫：

\[
\text{weak inversion}
\]

也叫：

\[
\text{subthreshold region}
\]

在低功耗模拟电路和超低功耗数字电路里很重要。

---


## 对比表

| 区域 | 条件，NMOS | 沟道状态 | MOS 像什么 | 主要用途 |
|---|---|---|---|---|
| Cutoff | \(V_{GS}<V_{TH}\) | 没有强反型沟道 | 关断开关 | 数字 OFF |
| Triode / Linear | \(V_{GS}>V_{TH}\), \(V_{DS}<V_{OV}\) | source 到 drain 沟道连续 | 电压控制电阻 | 开关导通、电阻、传输门 |
| Saturation | \(V_{GS}>V_{TH}\), \(V_{DS}\ge V_{OV}\) | drain 端 pinch-off | 电压控制电流源 | 放大器、电流镜、偏置 |
| Subthreshold | \(V_{GS}<V_{TH}\)，但有弱电流 | 弱反型 | 指数电流源 | 超低功耗电路 |

## 判断方法

对于 NMOS，先看：

### Step 1：有没有打开？

\[
V_{GS}>V_{TH}?
\]

如果没有：

\[
\text{cutoff 或 subthreshold}
\]

如果有：

\[
\text{triode 或 saturation}
\]

### Step 2：比较 \(V_{DS}\) 和 \(V_{OV}\)

\[
V_{OV}=V_{GS}-V_{TH}
\]

如果：

\[
V_{DS}<V_{OV}
\]

则：

\[
\text{triode / linear}
\]

如果：

\[
V_{DS}\ge V_{OV}
\]

则：

\[
\text{saturation}
\]

