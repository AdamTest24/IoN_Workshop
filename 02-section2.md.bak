---
title: "Neuro-Image Handling"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- 
-
-

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

-
-
-
::::::::::::::::::::::::::::::::::::::::::::::::

## Image Handling 


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


```python
image[0, 0]
```

```{.output}
array([255, 255, 255], dtype=uint8)
```


```python
fig, ax = subplots()

ax.imshow(image[50:70, 60:100]);

ax.set_xticklabels(());
ax.set_yticklabels(());

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-5-3.png" width="672" style="display: block; margin: auto;" />


```python
fig, ax = subplots()

ax.imshow(image[:,:, 2], cmap='gray');

ax.set_xticklabels(());
ax.set_yticklabels(());

show()
```

<img src="fig/02-section2-rendered-unnamed-chunk-6-5.png" width="672" style="display: block; margin: auto;" />


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
<PIL.Image.Image image mode=RGB size=154x327 at 0x7FD1CFE09090>
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

-
-
-

::::::::::::::::::::::::::::::::::::::::::::::::
[r-markdown]: https://rmarkdown.rstudio.com/
