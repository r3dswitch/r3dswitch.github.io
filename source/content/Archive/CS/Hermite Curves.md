Algebraic Form
$p(u)= au^3+bu^2+cu+d$
The algebraic coefficients are not the most convenient way of controlling the shape of a curve
Geometric Form
$p(u)=F_1(u)p_0+F_2(u)p_1+F_3(u)p_0^{u}+F_4(u)p_1^{u}$
Where the F terms are Hermite Basis Functions

Hermite Basis Functions
Characteristics of HBFs:
- Universality: hold for all cubic Hermite curves
- Dimensional Independance: identical fro all coordinates
- Separation of Boundary Condition Effects

Even degree polynomials aren't used because they have odd degrees of freedom prohibiting symmetrical boundary conditions at the curve-segment end points.

Matrix Form
$p(u)=UM_FB$
$A=M_FB$
$B=M_F^{-1}A$
$$M_F^{-1}=\begin{pmatrix}
  0 & 0 & 0 & 1 \\
  1 & 1 & 1 & 1 \\
  0 & 0 & 1 & 0 \\
  3 & 2 & 1 & 0
\end{pmatrix}$$

Tangent Vectors
By varying the magnitude to the tangent vectors we can control the curvature at each end or fix location of some intermediate point.

If the magnitudes including signs of the tangent vectors are varied, then mid point (p(0.5)) will always lie in a plane that is parallel to both end point tangents.

Reparametrisation is then just another mapping between mappings

Three Point Interpolation

Four Point Interpolation

Conic Hermite Curves

Composite Hermite Curves

