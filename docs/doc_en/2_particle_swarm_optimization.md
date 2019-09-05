## 2. PSO(Particle Swarm Optimization)


```py
def demo_func(x):
    x1, x2, x3 = x
    return x1 ** 2 + (x2 - 0.05) ** 2 + x3 ** 2

pso = PSO(func=demo_func, dim=3)
fitness = pso.fit()
print('best_x is ',pso.gbest_x)
print('best_y is ',pso.gbest_y)
pso.plot_history()
```


![GA_TPS](https://github.com/guofei9987/pictures_for_blog/blob/master/heuristic_algorithm/pso.png?raw=true)
