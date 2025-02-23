# -10-points-Problem-1.1..3
18.330 Problem set 3

**Download Link:https://programming.engineering/product/18-330-problem-set-3/**

Description
5/5 – (2 votes)
Exercise 1: Algorithmic differentiation

Complete the implementation of the Dual type from class, including deriva-tives for subtraction, division, and integer powers. For / you may assume that the denominator is not zero.

Add methods for each function to e.g. add a real number (type ::Real) to a Dual. Treat a real number as having derivative 0.

Put these definitions in a file dual.jl. This may be included with in-clude(“dual.jl”) from Juno or Jupyter, or from another file.

(You must make sure the files are in the same directory, or give the path to the file on your machine.)

For functions such as exp, we define the action of the function on a Dual using

( + ) = ( ) + ′( )

Use this to define exp, sin and log on Dual numbers.

Write a function derivative that takes a function and a point , and uses Dual numbers to calculate the derivative ′( ) of at . It should return only the derivative.

Define a function to calculate the directional derivative of a function ∶ ℝ → ℝ in a direction v.

Use this to write a function partial to calculate the th partial derivative of a function.

Write functions to calculate the gradient and Jacobian of a function∶

ℝ .

Write a few tests of the functions you have written. Use simple functions for which you can do the calculations by hand to write the tests.

Exercise 2: Newton for higher-dimensional functions

Implement the multidimensional Newton method. It should take a function and an initial guess 0.

You should preferably use your own function from [Exercise 1] for cal-culating the Jacobian. You may also use instead the function Forward-Diff.jacobian from the ForwardDiff.jl package.


You should first do a basic check that does the right thing by checking if ( 0) is of the same dimension as 0.

Iterate until the residual is small enough or until some maximum number of iterations is reached. To check the residual, use the norm function from the standard library LinearAlgebra package. This calculates the “size” (length) of a vector.

The function should return a pair (flag, r), where flag is a Boolean that indicates if a root was found, and r is the location of the root (if one was found).

2. Consider the nonlinear system

2

2

+

2

= 3

(1)

2

(2)

(

2

)

+ ( − )

= 1

Make a plot of the two functions for = 0.5. How many roots are there?

From your plot, identify by eye approximately where the top right root is. Use the Newton method to find it accurately.

Find the order of convergence of the method in this case. (As usual you probably need BigFloat to get a good result.)

Make a function all_roots that searches for all roots in a given rectangular box. (The size of the box should be given as arguments to the function). It should keep a list of the unique roots found so far (i.e. without duplicates). Use a tolerance to decide if two roots are the same or not.

You may use a grid search or a random search inside the box.

Use all_roots to find all solutions of the system.

Make an interactive visualization where you repeat the above for different values of . You should redraw the curves and draw all roots you find on top, for each value of .

Which qualitative change occurs and why? How could you think of going about finding numerically the critical value of for which this happens? You do not need to do so, just think about what you would do.

Extra credit if you actually do so.

Exercise 3: A more complicated example Consider the system


( +3)( −7)+18=0

(3)

(

( )−1))=0

sin

exp

(4)

3

(taken from here).

Draw plots of the two functions.

Find as many roots as you can in the region [−5, 5]2. How many are there?

Plot them on top of the graph. Did you find them all?

Exercise 4: Lorenz equations The Lorenz equations are a system of 3 or-dinary differential equations that give a “simple” model of convection in the at-mosphere. They are famous since their solutions form beautiful patterns and are an early example of the identification of chaos in deterministic dynamical systems:

d

=(−),

(5)

d

d

(6)

d

=(−)−,

d

(7)

d

= − .

We will take the standard parameter values: = 10 and = 8/3.

We will come back to look at their dynamics later in the course. For now we will look only at the stationary points, which are obtained by setting all of the time derivatives equal to 0 and solving the resulting system of nonlinear equations. [If the system starts at a stationary point, it will remain there.]

[Note that for this particular system the roots may be found analytically, which you may use to check your work. But if you were to perturb the original system a bit, it would no longer be possible to find the roots analytically.]

Make a function lorenz(x, y, z, σ, ρ, β) and a method lorenz(ρ) that

takes a vector x and uses the standard parameter values. for and .

Make a function all_roots3 that is a 3D version of all_roots. [Extra credit: Make a generic version that works in any number of dimensions.]

Use all_roots3 to find all the stationary points for = 2. You should search in a box [−5, 5]3. How many stationary points are there?


The stability of a stationary point turns out to be given by the eigenvalues of the Jacobian matrix at that point. [A trajectory starting close to an unstable point will move away from that point.] We will see how to calculate eigenvalues of a matrix later in the course; for now, use the eigvals function from LinearAlgebra. Recall that the eigenvalues of a matrix are complex numbers in general.

A stationary point is stable if the real part of each eigenvalue is < 0, and unstable if any eigenvalue has real part > 0.

Write a function maximum_stability(f, x) that calculates the maximum of the real parts of all the eigenvalues, assuming that is a stationary point of .

Write a function that “follows” each stationary point found in [3.]: increase by an increment = 0.1 and use the stationary points from the pre-vious value of as initial conditions for the Newton method for the new value of . [This is an example of numerical continuation. It assumes that the number of stationary points will not change.]

Plot the maximum stability as a function of between 2 and 25.

Use a suitable numerical method to accurately find the critical value at which the stability of the stationary points changes.

