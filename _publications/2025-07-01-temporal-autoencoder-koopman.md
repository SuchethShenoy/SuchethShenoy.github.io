---
title: "Temporal Autoencoder for Identification and Predictive Control of Nonlinear Dynamics Based on Koopman Operator Theory"
collection: publications
category: conferences
permalink: /publication/2025-temporal-autoencoder
excerpt: "Temporal autoencoder-based system identification for Koopman-based predictive control."
date: 2025-07-01
venue: "American Control Conference (ACC)"
paperurl: 'https://ieeexplore.ieee.org/abstract/document/11108016'
citation: "Shenoy, S., Sharan, B., & Werner, H. (2025). <i>Temporal Autoencoder for Identification and Predictive Control of Nonlinear Dynamics based on Koopman Operator Theory</i>. American Control Conference."
---

**Abstract**  
This paper presents an approach to Model Predictive Control (MPC) for nonlinear systems by combining Koopman operator theory with autoencoder networks enhanced by temporal layers for time-delay embedding. Traditional Koopman-based methods miss temporal dependencies, so we incorporate Temporal Convolutional Networks (TCN), Long Short-Term Memory (LSTM), and Gated Recurrent Units (GRU) in the autoencoder. These layers capture spatial and temporal features, improving system identification and predictive capabilities.The framework is validated on Duffing and Van der Pol oscillators, showing that temporal models, especially TCN-based, outperform non-temporal ones in prediction and control. TCN-based Koopman MPC achieves faster settling times and better control, while non-temporal models show errors and poor control. The LSTM and GRU models exhibit oscillatory control behavior. We also introduce a python package PyKoopman-AE, which facilitates Koopman operator-based system identification using both temporal and non-temporal autoencoders.