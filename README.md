# Simple Neural Network for XOR Problem

This project demonstrates the implementation of a simple feedforward neural network trained to solve the XOR problem. The neural network is designed using the `SimpleNeuralNetwork` class, which is assumed to be part of a custom library (`NeuralNetwork.h`).

---

## Features

- **Feedforward Neural Network**: The network can handle a customizable topology (number of layers and neurons per layer).
- **Backpropagation Algorithm**: The network is trained using the backpropagation algorithm to adjust weights based on error.
- **XOR Problem**: Trains the neural network to solve the XOR problem, where:
  - Input: {0,0}, {1,1}, {1,0}, {0,1}
  - Output: 0 for {0,0} and {1,1}; 1 for {1,0} and {0,1}

---

## Prerequisites

Before running the program, ensure you have the following:

- A C++ compiler supporting C++11 or higher (e.g., GCC, Clang, MSVC).
- The `NeuralNetwork.h` and associated source files (`NeuralNetwork.cpp`) in your project directory.

---

## How to Compile and Run

1. Clone or download this repository.
2. Ensure the `NeuralNetwork.h` file and corresponding implementation are included in your project.
3. Compile the program using a C++ compiler. For example, using `g++`:
   ```bash
   g++ -o neural_network main.cpp NeuralNetwork.cpp
4.Run the executable:
   ```bash
   ./neural_network

```

## Code Overview
### Neural Network Topology
The neural network is defined by its topology:
  ```cpp
std::vector<uint32_t> topology = { 2,3,1 };
```
This means:
Input layer with 2 neurons.
Hidden layer with 3 neurons.
Output layer with 1 neuron.

### Training Data
The network is trained on the XOR dataset:
```cpp
std::vector<std::vector<float>> targetInputs = {
    {0.0f,0.0f},
    {1.0f,1.0f},
    {1.0f,0.0f},
    {0.0f,1.0f}
};
std::vector<std::vector<float>> targetOutputs = {
    {0.0f},
    {0.0f},
    {1.0f},
    {1.0f}
};
```
Inputs: Pairs of binary numbers representing the XOR inputs.
Outputs: Expected results for the XOR operation.
### Training Loop
The neural network is trained using backpropagation over 10,000 epochs:
```cpp
for (uint32_t i = 0; i < epoch; i++)
{
    uint32_t index = rand() % 4;  // Randomly select a training example
    nn.FeedForward(targetInputs[index]);
    nn.backPropogate(targetOutputs[index]);
}
```
Each epoch, a random training example is chosen, and the network adjusts its weights accordingly using backpropagation.

### Predictions
After training, the network makes predictions for each input in the XOR dataset:
```cpp
for (std::vector<float> input : targetInputs)
{
    nn.FeedForward(input);
    std::vector<float> preds = nn.getPrediction();
    std::cout << input[0] << "," << input[1] << " => " << preds[0] << std::endl;
}
```
### Expected Output
After training, the network will make predictions for the XOR problem. An example output might look like:
```0,0 => 0.0234
1,1 => 0.0178
1,0 => 0.9811
0,1 => 0.9775
```

### Future Improvements
- Add support for more complex activation functions.
- Implement additional performance optimizations.
- Extend the neural network to handle other classification problems.
### License
This project is licensed under the MIT License. See the LICENSE file for more details.
