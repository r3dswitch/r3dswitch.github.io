What are curves?
Locus of a point moving with one degree of freedom or one-parameter family of points.

How to represent curves?
Intrinsic Equations
Definition: depends only on the figure in question and not its relation to an external coordinate system. Therefore they are more localised compared to other forms.
Equations:
Curvature: $$ 1/ \rho = f(s) $$
Torsion: measure of how much a space curve deviates form a plane curve with s being the arc length.
$$ \tau = g(s) $$
Natural Equation: any equation connecting its curvature, torsion and arc length

Solving two natural equations simultaneously for curvature and torsion as functions of arc length produces intrinsic equations. Two natural equations determine a curve uniquely except it's position in space.

For plane curves, given the initial point of a curve, the variation of $\theta$ with arc length s can completely define a curve where $\theta$ is the angle subtended by the tangent to the curve with the x axis.
$$ \kappa = d\theta / ds $$
$$ dx/ds = \cos\theta, dy/ds = \sin\theta $$
Differentiating wrt s and substituting kappa we get the differential equations

$$d^2x/ds^2+\kappa(s)dy/ds = 0$$
$$d^2y/ds^2+\kappa(s)dx/ds = 0$$
Explicit Equations
In a plane, explicit equation takes the form: $y=f(x)$ with one y value for each x value.

Implicit Equations
To represent closed or multiple valued curves we use implicit equations of form: $f(x,y)=0$

Both implicit and explicit are axis dependant.

Every parametric form has an implicit form but not vice versa.

Parametric Equations
$p(u)=[x(u),  y(u),  z(u)]$ for space curves
$p(u,w)=[x(u,w), y(u,w), z(u,w)]$ for surfaces

one equation in x,y,z represents a surface, two independent equations represent the intersection of two surfaces which is locally a curve.

Conic Curves
A conic curve is defined by a second degree implicit equation

Points on a Curve
Direct Point Solution
Evaluate polynomial at predetermined increments of u

Horner's Rule: To evaluate a polynomial write it in nested form. 

De Casteljau Algorithm: Use recursion to evaluate polynomial. Uses n additions and n multiplications for a n degree polynomial.

Forward Differences Method: Uses n additions but rounding errors accumulate and subdivision doesn't always give good results.

Indirect Point Solution
Determine the value of the parameter u corresponding to a point p(u)