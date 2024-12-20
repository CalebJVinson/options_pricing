\usepackage{physics}

This project was based on a final project where I used equations for the value/price of European Options based on the Options, Futures, and derivatives by Hull and the Primer for Financial Engineering by Dan Stefanica.

# Derivation

## Assumptions of the Black-Scholes-Merton Model (Options, Futures, & Derivatives, pg. 354)


## Stock Price Process 
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

## Constructing a Portfolio to remove the Weiner process.

We define the portfolio as $\Pi$ and use:

$$\Pi = -f + \frac{\partial{f}}{\partial{S}}S$$

- as our portfolio. In this form, we represent the *-f* as the short position of a derivative and  $\frac{\partial{f}}{\partial{S}}$ as a long position on shares of the underlying. If we then allow for discrete time steps we get
