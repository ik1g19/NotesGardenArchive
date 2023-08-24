Tries to maximise the space between the plane/hyperplane and the data

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626114641.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626114649.png|450]]

The dashed lines are support vectors

Important initial step - Feature scaling

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626114934.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626114942.png|450]]

# Soft Margin Classification

Some data points can be within the margin

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626115547.png|450]]

Need to minimize the number of violations

Wide margin vs. low violations
- In scikit-learn, there is a hyperparameter C
- Small C = wider margin but higher violations
- Large C = smaller margin (low generalisation power), but low violations

# Linear SVM

1. Model

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626120352.png|450]]

2. Loss Function

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626120419.png|450]]

3. Gradient Descent




![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627115407.png|450]]

# Hinge Loss Function

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627115449.png|450]]

# Nonlinear SVM

For linearly not separable data

Add new polynomial features

$x_1$ = 1 dimensional feature
- $x_2$ = $x_1^2$
- Data becomes linearly separable

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627122424.png|600]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627122444.png|450]]

Polynomial Feature Expansion with $d=3$

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627122537.png|450]]

# The Kernel Trick

Polynomial Features
- Too low degree - Underfitting
- Too high degree - Very slow computation time

**Kernel Trick** - Makes it possible to get the same result as if you added many polynomial features, even with very high-degree polynomials, without actually having to add them
Useful for non-linear data

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627122828.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627123133.png|500]]

$d$ = degree
$C$ = margin hyperparameter
$r$ = how much the model is influenced by high-degree polynomials vs low-degree ones

# Radial Basis Functions

- A set of landmarks (i.e., some chosen data points): $l_1,l_2,$ ...
- Measure similarity of other data points to these landmarks
- Similarity function: Gaussian radial basis function

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627123521.png|400]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627123527.png|450]]

- Example: $x1$ = original feature
- $x2$ & $x3$ calculated from RBFs

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627123634.png|600]]

In feature space $x_2$ vs. $x_3$: data is linearly separable

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627123724.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230627123737.png|600]]

