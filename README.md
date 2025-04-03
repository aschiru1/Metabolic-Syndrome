                                            #Hypothesis
Ho: There is no significant association between demographic and health factors with metabolic syndrome. Ha: There is a significant association between demographic and health factors with metabolic syndrome.

library(dplyr)
## Warning: package 'dplyr' was built under R version 4.3.3
## 
## Attaching package: 'dplyr'
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
library(ggplot2)
## Warning: package 'ggplot2' was built under R version 4.3.3
df<-read.csv('C:/Users/ashac/OneDrive - Indiana University/Third Semester/Security and Privacy/Second Semester/Applied Statistics/Metabolic Syndrome.csv')
head(df)
##    seqn Age    Sex Marital Income  Race WaistCirc  BMI Albuminuria UrAlbCr
## 1 62161  22   Male  Single   8200 White      81.0 23.3           0    3.88
## 2 62164  44 Female Married   4500 White      80.1 23.2           0    8.55
## 3 62169  21   Male  Single    800 Asian      69.6 20.1           0    5.07
## 4 62172  43 Female  Single   2000 Black     120.4 33.3           0    5.22
## 5 62177  51   Male Married     NA Asian      81.1 20.1           0    8.13
## 6 62178  80   Male Widowed    300 White     112.5 28.5           0    9.79
##   UricAcid BloodGlucose HDL Triglycerides MetabolicSyndrome
## 1      4.9           92  41            84                 0
## 2      4.5           82  28            56                 0
## 3      5.4          107  43            78                 0
## 4      5.0          104  73           141                 0
## 5      5.0           95  43           126                 0
## 6      4.8          105  47           100                 0
#Checking the missing values
col_missing <- colSums(is.na(df))
col_missing
##              seqn               Age               Sex           Marital 
##                 0                 0                 0                 0 
##            Income              Race         WaistCirc               BMI 
##               117                 0                85                26 
##       Albuminuria           UrAlbCr          UricAcid      BloodGlucose 
##                 0                 0                 0                 0 
##               HDL     Triglycerides MetabolicSyndrome 
##                 0                 0                 0
#Dropping Un-necessary columns
Metabolic_Syndrome<-select(df, -c(WaistCirc, Albuminuria, UrAlbCr, Marital, Triglycerides, Income))
head(Metabolic_Syndrome)
##    seqn Age    Sex  Race  BMI UricAcid BloodGlucose HDL MetabolicSyndrome
## 1 62161  22   Male White 23.3      4.9           92  41                 0
## 2 62164  44 Female White 23.2      4.5           82  28                 0
## 3 62169  21   Male Asian 20.1      5.4          107  43                 0
## 4 62172  43 Female Black 33.3      5.0          104  73                 0
## 5 62177  51   Male Asian 20.1      5.0           95  43                 0
## 6 62178  80   Male White 28.5      4.8          105  47                 0
summary(Metabolic_Syndrome)
##       seqn            Age            Sex                Race          
##  Min.   :62161   Min.   :20.00   Length:2401        Length:2401       
##  1st Qu.:64591   1st Qu.:34.00   Class :character   Class :character  
##  Median :67059   Median :48.00   Mode  :character   Mode  :character  
##  Mean   :67031   Mean   :48.69                                        
##  3rd Qu.:69495   3rd Qu.:63.00                                        
##  Max.   :71915   Max.   :80.00                                        
##                                                                       
##       BMI          UricAcid       BloodGlucose        HDL        
##  Min.   :13.4   Min.   : 1.800   Min.   : 39.0   Min.   : 14.00  
##  1st Qu.:24.0   1st Qu.: 4.500   1st Qu.: 92.0   1st Qu.: 43.00  
##  Median :27.7   Median : 5.400   Median : 99.0   Median : 51.00  
##  Mean   :28.7   Mean   : 5.489   Mean   :108.2   Mean   : 53.37  
##  3rd Qu.:32.1   3rd Qu.: 6.400   3rd Qu.:110.0   3rd Qu.: 62.00  
##  Max.   :68.7   Max.   :11.300   Max.   :382.0   Max.   :156.00  
##  NA's   :26                                                      
##  MetabolicSyndrome
##  Min.   :0.0000   
##  1st Qu.:0.0000   
##  Median :0.0000   
##  Mean   :0.3424   
##  3rd Qu.:1.0000   
##  Max.   :1.0000   
## 
#PREPROCESSING (Only BMI has 26 null values)
Metabolic_Syndrome <- Metabolic_Syndrome[!is.na(Metabolic_Syndrome$BMI), ]
summary(Metabolic_Syndrome)
##       seqn            Age            Sex                Race          
##  Min.   :62161   Min.   :20.00   Length:2375        Length:2375       
##  1st Qu.:64563   1st Qu.:34.00   Class :character   Class :character  
##  Median :67058   Median :48.00   Mode  :character   Mode  :character  
##  Mean   :67028   Mean   :48.67                                        
##  3rd Qu.:69501   3rd Qu.:63.00                                        
##  Max.   :71915   Max.   :80.00                                        
##       BMI          UricAcid       BloodGlucose        HDL        
##  Min.   :13.4   Min.   : 1.800   Min.   : 39.0   Min.   : 14.00  
##  1st Qu.:24.0   1st Qu.: 4.500   1st Qu.: 92.0   1st Qu.: 43.00  
##  Median :27.7   Median : 5.400   Median :100.0   Median : 51.00  
##  Mean   :28.7   Mean   : 5.481   Mean   :108.3   Mean   : 53.36  
##  3rd Qu.:32.1   3rd Qu.: 6.400   3rd Qu.:110.0   3rd Qu.: 62.00  
##  Max.   :68.7   Max.   :11.300   Max.   :382.0   Max.   :156.00  
##  MetabolicSyndrome
##  Min.   :0.000    
##  1st Qu.:0.000    
##  Median :0.000    
##  Mean   :0.344    
##  3rd Qu.:1.000    
##  Max.   :1.000
#COUNT OF NUMBER OF ROWS
nrow(Metabolic_Syndrome)
## [1] 2375
#TYPE OF DATA
str(Metabolic_Syndrome)
## 'data.frame':    2375 obs. of  9 variables:
##  $ seqn             : int  62161 62164 62169 62172 62177 62178 62184 62189 62195 62199 ...
##  $ Age              : int  22 44 21 43 51 80 26 30 35 57 ...
##  $ Sex              : chr  "Male" "Female" "Male" "Female" ...
##  $ Race             : chr  "White" "White" "Asian" "Black" ...
##  $ BMI              : num  23.3 23.2 20.1 33.3 20.1 28.5 22.1 22.4 28.2 28 ...
##  $ UricAcid         : num  4.9 4.5 5.4 5 5 4.8 5.4 6.7 6.7 6 ...
##  $ BloodGlucose     : int  92 82 107 104 95 105 87 83 94 100 ...
##  $ HDL              : int  41 28 43 73 43 47 61 48 46 35 ...
##  $ MetabolicSyndrome: int  0 0 0 0 0 0 0 0 0 1 ...
# Assuming 'Metabolic_Syndrome' is the name of your dataset

# Boxplot for Age
boxplot(Metabolic_Syndrome$Age,
        main = "Boxplot of Age",
        ylab = "Age",
        col = "lightblue",
        border = "black"
)


# Boxplot for Blood Glucose Level
boxplot(Metabolic_Syndrome$BloodGlucose,
        main = "Boxplot of Blood Glucose",
        ylab = "Blood Glucose ",
        col = "lightgreen",
        border = "black"
)


# Boxplot for BMI
boxplot(Metabolic_Syndrome$BMI,
        main = "Boxplot of BMI",
        ylab = "BMI",
        col = "lightpink",
        border = "black"
)


boxplot(Metabolic_Syndrome$HDL,
        main = "Boxplot of HDL",
        ylab = "HDL",
        col = "yellow",
        border = "black"
)


boxplot(Metabolic_Syndrome$UricAcid,
        main = "Boxplot of UricAcid",
        ylab = "Uric Acid ",
        col = "purple",
        border ="black")


# Counting the number of outliers
count_outliers <- function(data, column_name) {
  # Calculate the first and third quartiles
  q1 <- quantile(data[[column_name]], 0.25)
  q3 <- quantile(data[[column_name]], 0.75)
  
  # Calculate the interquartile range (IQR)
  iqr <- q3 - q1
  
  # Define the lower and upper bounds for outliers
  lower_bound <- q1 - 1.5 * iqr
  upper_bound <- q3 + 1.5 * iqr
  
  # Identify outliers
  outliers <- data[[column_name]] < lower_bound | data[[column_name]] > upper_bound
  
  # Count the number of outliers
  num_outliers <- sum(outliers)
  
  # Return the count of outliers
  return(num_outliers)
}


# Count outliers for BMI
num_outliers_bmi <- count_outliers(Metabolic_Syndrome, "BMI")
cat("Number of outliers for BMI:", num_outliers_bmi, "\n")
## Number of outliers for BMI: 67
# Count outliers for Blood Glucose Level
num_outliers_bg <- count_outliers(Metabolic_Syndrome, "BloodGlucose")
cat("Number of outliers for Blood Glucose Level:", num_outliers_bg, "\n")
## Number of outliers for Blood Glucose Level: 218
num_outliers_hdl <- count_outliers(Metabolic_Syndrome, "HDL")
cat("Number of outliers for HDL:", num_outliers_hdl, "\n")
## Number of outliers for HDL: 53
num_outliers_bg <- count_outliers(Metabolic_Syndrome, "UricAcid")
cat("Number of outliers for UricAcid:", num_outliers_bg, "\n")
## Number of outliers for UricAcid: 29
#Capping outliers for required columns.
# Function to cap outliers for specified columns
cap_outliers <- function(data, columns) {
  for (col in columns) {
    # Calculate the first and third quartiles
    q1 <- quantile(data[[col]], 0.25)
    q3 <- quantile(data[[col]], 0.75)
  
    # Calculate the interquartile range (IQR)
    iqr <- q3 - q1
  
    # Define the lower and upper bounds for outliers
    lower_bound <- q1 - 1.5 * iqr
    upper_bound <- q3 + 1.5 * iqr
  
    # Cap outliers
    data[[col]][data[[col]] < lower_bound] <- lower_bound
    data[[col]][data[[col]] > upper_bound] <- upper_bound
  }
  
  # Return the updated dataset
  return(data)
}

# Columns to cap outliers for (e.g., "BMI" and "BloodGlucoseLevel")
columns <- c("BMI", "BloodGlucose", "HDL", "UricAcid")

# Cap outliers for specified columns
Metabolic_Syndrome_final <- cap_outliers(Metabolic_Syndrome, columns)

# View the updated dataset
head(Metabolic_Syndrome_final)
##    seqn Age    Sex  Race  BMI UricAcid BloodGlucose HDL MetabolicSyndrome
## 1 62161  22   Male White 23.3      4.9           92  41                 0
## 2 62164  44 Female White 23.2      4.5           82  28                 0
## 3 62169  21   Male Asian 20.1      5.4          107  43                 0
## 4 62172  43 Female Black 33.3      5.0          104  73                 0
## 5 62177  51   Male Asian 20.1      5.0           95  43                 0
## 6 62178  80   Male White 28.5      4.8          105  47                 0
#boxplot after capping
boxplot(Metabolic_Syndrome_final$BMI,
        main = "Boxplot of BMI",
        ylab = "BMI",
        col = "lightgreen",
        border = "black"
)


boxplot(Metabolic_Syndrome_final$BloodGlucose,
        main = "Boxplot of BloodGlucose",
        ylab = "BloodGlucose",
        col = "lightpink",
        border = "black"
)


boxplot(Metabolic_Syndrome_final$HDL,
        main = "Boxplot of HDL",
        ylab = "HDL",
        col = "yellow",
        border = "black"
)


boxplot(Metabolic_Syndrome_final$UricAcid,
        main = "Boxplot of UricAcid",
        ylab = "Uric Acid ",
        col = "purple",
        border ="black")


#contigency table for categorical variables
addmargins(table(Sex = Metabolic_Syndrome_final$Sex , Metabolicsyndrome= Metabolic_Syndrome_final$MetabolicSyndrome))
##         Metabolicsyndrome
## Sex         0    1  Sum
##   Female  797  400 1197
##   Male    761  417 1178
##   Sum    1558  817 2375
addmargins(table(Race = Metabolic_Syndrome_final$Race , Metabolicsyndrome= Metabolic_Syndrome_final$MetabolicSyndrome))
##              Metabolicsyndrome
## Race             0    1  Sum
##   Asian        264   81  345
##   Black        363  179  542
##   Hispanic     153  102  255
##   MexAmerican  146  103  249
##   Other         44   17   61
##   White        588  335  923
##   Sum         1558  817 2375
#Visualisations

#Distribution of Age
library(ggplot2)
ggplot(data = Metabolic_Syndrome_final, aes(x = Age)) +
  geom_histogram(binwidth = 5, fill = "skyblue", color = "black") +
  labs(title = "Distribution of Age", x = "Age", y = "Frequency")


library(ggplot2)

# Define the intervals or values you want to display on the x-axis
custom_breaks <- c(80, 85, 90, 95, 100, 105, 110, 115, 120)

# Create a ggplot bar plot with custom x-axis breaks and space between intervals
ggplot(data = Metabolic_Syndrome_final, aes(x = factor(BloodGlucose))) +
  geom_bar(fill = "lightcoral") +
  labs(title = "Distribution of Blood Glucose Levels", x = "Blood Glucose Level", y = "Count") +
  scale_x_discrete(breaks = custom_breaks) +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust = 1))


ggplot(data = Metabolic_Syndrome_final, aes(x = factor(MetabolicSyndrome), y = HDL, fill = factor(MetabolicSyndrome))) +
  geom_violin(trim = FALSE) +
  labs(title = "Distribution of HDL by Metabolic Syndrome", x = "Metabolic Syndrome", y = "HDL") +
  scale_fill_manual(values = c("0" = "lightblue", "1" = "lightgreen")) +
  theme_minimal()


library(ggplot2)

sex_counts <- table(Metabolic_Syndrome_final$Sex)
sex_data <- data.frame(Sex = names(sex_counts), Count = as.numeric(sex_counts))

ggplot(data = sex_data, aes(x = "", y = Count, fill = Sex)) +
  geom_bar(width = 1, stat = "identity") +
  coord_polar("y", start = 0) +
  labs(title = "Distribution by Sex", fill = "Sex") +
  theme_void() +
  scale_fill_manual(values = c("Female" = "pink", "Male" = "skyblue"))


ggplot(data = Metabolic_Syndrome_final, aes(x = Race, fill = factor(MetabolicSyndrome))) +
  geom_bar(position = "dodge", width = 0.7) +
  labs(title = "Distribution of Metabolic Syndrome by Race", x = "Race", y = "Count") +
  scale_fill_manual(values = c("0" = "lightblue", "1" = "lightgreen"), name = "Metabolic Syndrome") +
  theme_minimal()


# Box plot for BMI vs Metabolic Syndrome
ggplot(data = df, aes(x = factor(MetabolicSyndrome), y = BMI, fill = factor(MetabolicSyndrome))) +
  geom_boxplot() +
  labs(title = "Distribution of BMI with Metabolic Syndrome",
       x = "Metabolic Syndrome", y = "BMI", fill = "Metabolic Syndrome") +
  scale_fill_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  theme_minimal()
## Warning: Removed 26 rows containing non-finite outside the scale range
## (`stat_boxplot()`).


# Scatter plot for Age vs HDL with Metabolic Syndrome
ggplot(data = df, aes(x = Age, y = HDL, color = factor(MetabolicSyndrome))) +
  geom_point() +
  labs(title = "Relationship between Age, HDL Levels, and Metabolic Syndrome",
       x = "Age", y = "HDL Level", color = "Metabolic Syndrome") +
  scale_color_manual(values = c("blue", "red"), labels = c("No", "Yes")) +
  theme_minimal()


library(ggplot2)

# Create a density plot for the 'UricAcid' variable
ggplot(data = df, aes(x = UricAcid, y = ..density..)) +
  geom_density(fill = "lightblue", color = "black") +
  labs(title = "Distribution of Uric Acid Levels", x = "Uric Acid Level", y = "Density") +
  theme_minimal()
## Warning: The dot-dot notation (`..density..`) was deprecated in ggplot2 3.4.0.
## ℹ Please use `after_stat(density)` instead.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.


# Box plot for Uric Acid vs Metabolic Syndrome
ggplot(data = df, aes(x = factor(MetabolicSyndrome), y = UricAcid, fill = factor(MetabolicSyndrome))) +
  geom_boxplot() +
  labs(title = "Distribution of Uric Acid with Metabolic Syndrome",
       x = "Metabolic Syndrome", y = "Uric Acid", fill = "Metabolic Syndrome") +
  scale_fill_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  theme_minimal()


# Stacked bar plot for Race vs Metabolic Syndrome
ggplot(data = df, aes(x = Race, fill = factor(MetabolicSyndrome))) +
  geom_bar(position = "stack") +
  labs(title = "Race vs Metabolic Syndrome",
       x = "Race", y = "Count", fill = "Metabolic Syndrome") +
  scale_fill_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  theme_minimal()


# Histogram with density overlay for Blood Glucose Levels and Metabolic Syndrome
ggplot(data = df, aes(x = BloodGlucose, fill = factor(MetabolicSyndrome), color = factor(MetabolicSyndrome))) +
  geom_histogram(aes(y = ..density..), bins = 30, alpha = 0.5) +
  geom_density(alpha = 0.5) +
  labs(title = "Distribution of Blood Glucose Levels by Metabolic Syndrome",
       x = "Blood Glucose Level", y = "Density", fill = "Metabolic Syndrome", color = "Metabolic Syndrome") +
  scale_fill_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  scale_color_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  theme_minimal()


#STATISTICAL ANALYSIS #Exploratory data Analysis

summary(Metabolic_Syndrome_final)
##       seqn            Age            Sex                Race          
##  Min.   :62161   Min.   :20.00   Length:2375        Length:2375       
##  1st Qu.:64563   1st Qu.:34.00   Class :character   Class :character  
##  Median :67058   Median :48.00   Mode  :character   Mode  :character  
##  Mean   :67028   Mean   :48.67                                        
##  3rd Qu.:69501   3rd Qu.:63.00                                        
##  Max.   :71915   Max.   :80.00                                        
##       BMI           UricAcid      BloodGlucose        HDL       
##  Min.   :13.40   Min.   :1.800   Min.   : 65.0   Min.   :14.50  
##  1st Qu.:24.00   1st Qu.:4.500   1st Qu.: 92.0   1st Qu.:43.00  
##  Median :27.70   Median :5.400   Median :100.0   Median :51.00  
##  Mean   :28.55   Mean   :5.474   Mean   :102.9   Mean   :53.12  
##  3rd Qu.:32.10   3rd Qu.:6.400   3rd Qu.:110.0   3rd Qu.:62.00  
##  Max.   :44.25   Max.   :9.250   Max.   :137.0   Max.   :90.50  
##  MetabolicSyndrome
##  Min.   :0.000    
##  1st Qu.:0.000    
##  Median :0.000    
##  Mean   :0.344    
##  3rd Qu.:1.000    
##  Max.   :1.000
#Checking Normality of data

numeric_columns = Metabolic_Syndrome_final[sapply(Metabolic_Syndrome_final,is.numeric)]
normality_results = sapply(numeric_columns,function(x) {
  shapiro.test = shapiro.test(x) 
  p_value = shapiro.test$p.value
})
normality_results
##              seqn               Age               BMI          UricAcid 
##      7.679795e-27      8.851966e-26      3.886852e-23      4.517758e-13 
##      BloodGlucose               HDL MetabolicSyndrome 
##      3.090104e-33      3.288860e-23      4.070491e-59
The data is not normally distributed.

#DENSITY PLOTS

library(ggplot2)

# Convert MetabolicSyndrome to a factor if it's not already
Metabolic_Syndrome_final$MetabolicSyndrome <- factor(Metabolic_Syndrome_final$MetabolicSyndrome)

# Define color palette for each variable
color_palette <- c("Age" = "blue", "BMI" = "darkgreen", "Blood Glucose" = "red","HDL" = "brown", "UricAcid" = "purple")

# Create the plot
ggplot(data = Metabolic_Syndrome_final) +
  geom_density(aes(x = Age, color = "Age"), alpha = 0.6) +
  geom_density(aes(x = BMI, color = "BMI"), alpha = 0.6) +
  geom_density(aes(x = HDL, color = "HDL"), alpha = 0.6) +
  geom_density(aes(x = UricAcid, color = "UricAcid"), alpha = 0.6) +
  geom_density(aes(x = BloodGlucose, color = "Blood Glucose"), alpha = 0.6) +
  facet_wrap(~ Sex) +  # Facet by Sex
  scale_color_manual(values = color_palette, name = "Variables", labels = c("Age", "BMI", "Blood Glucose" , "HDL", "UricAcid")) +
  labs(title = "Density plots of Metabolic Syndrome by Age, BMI, and Blood Glucose , HDL, UricAcid", 
       x = "Variables", y = "Density") +
  theme_bw() +  # Change plot background to white
  theme(panel.grid = element_blank())  # Remove grid lines


FOR RQ1

#chi-square test

# Create a contingency table of Sex and Metabolic Syndrome
contingency_table <- table(Metabolic_Syndrome_final$Sex, Metabolic_Syndrome_final$MetabolicSyndrome)

# Perform chi-square test
chi_square_result <- chisq.test(contingency_table)

# Print the results
print(chi_square_result)
## 
##  Pearson's Chi-squared test with Yates' continuity correction
## 
## data:  contingency_table
## X-squared = 0.94767, df = 1, p-value = 0.3303
# Check for significance and provide interpretation
if (chi_square_result$p.value < 0.05) {
  cat("\nThere is a significant association between Sex and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between Sex and Metabolic Syndrome.\n")
}
## 
## There is no significant association between Sex and Metabolic Syndrome.
# Create a contingency table of Race and Metabolic Syndrome
contingency_table_race <- table(Metabolic_Syndrome_final$Race, Metabolic_Syndrome_final$MetabolicSyndrome)

# Perform chi-square test for Race
chi_square_result_race <- chisq.test(contingency_table_race)

# Print the results for Race
print(chi_square_result_race)
## 
##  Pearson's Chi-squared test
## 
## data:  contingency_table_race
## X-squared = 30.209, df = 5, p-value = 1.342e-05
# Check for significance and provide interpretation
if (chi_square_result_race$p.value < 0.05) {
  cat("\nThere is a significant association between Race and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between Race and Metabolic Syndrome.\n")
}
## 
## There is a significant association between Race and Metabolic Syndrome.
#Kruskal-Wallis test

# Perform Kruskal-Wallis test for Age
kruskal_test_age <- kruskal.test(Age ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for Age
print(kruskal_test_age)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  Age by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 155.73, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_age$p.value < 0.05) {
  cat("\nThere is a significant association between Age and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between Age and Metabolic Syndrome.\n")
}
## 
## There is a significant association between Age and Metabolic Syndrome.
# Perform Kruskal-Wallis test for BMI
kruskal_test_bmi <- kruskal.test(BMI ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for BMI
print(kruskal_test_bmi)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  BMI by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 497.51, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_bmi$p.value < 0.05) {
  cat("\nThere is a significant association between BMI and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between BMI and Metabolic Syndrome.\n")
}
## 
## There is a significant association between BMI and Metabolic Syndrome.
# Perform Kruskal-Wallis test for Blood Glucose
kruskal_test_glucose <- kruskal.test(BloodGlucose ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for Blood Glucose
print(kruskal_test_glucose)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  BloodGlucose by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 655.43, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_glucose$p.value < 0.05) {
  cat("\nThere is a significant association between Blood Glucose and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between Blood Glucose and Metabolic Syndrome.\n")
}
## 
## There is a significant association between Blood Glucose and Metabolic Syndrome.
# Perform Kruskal-Wallis test for HDL
kruskal_test_HDL <- kruskal.test(HDL ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for Blood Glucose
print(kruskal_test_HDL)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  HDL by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 407.91, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_HDL$p.value < 0.05) {
  cat("\nThere is a significant association between HDL and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between HDL and Metabolic Syndrome.\n")
}
## 
## There is a significant association between HDL and Metabolic Syndrome.
# Perform Kruskal-Wallis test for UricAcid
kruskal_test_UricAcid <- kruskal.test(UricAcid ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for Blood Glucose
print(kruskal_test_UricAcid)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  UricAcid by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 130.64, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_UricAcid$p.value < 0.05) {
  cat("\nThere is a significant association between HDL and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between HDL and Metabolic Syndrome.\n")
}
## 
## There is a significant association between HDL and Metabolic Syndrome.
#{r}install.packages("reshape2")

#correlation

library(ggplot2)
library(reshape2)
## Warning: package 'reshape2' was built under R version 4.3.3
numerical_data <- Metabolic_Syndrome_final[, c("Age", "BMI", "BloodGlucose","HDL","UricAcid")]

correlation_matrix <- cor(numerical_data)
melted_correlation <- melt(correlation_matrix, value.name = "Correlation")

ggplot(data = melted_correlation, aes(Var1, Var2, fill = Correlation)) + 
  geom_tile() + 
  geom_text(aes(label = round(Correlation, 2)), color = "black", size = 3) + 
  scale_fill_gradient(low = "#4E79A7", high = "skyblue") + 
  labs(title = "Correlation HeatMap", x = "", y = "") + 
  theme_minimal() + 
  theme(axis.text.x = element_text(angle = 45, vjust = 1, hjust = 1))


#logistic regression

# Fit logistic regression model for Age
logistic_model_age <- glm(MetabolicSyndrome ~ Age, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model for Age
summary(logistic_model_age)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ Age, family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##             Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -2.20847    0.14105  -15.66   <2e-16 ***
## Age          0.03119    0.00260   12.00   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2904.1  on 2373  degrees of freedom
## AIC: 2908.1
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio for Age
odds_ratio_age <- exp(coef(logistic_model_age)["Age"])

# Print the odds ratio with interpretation for Age
cat("Odds Ratio for Age:", odds_ratio_age, "\n")
## Odds Ratio for Age: 1.031683
# Interpretation for Age
cat("For every one year increase in age, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio_age, 2), "times, holding all other variables constant.\n")
## For every one year increase in age, the odds of having metabolic syndrome increase by a factor of 1.03 times, holding all other variables constant.
# Fit logistic regression model
logistic_model <- glm(MetabolicSyndrome ~ BMI, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model
summary(logistic_model)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ BMI, family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##              Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -5.682010   0.268580  -21.16   <2e-16 ***
## BMI          0.172429   0.008945   19.28   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2570.8  on 2373  degrees of freedom
## AIC: 2574.8
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio
odds_ratio <- exp(coef(logistic_model)["BMI"])

# Print the odds ratio with interpretation
cat("Odds Ratio for BMI:", odds_ratio, "\n")
## Odds Ratio for BMI: 1.188187
# Interpretation
cat("For every one unit increase in BMI, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio, 2), "times, holding all other variables constant.")
## For every one unit increase in BMI, the odds of having metabolic syndrome increase by a factor of 1.19 times, holding all other variables constant.
# Fit logistic regression model for Blood Glucose
logistic_model_glucose <- glm(MetabolicSyndrome ~ BloodGlucose, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model for Blood Glucose
summary(logistic_model_glucose)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ BloodGlucose, family = binomial, 
##     data = Metabolic_Syndrome_final)
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  -8.858154   0.396141  -22.36   <2e-16 ***
## BloodGlucose  0.078647   0.003759   20.92   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2434.1  on 2373  degrees of freedom
## AIC: 2438.1
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio for Blood Glucose
odds_ratio_glucose <- exp(coef(logistic_model_glucose)["BloodGlucose"])

# Print the odds ratio with interpretation for Blood Glucose
cat("Odds Ratio for Blood Glucose:", odds_ratio_glucose, "\n")
## Odds Ratio for Blood Glucose: 1.081822
# Interpretation for Blood Glucose
cat("For every one unit increase in blood glucose level, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio_glucose, 2), "times, holding all other variables constant.\n")
## For every one unit increase in blood glucose level, the odds of having metabolic syndrome increase by a factor of 1.08 times, holding all other variables constant.
# Fit logistic regression model for HDL
logistic_model_HDL <- glm(MetabolicSyndrome ~ HDL, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model for HDL
summary(logistic_model_HDL)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ HDL, family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##              Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  3.126841   0.215954   14.48   <2e-16 ***
## HDL         -0.074356   0.004325  -17.19   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2653.2  on 2373  degrees of freedom
## AIC: 2657.2
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio for HDL
odds_ratio_HDL <- exp(coef(logistic_model_HDL)["HDL"])

# Print the odds ratio with interpretation for HDL
cat("Odds Ratio for HDL:", odds_ratio_HDL, "\n")
## Odds Ratio for HDL: 0.9283408
# Interpretation for HDL
cat("For every one unit increase in HDL, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio_HDL, 2), "times, holding all other variables constant.\n")
## For every one unit increase in HDL, the odds of having metabolic syndrome increase by a factor of 0.93 times, holding all other variables constant.
# Fit logistic regression model for UricAcid
logistic_model_UricAcid <- glm(MetabolicSyndrome ~ HDL, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model for UricAcid
summary(logistic_model_UricAcid)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ HDL, family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##              Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  3.126841   0.215954   14.48   <2e-16 ***
## HDL         -0.074356   0.004325  -17.19   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2653.2  on 2373  degrees of freedom
## AIC: 2657.2
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio for HDL
odds_ratio_UricAcid <- exp(coef(logistic_model_UricAcid)["UricAcid"])

# Print the odds ratio with interpretation for UricAcid
cat("Odds Ratio for UricAcid:", odds_ratio_UricAcid, "\n")
## Odds Ratio for UricAcid: NA
# Interpretation for UricAcid
cat("For every one unit increase in UricAcid, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio_UricAcid, 2), "times, holding all other variables constant.\n")
## For every one unit increase in UricAcid, the odds of having metabolic syndrome increase by a factor of NA times, holding all other variables constant.
FOR RQ2:

Which demographic or health factor has the highest impact on the prevalence of metabolic syndrome among individuals with certain risk factors?

Null Hypothesis (H0): There is no significant difference in the prevalence of metabolic syndrome among individuals with certain risk factors based on demographic or health factors. Alternate Hypothesis (H1): At least one demographic or health factor has a significant impact on the prevalence of metabolic syndrome among individuals with certain risk factors.

# Load necessary libraries
library(dplyr)   # For data manipulation
library(tidyr)   # For data tidying
## Warning: package 'tidyr' was built under R version 4.3.3
## 
## Attaching package: 'tidyr'
## The following object is masked from 'package:reshape2':
## 
##     smiths
library(broom)   # For tidying model results
## Warning: package 'broom' was built under R version 4.3.3
# Select relevant variables for analysis
#variables <- c("BMI", "UricAcid", "BloodGlucose", "HDL")
variables1 <- c("Age", "Sex","Race")

# Define outcome variable
outcome_var1 <- "MetabolicSyndrome"

# Fit logistic regression model
logit_model1 <- glm(as.formula(paste(outcome_var1, "~", paste(variables1, collapse = " + "))),
                   data = Metabolic_Syndrome_final,
                   family = binomial)

# Tidy up the model results
tidy_results1 <- tidy(logit_model1)

# Print coefficient estimates
print(tidy_results1)
## # A tibble: 8 × 5
##   term            estimate std.error statistic  p.value
##   <chr>              <dbl>     <dbl>     <dbl>    <dbl>
## 1 (Intercept)      -2.71     0.191     -14.2   1.19e-45
## 2 Age               0.0313   0.00265    11.8   2.55e-32
## 3 SexMale           0.0811   0.0900      0.902 3.67e- 1
## 4 RaceBlack         0.399    0.161       2.48  1.31e- 2
## 5 RaceHispanic      0.667    0.186       3.59  3.25e- 4
## 6 RaceMexAmerican   0.899    0.186       4.83  1.37e- 6
## 7 RaceOther         0.287    0.322       0.890 3.74e- 1
## 8 RaceWhite         0.463    0.149       3.11  1.89e- 3
# Visualize coefficient estimates
plot(tidy_results1, main = "Coefficient Estimates")


# Check statistical significance of coefficients
summary(logit_model1)
## 
## Call:
## glm(formula = as.formula(paste(outcome_var1, "~", paste(variables1, 
##     collapse = " + "))), family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##                  Estimate Std. Error z value Pr(>|z|)    
## (Intercept)     -2.709339   0.191045 -14.182  < 2e-16 ***
## Age              0.031309   0.002645  11.836  < 2e-16 ***
## SexMale          0.081120   0.089967   0.902 0.367236    
## RaceBlack        0.399407   0.161006   2.481 0.013113 *  
## RaceHispanic     0.667227   0.185622   3.595 0.000325 ***
## RaceMexAmerican  0.898895   0.186159   4.829 1.37e-06 ***
## RaceOther        0.286902   0.322467   0.890 0.373622    
## RaceWhite        0.462566   0.148862   3.107 0.001888 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2876.0  on 2367  degrees of freedom
## AIC: 2892
## 
## Number of Fisher Scoring iterations: 4
# Assuming you have already fitted a logistic regression model named logit_model

# Get summary of the model
summary_logit <- summary(logit_model1)

# Extract coefficient estimates and p-values
coefficients <- coef(logit_model1)
p_values <- summary_logit$coefficients[, 4]

# Exclude intercept (if present)
if ("(Intercept)" %in% names(coefficients)) {
  coefficients <- coefficients[-1]
  p_values <- p_values[-1]
}

# Calculate absolute coefficients
abs_coefficients <- abs(coefficients)

# Find the index of the variable with the highest absolute coefficient
highest_impact_index <- which.max(abs_coefficients)

# Print the variable with the highest impact and its coefficient
cat("Variable with the highest impact: ", names(coefficients)[highest_impact_index], "\n")
## Variable with the highest impact:  RaceMexAmerican
cat("Coefficient estimate: ", coefficients[highest_impact_index], "\n")
## Coefficient estimate:  0.8988951
cat("P-value: ", p_values[highest_impact_index], "\n")
## P-value:  1.37472e-06
# Load necessary libraries
library(dplyr)   # For data manipulation
library(tidyr)   # For data tidying
library(broom)   # For tidying model results



# Select relevant variables for analysis
variables2 <- c("BMI", "UricAcid", "BloodGlucose", "HDL")


# Define outcome variable
outcome_var2 <- "MetabolicSyndrome"

# Fit logistic regression model
logit_model2 <- glm(as.formula(paste(outcome_var2, "~", paste(variables2, collapse = " + "))),
                   data = Metabolic_Syndrome_final,
                   family = binomial)

# Tidy up the model results
tidy_results2 <- tidy(logit_model2)

# Print coefficient estimates
print(tidy_results2)
## # A tibble: 5 × 5
##   term         estimate std.error statistic  p.value
##   <chr>           <dbl>     <dbl>     <dbl>    <dbl>
## 1 (Intercept)   -9.47     0.625      -15.2  6.32e-52
## 2 BMI            0.134    0.0104      12.9  5.10e-38
## 3 UricAcid       0.0868   0.0424       2.05 4.04e- 2
## 4 BloodGlucose   0.0698   0.00417     16.7  1.07e-62
## 5 HDL           -0.0573   0.00512    -11.2  4.33e-29
# Visualize coefficient estimates
plot(tidy_results2, main = "Coefficient Estimates")


# Check statistical significance of coefficients
summary(logit_model2)
## 
## Call:
## glm(formula = as.formula(paste(outcome_var2, "~", paste(variables2, 
##     collapse = " + "))), family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  -9.469499   0.624559  -15.16   <2e-16 ***
## BMI           0.134302   0.010419   12.89   <2e-16 ***
## UricAcid      0.086849   0.042366    2.05   0.0404 *  
## BloodGlucose  0.069759   0.004174   16.71   <2e-16 ***
## HDL          -0.057337   0.005122  -11.20   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 1966.3  on 2370  degrees of freedom
## AIC: 1976.3
## 
## Number of Fisher Scoring iterations: 5
# Get summary of the model
summary_logit2 <- summary(logit_model2)

# Extract coefficient estimates and p-values
coefficients2 <- coef(logit_model2)
p_values2 <- summary_logit2$coefficients2[, 4]

# Exclude intercept (if present)
if ("(Intercept)" %in% names(coefficients2)) {
  coefficients2 <- coefficients2[-1]
  p_values2 <- p_values2[-1]
}

# Calculate absolute coefficients
abs_coefficients2 <- abs(coefficients2)

# Find the index of the variable with the highest absolute coefficient
highest_impact_index2 <- which.max(abs_coefficients2)

# Print the variable with the highest impact and its coefficient
cat("Variable with the highest impact: ", names(coefficients2)[highest_impact_index2], "\n")
## Variable with the highest impact:  BMI
cat("Coefficient estimate: ", coefficients2[highest_impact_index2], "\n")
## Coefficient estimate:  0.1343017
cat("P-value: ", p_values2[highest_impact_index2], "\n")
## P-value:
# Install and load the pROC package
if (!requireNamespace("pROC", quietly = TRUE)) {
    install.packages("pROC")
}
library(pROC)
## Warning: package 'pROC' was built under R version 4.3.3
## Type 'citation("pROC")' for a citation.
## 
## Attaching package: 'pROC'
## The following objects are masked from 'package:stats':
## 
##     cov, smooth, var
# Plot ROC curve and calculate AUC
roc_response <- roc(response = as.numeric(as.character(Metabolic_Syndrome_final$MetabolicSyndrome)) - 1, 
                    predictor = fitted(logit_model2))
## Setting levels: control = -1, case = 0
## Setting direction: controls < cases
plot(roc_response)


auc(roc_response)
## Area under the curve: 0.8778
