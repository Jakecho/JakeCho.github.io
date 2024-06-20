---
layout: single
title: "Classification Error of Rudner Mathod"
---
# False Positive and False Negative.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Parameters for true proficiency distribution
mu_true = -0.5  # Mean of true proficiency
sigma_true = 1.0 # Standard deviation of true proficiency
cut_score_u = 0.0 # Cut score for true proficiency

# Parameters for estimated proficiency distribution
mu_est = 0.0  # Mean of estimated proficiency
sigma_est = np.sqrt(0.5)  # Standard deviation of estimated proficiency
cut_score_t = 0.0 # Cut score for estimated proficiency

# Define theta values for the plot
theta_values = np.linspace(-3, 3, 500)

# True proficiency distribution (Normal distribution)
true_pdf = norm.pdf(theta_values, mu_true, sigma_true)

# Estimated proficiency distribution for theta = -1.0
theta_i = -1.0
est_pdf_theta_i = norm.pdf(theta_values, theta_i, sigma_est)

# False positive visualization
fig, ax = plt.subplots(figsize=(10, 6))
ax.plot(theta_values, true_pdf, label='True Proficiency Distribution', color='blue')
ax.plot(theta_values, est_pdf_theta_i, label='Estimated Proficiency Distribution for θ=-1.0', color='red')

# Fill area for false positive
false_positive_region = np.where((theta_values > cut_score_t) & (theta_values <= 3))
ax.fill_between(theta_values[false_positive_region], 0, est_pdf_theta_i[false_positive_region], color='red', alpha=0.5, label='False Positive Region')

# Add lines and labels
ax.axvline(cut_score_u, color='black', linestyle='--', label='Cut Score (u) for True Proficiency')
ax.axvline(cut_score_t, color='green', linestyle='--', label='Cut Score (t) for Estimated Proficiency')
ax.axvline(theta_i, color='purple', linestyle='--', label='True Proficiency θ=-1.0')

# Add legend and titles
ax.set_xlabel('Proficiency (θ)')
ax.set_ylabel('Probability Density')
ax.set_title('False Positive Error Visualization')
ax.legend()
ax.grid(True)

# Display the plot
plt.show()

# Parameters for true proficiency distribution for false negative example
mu_true_fn = 0.5 # Mean of true proficiency for false negative example

# Define theta values for the plot for false negative example
theta_values_fn = np.linspace(-3, 3, 500)

# True proficiency distribution (Normal distribution)
true_pdf_fn = norm.pdf(theta_values_fn, mu_true_fn, sigma_true)

# Estimated proficiency distribution for theta = 1.0
theta_i_fn = 1.0 # Estimated proficiency value for false negative example
est_pdf_theta_i_fn = norm.pdf(theta_values_fn, theta_i_fn, sigma_est)

# False negative visualization
fig, ax = plt.subplots(figsize=(10, 6))
ax.plot(theta_values_fn, true_pdf_fn, label='True Proficiency Distribution', color='blue')
ax.plot(theta_values_fn, est_pdf_theta_i_fn, label='Estimated Proficiency Distribution for θ=1.0', color='red')

# Fill area for false negative
false_negative_region = np.where((theta_values_fn < cut_score_t) & (theta_values_fn >= -3))
ax.fill_between(theta_values_fn[false_negative_region], 0, est_pdf_theta_i_fn[false_negative_region], color='red', alpha=0.5, label='False Negative Region')

# Add lines and labels
ax.axvline(cut_score_u, color='black', linestyle='--', label='Cut Score (u) for True Proficiency')
ax.axvline(cut_score_t, color='green', linestyle='--', label='Cut Score (t) for Estimated Proficiency')
ax.axvline(theta_i_fn, color='purple', linestyle='--', label='True Proficiency θ=1.0')

# Add legend and titles
ax.set_xlabel('Proficiency (θ)')
ax.set_ylabel('Probability Density')
ax.set_title('False Negative Error Visualization')
ax.legend()
ax.grid(True)

# Display the plot
plt.show()

```


    
![png](theta_dist_files/theta_dist_0_0.png)
    



    
![png](theta_dist_files/theta_dist_0_1.png)
    

