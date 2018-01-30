# tfzip
An experimental compression pipeline for TensorFlow.

# Goal
This project aims to implement a TensorFlow version of the Pruning neural networks by [Han et al.](https://arxiv.org/abs/1506.02626)

# Current Progress
### This project is still in the experimental stage, it is not currently ready for production use
### Pruning
- Initial results:
  - Running `compression_test.py` can generate uncompressed_model and compressed_model protobuf files from a simple MNIST model for comparison. (Original version is not optimized for tensorflow 1.4.0 version, it causes error and warning. Also, it set threshold constant value for all layers.)
  - Running 'compression_test2.py' can generate uncompressed_model and compressed_model protobuf files from a simple MNIST model for comparison. (This version is optimized for tensorflow 1.4.0 version, also change choosing threshold by setting standard deviation for each layers.)
  - Note that there is no difference in the protobuf file sizes until you apply `gzip` or some other compression tool.
  - The provided protobuf files were generated using a LeNet-300-100 model trained for MNIST digit classification.
  
|              | Parameters | Parameter Compression | Protobuf Size | Protobuf Size (gzipped) | Protobuf Compression | Accuracy |
|--------------|------------|-----------------------|---------------|-------------------------|----------------------|----------|
| Uncompressed | ~267k      |                       | 3.2MB         | ~2.8MB                  |                      | 98.19%   |
| Compressed1  | ~27k       | **~10x**              | 3.2MB         | ~490kB                  | **~6x**              | 97.31%   |
| Compressed2  | ~18k       | **~15x**              | 3.2MB         | ~290kB                  | **~10x**             | 97.38%   |
- Next steps:
  - Improve accuracy preservation and increase compression ratio.
    - [Learning both Weights and Connections for Efficient Neural Networks](http://arxiv.org/pdf/1506.02626v3.pdf) suggests ~12x parameter compression without loss of accuracy can be obtained for this architecture.  (maybe implemented by my version)
  - Refactor compression logic so that it can be more easily applied to other networks.

