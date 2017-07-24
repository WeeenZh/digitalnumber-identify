# digitalnumber-identify
labview recognizing digital number with vision assistant

First of all, the camera to collect the image gray-scale transformation, and then gray-scale image to enhance the local noise, automatic threshold segmentation to obtain binary images. Through the machine visual function, positioning the digital area, setting the character spacing, threshold, normalization and so on, through the optical character recognition OCR (opti-cal character recognition) training, get the character training set. Finally, the numbers are compared with the characters in the character training set and the recognition results are displayed.

# Image enhancement and denoising
Since the collected image is blurred by the large amount of noise, it is necessary to locally enhance the image. LUT (LookupTable) lookup table conversion technology improves contrast and brightness by improving the dynamic density of the contrast difference region. The system uses the histogram equalization processing and Gamma correction technology. Histogram equalization is through the conversion of the image of the gray-scale dynamic density becomes larger, so that the gray scale frequency smaller gray-scale conversion, the frequency will become larger, so that after conversion image gray histogram in a larger dynamic range Tends to be homogeneous, so that the image becomes clear. Gamma correction is to expand the high gray scale range while compressing the low gray scale range.
In addition, the actual image is inevitably there is internal and external interference, so image denoising is also an important step in image preprocessing. Median filtering is a commonly used filtering method, which can make the image smooth, but also to remove the noise in the image, and can make the image edge contours remain clear. The IMAQ Nth Order filter used in this paper is its extension.

# OCR training
OCR (Optical Character Recognition) training is an important step in this identification system. In this system, NI Vision Assistant's OCR training interface is used to train the characters to be recognized and the training results are saved as a standard character set. During training, by specifying the region of interest, adjust the spacing between discontinuous characters, use morphological corrosion operations to filter the irrelevant particles in the background, and normalize the threshold segmentation to extract a single character. Finally enter the characters that need to be trained to complete the production of the character set.

# Digital identification
In the digital recognition process, the IMAQ Vision function is used to retrieve the previously saved OCR-trained character set file, specify the region of interest, and then use the IMAQOCR Read Text 2 function to associate the number in the digital tube with the character set Character one by one comparison, select the most closely matched with the character set number, identify the digital tube in the number.

# Conclusion
The workflow of the whole program includes the following steps: the camera opens, displays the moving picture, starts the sampling image, intercepts the image, saves the image, binarizes, rotates the image, divides the image, loads the image, loads the image recognition document, Identify numbers. The final effect is to identify the program can be identified on the digital tube on the four positions of digital information.
In general, in the camera to collect the image quality is very good, complete the identification of basic no problem.
If the camera is affected by the light, the collected image quality is not high, subject to the binarization function level, the need for edge scanning steps will be affected, thus affecting the identification.
