## Least Squares with Neural Network Residual Correction for SECOM Data


### I. Objective

The objective of this project is to develop a practical method for classifying passing and defective semiconductor products using the [SECOM dataset](https://archive.ics.uci.edu/dataset/179/secom) obtained from the UCI Machine Learning Repository.


### II. Files

1. `secom.data`: A data file containing 1,567 samples, each with 590 numerical sensor and process measurements.

2. `secom_labels.data`: A label file containing the corresponding quality classification and timestamp for each of the 1,567 samples, where `-1` represents a passing product and `1` represents a defective product.

3. `secom.names`: A documentation file containing general information about the SECOM dataset, including its authors, data structure, pass/fail label definitions, missing-value representation, intended classification and feature-selection tasks, and baseline results obtained using several feature-selection methods.

4. `Secom_Project.ipynb`: The main project notebook, containing data preprocessing, mathematical background, model development, experimental design, numerical implementation, results, and conclusions.


### III. Proposed Method

Rather than merely applying an off-the-shelf classifier, this project develops a hybrid model that combines least squares with neural-network to address the classification problem. 

A linear SVM is first used to rank and select relevant sensor measurements. Least squares then provides the primary linear prediction, while a small neural network learns to correct the residual errors that remain unexplained by the linear model. The final classification score is obtained by combining the least squares prediction with the neural-network correction.


### IV. Results

Compared with least squares alone, the neural-network residual correction increased the test balanced accuracy from `0.7039` to `0.7771`. It also reduced the number of passing products incorrectly classified as defective from 34 to 19, while increasing the number of correctly detected defective products from 11 to 13.


<div align="center">

<table>
  <thead>
    <tr>
      <th align="center">Metric</th>
      <th align="center"><a href="https://doi.org/10.3390/s24175461">Park et al. (2024)</a></th>
      <th align="center">Proposed WLS–NN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">Classification model</td>
      <td align="center">SVM</td>
      <td align="center">WLS with NN residual correction</td>
    </tr>
    <tr>
      <td align="center">Number of selected sensors</td>
      <td align="center">12</td>
      <td align="center">20</td>
    </tr>
    <tr>
      <td align="center">Test accuracy</td>
      <td align="center">0.8514</td>
      <td align="center"><strong>0.9140</strong></td>
    </tr>
    <tr>
      <td align="center">Passing-product recall</td>
      <td align="center">0.8682</td>
      <td align="center"><strong>0.9352</strong></td>
    </tr>
    <tr>
      <td align="center">Defective-product recall</td>
      <td align="center">0.6129</td>
      <td align="center"><strong>0.6190</strong></td>
    </tr>
    <tr>
      <td align="center">Balanced accuracy</td>
      <td align="center">0.7405</td>
      <td align="center"><strong>0.7771</strong></td>
    </tr>
    <tr>
      <td align="center">Geometric mean</td>
      <td align="center">0.7295</td>
      <td align="center"><strong>0.7609</strong></td>
    </tr>
    <tr>
      <td align="center">Defective-product precision</td>
      <td align="center">0.2468</td>
      <td align="center"><strong>0.4063</strong></td>
    </tr>
    <tr>
      <td align="center">Defective-product F1 score</td>
      <td align="center">0.3519</td>
      <td align="center"><strong>0.4906</strong></td>
    </tr>
  </tbody>
</table>

<p><strong>Table. Comparison Between the Results of Park et al. (2024) and the Proposed Hybrid Model</strong></p>

</div>

The better value for each quantitative performance metric is shown in bold. The proposed WLS–NN model achieved numerically higher values for all the listed performance metrics and therefore demonstrated competitive performance on the SECOM classification problem.

Nevertheless, this comparison should be interpreted with caution because the two studies used different training–test partitions and model-selection procedures. In addition, the test set in the present project was used for exploratory model comparison. Therefore, these results provide evidence of competitive performance rather than a strictly controlled demonstration that the proposed method outperforms the approach of [Park et al. (2024)](https://doi.org/10.3390/s24175461).
