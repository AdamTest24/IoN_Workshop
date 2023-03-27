---
title: "Neuro-Image Handling"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- How an image is read in Python?
- What does masking do?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explaining data in images
- Understanding image masking 

::::::::::::::::::::::::::::::::::::::::::::::::

## Image Handling 

### Reading and Processing Images
In biology, we often deal with images, for example from microscopy and different medical imaging modalities. In many cases, we wish to extract some quantitative information from these images. The focus of this session is to read and process images in Python. This includes:

- Working with 2-dimensional images
- Creating and applying binary image masks
- Working with 2-dimensional colour images, and interpreting colour channels

First, we want to read in an image. For this part of the lesson, we use a 2D image of brain part,Cerebellum, as an example. We use Matplotlib’s `image` module, from which we import `imread` to store the image in a variable called image. The function `imread` can interpret many different image formats, including jpg, png and tif images.




```python
from matplotlib.pyplot import subplots, show

from matplotlib.image import imread
```


```python
image = imread('fig/Cerebellum.jpg')

fig, ax = subplots()

ax.imshow(image);

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-2-1.png" width="672" style="display: block; margin: auto;" />


```python
image.shape
```

```{.output}
(154, 327, 3)
```

This tells us that our image is composed of 154 by 327 data units, or pixels as we are dealing with an image. It is equivalent to the image resolution. The array has three dimensions.  


```python
image[0, 0]
```

```{.output}
array([255, 255, 255], dtype=uint8)
```

The color intensities go up to 255. This is because RGB (red, green and blue) colours are defined within the range 0-255. 

Let us now use matplotlib.pyplot’s imshow function to plot the section of image to see what it looks like. The x and y coordinates are chosen to specify section of the image. 


```python
fig, ax = subplots()

ax.imshow(image[50:70, 60:100]);

ax.set_xticklabels(());
ax.set_yticklabels(());

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-5-3.png" width="672" style="display: block; margin: auto;" />

Each square is a pixel and it has one value. So how exactly are the pixel values assigned? By the numbers stored in the Numpy array, image.


```python
fig, ax = subplots()

ax.imshow(image[:,:, 2], cmap='gray');

ax.set_xticklabels(());
ax.set_yticklabels(());

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-6-5.png" width="672" style="display: block; margin: auto;" />

Here we assigned a grey colour map.


Now that we know that the images are composed of a set of intensities that are just numbers in a Numpy array, we can start using these numbers to process our image.

As a first approach, we can plot a histogram of the original image intensities. We use the `.ravel()` method to turn the original 154 x 327 array into a one-dimensional array with 503,58 values. This rearrangement allows the inclusion of an image as a single column in a matrix or dataframe!

The histogram plot shows how many of the intensities are found in one layer of this image:


```python
layer = 2

fig, ax = subplots()

ax.hist(image[:, :, layer][image[:, :, layer] < 255].ravel(), bins=500);

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-7-7.png" width="672" style="display: block; margin: auto;" />


```python
image.size
```

```{.output}
151074
```


```python
from PIL import Image

image = Image.open('fig/Cerebellum.jpg')

fig, ax = subplots()

ax.imshow(image);

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-9-9.png" width="672" style="display: block; margin: auto;" />


```python
type(image)
```

```{.output}
<class 'PIL.JpegImagePlugin.JpegImageFile'>
```



```python
image.show()
```


```python
image.entropy()
```

```{.output}
5.594248793777234
```


```python
image.rotate(-90, expand=True)
```

```{.output}
<PIL.Image.Image image mode=RGB size=154x327 at 0x7F5868598940>
```

## Image Masking



```python
from matplotlib.image import imread
from matplotlib.pyplot import subplots, show
```


```python
image = imread('fig/rose.jpg')

fig, ax = subplots()

ax.imshow(image);

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-15-11.png" width="672" style="display: block; margin: auto;" />

### Transpose Image

```python
image.shape
```

```{.output}
(3648, 2736, 3)
```


```python
image_t = image.transpose((1, 0, 2))

fig, ax = subplots()

ax.imshow(image_t)

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-17-13.png" width="672" style="display: block; margin: auto;" />

### Only red Component


```python
fig, ax = subplots()

ax.imshow(image_t[:, :, 0]);

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-18-15.png" width="672" style="display: block; margin: auto;" />

### Histogram of Red Component


```python
fig, ax, = subplots()

ax.hist(image_t[:, :, 0].ravel(), bins=500);

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-19-17.png" width="672" style="display: block; margin: auto;" />

### Masking the Red Component

```python
threshold = 90

mask = image_t[:, :, 0] < threshold

image_masked = image_t[:, :, 0] * mask

fig, ax = subplots(ncols=3)

ax[0].imshow(image_t[:, :, 0], cmap='gray')
ax[1].imshow(mask, cmap='gray')
ax[2].imshow(image_masked, cmap='gray');

fig.tight_layout()

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-20-19.png" width="672" style="display: block; margin: auto;" />

### False Colour

```python
fig, ax = subplots()

ax.imshow(image_masked);

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-21-21.png" width="672" style="display: block; margin: auto;" />

### Apply mask to all layers
Choose grey value for background


```python
image_new = image_t.copy()

grey_value = 100

image_new[mask, :] = grey_value


fig, ax = subplots()

ax.imshow(image_new);

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-22-23.png" width="672" style="display: block; margin: auto;" />


```python
fig.savefig('fig/rose_masked.png', format='png')
```


:::::::::::::::::::::::::::::::::::::keypoints 

- `imread` function is used to read images.
- `ravel` function flattens a multi-dimentional array into a single array.
- Image masking help in identifying objects based on colur intensities.

::::::::::::::::::::::::::::::::::::::::::::::::
[r-markdown]: https://rmarkdown.rstudio.com/
