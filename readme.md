## EDA and Satistical Inference

**Project Background:**

Abalones are an economic and recreational resource that is threatened by a variety of factors 
which include: pollution, disease, loss of habitat, predation, commercial harvesting, sport 
fishing and illegal harvesting. Environmental variation and the availability of nutrients affect the 
growth and maturation rate of abalones. Over the last 20+ years it is estimated the commercial 
catch of abalone worldwide has declined in the neighborhood of 40%. Abalones are easily over 
harvested because of slow growth rates and variable reproductive success. Being able to quickly 
determine the age composition of a regional abalone population would be an important 
capability. The information so derived could be used to manage harvesting requirements.

The intent of the investigators was to predict the age of abalone from physical measurements thus avoiding the 
necessity of counting growth rings for aging. Ideally, a growth ring is produced each year of age.

**EDA:**

Exploratory data analysis to determine plausible reasons why the original study was unsuccessful in predicting abalone age based on 
physical characteristics. A random 200 samples were selected from the dataset. Scatter Plots, Histograms, Q-Q plots and boxplots were used to examine the distribution of features. 

The observational studies can hardly yield definitive or quantitative conclusions of a population. 
We can get an idea of sample distribution through different graphs; some graphs may help to reveal correlations between different parameters. 
However, we cannot yield any results of causality without quantitative data analysis of a carefully controlled experiment. 
It is very helpful in getting the big picture of data collected and identifying proper candidates for further analysis. 
For example a strong correlation between two parameters will indicate possible good predictors so that researchers can build models with a focus on these parameters.

![Alt text](/EDA1.png)

![Alt text](/EDA2.png)

![Alt text](/eda3.png)

**Statistical Inference:**

The Ratio variable is log-transformed to L_RATIO. L_Ratio exhibits better confirmance to normal distribution and it has a homogeneous variance across age class. 
The difference in normality can be observed via the histogram shapes, and the QQ plot-the logged number show a much more normally distibuted shape. 
The skewness and kurtosis also show significant difference. The Barlett test of homogeneity of variance yield significant difference (inhomogeneous) (p value less than 0.01) for Ratio by Class.
And the test for L_Ratio yield p value of 0.53- we cannot reject the null hypothesis and thus the logged ratio shows homogeneous variance across age classes.

Analysis of variance is performed with aov() on L_RATIO using CLASS and SEX as the independent variables. The interaction term is also evaluated.
The model with the interaction shows a pvalue of 0.87 for the interaction between Class and Sex, meaning that there is no strong interaction between the two variables. 
For this reason, we can safely perform modeling without the interaction term. 
As both analyses show, there are significant correlation between Class and L_Ratio, as well as Sex and L_Ratio. 
We can consider both variables affect the L_Ratio and they don’t have a strong interaction with each other.

Tukey's multiple comparisons of means is performed to evaluate the different levels of CLASS variable. Most values of this variable is significantly related to the 
variable of interest (L_Ratio). New variables are created by summing or log-transform current features. And a multiple regression model is created. 

![Alt text](/Residual.png)

The Residuals of each variable in the model is analyzed. The display of residuals of the model, as well as the skewness and kurtosis calculations, show a normally distributed pattern. 
That is one of the indications that the regression model of L_Volume, class and type is fit. The scatter plots shows no obvious pattern of residuals across different class and types. 
The box plots are also centered at 0 and are well-balanced. These graphs help to show that the model “fits”.

**ROC Curve Analysis and Recommendation:**

Construct an ROC curve by plotting (1 - prop.adults) versus (1 - prop.infants). Each point which appears corresponds to a particular volume.value. Numerically integrate the area under the ROC curve.

![Alt text](/ROC.png)

The three cutoff points shown on the ROC curve represents three different strategies, each with a compromise. 
The maximum difference in harvest rate has the highest cutoff volume and Zero A1 strategy has the lowest cutoff volume. 
The max. difference strategy harvest least percentage of adults but also least percentage of infants (lowest false positive rate). 
The zero A1 strategy is the opposite—resulting in a highest true positive but also highest false positive. T
he Equal Error cutoff is a compromise between max diff. and zero A1 cutoff.

