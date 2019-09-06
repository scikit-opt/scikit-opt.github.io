
## repo

[reop](https://github.com/guofei9987/scikit-opt)


## install

```bash
pip install scikit-opt
```

## Getting started
```python
demo_func=lambda x: x[0]**2 + x[1]**2 + x[2]**2
ga = GA(func=demo_func,n_dim=3, max_iter=500, lb=[-1, -10, -5], ub=[2, 10, 2])
best_x, best_y = ga.fit()
```

## do with UDF
**UDF** (user defined function) will be available in the next release! (version 0.2)

For example, if you just worked out a new type of `selection` function.  
Your `selection` function is like this:
```python
def selection_elite(self, FitV):
    '''
    A new selection strategy.
    This strategy makes the elite (defined as the best one for a generation)
    100% survive the selection
    '''
    print('udf selection actived')

    FitV = (FitV - FitV.min()) / (FitV.max() - FitV.min() + 1e-10) + 0.2
    # the worst one should still has a chance to be selected
    # the elite(defined as the best one for a generation) must survive the selection
    elite_index = np.array([FitV.argmax()])

    # do Roulette to select the next generation
    sel_prob = FitV / FitV.sum()
    roulette_index = np.random.choice(range(self.size_pop), size=self.size_pop - 1, p=sel_prob)
    sel_index = np.concatenate([elite_index, roulette_index])
    self.Chrom = self.Chrom[sel_index, :]  # next generation
    return self.Chrom
```

Regist your udf to GA
```python
from sko.GA import register_udf
GA_1 = register_udf({'selection': selection_elite})
```

Now do GA as usual
```python
demo_func = lambda x: x[0] ** 2 + (x[1] - 0.05) ** 2 + x[2] ** 2
ga = GA_1(func=demo_func, n_dim=3, max_iter=500, lb=[-1, -10, -5], ub=[2, 10, 2])
best_x, best_y = ga.fit()
#
print('best_x:', best_x, '\n', 'best_y:', best_y)
```
>Until Now, the **udf** surport `crossover`, `mutation`, `selection`, `ranking` of GA



## other


[donate me](https://guofei9987.github.io/donate/)
