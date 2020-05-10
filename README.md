# DataGene - Data Transformations and Similarity Statistics

![](assets/datavis.png)

The first thing we want to do is generate various datasets and load them into a list. See [this](https://colab.research.google.com/drive/1aenzDNjZjRHdR9YO1iPBTrzoTrqYaHtQ?usp=sharing) notebook for an example of generating synthetic datasets by Turing Fellow, [Mihaela van der Schaar](https://www.turing.ac.uk/people/researchers/mihaela-van-der-schaar), Jinsung Yoon, Daniel Jarrett. As soon as we have these datasets, we load them into a list, starting with the original data.

As of now, this packakge is catering to time-series regression tasks, and more specifically input arrays with a three dimensional structure. The hope is that it will be extended to time-series classification and cross-sectional regression and classification tasks. This package can still be used for other tasks, but some functions won't apply.

```python
datasets = [org, gen_1, gen_2]
```

Installation and import modules:

```
pip install datagene
```

```python
from datagene import distance as dist          # Distance Functions
from datagene import transform as tran         # Transformation Functions
from datagene import mod_utilities as mod      # Model Development Utilities
from datagene import dist_utilities as distu   # Distance Utilities
from datagene import vis_utilities as visu     # Visualisation Utility Functions
```

As of now, you would also have to install the following package, until we find an alternative

``
pip install git+git://github.com/FirmAI-Research/ecopy.git
``


&nbsp;

# Transformation Recipes

*You have the ability to work with 2D and 3D generated data. This notebook will work with a 3D time series array. Data has to organised as samples, time steps, features, ```[i,s,f]```. If you are working with a 2D array, the data has to be organised as samples, features ```[i,f]```.*


This first recipe uses six arbitary transformations to identify the similarity of datasets. As an analogy, imagine you're importing similar looking oranges from two different countries, and you want to see whether there is a difference in the constitution of these oranges compared to the local variety your customers have gotten used to. To do that you might follow a six step process, first you press the oranges for pulp, then you boil the pulp, you then maybe sift the pulp out and drain the juice, you add apple juice to the pulp, and then add an organge concentrate back to the pulp, you then dry the concoction on a translucent petri dish and shine light through the petri dish to identify differences in patterns between the organges using various distance metrics. You might want to do the process multiple times and establish an average and possibly even a significance score. The transformation part, is the process we put the data through to be ready for similarity calculations.


From Tesseract:
---------------

```tran.mps_decomp_4_to_2()``` - Matrix-product state are as the de facto standard for the representation of one-dimensional quantum many body states.


From Tensor:
-----------------

```tran.gaf_encode_3_to_4()``` - A Gramian Angular Field is an image obtained from a time series, representing some temporal correlation between each time point. 

```tran.mrp_encode_3_to_4()``` - Recurrence Plots are a way to visualize the behavior of a trajectory of a dynamical system in phase space.

```tran.mtf_encode_3_to_4()``` - A Markov Transition Field is an image obtained from a time series, representing a field of transition probabilities for a discretized time series.

```tran.mps_decomp_3_to_2()``` - Matrix-product state are as the de facto  standard for the representation of one-dimensional quantum many body states.

```tran.jrp_encode_3_to_3()``` - A joint recurrence plot (JRP) is a graph which shows all those times at which a recurrence in one dynamical system occurs simultaneously with a recurrence in a second dynamical system

```tran.mean_3_to_2()``` - Mean aggregation at the sample level.

```tran.sum_3_to_2()``` - Sum aggregation at the sample level.

```tran.min_3_to_2()``` - Minimum aggregation at the sample level.

```tran.var_3_to_2()``` - Variation aggregation at the sample level.

```tran.tucker_decomp_3_to_2()``` - Tucker decomposition decomposes a tensor into a set of matrices and one small core tensor

```tran.parafac_decomp_3_to_2()``` - The PARAFAC decomposition may be regarded as a generalization of the matrix singular value decomposition, but for tensors.

```tran.pca_decomp_3_to_2()``` - Long to wide array conversion with a PCA Decomposition. 


From Matrix:
------------

```tran.rp_encode_2_to_3()``` - Recurrence Plots are a way to visualize the behavior of a trajectory of a dynamical system in phase space.

```tran.gaf_encode_2_to_3()``` - A Gramian Angular Field is an image obtained from a time series, representing some temporal correlation between each time point. 

```tran.mtf_encode_2_to_3()``` - A Markov Transition Field is an image obtained from a time series, representing a field of transition probabilities for a discretized time series.

```tran.pca_decomp_2_to_2()``` - Principal component analysis (PCA) is a mathematical algorithm that reduces the dimensionality of the data while retaining most of the variation in the data set.

```tran.svd_decomp_2_to_2()``` - Singular value decomposition (SVD) is a factorization of a real or complex matrix that generalizes the eigendecomposition of a square normal matrix.

```tran.qr_decomp_2_to_2()``` - QR decomposition (also called the QR factorization) of a matrix is a decomposition of the matrix into an orthogonal matrix and a triangular matrix. 

```tran.lik_kernel_2_to_2()``` - A special case of polynomial_kernel with ```degree=1``` and ```coef0=0```.

```tran.cos_kernel_2_to_2()``` - The chi-squared kernel is a very popular choice for training non-linear SVMs in computer vision applications.

```tran.pok_kernel_2_to_2()``` - The function polynomial_kernel computes the degree-d polynomial kernel between two vectors. 

```tran.lak_kernel_2_to_2()``` - The function laplacian_kernel is a variant on the radial basis function kernel.

```tran.cov_2_to_2()``` - A covariance matrix is a square matrix giving the covariance between each pair of elements of a given random vector.

```tran.corr_2_to_2()``` - A correlation matrix is a table showing correlation coefficients between sets of variables.

```tran.hist_2d_2_to_2()``` - 2D histograms are useful when you need to analyse the relationship between 2 numerical variables that have a large number of values.

```tran.pwd_2_to_2()``` - Computes the distance matrix from a vector array X and optional Y.

```tran.prp_encode_2_to_2()``` - Recurrence Plots are a way to visualize the behavior of a trajectory of a dynamical system in phase space.

```tran.pca_decomp_2_to_1()``` - Principal component analysis (PCA) is a mathematical algorithm that reduces the dimensionality of the data while retaining most of the variation in the data set.


From Vector:
---------

```tran.sig_encode_1_to_2()``` - The signature method is a transformation of a path into a sequence that encapsulates summaries of the path.

```tran.vect_extract_1_to_1()``` -  The vector extraction function calculates a large number of time series characteristics.

```tran.autocorr_1_to_1()``` - Autocorrelation is the correlation of a signal with a delayed copy of itself as a function of delay. 

Examples:
---------

#### Example Transformation Recipe Pipeline 1
There are an infinite number of ways in which you can pipe transformations. Sometimes it is better to just use one transformation at a time. Your architecture should be emperically driven. That generally means developing a knowingly bad and knowingly good synthetic dataset, and comparing them using a range of transformations and distance metrics to identify which methods best capture their difference. We have developed a very simple pipeline that can take in many datasets to perform multiple operations resulting in a range of encoded-decomposition on which various similarity statistics can be calculated. In the future, we will add more tranformations to this pipeline to help with array operations like swapping axes, transpositions, and others.

```python

def transf_recipe_1(arr):
  return (tran.pipe(arr)[tran.mrp_encode_3_to_4]()
            [tran.mps_decomp_4_to_2]()
            [tran.gaf_encode_2_to_3]()
            [tran.tucker_decomp_3_to_2]()
            [tran.qr_decomp_2_to_2]()
            [tran.pca_decomp_2_to_1]()
            [tran.sig_encode_1_to_2]()).value

recipe_1_org,recipe_1_gen_1,recipe_1_gen_2 = transf_recipe_1(datasets)

```

#### Example Transformation Recipe Pipeline 2
Here we just reorder the transformation performed in Pipeline 1, naturally leading to a different matrix output. 

```python
def transf_recipe_2(arr):
  return (tran.pipe(arr)[tran.mrp_encode_3_to_4]()
            [tran.mps_decomp_4_to_2]()
            [tran.qr_decomp_2_to_2]()
            [tran.pca_decomp_2_to_1]()
            [tran.sig_encode_1_to_2]()
            [tran.gaf_encode_2_to_3]()
            [tran.tucker_decomp_3_to_2]()).value

recipe_2_org,recipe_2_gen_1,recipe_2_gen_2 = transf_recipe_2(datasets)

```
&nbsp;

# Distance Recipes

A range of distance measures have been developed to calculate differences between 1D, 2D, and 3D arrays. A few of these methods are novel and new to academia, and would require some benchmarking in the future; they have been signed (NV). In the future, this package would be branched out to look into privacy measurements aswell.

Model (Mixed)
------------
The model includes a transformation from tensor/matrix (the input data) to the local shapley values of the same shape, as well as tranformations to prediction vectors, and feature rank vectors. 

```dist.regression_metrics()``` - Prediction errors metrics.

```mod.shapley_rank()``` + ```dist.boot_stat()``` - Statistical feature rank correlation. 

```mod.shapley_rank()``` - Feature direction divergence. (NV)

```mod.shapley_rank()``` + ```dist.stat_pval()``` - Statistical feature divergence significance. (NV)


Matrix
-----------
Transformations like Gramian Angular Field, Recurrence Plots, Joint Recurrence Plot, and Markov Transition Field, returns an image from time series. This makes them perfect candidates for image similarity measures. From this matrix section, only the first three measures, take in images, they have been tagged (IMG). From what I know, image similarity metrics have not yet been used on 3D time series data. Furthermore, correlation heatmaps, and 2D KDE plots, and a few others, also work fairly well with image similarity metrics. 

```dist.ssim_grey()``` - Structural grey image similarity index. (IMG)

```dist.image_histogram_similarity()``` - Histogram image similarity. (IMG)

```dist.hash_simmilarity()``` - Hash image similarity. (IMG)

```dist.distance_matrix_tests()``` - Distance matrix hypothesis tests. (NV)

```dist.entropy_dissimilarity()``` - Non-parametric entropy multiples. (NV)

```dist.matrix_distance()``` - Statistical and geometrics distance measures.


Vector
------------

```dist.pca_extract_explain()``` - PCA extraction variance explained. (NV)

```dist.vector_distance()``` - Statistical and geometric distance measures.

```dist.distribution_distance_map()``` - Geometric distribution distances feature map.

```dist.curve_metrics()``` - Curve comparison metrics. (NV)

```dist.curve_kde_map()``` - dist.curve_metrics kde feature map. (NV)

```dist.vector_hypotheses()``` - Vector statistical tests.


Examples
---------------

#### **Prediction Errors**
Model prediction errors can be used as a distance metric to compare datasets. We have to control for the prediction problem, which in this example is a next-day closing stock price prediction task. A model is trained on each respective dataset, and the model is tested on a real hold-out set, to identify the differences in generalised performance. For interest sake, I have also included a simple previous day prediction. This and other benchmarks help you to consider if the regression prediction task is at all worthy for comparison purposes. This method would ordinarily be considered a utility metric, as it has a supervised learning component, but it could also be indicative of similarity accross datasets. The prima facie results would indicate that generated-1 (gen_1) data are more prediction-worthy than generated-2 (gen_2) data.

```python
pred_dict = dist.regression_metrics(pred_list=[y_pred_org, y_pred_gen_1,y_pred_gen_2,org_y_vl_m1 ],name_list=["original","generated_1","generated_2","previous day"],valid=org_y_vl)
```

```

                               original	        generated_1	generated_2	previous day
explained_variance_score	0.988543	0.991786	0.989290	0.997897
max_error	                0.125190	0.115178	0.128092	0.100051
mean_absolute_error	        0.030326	0.026712	0.036038	0.010663
mean_squared_error	        0.001326	0.001017	0.001825	0.000251
mean_squared_log_error	        0.000521	0.000382	0.000592	0.000087
median_absolute_error	        0.027985	0.025136	0.033403	0.006978
r2_score	                0.987251	0.990348	0.982379	0.997897
```

#### **Statistical feature rank correlation**
This measure is based on the belief that datasets that if datasets are similar and are used to predict the same value or outcome using the same model, they will have the same or similar feature rank ordering. Because there is some inherent randomness in the model development process, the rank correlation are taken multiple times, then the orginal-original rank correlations are compared against original-generated rank correlations. A t-stat and p-value is also derived from this comparison. A low p-value would signifify a true difference. The p-values of generated datasets can be compared against eachother. 

```python
dist.boot_stat(gen_org_arr,org_org_arr)
```

```
t-stat and p-value:
Original: 0.30857142857142855, Generated: 0.15428571428571428, Difference: 0.15428571428571428

(0.8877545314489291, 0.3863818038855802)
```

#### **Statistical feature direction**
Following along from the previous method, this method trains a model on the different generated datasets. The difference is that for each real hold-out instance (row) that are used to obtain local shapley values, the generated and real data models are compared against eachother to see which one gives a higher contribution value and are given a value of 1. In aggregate each feature should as a result not deviate too far from 0.5 as it would be indicative of non-random biases. 

```python
divergence_total.mean(axis=0)
```

```
Open         0.469565
High         0.378261
Low          0.447826
Close        0.604348
Adj_Close    0.504348
Volume       0.600000
```

Because we are generating a 3D array, another axis can also be investigated, for us this would be the time step axis, again, any divergence away from 0.5 would be intial evidence of differences in dataset construction. Here we can see that time 15 to 20 (i.e., lag 8-3) seems to be diverging from the original model. This would call for further investigation. 

```python
divergence_total.mean(axis=1)
```

```
0     0.516667
1     0.533333
2     0.516667
3     0.500000
4     0.500000
5     0.516667
6     0.500000
7     0.466667
8     0.516667
9     0.516667
10    0.516667
11    0.450000
12    0.500000
13    0.483333
14    0.483333
15    0.633333
16    0.700000
17    0.616667
18    0.383333
19    0.283333
20    0.383333
21    0.500000
22    0.500000
```


#### **Statistical feature divergence significance**

This function looks at the actual overall effect size differences, this method is itterated multiple times, and as a result of the random component, we can obtain t-stats p-value and. We can see that here, there is no statistically significant element-wise differences in local feature contributions accross any of the features in the third axis. Here like before, we can also investigate the time-step axis, or even a matrix looking at both dimensions. These methods will be made available in future iterations. 

```python
un_var_t, df_pval = dist.stat_pval(single_org_total,single_gen_total)
```

```
Open         0.159681
High         0.941508
Low          1.134092
Close       -1.335381
Adj_Close    1.351427
```

```
Open       0.87386
High       0.35159
Low        0.26290
Close      0.18862
Adj_Close  0.18347
```

#### **Structural grey image similarity**

```python
dist.ssim_grey(gray_org,gray_gen_1)
```

```
Image similarity: 0.3092467224082394
Image similarity: 0.21369506433133445
```

 #### **Histogram image similarity**
```python
dist.image_histogram_similarity(visu.array_3d_to_rgb_image(rp_sff_3d_org), visu.array_3d_to_rgb_image(rp_sff_3d_gen_1) ))
```
```
Recurrence
25.758089344255847
17.455374649851166
```
#### **Hash image similarity**

```python
print(dist.hash_simmilarity(visu.array_4d_to_rgba_image(mtf_fsdd_4d_org),  visu.array_4d_to_rgba_image(mtf_fsdd_4d_gen_1)))
print(dist.hash_simmilarity(visu.array_4d_to_rgba_image(mtf_fsdd_4d_org),  visu.array_4d_to_rgba_image(mtf_fsdd_4d_gen_2)))
```
```
51.5625
40.625
```

#### **Distance matrix hypothesis tests**
```python
pvalue, stat = dist.distance_matrix_tests(pwd_ss_2d_org,pwd_ss_2d_gen_1)
```

```
{'mantel': 0.0, 'procrustes': 0.0, 'rda': -0.0}
{'mantel': 0.5995869421294606, 'procrustes': 0.4925792204150222, 'rda': 0.9999999999802409}
```

#### **Non-parametric entropy multiples**

```python
diss_np_one = dist.entropy_dissimilarity(org.var(axis=0),gen_1.var(axis=0)); print(diss_np_one)
```
```
OrderedDict([('incept_multi', 0.00864), ('cent_multi', 0.25087), ('ctc_multi', 28.56361), ('corexdc_multi', 0.14649), ('ctcdc_mult', 0.15839), ('mutual_mult', 0.32102), ('minfo', 0.91559)])
```

#### **Statistical and geometrics distance measures**
```python
dist.matrix_distance(recipe_2_org,recipe_2_gen_1)
```
```
OrderedDict([('correlation', 0.00039),
             ('intersection', 0.0),
             ('renyi_divergence', nan),
             ('pearson_rho', 0.0),
             ('jensen_shannon_divergence', nan),
             ('ks_statistic_kde', 0.09268),
             ('js_metric', 0.12354),
             ('dice', 1.75803),
             ('kulsinski', 0.00031),
             ('rogerstanimoto', 0.15769),
             ('russellrao', 5.46193),
             ('sokalmichener', 0.15769),
             ('sokalsneath', 0.00472),
             ('yule', 0.0372),
             ('braycurtis', 0.19269),
             ('directed_hausdorff', 5.38616),
             ('manhattan', 7.19403),
             ('chi2', 0.62979),
             ('euclidean', 5.64465),
             ('variational', 7.19403),
             ('kulczynski', nan),
             ('bray', 0.1941),
             ('gower', 0.33268),
             ('hellinger', 0.02802),
             ('czekanowski', 0.55339),
             ('whittaker', 0.00501),
             ('canberra', 4.44534)])
```

#### **PCA extraction variance explained**

```python
dist.pca_extract_explain(np.sort(y_pred_org.mean(axis=1)),np.sort(y_pred_gen_1.mean(axis=1)))
```

```
PCA Error: 0.07666231511948172, PCA Correlation: 0.9996278922766885, p-value: 8.384146445855097e-14

(0.07666231511948172, 0.9996278922766885, 8.384146445855097e-14)
```

Statistical and geometric distance measures**

```
braycurtis	canberra	correlation	  cosine	dice	       euclidean	...
Iteration_0	0.101946	318.692930	0.030885	0.019464	0.571581	...
Iteration_1	0.097229	306.932707	0.028121	0.017263	0.556409	...
Iteration_2	0.102882	314.205121	0.031078	0.019340	0.602853	...
Iteration_3	0.094278	304.127560	0.028063	0.017154	0.535805	...
Iteration_4	0.097794	325.415987	0.029636	0.018002	0.566395    ...
```

#### **Geometric distribution distances feature map**

```python
vect_gen_dens_dist, vect_org_dens_dist = dist.distribution_distance_map(pd.DataFrame(org.mean(axis=(1)),columns=f_names),pd.DataFrame(gen_1.mean(axis=(1)),columns=f_names),f_names)
```

```

           	Open    	High    	Low             Close   	Adj_Close       Volume 
braycurtis 	0.584038 	0.586344 	0.591567 	0.582749 	0.587926 	0.725454
canberra 	9.810338 	9.941922 	10.033852 	9.815635 	9.960998 	14.140223
correlation 	0.877240 	0.823857 	0.823024 	0.826746 	0.813448 	1.145181
... 	... 	... 	... 	... 	... 	...
```

#### **Curve comparison metrics**

```python
dist.curve_metrics(matrix_org_s, matrix_gen_s_1)
```

```
{'Area Between Curves': 0.60957,
 'Curve Length Difference': 25.60853,
 'Discrete Frechet Distance': 2.05938,
 'Dynamic Time Warping': 217.50606,
 'Mean Absolute Difference': 0.53275,
 'Partial Curve Mapping': 159.14488}
 ```
 
#### **Curve KDE Map**
```python
vect_org_dens_curve = dist.curve_kde_map(df_org_2d_flat.sample(frac=frac).astype('double'),df_org_2d_flat.sample(frac=frac).astype('double'), f_names, 0.01)
```

```
                                  Open	        High	        Low	        Close	        Adj_Close	  Volume
Curve Length Difference	          0.499444	0.513556	0.518112	0.526037	0.527647	0.351608
Partial Curve Mapping	          0.366652  	0.362188	0.359239	0.373632	0.366966	0.296968
Discrete Frechet Distance         0.090328	0.092736	0.090900	0.093791	0.093466	0.073793
Dynamic Time Warping	          1.898949  	2.055921	1.914067	2.013428	1.969417	1.789365
Area Between Curves	          0.035566	0.036917	0.035882  	0.036786	0.036718	0.031578
```

 
#### **Vector statistical tests**

```python
 dict_sta, dict_pval  = dist.vector_hypotheses(matrix_org[:, 1],matrix_gen_1[:, 1])
```

```
Statistic
{'pearsonr': 0.6489227957382259, 'ranksums': -267.40109998538, 'mood': 74.66159732420131, 'fligner': 18979.312108773225, 'ansari': 547045501353.0, 'bartlett': 299084.5868101086, 'levene': 15724.282328938525, 'mannwhitneyu': 432539640953.0}
P-Value
{'pearsonr': 0.0, 'ranksums': 0.0, 'mood': 0.0, 'fligner': 0.0, 'ansari': 3.880810985159465e-35, 'bartlett': 0.0, 'levene': 0.0, 'mannwhitneyu': 0.0}

```

### Parting Notes

**Methods**

The purpose of this package is to compare datasets for similarity. Why would we be interested in dataset-similarity and not just the utility or predictive quality of the data? The most important reason is to preserve the interpretability of the results. If the sole purpose of the generated data is to be used in black-box machine learning models, then simillarity is not a prerequisite, but for just about any other reason, data similarity is a must. Think along the lines of feature importance scores, data exploration, causal and associative analysis, decision-making, anomaly detection, scenario analysis, and software development.

There is a slight difference between testing dataset quality and testing models performance using data, for datasets comparison we test one dataset versus many, for models it is many datasets versus many datasets. In which case you might move into high-order tensors like tessaracts. Whether you want to compare a few datasets or series of datasets, this package would enable you to move into the appropriate dimension.

Datasets can largely be compared using quantitative and visual methods. Generated data can take on many formats, it can consist of multiple dimensions of various widths and heights. Original and generated datasets have to be transformed into an acceptable format before they can be compared, these transformation sometimes leads to a reduction in array dimensions. There are two reasons why we might want to reduce array dimensions, the first is to establish an acceptable format to perform distance calculations; the second is the preference for comparing like with like. The concatenated samples in a generated array are assumed independent from that of the original data and an aggregation across all samples could lead to more accurate and interpretable distance statistics. For that reason, data similarity is a function, of not just distance calculations and statistics, but also data transformations.

**Motivation**

The reason why one would want to emphasise data relationships is the importance of data integrity in the data science process. Generating data that preserves the predictive signal but increases the relationship noise might be beneficial for a black-box prediction task, but that is about it. 

This method is predicated on two ideas; the first being that certain distance and statistical metrics are only available, or are best tested, on data-structures of specific dimensions; the second, that lower and higher dimensional representations of data might lead to a better understanding of non-linear relationships within the data. 

Input data therefore generally requires a transformation (i.e. covariance matrix) plus a distance metric between the two transformed datasets in question (average element-wise euclidean distance). In such a way, one can develop transformation-distance recipes that best capture differences in you data. 

The benefit of an approach that catalogues various methods, is that the effectiveness of various transormation plus distance recipes can be tested against data that have been generated with known to be optimal vs non-optimal procedures by comparing the learning curves of discriminator and generator losses over time. One would then be able to emperically validate the performance of every distinct recipe. 

This package would eventually carry two streams of data statistics, those for time-series and those from cross-sectional data. 

**Transformations**

For most distance measures, we would prefer non-sample specific comparisons. Real versus generated sample-specific distance could be usefull as a measure of the overall bias of the generated data. Generally we also want to focus on the relationships and not just feature (columnular) bias, in which case it is important that the transformations blend the samples into the lower dimension for a row-agnostic comparison. Decomposition helps to decrease the data-structure dimensionality, and encoding increases it. A recipe could theoretically transform the data-structure up a dimension and brings it down again, and by virtue of this process could help to expose non-linear relationships.

Multivariate time series data are generally generated as chunks of two dimensional arrays. These chunks can be captured in an additional dimension to create a rank three tensor. In such a scenario we might face a problem because of a lack of tensor comparison techniques. In other circumstances, one might start with a lower dimensional array but have the need to identify higher dimensional relationships and therefore perform encoding functions that lead to high-dimensional data structures. 

Either way, there is a need to transform data to a lower acceptable dimensions to perform similarity calculations. For that reason we might want to transform a tesseract to a cubed tensor, a tensor to a matrix, and a matrix to a vector. With each additional transformation data similarity techniques become easier to perform. To do this we can use factorization, aggregation and other customised techniques. Some distance metrics have been adapted into statistical tests, the benefit of statistical tests is that we can set thresholds for what we will be comfortable with. We can also set thresholds with standardised data.


***Types of Transformations:***
1. Data transformations to blend in samples\*. (preferred)
1. Transformations to decrease feature dimensions. (sometimes preferred)
1. Additional transformations for distance functions. (sometimes needed)
1. Additional transformations for hypotheses tests. (sometimes needed)

Example of Blend Operations:
1. KDE lines.
1. Sort of data.
1. Cummulative sum. 
1. PCA on Features. 
1. 2D Histogram.


\*Moving away from element-wise sample comparison towards structured comparisons.

**GAN Methods**

Using GAN methods, we can reproduce or generate data of any dimensional type. Before the generation of synthetic datasets, we generally have an idea of the type of problem we want to solve. If it is a prediction problem that requires the anonimisation of data, one might prefer to generate data in a prediction-ready format.

In this example, the generated data is prepackaged for a prediction problem. It contains the standard 6 market data features, including the different price attributes (close, open etc.) and volume for a time series of Google's Stocks price for 3661 days. The generated data is constructed such that it looks back for 24 time-steps. We therefore have a three-dimensional data structure (array) when we include the sample dimension.

The first step in the comparison process is to ensure that all the data fits within one data structure, as this is a requirement for future transformation and distance metrics. Each of the above arrays, the generated version (gen_1) and the real verion (org) consists of 3661 samples of 2D arrays (matrices) with six features and 24 time steps each. In total the size is 3661 x 6 x 24 (527184.

We largely want to compare these two groups of data to identify how simlilar they are. What follows are some techniques that can facilitate this test for similarity. In a sense this then are not simply a library for comparison, but a library for data transformation, distance measurement, and statistical tests. Because we are working with distance metrics, it is better to normalise the datasets from the get go.

**Visualisations**

As a sanity test, I have also provided for a few plots of the data. See the Colab notebook for examples.  


*This package draws inspiration from a range of methods developed or expounded on by researchers outside and inside the Turing ([signitures](https://www.turing.ac.uk/research/interest-groups/rough-paths), [sktime](https://github.com/alan-turing-institute/sktime) and [quipp](https://github.com/alan-turing-institute/QUIPP-pipeline)). The data has been generated in the following [Colab](https://colab.research.google.com/drive/1_jrYUR7Rwl-8vGSAEFt4hSiXmUZf040g?usp=sharing); the model has been developed by Turing Fellow, [Mihaela van der Schaar](https://www.turing.ac.uk/people/researchers/mihaela-van-der-schaar).*

