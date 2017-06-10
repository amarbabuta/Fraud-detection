# Decision_tree
***DATA:***
The data was obtained from here: http://archive.ics.uci.edu/ml/datasets/banknote+authentication
The data contains the details of 1372 banknotes. The data set contained four features and one label, in a form of CSV. Data was extracted from images that were taken from genuine and forged banknote-like specimens. For digitization, an industrial camera usually used for print inspection was used. The final images have 400x 400 pixels. Due to the object lens and distance to the investigated object gray-scale pictures with a resolution of about 660 dpi were gained. Wavelet Transform tool were used to extract features from images.

***ALgorithm:***
This is the code to implement the decision tree algorithm from scratch. Proper commenting in the script is done as well. Please refer to that along with this.

`def data(fname):`

This returns the dataset from the .txt format after each value being converted to float from string.


`def k_fold_cross_validation(items, randomize=False):`

splits the data in k folds and returns the concatenated data. The advantage of this method over repeated random sub-sampling (see below) is that all observations are used for both training and validation, and each observation is used for validation exactly once.

`def calculate_accuracy(dataset):`

This is the function where the training and the testing data is formulated using each of the k folds of the dataset repeatedly. Each fold is made the testing set once when the other folds are kept as the training sets. The score for each arrangement is then obtained and the mean score is calculated which is the accuracy of the algorithm.

`def decision_tree(train, test):`

This is the function that helps in obtaining the prediction values of the algorithm for all the rows in the testing data set. It calls the splitting routine by sending the training data. The splitting function is explained later. Lets just say that it basically sends back the root node to the decision_tree for now which is sent to the node_split routine that formulate the rest of the tree.


`def gini(groups,class_values):`

This function calculates the gini index. 
The Gini index is the name of the cost function on the basis of which splitting in the dataset is done. The lower the value of the gini index the better the splitting is done. Lowest value being 0 and highest value being 1.
This gini function has to be explained in detail. To find the attribute according to which the splitting has to be done along with the value of the attribute that helps splitting the data in two sets, this value is calculated. 
Given a group and the class_values (labels), we calculate the purity of data. We calculate the ratio of the rows having the same labels over the total number of rows in the group. 




The formula of gini_index is:

`gini_index=ratio*(1-ratio)`

where the ratio is explained above. We sum all the gini_values for each group for a each class_value . This value is returned to the splitting routine which calculates the lowest gini_index value, thus calculates the attribute and the value for which the splitting should be done. 


`def test_split(index, value, dataset):`

This function is responsible for making the groups that are later send to the gini routine. It splits the data into left and right nodes, on the basis of whether the value in the chosen attribute of the particular row is lesser or greater than the value of the attribute in accordance to which the splitting is done. It returns with the groups that is send to gini for getting the gini index 

`def splitting(dataset):`

This is responsible for getting the perfect splitting. It uses the gini function and the test_split function to do so. 
We obtain the gini_index for each attribute in our dataset. This is done by taking the average of the values for each attribute and sending the value to the test_split that divides the data on the basis of that attribute. Then the groups that are formed are send to the def gini which calculates the gini value. The lowest value of gini is chosen and the splitting is done on the basis of that attribute

`def terminal_node(group):`

last node of the tree that contains the label that has the most frequency in the group that the node has.

`def node_split(node,depth):`

recursive function. Makes the tree by calling the splitting function. Checks if the particular node is terminal or not according to certain conditions like the min_size and the max_depth or if there cant be any more splitting done as no left or right node exists which occurs when all the values in the attribute is greater or less that the particular avg value of the attribute.
 
`def output_from_tree(node, row):`

This is used while making the predictions. This is done to traverse the tree to the terminal nodes to get the prediction that the test data belongs to. Th =e terminal node is returned that contains only the label that has the max frequency
