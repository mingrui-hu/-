## Background

-   Alpha/Beta指数
    -   beta： 市场所有stocks平均涨/跌幅
    -   alpha： 所选stocks涨跌幅
-   Portofolios: 资产池
    -   每个交易时间$t$ 所选做空(short portfolio $I'$)及做多(long portfolio $I$)的票池
-   常见因子: 
    -   PE/PB/PI/MACO 

## BWSL 策略

-   BWSL - 
-   
-   buy winner sell loser

-   买入卖出策略: Zero-investiment， BWSL 

    -   净资产为0

    -   bg：美股可以`借` stocks

    -   约束: budgets $\tilde{M}$

    -   一个time step里发生的操作:

        -   At time t:

            1.   Short portfolio: 向 $whom?$ 借 $\tilde{M}$价值的股票们 $I'$, 每只股票比例$b_i{-}$

                 -   假设已知每支股票配置比例 $b_t^{-(i)}$每支股票 $i$ 买入量(volume):
                     $$
                     u_t^{-(i)} = \tilde{M} \dotproduct b_t^{-(i)} / p_t^{i}
                     $$

            2.   在一个交易时间内立刻卖出， 得到 $\tilde{M}$的资金

            3.   Long portfolio: 用step2得到的资金，购买做多的股票 $I$, 每只股票比例$b_{i}^+$
                 $$
                 u_t^{+(i)} = \tilde{M} \dotproduct b_t^{+(i)} / p_t^{i}
                 $$
                 

        -   At the end of t-holding period (t+1时的价格):

            4.   将3中的$I$ 卖出， 此时价格$p_{t+1}$ (**获得$M_t^{+}$**)
                 $$
                 \begin{align}
                 M_t^{+} &= \sum_{i=1}^I u_t^{+(i)} * p_{t+1}^{(i)} \\
                 &= \sum_{i=1}^I [\tilde{M}b_t^{+(i)}/p_t^{(i)}] * p_{t+1}^{i} \\
                 &= \sum_{i=1}^I [\tilde{M}b_t^{+(i)}](p_{t+1}^{i}/p_t^{(i)}) \\
                 &= \sum_{i=1}^I [\tilde{M}b_t^{+(i)}]z_t^{(i)}
                 \end{align}
                 $$
                 

            5.   按照$p_{t+1}$的价格 重新买入 step1中股票们 $I'$还回 (**还回 $M_t^{-}$**)
                 $$
                 \begin{align}
                 M_t^{-} &= \sum_{i=1}^{I'} u_t^{-(i)} * p_{t+1}^{(i)} 
                 \\&= \sum_{i=1}^{I'} [\tilde{M}b_t^{-(i)}/p_t^{(i)}] * p_{t+1}^{i} 
                 \\&= \sum_{i=1}^{I'} [\tilde{M}b_t^{-(i)}](p_{t+1}^{i}/p_t^{(i)}) 
                 \\&= \sum_{i=1}^{I'} [\tilde{M}b_t^{-(i)}]z_t^{(i)}
                 \end{align}
                 $$


                 ​				
                 ​					

    -   **==从买入卖出策略 推得 获益==**： 

        -   Ensemble Profit : 
            $$
            M_t = M_t^{+} - M_t^{-} = \sum_{i=1}^I [\tilde{M}b_t^{+(i)}]z_t^{(i)} - \sum_{i=1}^{I'} [\tilde{M}b_t^{-(i)}]z_t^{(i)}
            $$

        -   Strategy Core: **Relative Price Relation**

            -   只要做多的部分跌幅不超过做空部分 -> 收益

            -   只要做多的部分涨幅大于做空部分 -> 收益

            -   formally：

                -    Positive Profits require **Rate of Return** $R_t > 0$

                    -   Rate of Return
                        $$
                        \begin{align}
                        R_t &= \frac{M_t }{\tilde{M}}\\
                        &= \frac{\sum_{i=1}^I [\tilde{M}b_t^{+(i)}]z_t^{(i)} - \sum_{i=1}^{I'} [\tilde{M}b_t^{-(i)}]z_t^{(i)}}{\tilde{M}}  \\
                        &= \sum_{i=1}^I b_t^{+(i)}z_t^{(i)} - \sum_{i=1}^{I'} b_t^{-(i)}z_t^{(i)}
                        \end{align}
                        $$
                        

                    -   $\sum_{i=1}^I b_t^{+(i)} * z_t^{i} > \sum_{i=1}^I' b_t^{-(i)} * z_t^{i}$ 

                    -    Price rising rate of stock i at time t

                        -   $$
                            z_t^{(i)} = \frac{p_{t+1}^{(i)}}{p_t^{(i)}}
                            $$

                        -   正获益时， $z_t^{i}$本身并不一定 大于1或小于1 

-   收益如何衡量：

    -   Optimization Goal : **Sharpe Ratio** ($\approx \frac{mean (rate-of-return)}{std.dev.(rate-of-return)}$ ) over trajectory $\pi$
        -   $H_T = \frac{A_T - \theta}{V_T}$
        -   $A_T$  :  Avg { rate of return $R_t$  }
        -   $V_T$ : Volatility $\rightarrow$ risk of investment
            -   Note: 此处就假设 *波动大则风险大* 
        -   $\theta$ : risk-free return rate
            -   Note: Risk-free 即考虑整体股市走向， 取市场所有股票计算$R_T$均值 作为 offset, 与我们所选的portfolio的收益做比较
    -   Evaluation Measurement: consider different aspects of trading, e.g. extreme loss

-   关于为什么用RL？

    -   Q: 因为没有direct label ? 但也可以使用时间窗$T-k, T$的Sharpe Ratio 作为时间$T$ 的label? 直接建模成Supervised Regression ?
    -   (According to the paper) To consider reward over a long trajectory, allow **risk management** (note, approximately equals to reduce variance by sampling over a trajectory and normalized by std. dev.)

-   AlphaStock:

    -   Part1 : Generate Portofolio at each step $t$ based on stock features

        -   Components: 

            1.   **LSTM + HA**: History encoder: shared over all stocks

                 -   LSTM + 1 FNN attention layer,

                 -   Output: last step of LSTM(attended) as history state for stock $i$ $X_t^{i}$ 

            2.   **CANN**: model cross-assets interrelation
                 -   Basic CANN: 1 standard dot-product self-attn layer + 1 softmax + 1 transformation layer (from attn output distribution $\rightarrow$ scores) 
                 -   Price Ranking Prior: 
                     -   Use a pre-calulated price ranking prior as weights of attention scores
                     -   Eq. to subsitute positional encoding with this `price-ranking prior`
            3.   **Portofolio Generator**: 
                 -   mask Attn scores to **a binary vector $b_c$**
                 -   $len(b_c) = I (所有可选stocks)$
                 -   Steps:
                     -   ranking scores in step2 
                     -   Top-G scores(stocks) marked as long portofolio $b_c^+$
                     -   Last-G scores(stocks) marked as short portofolio $b_c^-$
                     -   In exp setting session, they select $G = \frac{1}{4} I$
                     -   Middle-position scores marked as 0
                 -   Q: 生成 binary vector 如何计算配置比例 $b_c$呢？

    -   Part2: Optimize under policy-based RL framework

        -   Reward defination: **Sharpe Ratio**
        -   Action Space (Generated portofolio from Part 1)
        -   State Space(History State $X_t$ Generated from Part1)

    -   Explanability: Sensitivity Analysis

    -   Note: 

        -   每个时刻$t$ 的即时收益只用于计算final trajectory reward, 并没有参与计算下一个state 的action space

        

