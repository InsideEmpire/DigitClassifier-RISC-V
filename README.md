# RISC-V MNIST Classifier

## Overview
This project implements a simple **Artificial Neural Network (ANN)** in **RISC-V assembly** to classify handwritten digits from the **MNIST dataset**. The implementation runs on the **Venus RISC-V simulator** and includes basic neural network operations such as dot product, matrix multiplication, activation functions, and classification.

---

## Running the Project
For detailed instructions on setting up and running the project, refer to the [Tutorial](Tutorial.md). This includes steps to test the RISC-V assembly code, run the Venus RISC-V simulator, and execute unit tests for the MNIST classifier.

---

## Project Structure
The project directory is organized as follows:

```
.
├── inputs/             # Directory for test input data
├── outputs/            # Directory for test output data
├── README.md           # Project documentation
├── src/                # RISC-V assembly source files
│   ├── argmax.s        # Implements the argmax function
│   ├── classify.s      # Handles the classification logic
│   ├── dot.s           # Computes dot product
│   ├── main.s          # Main entry point for execution
│   ├── matmul.s        # Matrix multiplication implementation
│   ├── read_matrix.s   # Reads input matrices
│   ├── relu.s          # Implements the ReLU activation function
│   ├── utils.s         # Utility functions for the neural network
│   └── write_matrix.s  # Writes the output matrix
├── tools/              # Helper tools for conversion and simulation
│   ├── convert.py      # Converts matrix files from binary to readable format
│   └── venus.jar       # RISC-V simulator (Venus)
└── unittests/          # Unit testing framework
    ├── assembly/       # Stores outputs from unit tests
    ├── framework.py    # Test framework logic
    └── unittests.py    # Test cases for validating the implementation
```
