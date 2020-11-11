# Benford-Analysis-For-Fraud-Detection
Benford law helps in detecting the irregularity in a set of numbers. It can be used to detect fraud in image forensics(detecting whether the image is real or fake) or it can also be used to analyze inning scores of a cricketer(predicting whether that cricketer was involved in match fixing or not).
## INTRODUCTION

In the year 1938, a physicist named Frank Benford published a paper with a law that states that 

> "In many naturally occuring collections of numbers, the first digit is likely to be small. As a matter of fact, the number 1 appears as the leading significant digit in about 30% of the whole collection, while 9 appears as the leading significant digit in about less than 5%".

For example, if you collect a set of numbers, then, according to Benford's Law, 30.1% of those numbers have 1 as their leading significant digit, 17.6% of those number have 2 as their leading signifcant digit and so on. The graph and the table below shows the Benford Curve stating the distribution

<div style="text-align:center"><img src="https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/Benford_Distribution.png?raw=true" /></div>

There were rumouirs that some Tax Agencies used Benford's Law to detect fraud activity in user accounts. They would take all the tax invoices and apply benford's law on the set of numbers(basically the tax payment done by individual users) and if the numbers doesnt add up to the benford distribution, then, that person would be in trouble. Obviously, neither the agencies aggreed to this usage of methodology nor did they decline. But this law became a state-of-the-art workflow to detect fraud in any domain that had numbers involved. 

Numbers written on the front page of the newspaper(date, number of people killed, etc) were collected and evaluated into this algorithm and the results were shocking. The number set followed ***Benford's Law distribution***. When I came to know about it, I couldnt believe it. What I had were some facts written in words and my mind cannot accept anything unless there is an implementation proving the law, on realtime data. Therefore, I performed certain analysis based on different types of realtime data to see whether Benford's Law was true or was it just ancient.

## Implementation

When I came to know about this law, I was very much excited to see its implementation in real life, not because I was curious, but I didnt believe it. As a Machine Learning Engineer, I had access to different types of data all around me. So i gathered a cricket statistics dataset of the master blaster, the one and only Sachin Tendulkar. I am a fan of his cover drive. 

There were two things that came in my mind at that time. Firstly, when he played, he got out at 99 a lot and secondly, there was always this group of people who used to blame sachin for a lost match saying "YE TO SIRF APNA RECORD MAINTAIN KRNE K LIYE KHELTA HAI". Well, it was time to clear out a lot. And I applied Benford' Law to two features of the dataset. One was "***runs per inning***" and the other was "***balls faced per inning***". Here is a snippet of the dataset that I used for this analysis.

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/cricket_dataset_snippet.png?raw=true)

The dataset contained 820 rows reflecting 820 innings(both Test and ODI) of the Master Blaster and 19 different features of each inning like Runs scored, minutes played, Balls faced, etc. As a result, after complete implementation of the runs and balls faced, I plotted 2 graphs with the expected distribution of feature w.r.t Benford's Law and the actual statistics of the distribution extracted from Sachin's dataset. And I was SHOCKED. It followed Benford's Law. Can you believe it???

I had no idea how it happened. I mean its not even in the hands of the batsman to decide how much runs he/she scores in an inning. And apparantly, his whole batting record followed Benford's Law. Below are the 2 result graphs with the two considered attributes from the dataset namely Runs and balls faced.

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/run_analysis.png?raw=true)

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/balls_faced_analysis.png?raw=true)

There are two points that I would like to make in order to conclude from the above graphical representations.

1. Benford's Law is a state-of-the-art law.
2. Sachin Tendulkar was a master class cricketer and he never fixed any matches according to me and Benford.


Now, it was time to take things more visual. So, I took an image and started to think what numeric information could be extracted from it. As we all know, images are made of pixels and the pixel value is typically an 8-bit data value (with a range of 0 to 255). Below is the image that I took for analysis.

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/original_image.png?raw=true)

I had to evaulate whether the pixels of this image followed Benford's Law or not. Using OpenCV2 and numpy libraries from Python3, I read the image and evaluated the discrete cosine transform as I had to remove all the background noise from the image for analysis. The discrete cosine transform (DCT) helps separate the image into parts (or spectral sub-bands) of differing importance (with respect to the image's visual quality). The DCT is similar to the discrete Fourier transform: it transforms a signal or image from the spatial domain to the frequency domain.

The general equation for a 2D (N by M image) DCT is defined by the following equation:

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/DCT_f1.png?raw=true)

and the corresponding inverse 2D DCT transform is simple F-1(u,v), i.e.:

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/dct_f2.png?raw=true)

For a detailed mathematical explaination to DCT, visit [here](https://cs.stanford.edu/people/eroberts/courses/soco/projects/data-compression/lossy/jpeg/dct.htm).

Next course of action was to flatten the 2D matrix into a 1D vector to ease the analysis of pixel numbers. After the complete analysis of the 1D pixel vector, I was shocked again. The feature vector clearly followed Benford's algorithm. The distribution of the digits among the pixel values in the vector was the same as suggested by Benford's Law. Below is the graph of the distribution of the digits in the feature vector with the actual distribution of the digits that Benford predicted.

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/original_image_analysis.png?raw=true)

The graph clearly says that the image is original/true as it follows Benford's Law. At that time I just wanted to clap looking at the beauty of numbers. 

After recovering from the previous shock, I did a little experiment. I modified the original image, by applying some filters on it. Now, the image is tampered and is no more original. Below is the tampered image that I will analyze to check whether it is a tempored image or not(based on Benford's Law).

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/modified_image.png?raw=true)

I followed the same methodogy as before, by firstly applying DCT(discrete cosine transform) on the image pixels and then, generating a 2D matrix of the same. Then, flattened the image 2D vector and generated a 1D vector for analysis. After analysis, the results totally shocked me again. It was crystal clear that the image was tampered as the distribution of the digits in the 1D vector did not follow Benford's Law. Below is the graph representing the distributions of digits in 1D vector of the tampered image with the benford predicted distribution.

![Alt text](https://github.com/sjaishanker/Benford-Analysis-For-Fraud-Detection/blob/master/doc_snippets/modified_image_analysis.png?raw=true)

Well, as it is clear from the difference in distribution, Benford's Law was able to detect the tampered image.

This all looks fascinating, now one can easily differentiate between an original image and a tampered image. This can clearly help in the scenarios where there are chances of frauds w.r.t the identity of a person.

## CONCLUSIONS

Benford's Law can be used for fraud detection in many fields. In this article, it was used to determine whether a cricketer was involved in match fixing or not, by analyzing his/her entire career scores and other features. After that, Benford's Law also helped in detecting tampered/modified images and distinguising it from the original one. These are some realtime applications that I thought would be useful.
