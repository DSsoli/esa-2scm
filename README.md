# ESA-2SCM: Elastic Segment Allocation-based 2SLS Structural Causal Model for Causal Discovery

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/DSsoli/esa-2scm/blob/main/LICENSE)

ESA-2SCM is a new method for detecting causality based on Elastic Segment Allocation-based synthetic instrumental variables with 2SLS application for estimating structural causal models. 
<br>
<br>
For details of the model design, please refer to my Original Article:

* [Lee, Sanghoon (2024). **ESA-2SCM for Causal Discovery: Causal Modeling with Elastic Segmentation-based Synthetic Instrumental Variable**, *SnB Political and Economic Research Institute,* *1,* 16. <snbperi.org/article/227>](http://www.snbperi.org/article/227)

## Model Overview
Suppose that you are interested in discovering the causal relationship between $x_1$ and $x_2$ (e.g., determining the *true causal direction*: $x_1$ -> $x_2$ vs. $x_2$ -> $x_1$, measuring the magnitude of *causal impact*):
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/1.png?raw=true", width="200"/>
</p>

Estimation of the above equation under standard OLS is *structurally* biased and inconsistent due to endogeneity:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/2.png?raw=true" width="350"/>
</p>

where
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/3.png?raw=true" width="300"/>
</p>

thus,
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/4.png?raw=true" width="500"/>
</p>


The estimators are also inconsistent, as:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/5.png?raw=true" width="310"/>
</p>


**ESA-2SCM** provides a countermeasure to such problem, enabling the determination of true *causal direction* and estimation of the true *causal coefficient* through the following procedures.
1. Vector definition:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/6.png?raw=true" width="450"/>
</p>

2. Sorting:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/7.png?raw=true" width="500"/>
</p>

3. Set initial number of segments *(M)*:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/8.png?raw=true" width="500"/>
</p>

4. Segment size allocation:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/9.png?raw=true" width="400"/>
</p>

5. Elastic adjustment algorithm for adjusting the number of segments:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/10.png?raw=true" width="580"/>
</p>

6. Grouping:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/11.png?raw=true" width="450"/>
</p>

7. Segment value assignment:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/12.png?raw=true" width="420"/>
</p>

8. Apply 2SLS using the generated Synthetic IV vectors *(Z)*: <br>
Model Specification:

<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/13.png?raw=true" width="200"/>
</p>

Get $z_1$ and  $z_2$ via applying the process (1) to (7) for  $x_1$ and  $x_2$, then perform 2SLS to estimate for:
<p align="center">
  <img src="https://github.com/DSsoli/esa-2scm/blob/main/img/14.png?raw=true" width="200"/>
</p>



## Requirements

* Python3

* numpy

* pandas

* scipy

## Installation

To install the ESA-2SCM package, use `pip` as follows:

```sh
pip install esa-2scm
```

## Example Usage

```python
import numpy as np
import pandas as pd
from esa_2scm import Esa2Scm

# For causal discovery and determination of the true causal direction, input x_1 and x_2 as follows to initialize the ESA-2SCM model:
model = Esa2Scm(x1, x2)

# Fit the model, using Synthetic IV generation method(syniv_method, default: 'ESA') to estimate causality
# Adjust the parameter M(default=2) to manually manage the degree of correlation between the Synthetic IVs (2SLS-converted) and the respective endogenous variables
model.fit(syniv_method="esa", M=2)

# To confirm the estimated causal direction:
print(model.causal_direction)

# To confirm the causal impact coefficient for the detected causal direction:
print(model.causal_coef)

# To confirm the true goodness of fit of the ESA-2SCM for determination of the causal direction:
print(model.esa2scm_score)

# With causal direction determined via ESA-2SCM, to confirm the true goodness of fit of the Regression Model using original variables:
print(model.inverse_transformed_score)

# To check the degree of correlation between the generated Synthetic IVs and the endogenous variables (x1 and x2, respectively):
print(model.corr_x1_to_slsiv)
print(model.corr_x2_to_slsiv)

# For model summary:
model.summary()
```

## Documentation
Original Article of the ESA-2SCM:
* Lee, Sanghoon (2024). **ESA-2SCM for Causal Discovery: Causal Modeling with Elastic Segmentation-based Synthetic Instrumental Variable**, *SnB Political and Economic Research Institute,* *1,* 16. <snbperi.org/article/227> [[ARTICLE LINK]](http://www.snbperi.org/article/227)

## Examples
Examples of running ESA-2SCM in Jupyter Notebook are included in [esa_2scm/examples](https://github.com/DSsoli/esa-2scm/tree/main/examples)

## License
My package is licensed under the terms of the [MIT license](https://github.com/DSsoli/esa-2scm/blob/main/LICENSE)

## References

### ESA-2SCM Package

Should you use my package to perform ESA-2SCM for causal discovery, please kindly cite my Original Article:
* Lee, Sanghoon (2024). **ESA-2SCM for Causal Discovery: Causal Modeling with Elastic Segmentation-based Synthetic Instrumental Variable**, *SnB Political and Economic Research Institute,* *1,* 16. <snbperi.org/article/227> [[ARTICLE LINK]](http://www.snbperi.org/article/227)