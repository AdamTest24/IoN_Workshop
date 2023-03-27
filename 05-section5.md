---
title: "Neuro Images Clustering"
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

## Installing and using Nibabel Python Library



```python
from numpy import concatenate, zeros

from matplotlib.pyplot import subplots, tight_layout, show

import nibabel as nib
```

```{.error}
Error: ModuleNotFoundError: No module named 'nibabel'
```

### Load images and get data


```python
img_nibabel = nib.load("data/T1_mask.nii")
```

```{.error}
Error: NameError: name 'nib' is not defined
```

```python
type(img_nibabel)
```

```{.error}
Error: NameError: name 'img_nibabel' is not defined
```


```python
meta_info = img_nibabel.header
```

```{.error}
Error: NameError: name 'img_nibabel' is not defined
```

```python
print(meta_info)
```

```{.error}
Error: NameError: name 'meta_info' is not defined
```


```python
print(meta_info.get_xyzt_units())
```

```{.error}
Error: NameError: name 'meta_info' is not defined
```


```python
img1 = img_nibabel.get_fdata()
```

```{.error}
Error: NameError: name 'img_nibabel' is not defined
```

```python
print(type(img1), img1.shape)
```

```{.error}
Error: NameError: name 'img1' is not defined
```


```python
img_nibabel = nib.load("data/b0_mask.nii")
```

```{.error}
Error: NameError: name 'nib' is not defined
```

```python
img2 = img_nibabel.get_fdata()
```

```{.error}
Error: NameError: name 'img_nibabel' is not defined
```


```python
img1.shape
```

```{.error}
Error: NameError: name 'img1' is not defined
```



### plotting Images


```python
img_slice = 30
```


```python
fig, ax = subplots(ncols=2, figsize=(15, 5))

f1 = ax[0].imshow(img1[:, :, img_slice], cmap="gray")
```

```{.error}
Error: NameError: name 'img1' is not defined
```

```python
f2 = ax[1].imshow(img2[:, :, img_slice], cmap="gray")
```

```{.error}
Error: NameError: name 'img2' is not defined
```

```python
fig.colorbar(f1, ax=ax[0])
```

```{.error}
Error: NameError: name 'f1' is not defined
```

```python
fig.colorbar(f2, ax=ax[1]);
```

```{.error}
Error: NameError: name 'f2' is not defined
```

```python
ax[0].set_xlabel('T1 Image', fontsize=16);
ax[1].set_xlabel('B0 Image', fontsize=16);

show()
```

<img src="fig/05-section5-rendered-unnamed-chunk-9-1.png" width="1440" style="display: block; margin: auto;" />

## Data pre-processing

```python
img1_slice = img1[:, :, img_slice]
```

```{.error}
Error: NameError: name 'img1' is not defined
```

```python
img2_slice = img2[:, :, img_slice]
```

```{.error}
Error: NameError: name 'img2' is not defined
```
### Remove zeros

```python
fig, ax = subplots(ncols=2, figsize=(20, 5))

ax[0].hist(img1_slice.flatten(), bins=50)
```

```{.error}
Error: NameError: name 'img1_slice' is not defined
```

```python
ax[1].hist(img2_slice.flatten(), bins=50);
```

```{.error}
Error: NameError: name 'img2_slice' is not defined
```

```python
show()
```

<img src="fig/05-section5-rendered-unnamed-chunk-11-3.png" width="1920" style="display: block; margin: auto;" />


```python
mask = (img1_slice>0) & (img2_slice>0) 
```

```{.error}
Error: NameError: name 'img1_slice' is not defined
```

```python
img1_nz = img1_slice[mask]
```

```{.error}
Error: NameError: name 'img1_slice' is not defined
```

```python
img2_nz = img2_slice[mask]
```

```{.error}
Error: NameError: name 'img2_slice' is not defined
```

```python
fig, ax = subplots(nrows=1, ncols=2, figsize=(20, 5))

ax[0].hist(img1_nz, bins=50)
```

```{.error}
Error: NameError: name 'img1_nz' is not defined
```

```python
ax[1].hist(img2_nz, bins=50);
```

```{.error}
Error: NameError: name 'img2_nz' is not defined
```

```python
show()
```

<img src="fig/05-section5-rendered-unnamed-chunk-12-5.png" width="1920" style="display: block; margin: auto;" />

### Scaling

Standard Scaler: removing the mean and scaling to unit variance


```python
from sklearn.preprocessing import StandardScaler
```

```{.error}
Error: ModuleNotFoundError: No module named 'sklearn'
```

```python
scaler = StandardScaler()
```

```{.error}
Error: NameError: name 'StandardScaler' is not defined
```

```python
img1_scaled = scaler.fit_transform(img1_nz.reshape(-1, 1))
```

```{.error}
Error: NameError: name 'scaler' is not defined
```

```python
img2_scaled = scaler.fit_transform(img2_nz.reshape(-1, 1))
```

```{.error}
Error: NameError: name 'scaler' is not defined
```


```python
img1_scaled.shape
```

```{.error}
Error: NameError: name 'img1_scaled' is not defined
```

### Visualise and Concatenate

Seaborn: https://seaborn.pydata.org

c.f. pair grid example
https://seaborn.pydata.org/examples/pair_grid_with_kde.html

kdeplot documentation
https://seaborn.pydata.org/generated/seaborn.kdeplot.html


```python
fig, ax = subplots(1, 3, figsize=(20, 6))

# Scatter plot
ax[0].scatter(img1_nz, img2_nz)

# 2D Histogram
```

```{.error}
Error: NameError: name 'img1_nz' is not defined
```

```python
ax[1].hist2d(img1_nz, img2_nz, bins=50, vmax=10);
```

```{.error}
Error: NameError: name 'img1_nz' is not defined
```

```python
from seaborn import kdeplot

# Density Plot
```

```{.error}
Error: ModuleNotFoundError: No module named 'seaborn'
```

```python
kdeplot(x=img1_nz, y=img2_nz, ax=ax[2]);
```

```{.error}
Error: NameError: name 'kdeplot' is not defined
```

```python
show()
```

<img src="fig/05-section5-rendered-unnamed-chunk-15-7.png" width="1920" style="display: block; margin: auto;" />

### Scaled Images


```python
fig, ax = subplots(1, 3, figsize=(20, 6))

# Scatter plot
ax[0].scatter(img1_scaled[:,0], img2_scaled[:,0])

# 2D Histogram
```

```{.error}
Error: NameError: name 'img1_scaled' is not defined
```

```python
ax[1].hist2d(img1_scaled[:,0], img2_scaled[:,0], bins=50, vmax=10);
```

```{.error}
Error: NameError: name 'img1_scaled' is not defined
```

```python
from seaborn import kdeplot

# Density Plot
```

```{.error}
Error: ModuleNotFoundError: No module named 'seaborn'
```

```python
kdeplot(x=img1_scaled[:,0], y=img2_scaled[:,0], ax=ax[2]);
```

```{.error}
Error: NameError: name 'kdeplot' is not defined
```

```python
show()
```

<img src="fig/05-section5-rendered-unnamed-chunk-16-9.png" width="1920" style="display: block; margin: auto;" />


```python
all_img_scaled = concatenate([img1_scaled, img2_scaled], axis=1)
```

```{.error}
Error: NameError: name 'img1_scaled' is not defined
```

```python
all_img_scaled.shape
```

```{.error}
Error: NameError: name 'all_img_scaled' is not defined
```
## Segmenting images with Gaussian Mixtures

### GMM clustering


```python
from sklearn.mixture import GaussianMixture
```

```{.error}
Error: ModuleNotFoundError: No module named 'sklearn'
```


```python
n_components = 3

RANDOM_STATE = 12345

gmm = GaussianMixture(n_components=n_components, 
                      random_state=RANDOM_STATE)
```

```{.error}
Error: NameError: name 'GaussianMixture' is not defined
```

```python
all_img_labels = gmm.fit_predict(all_img_scaled)
```

```{.error}
Error: NameError: name 'gmm' is not defined
```

```python
all_img_labels[0]
```

```{.error}
Error: NameError: name 'all_img_labels' is not defined
```


```python
fig, ax = subplots(figsize=(8, 8))

ax.scatter(img1_nz, img2_nz, c=all_img_labels, s=100)
```

```{.error}
Error: NameError: name 'img1_nz' is not defined
```

```python
ax.set_xlabel('Image 1', fontsize=16)
ax.set_ylabel('Image 2', fontsize=16);

show()
```

<img src="fig/05-section5-rendered-unnamed-chunk-20-11.png" width="768" style="display: block; margin: auto;" />


```python
all_img_labels_mapped = zeros(img1_slice.shape)
```

```{.error}
Error: NameError: name 'img1_slice' is not defined
```

```python
all_img_labels_mapped[mask] = all_img_labels
```

```{.error}
Error: NameError: name 'all_img_labels' is not defined
```


```python
fig, ax = subplots(figsize=(20, 10))

ax.imshow(all_img_labels_mapped);
```

```{.error}
Error: NameError: name 'all_img_labels_mapped' is not defined
```

```python
show()
```

<img src="fig/05-section5-rendered-unnamed-chunk-22-13.png" width="1920" style="display: block; margin: auto;" />

:::::::::::::::::::::::::::::::::::::keypoints 

-
-
-

::::::::::::::::::::::::::::::::::::::::::::::::
[r-markdown]: https://rmarkdown.rstudio.com/
