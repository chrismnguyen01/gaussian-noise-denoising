# gaussian-noise-denoising
## About
Denoising Gaussian Noise using Fast Fourier Transforms and gradient descent for ROF model with total variation minimization

## Features
* Custom Gaussian Noise function
* Masking numpy FFT
* Implement gradient descent for ROF model with total variation minimization

## Dependencies
* numpy
* cv2
* matplotlib
* skimage

## Fast Fourier Transform

## ROF Model
The goal of this project is to use gradient descent for ROF to denoise images. The noisiness, or energy, of images is determined by the following equation, as described by the ROF model:

\begin{align*}
E(u) = \lambda {||f - u||}^2_{L^2} + \int_{\Omega} ||\nabla u(x)||
\end {align*}

In this equation, $f$ is the original input image, and $u$ is a new denoised image. In order to decrease the energy of $u$, we take the gradient of $E(u)$, which returns a vector with the same dimensions of $u$. This vector contains the changes required for every pixel in order to move along the gradient of $E(u)$, which, by definition of a gradient, reduces $E(u)$. The gradient of $E(u)$ is:

\begin{align*}
\nabla E(u) = -2 \lambda ||f - u|| - \nabla \cdot \frac{\nabla u}{||\nabla u||}
\end {align*}

For each iteration, the algorithm calculates an image that has been slightly denoised from the previous image by subtracting $\nabla E(u)$ from the previous image:

\begin{align*}
u_{k+1} = u_k - \alpha \nabla E(u_{k+1})
\end{align*}

The best parameters, $\lambda$ and $\alpha$, are found to be $\lambda = 0.01$ and $\alpha = 0.5$. This process is repeated until $\nabla E(u) = 0.5$, resulting in the finalized denoised images below. Figures 1, 2, and 3 are the original noisy images, and figures 4, 5, and 6 are the finalized denoised images. Figure 7, 8, and 9 show  $\nabla E(u)$ for each iteration. 

The original noisy images are blurred using Gaussian noise, which randomly adjusts the brightness of each pixel using a normal distribution. This results in static in the images. The algorithm  removes most of the static in the noisy images, resulting in a final image with less noise. This denoising process can be improved by adjusting the contrast of the denoised images so that they are less faded, similar to the original image.
