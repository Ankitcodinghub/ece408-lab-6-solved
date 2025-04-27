# ece408-lab-6-solved
**TO GET THIS SOLUTION VISIT:** [ECE408 Lab 6 Solved](https://www.ankitcodinghub.com/product/ece408-objective-solved-7/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;124012&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;ECE408 Lab 6 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
The lab’s objective is to implement a tiled image convolution using both shared and constant memory as discussed in class. Like what’s discussed in class, we will have a constant 5×5 convolution mask, but will have arbitrarily sized image (We will assume the image dimensions are greater than 5×5 in this Lab).

Convolution is used in many fields, such as image processing where it is used for image filtering. A standard image convolution formula for a 5×5 convolution filter M with an Image I is:

where P_{i,j,c} is the output pixel at position i,j in channel c, I_{i,j,c} is the input pixel at i,j in channel c (the number of channels will always be 3 for this MP corresponding to the RGB values), and M_{x,y} is the mask at position x,y.

Prerequisites

Before starting this lab, make sure that:

Input Data

The input is an interleaved image of height x width x channels. By interleaved, we mean that the the element I[y][x] contains three values representing the RGB channels. This means that to index a particular elementâ€™s value, you will have to do something like:

index = (yIndex*width + xIndex)*channels + channelIndex;

For this assignment, the channel index is 0 for R, 1 for G, and 2 for B. So, to access the G value of I[y][x], you should use the linearized expression I[(yIndex*width+xIndex)*channels + 1].

For simplicity, you can assume that channels is always set to 3.

Instruction

Edit the code in the code tab to perform the following:

allocate device memory copy host memory to device initialize thread block and kernel grid dimensions

invoke CUDA kernel copy results from device to host deallocate device memory

implement the tiled 2D convolution kernel with adjustments for channels

use shared memory to reduce the number of global accesses, handle the boundary conditions in when loading input list elements into the shared memory

Instructions about where to place each part of the code is demarcated by the //@@ comment lines.

Pseudo Code

Your sequential pseudo code would look something like

maskWidth := 5

maskRadius := maskWidth/2 # this is integer division, so the result is 2 for i from 0 to height do for j from 0 to width do for k from 0 to channels accum := 0

for y from -maskRadius to maskRadius do for x from -maskRadius to maskRadius do xOffset := j + x yOffset := i + y

if xOffset &gt;= 0 &amp;&amp; xOffset &lt; width &amp;&amp; yOffset &gt;= 0 &amp;&amp; yOffset &lt; height then

imagePixel := I[(yOffset * width + xOffset) * channels + k] maskValue := K[(y+maskRadius)*maskWidth+x+maskRadius] accum += imagePixel * maskValue end end end

# pixels are in the range of 0 to 1

P[(i * width + j)*channels + k] = clamp(accum, 0, 1) end end end

where clamp is defined as

def clamp(x, start, end) return min(max(x, start), end) end

Input Format

For people who are developing on their own system. The images are stored in PPM (P6) format, this means that you can (if you want) create your own input images. The easiest way to create image is via external tools. You can use tools such as bmptoppm. The masks are stored in a CSV format. Since the input is small, it is best to edit it by hand.
