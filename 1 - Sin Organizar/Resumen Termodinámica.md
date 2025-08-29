
---

# 1. Orígenes y propósito de la termodinámica

En la revolución industrial, surgió la necesidad de estudiar la eficiencia de las máquinas de vapor. La termodinámica nace de la búsqueda de optimizar recursos bajo el principio de sustentabilidad: **satisfacer necesidades presentes sin comprometer las futuras**.

Las **leyes de la termodinámica** imponen límites a la eficiencia energética:
1. **Primera Ley:** La energía no se crea ni se destruye, sólo se transforma. (*"No podemos ganar"*).
2. **Segunda Ley:** No se puede usar toda la energía disponible, excepto en el cero absoluto (*condición de empate*).
3. **Tercera Ley:** Es imposible alcanzar el cero absoluto (*"No se puede empatar"*).

---

# 2. Información y complejidad en sistemas físicos

En mecánica, describir el movimiento de una partícula requiere **posición** y **velocidad**:
$$
 r = (x,y,z), \quad \dot{r} = (r_x,r_y,r_z)
$$
Se necesitan **6 números** por partícula.

Para un gas (con $10^{23}$ partículas), describir microdetalles excede la capacidad de almacenamiento y cómputo.

**Ejemplo:** Rebote de una pelota. Energía inicial = energía potencial gravitatoria. Tras el rebote, hay pérdida de energía. ¿Dónde está esa energía? → Se dispersó en configuraciones microscópicas inaccesibles.

---

# 3. Probabilidad, información faltante y entropía

El **factor de probabilidad** mide la ocurrencia de eventos:
$$
0 \leq x_i \leq 1, \quad \sum_i x_i = 1
$$

La incertidumbre se mide con una función $f(x)$ que cumple ciertas propiedades. Su forma es:
$$
f(x) = -K \ln(x), \quad K > 0
$$

La **información faltante promedio** es:
$$
I = -K \sum_{i=1}^{\Omega} x_i \ln(x_i)
$$
- $I=0$ si un evento es seguro ($x_i=1$).
- $I$ es máxima si todos los eventos son equiprobables.

En bits:
$$
I = -\sum_i x_i \log_2(x_i)
$$

Ejemplo: Una memoria de $n$ casillas tiene $2^n$ configuraciones posibles.

---

# 4. Microestado, macroestado y configuraciones accesibles

- **Microestado:** Especifica las variables de cada partícula.
- **Macroestado:** Descripción en variables globales (P, V, T, etc.). Un macroestado puede provenir de muchos microestados.

El número de microestados que corresponden a un macroestado son las **configuraciones accesibles ($\Omega$)**.

Propiedades:
- $\Omega$ es multiplicativo: $\Omega_{A \cup B} = \Omega_A \cdot \Omega_B$.
- Crece rápidamente con la energía disponible.

---

# 5. Entropía: la medida de la información faltante

Definición:
$$
S = k_B \ln \Omega
$$

Propiedades:
- Aditiva: $S_{A \cup B} = S_A + S_B$.
- Máxima en equilibrio → todas las configuraciones son equiprobables.

**Observaciones:**
- Clausius: La entropía mide la capacidad transformadora de un sistema.
- Landauer: Borrar memoria disipa energía en forma de calor.

---

# 6. Segunda Ley de la Termodinámica

**Enunciado:** En un sistema aislado, la entropía nunca decrece:
$$
\Delta S \geq 0
$$

### Procesos
- **Reversible:** $\Delta S = 0$.
- **Irreversible:** $\Delta S > 0$.

### Ligaduras
Una restricción limita la evolución del sistema. Relajarla incrementa configuraciones accesibles:
$$
\Omega_f \geq \Omega_i \quad \Rightarrow \quad S_f \geq S_i
$$

### Sistemas no aislados
Para el universo local (sistema + medio):
$$
S_U = S_{sist} + S_{medio}
$$
Si el sistema disminuye su entropía, el medio la aumenta.

---

# 7. El sentido del tiempo

- **Microscópico:** Las leyes de Newton son reversibles temporalmente.
- **Macroscópico:** La entropía crece, estableciendo una flecha del tiempo.

### Distribución binomial
Para $N$ partículas repartidas en dos cámaras:
$$
P_N[m] = \frac{N!}{m!(N-m)!}\cdot \frac{1}{2^N}
$$

Esto describe probabilísticamente los estados accesibles.

---

# 8. Modelos termodinámicos

En un gas ideal:
$$
E = \sum_{i=1}^n \tfrac{1}{2}m v_i^2
$$
El número de configuraciones accesibles resulta:
$$
\Omega = cte \cdot V^N \cdot E^{\tfrac{3N}{2}}
$$

La entropía:
$$
S - S_0 = Nk \ln \left(\frac{V}{V_0}\right) + \tfrac{3}{2}Nk \ln \left(\frac{E}{E_0}\right)
$$

### Procesos
1. **Reversibles (isentrópicos).**
2. **Cuasiestáticos.**
3. **Reales (irreversibles).**

---

# 9. Trabajo y calor

### Trabajo macroscópico
$$
\mathbb{W} = \vec{F}\cdot d\vec{s}
$$

### Trabajo volumétrico
$$
\delta W = -P\, dV
$$

El trabajo depende del camino seguido.

### Otros trabajos
- **Eléctrico:** $\mathbb{W} = \phi d\Theta$
- **Tensión superficial:** $\mathbb{W} = \alpha dA$

### Experimentos históricos
- **Teoría del calórico** (Lavoisier, Rumford).
- **Joule:** Equivalencia entre trabajo y calor.

**Diferencia:**
- Trabajo: transferencia de energía vía variables macroscópicas.
- Calor: transferencia vía grados microscópicos (vibraciones).

---

# 10. Primera Ley de la Termodinámica

**Conservación de la energía:**
$$
dE = \delta Q + \delta W
$$

En un universo local aislado:
$$
 dE_U = 0
$$

---

# 11. Magnitudes termodinámicas y ecuación fundamental

- **Extensivas:** $E, V, S, N, M$
- **Intensivas:** $T, P$, etc.

La **ecuación fundamental** relaciona magnitudes extensivas:
$$
F(X_1, X_2, \dots, X_n) = 0
$$

En la representación de energía:
$$
E = E(S,V,N,\dots)
$$

**Ejemplo gas ideal monoatómico:**
$$
S - S_0 = Nk \ln\left(\frac{V}{V_0}\right) + \tfrac{3}{2}Nk \ln\left(\frac{E}{E_0}\right)
$$

---
