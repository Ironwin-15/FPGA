## Neural Network Model

For this project, I used the `Iris dataset` available on Kaggle. The dataset was split into 80% training and 20% testing set. Each data sample contains 4 input features.
There are **3 output classes (labels)**

### Model Architecture 

- **Input Layer:** 4 features  
- **Hidden Layer:**  
  - 8 neurons  + Activation: ReLU  
- **Output Layer:**  
  - 3 neurons  + Activation: Softmax

### Training & Testing

Epoch 1/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 3s 267ms/step - accuracy: 0.3417 - loss: 1.7091  
Epoch 10/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.3417 - loss: 1.2361  
Epoch 20/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.6750 - loss: 0.9454  
Epoch 30/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 11ms/step - accuracy: 0.6333 - loss: 0.8466  
Epoch 40/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 9ms/step - accuracy: 0.5833 - loss: 0.7964  
Epoch 50/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 9ms/step - accuracy: 0.6250 - loss: 0.7560   
Epoch 60/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 9ms/step - accuracy: 0.6750 - loss: 0.7189   
Epoch 80/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.7333 - loss: 0.6527  
Epoch 100/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.8000 - loss: 0.5952    
Epoch 120/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 9ms/step - accuracy: 0.8333 - loss: 0.5466   
Epoch 160/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.9167 - loss: 0.4687  
Epoch 200/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.9417 - loss: 0.4051  
Epoch 240/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 9ms/step - accuracy: 0.9667 - loss: 0.3504   
Epoch 280/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 11ms/step - accuracy: 0.9667 - loss: 0.3032  
Epoch 320/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.9750 - loss: 0.2622   
Epoch 360/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 17ms/step - accuracy: 0.9750 - loss: 0.2284  
Epoch 396/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.9750 - loss: 0.2034  
Epoch 397/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.9750 - loss: 0.2026  
Epoch 398/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.9750 - loss: 0.2021  
Epoch 399/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 10ms/step - accuracy: 0.9750 - loss: 0.2014  
Epoch 400/400  
4/4 ━━━━━━━━━━━━━━━━━━━━ 0s 11ms/step - accuracy: 0.9750 - loss: 0.2008  
-The model was trained with epochs ranging from **1 to 400**, achieving a training accuracy of **97.50%**, test accuracy of **93.33%** and loss **0.2008%** finally.
- All the **56 Weights & 11 biases** were saved in **.mem format** using hexadecimal representation after the testing
---

## Coding the Neuron Module in Vivado

### Functionality
The weights, biases and test_data were fed into the sources.
- Each neuron:
  - Takes consecutively **4 inputs** and **4 corresponding weights**
  - Performs a **MAC (Multiply-Accumulate)** operation on them
  - Applies **ReLU activation** finally

### Verilog Implementation

```verilog
assign relu_out = (sum[31]) ? 16'd0 : sum[23:8];
```
## Making the layer module (Multiple neurons in parallel)
Designed by combining multiple neuron modules to operate as a single computational unit. Each neuron in the layer receives the same input data but uses its own set of weights and bias values to perform independent MAC operations followed by activation . The outputs of all neurons are computed in parallel (or sequentially based on design constraints) and collectively form the output vector of the layer, and are presented as output.

## Final Output Layer (NN_TOP)

The NN_TOP module represents the complete neural network by integrating the hidden layer and the 3-neuron-output layer into a single top-level design. It manages the data flow between layers, feeds inputs through the network, and collects the final outputs. It processes the results from the hidden layer to produce classification scores for each class. The final prediction corresponds to the neuron with the highest output value, effectively implementing a hardware-based inference of the neural network.
