---
title: "Network Neuroscience"
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

## Neuron Network




```python
import networkx as nx
```

```{.error}
Error: ModuleNotFoundError: No module named 'networkx'
```

```python
from pandas import read_csv

from matplotlib.pyplot import subplots, show 
```

### The C elegans Neuron Network
#### Data Import

[Introduction to C elegans neurons](http://www.wormbook.org/chapters/www_celegansintro/celegansintro.html#sec5.4)

[C elegans neurons in the worm atlas](https://www.wormatlas.org/hermaphrodite/nervous/Neuroframeset.html)

Import the connectivity matrix.


```python
data = read_csv('data/celegans131matrix_50.csv', header=None, dtype = "int")

neurons = data.to_numpy()

print(len(neurons))
```

```{.output}
50
```


```python
fig, ax = subplots()

ax.imshow(neurons);

show()
```

<img src="fig/04-section4-rendered-unnamed-chunk-3-1.png" width="672" style="display: block; margin: auto;" />

Import the labels and convert the resulting dataframe into a dictionary. The function `to_dict` wraps the dictionary within a dictionary and therefore indexing is used to access the 'inner' dict.


```python
neuron_Names = read_csv('data/celegans131labels_50.csv', header=None)

neuronNames = neuron_Names.to_dict()

neuronLabels = neuronNames[0]

print(neuronLabels)
```

```{.output}
{0: 'ADFL', 1: 'ADFR', 2: 'ADLL', 3: 'ADLR', 4: 'AFDL', 5: 'AFDR', 6: 'AIAL', 7: 'AIAR', 8: 'AIBR', 9: 'AINL', 10: 'AINR', 11: 'AIZL', 12: 'AIZR', 13: 'ALA', 14: 'ASEL', 15: 'ASER', 16: 'ASGL', 17: 'ASGR', 18: 'ASHL', 19: 'ASHR', 20: 'ASIL', 21: 'ASIR', 22: 'ASJL', 23: 'ASJR', 24: 'ASKL', 25: 'ASKR', 26: 'AUAL', 27: 'AUAR', 28: 'AVAL', 29: 'AVAR', 30: 'AVBL', 31: 'AVBR', 32: 'AVDL', 33: 'AVDR', 34: 'AVEL', 35: 'AVER', 36: 'AVHL', 37: 'AVHR', 38: 'AVJL', 39: 'AVJR', 40: 'AVL', 41: 'AWAL', 42: 'AWAR', 43: 'AWBL', 44: 'AWBR', 45: 'AWCL', 46: 'AWCR', 47: 'BAGL', 48: 'BAGR', 49: 'CEPDL'}
```

### Graph Object and Network Display
The connectivity matrix can be converted to a Networkx graph.


```python
neuronGraph  = nx.from_numpy_matrix(neurons, 
                                    create_using=nx.DiGraph)   
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
neuronLayout = nx.random_layout(neuronGraph, seed=12)
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
nx.draw_networkx(neuronGraph, neuronLayout, 
        node_size=1000,
        labels=neuronLabels)
        
```

```{.error}
Error: NameError: name 'nx' is not defined
```

View the degrees:


```python
fig, ax = subplots()

ax.plot(dict(neuronGraph.degree).values(), '-o');
```

```{.error}
Error: NameError: name 'neuronGraph' is not defined
```

```python
ax.set_xlabel('Index');
ax.set_ylabel('Degree');

show()
```

<img src="fig/04-section4-rendered-unnamed-chunk-6-3.png" width="672" style="display: block; margin: auto;" />

The network displayed in circular layout:


```python
neuronGraph  = nx.from_numpy_matrix(neurons, 
                                    create_using=nx.DiGraph)   
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
neuronLayout = nx.circular_layout(neuronGraph)
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
nx.draw_networkx(neuronGraph, neuronLayout, 
        node_size=1000,
        labels=neuronLabels)
        
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
show()        
```

<img src="fig/04-section4-rendered-unnamed-chunk-7-5.png" width="672" style="display: block; margin: auto;" />

Find node indices:
The two BAG nodes 'BAGR' and 'BAGL' of the display (about 4 o'clock).


```python
for index, name in enumerate(neuronLabels.values()):
    
    if 'BAG' in name:
        
        print(neuronLabels[index], index)
```

```{.output}
BAGL 47
BAGR 48
```

## Anatomical Mapping

File 'celegans131positions_50.csv' contains information on how the nodes relate to each other in 2-D space. We can include this information to replace the layout.


```python
neuronPos = read_csv('data/celegans131positions_50.csv', header=None)

neuronPos.items
```

```{.output}
<bound method DataFrame.items of            0         1
0   0.082393 -0.000984
1   0.083279 -0.003184
2   0.082639 -0.013035
3   0.083279 -0.011512
4   0.086329 -0.002706
5   0.086463 -0.000980
6   0.065177  0.009346
7   0.059030  0.011512
8   0.075441  0.006123
9   0.061980 -0.006149
10  0.061969 -0.003429
11  0.048698  0.002706
12  0.057560  0.003184
13  0.094056 -0.013227
14  0.069112  0.000492
15  0.071767 -0.000735
16  0.077966 -0.007625
17  0.080095 -0.010287
18  0.075507  0.000492
19  0.078380 -0.000980
20  0.076982 -0.012789
21  0.077156 -0.011757
22  0.063455  0.006641
23  0.062704  0.009063
24  0.088542 -0.010084
25  0.088668 -0.009553
26  0.068620  0.006149
27  0.067113  0.005389
28  0.089526  0.001722
29  0.090872 -0.000245
30  0.069112 -0.004427
31  0.071767 -0.006368
32  0.061734 -0.001476
33  0.066378 -0.001470
34  0.082885  0.002214
35  0.084014  0.003184
36  0.072063 -0.008608
37  0.076421 -0.012737
38  0.067636 -0.009346
39  0.072992 -0.009798
40  0.060990  0.009063
41  0.077966 -0.002951
42  0.078380 -0.005389
43  0.079196 -0.003935
44  0.082789 -0.006858
45  0.078458  0.004919
46  0.078625  0.004164
47  0.112890  0.000492
48  0.114630  0.003184
49  0.094199 -0.016233>
```


```python
nx.draw_networkx(neuronGraph, neuronPos.values,
        node_size=1000,
        labels=neuronLabels)
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
show()
```

<img src="fig/04-section4-rendered-unnamed-chunk-10-7.png" width="672" style="display: block; margin: auto;" />



```python
new_pos = neuronPos.copy()
new_pos.values[:, 0] = -1*neuronPos.values[:, 0]

nx.draw_networkx(neuronGraph, new_pos.values,
        node_size=1000,
        labels=neuronLabels)
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
show()        
```

<img src="fig/04-section4-rendered-unnamed-chunk-11-9.png" width="672" style="display: block; margin: auto;" />

The two BAG nodes to the right of the display are the [sensory neurons used to monitor oxygen and carbon dioxide](https://www.wormatlas.org/neurons/Individual%20Neurons/BAGframeset.html).

Here is some background:
[BAG genes, functions and connections](http://wormweb.org/neuralnet#c=BAG&m=1)

The graph display is in Matplotlib and can be handled as such. E.g. for possible Node shapes see:
https://matplotlib.org/stable/api/markers_api.html#module-matplotlib.markers. 

If you have a multi-panel figure, specify the axes for the network with keyword argument `ax`:


```python
fig, ax = subplots(figsize=(14, 8), ncols=2)

nx.draw_networkx(neuronGraph, neuronLayout, 
        node_size=1000,
        labels=neuronLabels,
        ax=ax[0])
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
nx.draw_networkx(neuronGraph, neuronPos.values,
        node_shape='H',
        node_color='tomato',
        node_size=1300,
        labels=neuronLabels,
        ax=ax[1])
```

```{.error}
Error: NameError: name 'nx' is not defined
```

```python
ax[0].set_title('Circular view of C elegans network');
ax[1].set_title('Anatomical view of C elegans network');

show()
```

<img src="fig/04-section4-rendered-unnamed-chunk-12-11.png" width="1344" style="display: block; margin: auto;" />

:::::::::::::::::::::::::::::::::::::keypoints 

-
-
-

::::::::::::::::::::::::::::::::::::::::::::::::
[r-markdown]: https://rmarkdown.rstudio.com/
