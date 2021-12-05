edge detection
1. gradient 
2. laplacian

roberts, prewit, sobel

general method:
1. marr-hildreth

laplacian mask is a kind of high-pass filter, so the smoothing is necessarily performed before the laplacian.

we can first convolve the laplacian mask with the Gaussian mask to generate a LoG mask, then we convolve the LoG mask with the image.

the process of Marr-hildreth
1. filter the image with guassian mask
2. computes the Laplacian
3. find the zero crossing


drawbacks:
1. sensitive to noise and poor anti noise ability

2.7
how to get the best thresholding value???
using the otsu's method

Dilation expands the edge of image

opening is the compound operation of the Erosion followed by dilation.
opening is to remove some foreground pixels from the foreground regions and preserve the foreground region that can completely contain the structuring element
opening is less destructive the shape of the foreground pixels than erosion.

closing is the compound operation of the Dilation followed by erosion.
closing is to enlarge the boundaries of the foreground regions and shrink background holes in such regions
closing is less destructive the shape of the foreground pixels than dilation.

CC analysis:
1. recursive tracking
2. row-by-row
3. parallel growing