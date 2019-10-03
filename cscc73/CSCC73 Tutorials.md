# CSCC73

## Tutorials

### TUT 3: Tuesday, September 24, 2019

#### Complex Numbers: Representations and Operations

**Imaginary unit:** $i = \sqrt{-1} (i^2 = -1)$

**Complex number:** $z = a + bi | a,b \in\mathbb{R}$. $a$ is called the "real" part and $bi$ is called the "imaginary" part. Note that the $+$ in this scenario is just an abuse of notation, it just separates the different parts from each other. As in the real and imaginary part cannot be added together.

Think of this $z=a+bi$ as a pair $(a,b)$ (a quantity that bundles two real numbers). We can use this representation to visualize it as a point on a plane, where the $x$-axis is the real number line and the $y$-axis is the imaginary line.

$\mathbb{C} = $ **the set of complex numbers**

$z = a+bi, z' = a' + b'i$

**Equality:** $z = z'$ iff $a = a'$ and $b = b'$

##### Operations on Complex Numbers

- **Addition**: $z + z' = (a + bi) + (a' + b'i) = (a + a') + (b + b')i$
- **Multiplication:** $z \cdot z' = aa' + ab'i + a'bi + bb'i^2  = (aa'-bb') + (ab' + a'b)i$

**Field**: a set of object with operation $(+,\cdot)$ with certain properties:

- Commutativity of $(+,\cdot)$
  - $z + z' = z' + z$
  - $z \cdot z' = z' \cdot z$
- Associativity of $(+,\cdot)$
  - $z + (z' + z'') = (z + z') + z''$
  - $z \cdot (z' \cdot z'') = (z \cdot z') \cdot z''$
- Additive and Multiplicative Identities
  - $\exists c, \forall z | z + c = z$ (for $\mathbb{C}$, $c = (0 + 0i) = 0 \in \mathbb{C}$)
  - $\exists c, \forall z | z\cdot c = z$ (for $\mathbb{C}, c = (1 + 0i) = 1 \in \mathbb{C}$)
- Additive and Multiplicative Inverses
  - $\exists c, \forall z | z + c = 0$ (for $\mathbb{C}$, this is $(-a) + (-b)i$ for $a + bi \in \mathbb{C}$)
  - $\exists c, \forall z | c\cdot z = 1$ (for $\mathbb{C}$, this is $(\frac{a}{a^2+b^2}) + (\frac{-b}{a^2+b^2})i$ for $a + bi \in \mathbb{C}$) (note that $a,b$ cannot both be 0)

#### Polar Coordinates

Complex numbers can also be expressed by $(r,\theta)$ where $r$ is the radius and $\theta$ is the angle.

The relationship with cartesian coordinates is:

- $a = r \cdot \cos \theta$
- $b = r \cdot \sin \theta$
- $z = a + bi = r(\cos\theta + i \sin\theta)$

#### Euler's Formula

$e^{i\theta} = \cos\theta + i\sin\theta$

Note: if $\theta = \pi$ then $e^{i\pi} = \cos\pi + i\sin\pi = -1 + 0$ so $e^{i\pi} + 1 = 0$

$z = a + bi = r(\cos\theta + i\sin\theta) = re^{i\theta}$

So now we can write the product of two complex numbers as such:

$z = re^{i\theta}, z' = r'e^{i\theta'}$ ($r$ is sometimes called the magnitude, $\theta$ is called the argument/phase)

$z\cdot z' = rr' e^{i(\theta + \theta')}$

Now consider the unit circle, we can represent it as $z = (1)e^{i\theta}$, so $r = 1$.

If we take two points on the unit circle and multiply them together, their $r$ (radius) will stay the same, but the angle may change. So the product of two numbers on the unit circle is another number on the unit circle.

#### $n$th roots of 1

$z^n = r^n e^{i\theta n} = e^{i2\pi k}$ where $(r = 1, \theta = \frac{2\pi}{n}k)$

so if $z^n = 1$ then $z^n = 1 = 1+ 0i = e^{i2\pi n}$

so $z = e^{i\frac{2\pi}{n}k}$

This results in