## Penalties in the Objective Function

- $\lambda$: hyperparameter to tune.
- $\beta$: Coefficient to optimize.

### L1 Penalty (Lasso Regularization)
- **Definition:** The L1 penalty adds the absolute values of the coefficients to the objective function.
  
- **Mathematical Formulation:** 
  $$\text{L1 Penalty} = \lambda \sum_{j=1}^{n} |\beta_j|$$
  
  where $\lambda$ is the regularization parameter, and $\beta_j$ are the model coefficients. The function has a sharp corner at zero - as the derivative is 1 (non-differentiable: all values are the same across the function w/ abrupt change in its slope).

- **Effect:** Encourages sparsity (*many coefficients = 0*), meaning it can shrink some coefficients exactly to zero, effectively performing `feature selection`.

#### Non-Differentiable
- **Definition:** A function is non-differentiable at a point if it does not have a unique tangent line at that point. In other words, the slope of the function is not well-defined at that point.
  
- **Example with Absolute Value:** The absolute value function $f(\beta) = |\beta|$ is non-differentiable at $\beta = 0$. This is because:
  $$f(\beta) = 
  \begin{cases} 
  \beta & \text{if } \beta \geq 0 \\
  -\beta & \text{if } \beta < 0 
  \end{cases}
  $$
  At $\beta = 0$, the left and right derivatives are:
  $$f'(\beta) = 
  \begin{cases} 
  1 & \text{if } \beta > 0 \\
  -1 & \text{if } \beta < 0 
  \end{cases}
  $$
  Since the left and right derivatives are not equal, the function is non-differentiable at $\beta = 0$.

#### Non-Smooth Penalty
- **Non-Smooth Penalty:** In the context of regularization, a non-smooth penalty means that the regularization term introduces points where the function is not differentiable. For L1 regularization, the penalty term is $\lambda \sum_{j=1}^{n} |\beta_j|$. The absolute value function $|\beta|$ introduces a non-smooth penalty at $\beta = 0$.

- **Effect on Optimization:** The non-smooth penalty at $\beta = 0$ encourages some coefficients to be exactly zero because the optimizer can "jump" to zero to avoid the penalty's steep increase near zero. This results in sparsity, where many coefficients are zero.


### L2 Penalty (Ridge Regularization)
- **Definition:** The L2 penalty adds the squared values of the coefficients to the objective function.
  
- **Mathematical Formulation:** 
  $$\text{L2 Penalty} = \lambda \sum_{j=1}^{n} \beta_j^2$$
  
  where $\lambda$ is the regularization parameter, and $\beta_j$ are the model coefficients. $\beta_j$ has a continuous 1st and 2nd derivative - smooth and differentiable at all points, including zero. It has a continuous derivative everywhere (well defined slope at all points).

- **Effect:** Encourages smaller coefficients by shrinking them towards zero but does not set them exactly to zero. This helps to `prevent overfitting` by discouraging large coefficient values.

#### Why is L2 Differentiable at all points?

The function $f(\beta) = \beta^2$ is differentiable at all points, including 0:

1. **Function:**
   $$f(\beta) = \beta^2$$

2. **First Derivative:**
   The derivative of $f(\beta)$ with respect to $\beta$ is:
   $$f'(\beta) = \frac{d}{d\beta} (\beta^2) = 2\beta$$

3. **Second Derivative:**
   The second derivative is:
   $$f''(\beta) = \frac{d}{d\beta} (2\beta) = 2$$

4. **Evaluation at $beta = 0$:**
   The first derivative at $beta = 0$ is:
   $$f'(0) = 2 \cdot 0 = 0$$

   The second derivative at $\beta = 0$ is:
   $$f''(0) = 2$$

Since the first derivative $f'(\beta) = 2\beta$ is continuous and well-defined at $\beta = 0$, and the second derivative $f''(\beta) = 2$ is also continuous, the function $f(\beta) = \beta^2$ is smooth and differentiable at $\beta = 0$.


### Contrast of L2 (Ridge) with L1 Regularization (Lasso)

#### L1 Penalty:
The L1 penalty term is given by:
$$\lambda \sum_{j=1}^{n} |\beta_j|$$

#### Non-Differentiability of L1 at 0:
The function $f(\beta) = |\beta|$ is not differentiable at 0. Let's demonstrate this mathematically:

1. **Function:**
   $$f(\beta) = |\beta|$$

2. **Left and Right Derivatives:**
   - For $\beta > 0$:
     $$f'(\beta) = \frac{d}{d\beta} (\beta) = 1$$
   - For $\beta < 0$:
     $$f'(\beta) = \frac{d}{d\beta} (-\beta) = -1$$

3. **Evaluation at $\beta = 0$:**
   The left derivative at $beta = 0$ is:
   $$\lim_{\beta \to 0^-} f'(\beta) = -1$$

   The right derivative at $\beta = 0$ is:
   $$\lim_{\beta \to 0^+} f'(\beta) = 1$$

Since the left and right derivatives are not equal, the function $f(\beta) = |\beta|$ is not differentiable at $\beta = 0$.

### Summary
- **L1 Penalty (Lasso):** Promotes sparsity, can set some coefficients to zero.
- **L2 Penalty (Ridge):** Promotes smaller coefficients, reduces the impact of multicollinearity (Two independent variables are highly linearly related).

- Minimizing a larger penalty term (due to larger values of λ) emphasizes smaller model parameters, leading to simpler models that might generalize better but could underfit the training data.
- Minimizing a smaller penalty term (lower values of λ) allows the model to fit the training data more closely, possibly at the expense of increased complexity and overfitting. `Almost as if there was no penalty`

### Notations

The notation $\|\delta\|_2^2$ is a standard way to express the L2 norm (Euclidean norm) squared of the vector $\delta$. Here's what each part means:

- $\delta$: A vector of parameters, in this case, related to the changes at the trend changepoints.
- $\|\delta\|_2$: The L2 norm of $\delta$, which is calculated as $\sqrt{\sum_{i} \delta_i^2}$.
- $\|\delta\|_2^2$: The squared L2 norm, which simplifies to $\sum_{i} \delta_i^2$.

So, the term $\lambda_{\delta} \|\delta\|_2^2$ is effectively:

$$\lambda_{\delta} \sum_{i} \delta_i^2$$

This is a regularization term that penalizes large values of $\delta_i$.

