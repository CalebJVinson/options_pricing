This project was based on a final project where I used equations for the value/price of European and American Options based on the Options, Futures, and derivatives by Hull and the Primer for Financial Engineering by Dan Stefanica. The primary method used was binomial methods for both american and european. I initially attempted the finite differences method for american options, as an alternative, but had blown up values. Since this was a final course project, and it didn't have high reliability, I removed it from the file. However, I describe the process below that I initially implemented and describe where it may have failed. Due to this project, in conjunction with others, I am completing a Numerical Analysis course in Spring 2025.

# Stock Price Process to Black Scholes 
Using the stock process typically defined, we start with:

$$dS = \mu S dt + \sigma S dz$$

### Drift Rates
where we have the $\mu S$ defined as the drift rate since we take S as the price and the parameter $\mu$ as the expected rate of return on a stock. We can easily see that without the uncertainty and variation term $\mu S dt$ we would get $\int_{0}^{T}S_T = S_0e^{\mu T}$ as a compounding of the drift rate through time T, or time to maturity.

### Volatility/Uncertainty
Our assumption, is that the variability is constant over each of the short time periods($\Delta t$) s.t. we can utilize $\sigma$ throughout the model. This follows geometric brownian motion in a discrete time model as we are operating on small intervals of $\Delta t$.

So, with that we can actually further our understanding of the process using a **call** or **put**.

## Using Ito's Lemma for the price

Let *f* represent the price of a call, where *f* is a function of S and t.

$$df = \left( \frac{\partial{f}}{\partial{S}} \mu S + \frac{\partial{f}}{\partial{t}} + \frac{1}{2} \frac{\partial{f^2}}{\partial^2{S}} \right)dt + \frac{\partial{f}}{\partial{S}} \sigma S dz$$

Using the discrete values we have $\Delta S = \mu S \Delta t + \sigma S \Delta z$. Additionally, $Delta z = \epsilon \sqrt{ \Delta t}$

which we can use to reformat *f* as:

$$\Delta f = \left( \frac{\partial{f}}{\partial{S}} \mu S + \frac{\partial{f}}{\partial{t}} + \frac{1}{2} \frac{\partial{f^2}}{\partial^2{S}} \right) \Delta t + \frac{\partial{f}}{\partial{S}} \sigma S \epsilon \sqrt{\Delta t}$$

## Constructing the option

We define the portfolio as $\Pi$ and use:

$$\Pi = -f + \frac{\partial{f}}{\partial{S}}S$$

as our portfolio. In this form, we represent the *-f* as the short position of a derivative and  $\frac{\partial{f}}{\partial{S}}$ as a long position on shares of the underlying. If we then allow for discrete time steps we get the $\Delta \Pi$ format which enables us to input $\Delta f$ for the function. Taking into account the assumptions of the model that the values will follow the near term riskless security the function collapses to a simpler $\Delta \Pi = r \Pi \Delta t$. Since we have $ \Delta \Pi$ as a formula and $ \Pi$ as a formula, we can insert them as follows:

$$\left(\frac{\partial f}{\partial S} + 0.5 \cdot \frac{\partial^2 f}{\partial S^2} \sigma^2 \S^2 \right) \Delta t = r \left(f - \frac{\partial f}{\partial S} \right) \Delta t \Rightarrow \frac{\partial f}{\partial t} + r S \frac{\partial f}{\partial S} + 0.5 \cdot \sigma^2 S^2 \frac{\partial^2 f}{\partial S^2} - rf = 0$$

Our value is $f = \text{max}(S-K,0) \text{\quad when t = T}$, which results in our option.

# Finite Difference: Attempted/Reworking

My primary error was in the conversion to a diffusion process of the values. When I worked on this project for classes, I tried to do so for the issues related to boundary problems, but I didn't understand the Black-Scholes equation's clutter caused issues in converging to a solution. While it would be easier to transition, I do want to try out another form. Since my initial attempt at the Finite Difference method was the explicit, rather than the implicit method. Since I had rather large time steps, reviewing numerical procedures later with the Options, Futures, and Other Derivatives text made me realize my likely instability of the model was due to the combination of the complexity from early exercise in american options and the lesser stability of the explicit method.  

## Crank-Nicolson Finite Difference

In the first model I used, I had semi-trustworthy results, but not robust results. This is likely due to my usage of too large $\Delta t$ combined with the explicit finite difference method. The advantage of the Crank-Nicolson is its position as an average of the implicit and explicit finite difference method. The first issue in solving this problem is to shift the BSM model into a discretized form. The main way of doing this is to use a 1/2 fraction of the prior and current values with respect to price: $\frac{f_{i-1/2, j}}{\partial S} = 0.5 \cdot \left[\frac{\partial f_{i-1,j} + \partial f_{i,j}}{\partial S} + \frac{}{\partial S} \right]$
