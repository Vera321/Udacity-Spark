#### `Sparkify` 项目：
##### 库文件
```
# import libraries
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, lit, udf, isnan, count, when, desc, sort_array, asc, avg, lag, floor
from pyspark.sql.types import IntegerType, DateType
from pyspark.sql.window import Window
from pyspark.sql.functions import sum as Fsum
from pyspark.ml.feature import VectorAssembler
from pyspark.ml.feature import MinMaxScaler #used because won't distort binary vars
from pyspark.sql.types import DoubleType
from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
import datetime
from pyspark.ml import Pipeline 
from pyspark.ml.classification import LogisticRegression, RandomForestClassifier, LinearSVC, GBTClassifier
from pyspark.ml.evaluation import BinaryClassificationEvaluator, MulticlassClassificationEvaluator
from pyspark.mllib.evaluation import MulticlassMetrics

import matplotlib.pyplot as plt
import seaborn as sb
import time

%matplotlib inline
```

##### 数据集的特征变量
```
root
 |-- artist: string (nullable = true)
 |-- auth: string (nullable = true)
 |-- firstName: string (nullable = true)
 |-- gender: string (nullable = true)
 |-- itemInSession: long (nullable = true)
 |-- lastName: string (nullable = true)
 |-- length: double (nullable = true)
 |-- level: string (nullable = true)
 |-- location: string (nullable = true)
 |-- method: string (nullable = true)
 |-- page: string (nullable = true)
 |-- registration: long (nullable = true)
 |-- sessionId: long (nullable = true)
 |-- song: string (nullable = true)
 |-- status: long (nullable = true)
 |-- ts: long (nullable = true)
 |-- userAgent: string (nullable = true)
 |-- userId: string (nullable = true)
```

##### 结果分析
```
Random Forest
准确度: 1.0
f1分数: 1.0
验证集计算准确度与f1分数用时 23.99507474899292秒
```
```
Support Vector Machine
准确度: 1.0
f1分数: 1.0
验证集计算准确度与f1分数用时 19.415339708328247秒
```
```
Logistic Regression
准确度: 0.6666666666666666
f1分数: 0.5333333333333334
验证集计算准确度与f1分数用时 21.316346883773804秒
```
随机森林和`SVM`的准确度和f1分数都为`1.0`，很可能造成了过拟合。
逻辑回归模型的泛化能力更强。
