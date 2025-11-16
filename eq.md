### Mathematical Equations for Training Configurations

#### 1. CrossEntropyLoss (with Balanced Class Weights)

Cross-entropy loss is commonly used for classification problems. For a binary classification problem (like ours with Benign/Malignant), it's often referred to as Binary Cross-Entropy (BCE) loss. When dealing with imbalanced datasets, balanced class weights are incorporated to give more importance to under-represented classes during training.

The general formula for Cross-Entropy Loss for a single sample is:

$$L(y, \hat{y}) = -[y \log(\hat{y}) + (1 - y) \log(1 - \hat{y})]$$

Where:
*   $y$ is the true binary label (0 or 1)
*   $\hat{y}$ is the predicted probability of the positive class (malignant)

With balanced class weights, the loss for each class is scaled. Let $w_0$ be the weight for the benign class and $w_1$ for the malignant class. The weighted loss for a single sample becomes:

$$L_{weighted}(y, \hat{y}) = -[w_0 (1 - y) \log(1 - \hat{y}) + w_1 y \log(\hat{y})]$$

And the overall loss for a batch is the average of these weighted losses:

$$L_{total} = \frac{1}{N} \sum_{i=1}^{N} L_{weighted}(y_i, \hat{y}_i)$$

Where $N$ is the batch size.

The `compute_class_weight` function from `sklearn.utils` calculates these weights as:

$$w_c = \frac{\text{total samples}}{\text{number of classes} \times \text{number of samples in class } c}$$

#### 2. Adam Optimizer

Adam (Adaptive Moment Estimation) is an optimization algorithm that combines ideas from RMSprop and AdaGrad. It computes adaptive learning rates for each parameter.

For a parameter $\theta_t$ at time step $t$, the update rule is as follows:

1.  **Initialize moments:**
    *   First moment vector (mean of gradients): $m_0 = 0$
    *   Second moment vector (uncentered variance of gradients): $v_0 = 0$

2.  **Compute gradients:** $g_t = \nabla_{\theta} J(f(\theta_{t-1}))$, where $J$ is the loss function.

3.  **Update biased first and second moment estimates:**
    *   $m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t$
    *   $v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t$

4.  **Compute bias-corrected first and second moment estimates:**
    *   $\hat{m}_t = \frac{m_t}{1 - \beta_1^t}$
    *   $\hat{v}_t = \frac{v_t}{1 - \beta_2^t}$

5.  **Update parameters:**
    *   $\theta_t = \theta_{t-1} - \alpha \frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon}$

Where:
*   $\alpha$ is the learning rate (e.g., $1e-4$ in our case).
*   $\beta_1, \beta_2$ are exponential decay rates for the moment estimates (typically $0.9$ and $0.999$, respectively).
*   $\epsilon$ is a small constant to prevent division by zero (typically $1e-8$).
*   $t$ is the current time step (or epoch).

Adam is chosen for its efficiency and good performance across a wide range of deep learning tasks, as it effectively handles sparse gradients and noisy data.