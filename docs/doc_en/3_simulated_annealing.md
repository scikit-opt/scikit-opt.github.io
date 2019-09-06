
## Simulated Annealing
SA(Simulated Annealing)
```python
from sko.SA import SA
def demo_func(x):
    x1, x2, x3 = x
    return x1 ** 2 + (x2 - 0.05) ** 2 + x3 ** 2

sa = SA(func=demo_func, x0=[1, 1, 1])
x_star, y_star = sa.fit()
print(x_star, y_star)

```

```python
import matplotlib.pyplot as plt
import pandas as pd

plt.plot(pd.DataFrame(sa.f_list).cummin(axis=0))
plt.show()
```
![sa](https://github.com/guofei9987/pictures_for_blog/blob/master/heuristic_algorithm/sa.png?raw=true)

## SA for TSP
Firstly, your data (the distance matrix). Here I generate the data randomly as a demo (find it in GA for TSP above)

DO SA for TSP
```python
from sko.SA import SA_TSP
sa_tsp = SA_TSP(func=demo_func, x0=range(num_points))
best_points, best_distance = sa_tsp.fit()
```

plot the result
```python
fig, ax = plt.subplots(1, 1)
best_points_ = np.concatenate([best_points, [best_points[0]]])
best_points_coordinate = points_coordinate[best_points_, :]
ax.plot(best_points_coordinate[:, 0], best_points_coordinate[:, 1], 'o-r')
plt.show()
```
![sa](https://github.com/guofei9987/pictures_for_blog/blob/master/heuristic_algorithm/sa_tsp.png?raw=true)
