Download Link: https://assignmentchef.com/product/solved-elec4622-project-2
<br>
This is the second of three mini-projects to be demonstrated and assessed within the regular scheduled laboratory sessions. This project is due in Week 11. The project is worth a nominal 10 marks, out of the 30 marks available for the laboratory component of the course. However, there are two optional taskss which attract a lot of potential bonus marks.

In this project, you will implement and understand the Laplacian of Gaussian (LOG) filter. LOG filtering plays an important role in edge detection for image analysis. From an educational point of view, LOG filters also provide an excellent demonstration of the important connection between discrete and continuous LSI operators — derivative operators in particular. Further, the project will help to familiarize you with scale-space concepts. In the remainder of this introduction, we provide a brief overview of the theory behind LOG filtering.

1.1              The Laplacian Operator in Continuous Space

Let <em>f </em>(<strong>s</strong>) denote a spatially continuous signal. Throughout this treatment <strong>s</strong>≡ (<em>s</em><sub>1</sub><em>,s</em><sub>2</sub>) is a two-dimensional spatial location, although everything works for any number of spatial dimensions. In continuous space, the gradient operator is well-defined. Specifically, <em>f </em>is the vector field

which measures the rate of change of intensity in each of the vertical and horizontal directions. In the Fourier domain, we know that

where <em>D</em>ˆ<sub>1 </sub>(ω) = <em>jω</em><sub>1 </sub>and <em>D</em>ˆ<sub>2 </sub>(ω) = <em>jω</em><sub>2 </sub>are the transfer functions of the horizontal and vertical derivative operators, respectively. Of course, differentiation is an LSI operator (i.e., a filter), so that differentiation is nothing other than convolution in the continuous space domain, using PSF’s <em>D</em><sub>1 </sub>(<strong>s</strong>) = F−<sup>1 </sup>(<em>jω</em><sub>1</sub>) and <em>D</em><sub>2 </sub>(<strong>s</strong>) = F−<sup>1 </sup>(<em>jω</em><sub>2</sub>), respectively.

The Laplacian operator         <sup>2</sup>produces the scalar field

1

Figure 1: Horizontal profile of a vertical edge.

In vector calculus, the Laplacian operator is sometimes written as · . In fact, in the Fourier domain, the Laplacian operator behaves exactly like a dot product. Specifically, we have

Of course, the Laplacian operator is also LSI, so that the operation can also be viewed as a convolution in the space domain.

One important property of the laplacian operator is that it is isotropic. That is, the operation is invariant to rotation. This is easy to see, since

is circularly symmetric in the Fourier domain, meaning that the operator’s PSF must also be circularly symmetric.

Together, the second derivative and isotropic properties of the Laplacian operator have useful implications for its behaviour in the presence of edges. Suppose the spatially continuous image <em>f </em>(<strong>s</strong>) contains a vertical edge, so that <em>f </em>(<em>s</em>1<em>,s</em>2) = <em>f</em>edge (<em>x</em><sup>)</sup>|<em><sub>x</sub></em><sub>=<em>s</em></sub>2 <em>,</em>

where <em>f</em><sub>edge </sub>is the edge profile illustrated Figure 1. A reasonable definition for the location of the edge is the point <em>s</em><sub>2 </sub>= <em>x</em><sub>0 </sub>at which <sub>edge </sub>equals 0. Now

<em>,</em>

since all vertical derivatives of a vertical edge are zero. It follows that the edge location coincides with the zero crossing of the Laplacian <sup>2</sup><em>f </em>(<strong>s</strong>). Although we have considered only horizontal edges, the rotational invariance of the Laplacian operator ensures that the same property should hold for edges of all orientations. That is, the location of an edge in any orientation is well described by the zero crossings of <sup>2</sup><em>f </em>(<strong>s</strong>).

2

1.2              The LOG Operator in Continuous Space

One major problem with the Laplacian operator, as it stands, is that derivatives are very sensitive to noise. One way to see this is that the Laplacian operator amplifies high frequency components by. This amplification process strongly affects white noise which has constant power at all frequencies. The noise-free signal itself usually has most of its energy at lower frequencies. Even “high frequency” features such as sharp edges produce power spectra which are located at DC in the parallel direction and decay as  in the transverse direction.

To reduce the sensitivity to noise, we can think of first applying a low-pass filter to the image <em>f </em>(<strong>s</strong>). Gaussian filters are a natural candidate since they do not impact the circular symmetry of the Laplacian operator. The LOG operation may then be expressed in the Fourier domain as

Here, <em>σ</em><sup>2 </sup>is the variance of the Gaussian PSF

.

Notice that instead of low-pass filtering <em>f </em>and then taking the second derivatives of the result, we can just filter <em>f </em>directly with, where

(1)

In fact ∇<sup>2</sup><em><sub>σ </sub></em>is the just              <sup>2</sup><em>G</em><em>σ</em>, having PSF

(2)

It follows that the zero crossings of the LOG filtered image, <em>g</em><em>σ </em>(<strong>s</strong>), identify the locations of edges in the (Gaussian) low-pass filtered original image. The single parameter <em>σ</em><sup>2</sup>, determines the scale of the edge detection process: large values of <em>σ</em><sup>2 </sup>eliminate all but the lowest frequency components so that the edges of larger image features are detected; small values of <em>σ</em><sup>2 </sup>allow more rapid changes in the filtered image, so that the smaller image features can be detected.

1.3          Discrete LOG Filters

As discussed in Chapter 2 of your lecture notes, and also in lectures, Gaussian filtering can be implemented directly by discrete convolution with PSF

<em>G</em><em>σ </em>[<strong>n</strong>] = <em>G</em><em>σ </em>(<strong>s</strong>)|<strong>s</strong><sub>=<strong>n </strong></sub>,

so long as the variance is sufficiently large to ensure that <em>G</em><em>σ </em>is effectively Nyquist bandlimited — i.e., <em>G</em><em>σ </em>(ω) ≈ 0 for ω∈<em>/ </em>[−<em>π,π</em>]<sup>2</sup>. According to equation (1), ∇f<sup>2</sup><em><sub>σ </sub></em>(ω) also decays exponentially, but grows only quadratically, so the same argument shows that the LOG operator can be implemented with high accuracy,f by discrete convolution with

<em>,</em>

so long as <em>σ</em><sup>2 </sup>is sufficiently large.

You should expand equation (2), both for your practical implementation in this project and also to convince yourself that can be well approximated by an FIR filter. You need to make your own

(sensible) judgements concerning the region of support for this FIR filter.

<h1>1           Tasks</h1>

The tasks presented below build progressively on one another. For demonstration purposes, you may like to create a separate project for each task, within a single workspace. You can do this by using the “File → New → Project” option in Visual C++, replacing the “Create new solution” option with “Add to solution”.

Task 1: (3 marks) Write a C/C++ program which can perform LOG filtering on a monochrome or colour BMP image, writing the result to a new BMP image.

<ul>

 <li>Your program should accept the value of <em>σ </em>as one of its command-line arguments, for testing purposes. This means that the program should dynamically adjust its filter coefficients (and filter region of support) according to the value of <em>σ</em>.</li>

 <li>For this task, you should implement the FIR filter directly, using floating point arithmetic.</li>

 <li>Your program should accept a real-valued scaling factor <em>α </em>as another of its command-line arguments, that allows the LOG filtered values to be scaled prior to writing them to the output image file, so as to facilitate visual inspection.</li>

 <li>Noting that the sample values output by your LOG filter are naturally centred about 0, you should add 128 to all values prior to writing the output file.</li>

 <li>Be prepared to comment on the images you recover using the algorithm.</li>

</ul>

Task 2: (2 marks) The LOG filter itself is not separable; however, it is a sum of two separable filters. In this task, you modify the program created in Task 1 to exploit this separability for a more efficient implementation.

<ul>

 <li>Processing should still be performed in floating point arithmetic, for simplicity.</li>

 <li>Use release builds to compare the speed of your two implementations (Task 1 and Task 2). Make an electronic record of your results, but also be prepared to demonstrate the timing during the laboratory demonstration in Week 10.</li>

</ul>

Task 3: (2 marks) Modify your program to write a sequence of output images, corresponding to progressively larger values of <em>σ</em>, so that you can put this image sequence into a single (MFLEX) video file with the Media Interface tools and play it back. The resulting sequence of images is a type of scale space. Your modified program should accept arguments that identify minimum and maximum values for <em>σ</em>, i.e., <em>σ</em><sub>min </sub>and <em>σ</em><sub>max</sub>, along with the total number of scales <em>N</em><em>σ</em>, producing <em>N</em><em>σ </em>images whose scales <em>σ </em>are spaced logarithmically between <em>σ</em><sub>min </sub>and <em>σ</em><sub>max</sub>.

Task 4: (3 marks) Modify your program from Task 2 or Task 3 (your choice) to produce a candidate edge map for each scale <em>σ </em>— only one scale if you modify Task 2.

4

<ul>

 <li>The output from your program should be an image with only two values: 0 or 255, where 255 corresponds to a potential edge location.</li>

 <li>Notionally, the value 255 should be written to locations that correspond to zero crossing in the underlying spatially continuous LOG-filtered image. However, since you only have a discrete LOG-filtered image you will have to come up with (or research) an appropriate heuristic based on the immediate neighbours of each pixel, to determine whether a zero-crossing is likely to occur nearby.</li>

 <li>It is acceptable for your program to work only with monochrome input images, but to support colour images in this task it is sufficient to perform the same operation on each colour plane, producing a colour edge map where a non-zero value (255) in any colour plane corresponds to a potential zero-crossing in the plane’s LOG-filtered sample values.</li>

</ul>

Task 5: (optional, up to 2 bonus marks) Modify your program from Task 2 to work with integer sample values and all integer arithmetic — additions, multiplications and shifts.

Task 6: (optional, up to 2 bonus marks) Modify your program from Task 4 to add a simple morphological dilation stage, in which the potential zero-crossings are considered to be the foreground pixels, and the structuring set for the dilation operation is the 3 × 3 cross

It is important that you be able to quickly show the edge maps you obtain both before and after dilation, so both images should be output by your program.