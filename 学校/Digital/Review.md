edge detection
1. gradient 
2. laplacian

roberts, prewit, sobel

general method:
1. marr-hildreth

laplacian mask is a kind of high-pass filter, so the smoothing is necessarily performed before the laplacian.

we can first convolve the laplacian mask with the Gaussian mask to generate a LoG mask, then we convolve