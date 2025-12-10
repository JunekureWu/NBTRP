# NBTRP
NBTRP (Neuroblastoma Treatment-Related Prognostic signature), a tumor-driven prognostic program in neuroblastoma. <br>
### Usage
We constructed NBTRP using XGBoost (Extreme Gradient Boosting) machine learning. The trained NBTRP model can be found in the <u>*model*</u> directory.
Usage example is provided as follow:<br>
```r
library(xgboost)
xgb.fit <- readRDS("./model/xgb.fit_model.rds")
features <- xgb.fit$feature_names
#E-MTAB-8248
EMTAB_exp <- read.table("./example_data/example_E-MTAB-8248_gene_matrix.txt",sep = "\t",check.names = F,header = T)
val_x <- as.data.frame(EMTAB_exp[features,, drop = FALSE]) 
val_x <- as.data.frame(t(val_x))
val_expr_scaled <- scale(val_x)
valMat <- xgb.DMatrix(data = as.matrix(val_expr_scaled))
riskScore <- predict(xgb.fit, newdata = valMat)
```
### License
NBTRP is distributed for **academic research use only**.  
Any commercial use, distribution, or modification of this repository or its code is strictly prohibited.

