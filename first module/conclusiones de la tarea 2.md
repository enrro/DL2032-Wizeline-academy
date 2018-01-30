# Notes and conclusions.

Activity recognition aims to recognize the actions and goals of one or more agents from a series of observations on the agents' actions and the environmental conditions. Since the 1980s, this research field has captured the attention of several computer science communities due to its strength in providing personalized support for many different applications and its connection to many different fields of study such as medicine, human-computer interaction, or sociology.

We aim to find patters using the University of California data set the dataset used in this example was build using inertial data obtained from smartphone accelerometers and gyroscopes. The dataset came from the recordings from 30 subjects doing the following human activities:
1. Walking
2. Walking Upstairs
3. Walking Downstairs
4. Sitting
5. Standing
6. Laying


In this document I write down some of my observations by header


In the **dataset download** we extracted the information from the ICS website and extracted the compressed data


While **reading the dataset** we extracted some of the observations to create a training dataset. Aproximately 70% of the data was used for the porpouse of this example. 


In the **reading the dataset** header we also made some useful functions. `get_key_value_pairs(filename):` makes it confortable to extract information from the dataset. `HCA` was useful to create and plot the results of theHierarchical Clustering Analysis most of the information was presented by dendrogram since only having the values is not really useful for the study of the dataset. `facet_plot` created plots of diferent categories to visualise the distance between them. At the end of this we Report the row count by activity.


In **Subject 1** we make some experimentation of the data and see how some features are not feed to separate by categories. In *Non-Discriminative Features* The scatter plot clearly shows that most of the information is more or less at the same range height and this makes it really hard for the HCA to polarice in diferent categories the data. In the dendrogram its clear how most of the categories are so close togheter that they are not representative at all. On the other hand *Discriminative Features* takes features that clearly contrast with each other `'Walk','Walk up','Walk down','Sit','Stand','Lay'` are features that clearly contrast with each other in each of their max acceleration, that was easy to intuit but we made it even clearer by plotting the values. We follow the scatter plot with the dendrogram; the categories this time were very far apart at the beggining but they were harder to discriminate along the same subset.


**Strategy** At this point we have discovered that there are some features that are really easy to diference from one another, the static and dynamic activities are very recognisable one from other, we use  **PCA** to discriminate between this two crearly diferent subsets. As explained in class *Principal component analysis* is a statistical procedure that uses an orthogonal transformation to convert a set of observations of possibly correlated variables into a set of values of linearly uncorrelated variables called principal components. The number of distinct principal components is equal to the smaller of the number of original variables or the number of observations minus one.


 **Descriptive Model**  In this part of the exercice we have discovered that there is a relation as a tree structure in the data analysis and while the trees we have studied until now were useful they are not very accurate at predicting patterns. Now we need supervised learning algorithm for description purposes. We used the *Decision Tree Classifier* in the sklearn library. I would like to point out that in this exercise I leave the `min_sample_leaf` in the default value of 1, because the sample size is small and the max depth of this tree was of only 8. With at less one member per leaft we reached a 100 percent accuracy I kept experimenting with the min sample leaf and found a 90% accuracy with `min_sample_leaf=47`  and a  a 95% accuracy with `min_sample_leaf=18`. In my opinion the sample size of the leaf must not be leaft to 1 per leaf since that in most of the cases when we are not using training data but testing data our algorithm would not fit every need. In general de DecisionTreeClassifier is a very versatile function `DecisionTreeClassifier(criterion=’gini’, splitter=’best’, max_depth=None, min_samples_split=2, min_samples_leaf=1, min_weight_fraction_leaf=0.0, max_features=None, random_state=None, max_leaf_nodes=None, min_impurity_decrease=0.0, min_impurity_split=None, class_weight=None, presort=False)` For me the most notable one was the criterion; the *criterion*  measure the quality of the split, the default split is the gini, the Gini impurity is a measure of how often a randomly chosen element from the set would be incorrectly labeled if it was randomly labeled according to the distribution of labels in the subset. There are many others that are useful to determinate the depgth of the tree in case that no min sample was given or the splitter that can be the `best` or `random` that self explanatorily diference if each category was to be chosen at random or not. At the very end we create the confusion matrix and the decision tree, the confusion matrix shows true positives, false positives, false negatives, true positives and false negatives. according to were the data was clasified in the decision tree. On the other hand the decision tree selects the two diferent paths in with the data is classified in the tree. The leafs or nodes of the tree that have no children are the part were a certain amount of individual touples of information fit in to the scheme. Once more I would like to highlight that due to the low amount of data presented in this example and although I experimented with diferent heights and amount of leafs I leave it as it is because the deapth. 


## Conclusions.
In this practiced I learned the importance of the supervised and unsupervised algorithms. In the supervised, all data is labeled and the algorithms learn to predict the output from the input data. In the unsupervised: All data is unlabeled and the algorithms learn to inherent structure from the input data.
In this particular case the unsupervised algorithms that we used at the begining of the practice worked very well as a reference, where we appreciated that there was some relationship between the dataset and could expose the contrast between two very diferent kind clusters. The supervised algorith was really practical and was useful to shape down the real structure that at the end was the information of the training data. The depth, the criterion, the amount of leafs are all to be taken into account when making the algorithm model.

# References
 https://en.wikipedia.org/wiki/Gini_coefficient
 https://en.wikipedia.org/wiki/Confusion_matrix
 http://www.dataschool.io/simple-guide-to-confusion-matrix-terminology/
 http://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn.tree.DecisionTreeClassifier
 http://scikit-learn.org/stable/modules/tree.html
