# RISC-V MNIST Classifier - Setup & Run Guide

This guide will help you set up the environment, run the RISC-V assembly code, and execute tests for the MNIST classifier.

---

## Prerequisites

Before running this project, ensure you have the following installed on your system:

### Install Java (for Venus RISC-V Simulator)
The Venus simulator requires Java to run. If you don’t have Java installed, download and install it.

### Install Python 3 (for Unit Tests & Tools)
Python is required for running the unit tests and the matrix conversion script.

---

## Run the Venus RISC-V Simulator
Ensure `venus.jar` is in the `tools/` directory. Then run Venus with:
```bash
java -jar tools/venus.jar . -dm
```
When you run it, you should see a Javalin message, launching the server and listening on `http://localhost:6161/` or `http://venus.cs61c.org`. Then run the following command from your Venus Web Interface Terminal.

```bash
mount local proj2
```
This will mount the repository and give you access to all your project files from within the Venus Web Interface to edit, run, and debug! Navigate to the Files tab on Venus to see your repository’s contents.

---

## Run the Assembly Code
To execute the neural network classification, run:
```bash
java -jar tools/venus.jar src/main.s
```

Alternatively, you can run individual functions (e.g., dot product):
```bash
java -jar tools/venus.jar src/dot.s
```

---

## Run Unit Tests
To verify the correctness of your implementation, run:
```bash
python3 unittests/unittests.py
```
If the tests pass, your implementation is correct. If there are errors, debug using Venus.

---

## Running Basic Tests

To perform a simple sanity check:
```bash
python3 -m unittest unittests.unittests.TestMain -v
```
You should **add more test cases** to `TestClassify` to cover additional edge cases.

**Hint:** You may not reach 100% test coverage due to neural network limitations—do you know why?

---

## Test Inputs and Outputs
- **Test inputs** are stored in the `inputs/` folder.  
- **Each network folder** (`mnist`, `simple0`, `simple1`, `simple2`) contains:  
  - `bin/` → Binary files for execution.  
  - `txt/` → Plaintext versions for debugging.  

For **MNIST**, additional folders:
- `txt/labels/` → True labels for each input.  
- `student_inputs/` → Scripts to test your own images.

---

## Testing on Small Networks
For debugging, use smaller test networks (`simple0`, `simple1`, `simple2`).

To test on `simple0/input0`:
```bash
java -jar tools/venus.jar src/main.s -ms -1 inputs/simple0/bin/m0.bin inputs/simple0/bin/m1.bin inputs/simple0/bin/inputs/input0.bin outputs/test_basic_main/student_basic_output.bin
```
Then convert the output to a readable format:
```bash
python3 tools/convert.py --to-ascii outputs/test_basic_main/student_basic_output.bin outputs/test_basic_main/output.txt
```
Use a **matrix multiplication calculator** to verify correctness, and manually set values to zero for ReLU.

---

## Running MNIST Classification
To test on the first MNIST input:
```bash
java -jar tools/venus.jar src/main.s -ms -1 inputs/mnist/bin/m0.bin inputs/mnist/bin/m1.bin inputs/mnist/bin/inputs/mnist_input0.bin outputs/test_mnist_main/student_mnist_outputs.bin
```
- The predicted digit should match the corresponding file in:
  ```bash
  inputs/mnist/txt/labels/label0.txt
  ```
- You can **view the MNIST image as ASCII art**:
  ```bash
  python3 inputs/mnist/txt/print_mnist.py 8
  ```

**Note:** `mnist_input2` and `mnist_input7` will be misclassified as `9` and `8`, respectively.

---

## Generating Your Own MNIST Inputs
1. Open a drawing tool (e.g., **Microsoft Paint**).  
2. Resize the image to **28x28 pixels** and draw a digit.  
3. Save it as a **.bmp** file inside:  
   ```bash
   inputs/mnist/student_inputs/
   ```
4. Convert the BMP to BIN format:  
   ```bash
   python3 inputs/mnist/student_inputs/bmp_to_bin.py example
   ```
5. Run classification:  
   ```bash
   java -jar tools/venus.jar src/main.s -ms -1 inputs/mnist/bin/m0.bin inputs/mnist/bin/m1.bin inputs/mnist/student_inputs/example.bin outputs/test_mnist_main/student_input_mnist_output.bin
   ```
Now you can classify your own handwritten digits!