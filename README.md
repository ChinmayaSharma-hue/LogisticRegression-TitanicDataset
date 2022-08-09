# Neural-Networks
Neural Networks are complex architectures thaat use the concept of feedforward and backpropagation in order to optimize prediction by inferene using weights that are varied based on backpropagation.
## Feedforward
The weights are randomly initialized in the beginning and the inputs are fed into the model. After a set of matrix operations, an output is obtained. This part
of the model is called feedforward. Feedforward involves using the weights in order to make a prediction which can be compared with the actual prediction in
order to make changes to the weights and bias accordingly.
## Backpropagation
The output from the model is compared with the actual output, and based on the difference that is measured using a desired metric, the weights and bias are
changed, by using what is known as Gradient Descent, which hopes to get the model weights to converge to values that give the least possible error in the metric used
for comparison between model predictions and the desired output.

## Logistic Regression with a single output
In a logistic regression model described by n features and one output as shown, each of the features are weighted and added, and then the weighted sum is passed through an activation function that gives a probability of the input belonging to a specific class. <br><br>
![image](https://user-images.githubusercontent.com/76653568/183704099-058b7c13-f0a9-4b3f-a195-0e911a3c6a7a.png) <br><br>
The expression for the output can be obtained as,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183706043-993ce562-4cdf-41bb-9d80-aad13289f940.png) <br><br>
where the subscript 'i' represents the index of the sample of the input that is passed through the model, since the model has to train on several samples to learn.
The weights and the input can be written in the form of matrices in order to make the expression simpler,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183706227-8350be21-7240-4421-bca6-4b7362cb6961.png) <br><br>
The bias is a single scalar, since the number of outputs is 1. The matrix multiplication of the weights and inputs matrices gives a matrix with a single element, which is added to the bias and then passed through the activation function to get the output. The output can therefore be expressed as,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183706283-bbf9a1fa-1ee2-4ce0-a4a1-815da59ed5ed.png)<br><br>
If there are several samples of data that is passed through the model, the input matrix needs to be extended to include all the samples of the data, and the output can be represented as a matrix consisting of the outputs of different samples. If the number of samples is r, the input matrix can be represented as, <br><br>
![image](https://user-images.githubusercontent.com/76653568/183706369-ede70772-3c0f-4e21-aabe-97d93d257fc3.png)<br><br>
which is a matrix with dimensions [n x r], with each column representing one sample of data, and each row representing the index of the input. Similarly, the output matrix can be represented as, <br><br>
![image](https://user-images.githubusercontent.com/76653568/183706841-fe8e9415-ce4d-4220-9100-b88b6ace014c.png) <br><br>
which is a matrix with dimensions [1 x r], with each column representing the output of one sample of data.
The weight matrix remains unchanged, as the same set of weights is used for different samples of the data. The bias matrix, however, is broadcasted in order to have the same dimension as the input. <br><br>
![image](https://user-images.githubusercontent.com/76653568/183707043-0754929a-07ec-45ae-85a8-bbd585c065ae.png) <br><br>
which is a matrix with dimensions [1 x r], with each of the column having the same value for b as the same bias is used for different samples of data. Now, the output matrix can be expressed in terms of the weights matrix, inputs matrix and the bias matrix as,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183707316-7503f5aa-a90a-4987-8a94-b1293964c404.png) <br><br>
Dimensionally speaking, the matrix multiplication of the weights and the inputs matrix gives a matrix of dimension [1 x r], and the bias matrix is of the same dimension which is added to get a matrix of the same dimension, and the activation function is applied to each element of the matrix individually to get the output matrix with the dimension [1 x r]
This is the vectorization of the model when the number of outputs is 1. When the number of outputs is more than 1, the outputs matrix has to be extended by increasing the number of rows, with each row corresponding to a distinct output of the model. <br><br>

## Logistic Regression with multiple outputs
The output matrix when the number of outputs of the model is more than 1, say m, is given by,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183707700-949153e2-3c55-4b57-8232-b5eb568ed6c9.png)<br><br>
where each column represents the outputs for a distinct sample of data, and each row represents the index of the output of the model. The weights matrix also needs to be extended as different sets of weights are used for different outputs of the model, and the bias matrix also needs to be extended as different bias is used for different outputs of the model, while the inputs matrix remains the same. <br><br>
The weights matrix is given by a matrix with dimensions [m x n], where each row corresponds to a set of weights that is used to obtain a distinct output of the model, and each column corresponds to the set of weights that is used on a specific input index. <br><br>
![image](https://user-images.githubusercontent.com/76653568/183707864-63937c20-2183-4474-9dea-c6580dbecd95.png) <br><br>
The bias matrix is given by a matrix with dimensions [m x r], where each row corresponds to the bias used to obtain a distinct output irrespective of the sample used, and each column corresponds to the bias used for different samples, which is the same for all the samples.
If there are several samples of data that is passed through the model, the input matrix needs to be extended to include all the samples of the data, and the output can be represented as a matrix consisting of the outputs of different samples. If the number of samples is r, the input matrix can be represented as, <br><br>
![image](https://user-images.githubusercontent.com/76653568/183708022-29ce5a43-d3d0-495a-a282-9bfdaf49fe38.png) <br><br>
The output matrix of the model can be expressed in terms of the weights matrix, inputs matrix and the bias matrix as, <br><br>
![image](https://user-images.githubusercontent.com/76653568/183708130-7e8093aa-72cb-42b4-8228-631c9a36e6d1.png) <br><br>

## Backpropagation through a Logistic Regression Model
Let the cost function be denoted by C. The objective is to find the variation of the cost with respect to the weights. The cost is calculated from the actual value of the output to be predicted, and the value predicted by the model. <br><br>
Let the weighted sum of the inputs be given by z and the activated value of z be given by y. Therefore, the output of the model is y. <br><br>
![image](https://user-images.githubusercontent.com/76653568/183708391-ce9ca8ad-6665-4c09-9627-d0b947944d85.png) <br><br>
The above equation follows from the chain rule of derivatives. This expression has three terms, <br>
1. Derivative of the cost with respect to the output
2. Derivative of the output with respect to the weighted sum of the inputs
3. Derivative of the weighted sum of outputs with respect to the weight
###  Finding the first term 
If the cost function taken is the Mean Square Error function, <br><br>
![image](https://user-images.githubusercontent.com/76653568/183708622-6a61a275-f78c-4865-89e3-b9462c24ccfd.png)<br><br>
which is the sum of the squares of the difference of the actual and the predicted values, which is averaged over all the samples.<br>
The derivative of the cost function with respect to the output is given by,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183708726-3cfc6e71-3d23-408c-9a26-370203c3cf67.png)<br><br>
### Finding the second term
If the activation function taken is represented by  σ, the value of y in terms of z is given by,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183708846-26481937-10e6-40c5-9461-28fb73f08b9e.png)<br><br>
The derivative of the output (y) in terms of the weighted sum of the inputs (z) is given by,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183709483-b2095dae-8748-46e4-9000-62c193403048.png)
### Finding the third term
The weighted sum of the inputs (z) in terms of the weights (w) is given by,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183709596-a9c43d7c-cd22-455a-a8ad-74973ece373d.png)<br><br>
The derivative of the weighted sum of inputs (z) with respect to a specific weight is given by,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183709703-2319d056-78f3-43e5-8078-1aefdfffa35f.png)<br><br>
Therefore, the derivative of the weighted sum of inputs in terms of a specific weight is the input data point which is multiplied with that specific weight in the expression of the weighted sum of inputs.<br>
Combining the three terms, and averaging over all the samples,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183710351-1c1f9166-80e5-47d6-b58c-b5ba8c2e0767.png)<br><br>
In order to find the variation of the cost with the bias,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183710410-2d78e717-c815-4c61-8875-17e8767fa440.png)<br><br>
The first two terms are the same as that of the derivative of the cost with respect to the weights. In order to find the third term,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183710491-191b1ab7-07db-4973-88b6-3d21f225af80.png)<br><br>
Combining the three terms, and averaging over all the samples,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183710563-0b7cd69f-2a26-47ae-bca4-4726bdac402c.png)<br><br>
The variation of the cost with respect to the weights and the bias are given by,<br><br>
![image](https://user-images.githubusercontent.com/76653568/183710629-d13d7a8d-8700-425d-971d-923620106aa3.png)
Using these two equations, the gradient matrix of the weights and the bias can be found.<br><br>
![image](https://user-images.githubusercontent.com/76653568/183710697-095be1e6-222d-4b4a-92f7-86e1489f91f4.png)

