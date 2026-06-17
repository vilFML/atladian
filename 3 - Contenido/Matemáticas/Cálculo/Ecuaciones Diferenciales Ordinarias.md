Con el análisis del cálculo se pudieron modelar comportamientos de la naturaleza con relaciones entre una función y sus propias derivadas, las cuales se denominan [[2 - Tags/Ecuaciones Diferenciales Ordinarias]] (EDO). Son 'ordinarias' por tener sólo una variable real con una derivada habitual. Para el caso de varias variables, se conocen como Ecuaciones Diferenciales Parciales (EDP).

### Ejemplos de EDOs
1. **Decaimiento Radioactivo**: Considerando un material radioactivo: "La tasa de decaimiento radioactivo es proporcional a la cantidad de isótopo existente en cada instante de tiempo." 
   Si $y(t)$ es la masa del material existente en el instante $t$, entonces:
   $$y'(t) = -\alpha \cdot y(t), \alpha > 0$$
   $\alpha > 0$ indica un decaimiento.
   Así, se debe buscar una función $y(t)$ tal que al derivarla ($y´(t)$), se obtenga el opuesto de la misma función $y(t)$:
   $$y(t) = C \cdot e^{\alpha \cdot t}, t \in \mathbb{R},  C \in \mathbb{R}$$