<script src="load-mathjax.js" async></script>

## \\(\\text{V}\\ \\) On The Adjoint Representation

The whole intention of the previous parts was to show that one could strictly discuss the \\(3D\\) imaginary quaternion subspace, as the whole information lies there. This is what is exponentiated (to get the unit-quaternion as a transformation object), and at the same time what the transformation is applied on (as a \\(3\\)-dimensional vector).

&nbsp;&nbsp;&nbsp;&nbsp;Section&nbsp;[\\(14\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation#14--deriving-the-explicit-rotation-matrix-form) reintroduces the \\(4^{\\text{th}}\\) dimension, the one that was avoided all along. We would like to investigate how a unit-quaternion acts on other quaternions. We relate the unit-quaternion, as an \\(SU\\!\\left(2\\right)\\) transformation, to a \\(4 \\times 4\\) \\(SO\\!\\left(3\\right)\\) matrix. Yes, this is not a typo. We will see, though, that the \\(4^{\\text{th}}\\) dimension is, in fact, some sort of a side effect - the principle elements in these \\(4 \\times 4\\) matrices would remain \\(3 \\times 3\\) \\(SO\\!\\left(3\\right)\\) matrices.

&nbsp;&nbsp;&nbsp;&nbsp;In Section&nbsp;[\\(12\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#12--the-connection-between-suleft2right-and-soleft3right), we derived an implicit formula for extracting the \\(3 \\times 3\\) \\(SO\\!\\left(3\\right)\\) matrix elements out of the \\(2 \\times 2\\) \\(SU\\!\\left(2\\right)\\) matrix elements. Section&nbsp;[\\(14\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation#14--deriving-the-explicit-rotation-matrix-form) closes the mathematical discussion of this text by deriving an explicit expression, also in terms of the quaternion parameters. This allows us to derive the inverse process.

&nbsp;&nbsp;&nbsp;&nbsp;Throughout the internet and literature, I could only find two algorithms for extracting the quaternion coefficients out of a rotation matrix: the naïve algorithm, which involves \\(4\\) evaluations of the square-root function; and the classic algorithm, which involves one square-root evaluation, but up to \\(3\\) [branches](https://en.wikipedia.org/wiki/Branch_(computer_science)). In Section&nbsp;[\\(15\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation#15--a-branchless-matrix-to-quaternion-translation) I would like to introduce a branchless algorithm, for the extraction of quaternion parameters out of a \\(3D\\) rotation matrix, with the evaluation of only one square-root function. We do it by combining all the knowledge we had gained.
<br><br>

### \\(14\\ \\) Deriving The Explicit Rotation Matrix Form
<div style="display:none">\(\setSection{14}\)</div>

#### \\(14.1\\ \\) Reminder

In previous sections, we wrote an \\(SU\\!\\left(2\\right)\\) matrix using real parameters. We rewrite it now, using complex numbers
\\begin{equation}
	S = \\begin{pmatrix} a & -b^{\\ast} \\\\ b & a^{\\ast} \\end{pmatrix} \\qquad \\left(a, b \\in \\mathbb{C}\\,;\\ \\left|a\\right|^{2} + \\left|b\\right|^{2} = 1\\right)\\,.
\\end{equation}
Remember: \\(S\\) is the result of the exponentiation of an \\(SU\\!\\left(2\\right)\\) algebra vector, \\(V \\in \\mathfrak{su}\\!\\left(2\\right)\\),
\\begin{equation}
	S = e^{V}\\,.
\\end{equation}
We have established the transformation rule of \\(V\\), but never discussed how \\(S \\in SU\\!\\left(2\\right)\\) transforms. Well, it is easy to derive, as we just need to transform \\(V\\). Applying \\(U \\in SU\\!\\left(2\\right)\\), this will be
\\begin{equation}
	S \\longmapsto e^{U V U^{\\dagger}} = \\cdots = U e^{V} U^{\\dagger} = U S U^{\\dagger}\\,.
\\end{equation}
As expected, this is just a change of basis transformation for \\(S\\) (as it was for \\(V\\)).

&nbsp;&nbsp;&nbsp;&nbsp;In a similar way, remember that exponentiating the imaginary subspace of the quaternion space results in a unit-quaternion (Eq.&nbsp;[\\(\\left(8.3\\right)\\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#mjx-eqn%3Aeq%3AQuaterniEuler%E2%80%99s_Formula))
\\begin{equation}
	\\label{eq:QuaterniEuler's Formula Theta}
	q = e^{\\frac{1}{2} \\vec{I} \\cdot \\vec{\\theta}} = \\cos\\!\\left(\\frac{\\theta}{2}\\right) \\underline{1} + \\vec{I} \\cdot \\hat{n} \\sin\\!\\left(\\frac{\\theta}{2}\\right)\\,.
\\end{equation}
We introduced a factor of half, so we can interpret \\(\\theta\\) as our angle of rotation. \\(\\hat{n}\\) is the axis around which the rotation is being performed. This interpretation for \\(\\theta\\) and \\(\\hat{n}\\) was not discussed. It is easy to verify by just experimenting with examples.

&nbsp;&nbsp;&nbsp;&nbsp;We write \\(q\\) in matrix form, using the Fundamental representation for quaternions, Eq.&nbsp;[\\(\\left(8.5\\right)\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#mjx-eqn%3Aeq%3A2D_Quaternion_Representation),
\\begin{align}
	\\label{eq:Q Decomposition} Q \\equiv D\\!\\left(q\\right) = &\\ w \\!\\left(\\underline{1}\\right) + x D\\!\\left(\\underline{i}\\right) + y D\\!\\left(\\underline{j}\\right) + z D\\!\\left(\\underline{k}\\right) \\\\ = & \\begin{pmatrix} w + i z & -y + i x \\\\ y + i x & w - i z \\end{pmatrix}\\,.
\\end{align}
\\(q\\)'s coefficients are, of course, all real. Notice that the condition for a unit-quaternion, as an \\(SU\\!\\left(2\\right)\\) transformation, is
\\begin{equation}
	\\label{eq:Q Transformation Normalization Condition}
	\\det\\!\\left[Q\\right] = \\left|q\\right|^{2} = w^{2} + x^{2} + y^{2} + z^{2} = 1\\,.
\\end{equation}
We have already established the fact that \\(Q\\) has the properties of \\(S\\) in Section&nbsp;[\\(8\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#8--fun-with-quaternions), hence also all quaternions (not just their imaginary part) are being transformed by a sandwich product - one can replace \\(v\\) in Eq.&nbsp;[\\(\\left(2.5\\right)\\\)](https://07U.github.io/Quaternions/Preamble#mjx-eqn%3Aeq%3AUnit_Quaternion_Transformation) by a generic quaternion to qet their transformation rule. The relation between \\(Q\\)'s elements and \\(S\\)'s is obvious,
\\begin{equation}
	\\label{eq:Q to S}
	a = w + i z\\,,\\ b = y + i x\\,.
\\end{equation}
It is all very intuitive, I know, but we would like to see it explicitly, from an equivalent but different angle.
<br><br>

#### \\(14.2\\ \\) A Reducible Representation

The goal of the previous subsection was to become convinced that a quaternion can be considered as a tensor \\(Q \\sim \\boldsymbol{2} \\otimes \\boldsymbol{\\overline{2}}\\). Or, alternatively, \\(Q\_{\\alpha \\dot{\\alpha}}\\) - where \\(\\alpha\\) and \\(\\dot{\\alpha}\\) transform under the Fundamental and Anti-Fundamental of \\(SU\\!\\left(2\\right)\\)
\\begin{equation}
	Q\_{\\alpha \\dot{\\alpha}} \\longmapsto \\sum\_{\\beta = 1}^{2} \\sum\_{\\dot{\\beta} = 1}^{2} U\_{\\alpha \\beta} U^{\\ast}\_{\\dot{\\alpha} \\dot{\\beta}} Q\_{\\beta \\dot{\\beta}}\\,.
\\end{equation}

&nbsp;&nbsp;&nbsp;&nbsp;\\(Q\\) is also a vector in a \\(4\\)-dimensional vector space, spanned by \\(\\Set{𝟙,X\_{1},X\_{2},X\_{3}}\\) (see Eq.&nbsp;\eqref{eq:Q Decomposition} and replace for Eq.&nbsp;[\\(\\left(11.1\\right)\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#mjx-eqn%3Aeq%3Asu(2)_Basis)). The dot-product between two vectors in this space, \\(M\\) and \\(N\\), is the same one presented in Section&nbsp;[\\(11\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#11--the-suleft2right-algebra-and-generators),
\\begin{equation}
	\\label{eq:Dot Product}
	M \\cdot N = \\frac{1}{2} \\mathrm{Tr}\\!\\left[M N^{\\dagger}\\right]\\,.
\\end{equation}
With this dot-product, we clearly see that \\(Q\\), now as a vector, is normalized
\\begin{equation}
	\\label{eq:Q Vector Normalization Condition}
	\\left|Q\\right|^{2} = Q \\cdot Q = \\frac{1}{2} \\mathrm{Tr}\\!\\left[Q Q^{\\dagger}\\right] = w^{2} + x^{2} + y^{2} + z^{2} = 1\\,.
\\end{equation}
Notice the subtle difference between Eq.&nbsp;\\eqref{eq:Q Transformation Normalization Condition} and Eq.&nbsp;\\eqref{eq:Q Vector Normalization Condition}: the former guarantees that as a transformation, \\(Q\\) does not affect scales; while the latter guarantees that as a vector, \\(Q\\) has a unit norm.

&nbsp;&nbsp;&nbsp;&nbsp;The tensor \\(Q\\) can be written as a \\(4D\\) vector, by sticking its columns one above the other
\\begin{equation}
	\\vec{Q} = \\begin{pmatrix} \\begin{pmatrix} Q\_{11} \\\\ Q\_{21} \\end{pmatrix} \\\\ \\begin{pmatrix} Q\_{12} \\\\ Q\_{22} \\end{pmatrix} \\end{pmatrix} = \\begin{pmatrix} w + i z \\\\ y + i x \\\\ -y + i x \\\\ w - i z \\end{pmatrix}\\,.
\\end{equation}
In this \\(4D\\) space, the Tensor representation \\(D\_{\\text{T}}\\!\\left(U\\right) \\equiv U \\otimes U^{\\ast}\\) [is written as](https://en.wikipedia.org/wiki/Tensor_product#Tensor_product_of_linear_maps)
\\begin{equation}
	D\_{\\text{T}}\\!\\left(U\\right) = \\begin{pmatrix} \\left(U\_{11} \\cdot U^{\\ast}\\right) & \\left(U\_{12} \\cdot U^{\\ast}\\right) \\\\ \\left(U\_{21} \\cdot U^{\\ast}\\right) & \\left(U\_{22} \\cdot U^{\\ast}\\right) \\end{pmatrix} = \\begin{pmatrix} \\left|a\\right|^{2} & -a b & -b^{\\ast} a^{\\ast} & \\left|b\\right|^{2} \\\\ a b^{\\ast} & a^{2} & -b^{\\ast2} & -b^{\\ast} a \\\\ b a^{\\ast} & -b^{2} & a^{\\ast2} & -a^{\\ast} b \\\\ \\left|b\\right|^{2} & b a & a^{\\ast} b^{\\ast} & \\left|a\\right|^{2} \\end{pmatrix}\\,.
\\end{equation}
There is an equivalence of transformations
\\begin{equation}
	D\_{\\text{T}}\\!\\left(U\\right) \\vec{Q} \\ \\longleftrightarrow\\ U Q U^{\\dagger}\\,.
\\end{equation}
We have replaced the sandwich operation with the known matrix-vector multiplication.

&nbsp;&nbsp;&nbsp;&nbsp;However, \\(\\vec{Q}\\) has some mixing in its quaternion components. We would like to write it in the natural basis. We perform a change of basis by the complex basis transformation
\\begin{equation}
	B = \\begin{pmatrix} \\frac{1}{\\sqrt{2}} & 0 & 0 & \\frac{1}{\\sqrt{2}} \\\\ 0 & -\\frac{i}{\\sqrt{2}} & -\\frac{i}{\\sqrt{2}} & 0 \\\\ 0 & \\frac{1}{\\sqrt{2}} & -\\frac{1}{\\sqrt{2}} & 0 \\\\ -\\frac{i}{\\sqrt{2}} & 0 & 0 & \\frac{i}{\\sqrt{2}} \\end{pmatrix}\\,.
\\end{equation}
\\(\\vec{Q}\\) then transforms into
\\begin{equation}
	\\vec{Q} \\longmapsto B \\vec{Q} = \\sqrt{2} \\begin{pmatrix} w \\\\ x \\\\ y \\\\ z \\end{pmatrix}\\,.
\\end{equation}
Well, this factor of \\(\\sqrt{2}\\) is awkward. The reason for its appearance is that in this space, our dot-product is *weighted*! Remember Eq.&nbsp;\\eqref{eq:Dot Product}? Its vector equivalent is
\\begin{equation}
	\\left|\\vec{Q}\\right|^{2} \\equiv \\frac{1}{2} \\vec{Q} \\cdot \\vec{Q} = w^{2} + x^{2} + y^{2} + z^{2} = 1\\,.
\\end{equation}
But do not be bothered by this too much. Prepare to say Hocus-Pocus, as the real magic happens when applying the transformation to \\(D\_{\\text{T}}\\!\\left(U\\right)\\)
\\begin{equation}
	\\label{eq:Reducable Representation}
	\\!\\!\\!\\!D\_{\\text{T}}\\!\\left(U\\right) \\longmapsto B D\_{\\text{T}}\\!\\left(U\\right) B^{\\dagger} \\!=\\! \\begin{pmatrix} 1 & 0 & 0 & 0 \\\\ 0 & \\mathfrak{Re}\\!\\left[a^{2} \\!-\\! b^{2}\\right] & \\mathfrak{Im}\\!\\left[a^{2} \\!-\\! b^{2}\\right] & 2 \\mathfrak{Re}\\!\\left[a b^{\\ast}\\right] \\\\ 0 & -\\mathfrak{Im}\\!\\left[a^{2} \\!+\\! b^{2}\\right] & \\mathfrak{Re}\\!\\left[a^{2} \\!+\\! b^{2}\\right] & -2 \\mathfrak{Im}\\!\\left[a b^{\\ast}\\right] \\\\ 0 & -2 \\mathfrak{Re}\\!\\left[a b\\right] & -2 \\mathfrak{Im}\\!\\left[a b\\right] & \\left|a\\right|^{2} \\!-\\! \\left|b\\right|^{2} \\end{pmatrix}\\,.\\!\\!\\!\\!
\\end{equation}
We can clearly see that under this basis, the \\(4\\)-dimensional Tensor representation of \\(U\\) got decomposed into:
* A \\(1 \\times 1\\) block - called the *Trivial Representation*, and denoted by \\(\\boldsymbol{1}\\). The Trivial representation is the map \\(D\_{\\text{Triv}}\\!\\left(U\\right) \\equiv 1\\), for any \\(U\\).
* A \\(3 \\times 3\\) block - ladies and gentlemen, I give you the Adjoint representation. It is denoted by \\(\\boldsymbol{3}\\).

To summarize, we have shown that \\(\\boldsymbol{2} \\otimes \\boldsymbol{\\overline{2}} = \\boldsymbol{1} \\oplus \\boldsymbol{3}\\).

&nbsp;&nbsp;&nbsp;&nbsp;The Adjoint representation is a *purely real* transformation matrix, and is equivalent to a rotation matrix! This is the object that acts on the imaginary part of the quaternion, and applies the rotation. We also clearly see that the imaginary quaternion subspace (the \\(\\left(x,y,z\\right)\\) coordinates) is an *invariant* subspace under this operation, so we can treat it as a closed \\(3D\\) Euclidean space!

&nbsp;&nbsp;&nbsp;&nbsp;As a final step, let us derive the (well-known form of the) Adjoint representation of \\(q\\). For that, the relation between \\(a\\) and \\(b\\), and the quaternion coefficients, Eq.&nbsp;\\eqref{eq:Q to S}, is inserted into the Adjoint block of Eq.&nbsp;\\eqref{eq:Reducable Representation}
\\begin{equation}
	\\label{eq:Quaternion Adjoint Representation}
	D\_{\\text{Ad}}\\!\\left(q\\right) = \\begin{pmatrix} 2 \\left(w^{2} + x^{2}\\right) - 1 & 2 \\left(x y + w z\\right) & 2 \\left(x z - w y\\right) \\\\ 2 \\left(x y - w z\\right) & 2 \\left(w^{2} + y^{2}\\right) - 1 & 2 \\left(y z + w x\\right) \\\\ 2 \\left(x z + w y\\right) & 2 \\left(y z - w x\\right) & 2 \\left(w^{2} + z^{2}\\right) - 1 \\end{pmatrix}\\,.
\\end{equation}

&nbsp;&nbsp;&nbsp;&nbsp;We did it. The relation between the quaternion coefficients and those of a rotation matrix is fully understood. We also understand why the matrix elements depend on the multiplication of two of the quaternion's components - it is a result of a tensor multiplication. The translation of a quaternion into a matrix is done easily enough by using Eq.&nbsp;\\eqref{eq:Quaternion Adjoint Representation}. However, when one wishes to extract the quaternion's coefficients out of a rotation matrix, there is "hard work" involved.
<br><br>

### \\(15\\ \\) A Branchless Matrix-To-Quaternion Translation
<div style="display:none">\(\setSection{15}\)</div>

The quaternion Adjoint representation, Eq.&nbsp;\\eqref{eq:Quaternion Adjoint Representation}, is the dictionary for extracting the transformation's principle axes out of a quaternion. But what about the inverse translation? How can we extract the quaternion coefficients out of a generic rotation matrix[^17]
\\begin{equation}
	O = \\begin{pmatrix} O\_{00} & O\_{01} & O\_{02} \\\\ O\_{10} & O\_{11} & O\_{12} \\\\ O\_{20} & O\_{21} & O\_{22} \\end{pmatrix}\\,?
\\end{equation}

&nbsp;&nbsp;&nbsp;&nbsp;Identifying \\(O\\) with \\(D\_{\\text{Ad}}\\!\\left(q\\right)\\), one finds
\\begin{equation}
	\\text{Tr}\\!\\left[O\\right] = 4 w^{2} - 1 \\quad\\Longrightarrow\\quad w = \\frac{\\sqrt{1 + \\text{Tr}\\!\\left[O\\right]}}{2}\\,.
\\end{equation}
Furthermore, the off-diagonal elements of the Adjoint matrix are composed of symmetric and anti-symmetric terms. This means that they could be combined together by addition or subtraction to eliminate one part or the other. Having an expression for \\(w\\), we could subtract opposite off-diagonal elements, to extract the other quaternion parameters.
\\begin{equation}
	\\label{eq:Off-Diagonal Manipulation}
	x = \frac{O\_{12} - O\_{21}}{2 \\sqrt{1 + \\text{Tr}\\!\\left[O\\right]}}\\,,\\ y = \frac{O\_{20} - O\_{02}}{2 \\sqrt{1 + \\text{Tr}\\!\\left[O\\right]}}\\,,\\ z = \frac{O\_{01} - O\_{10}}{2 \\sqrt{1 + \\text{Tr}\\!\\left[O\\right]}}\\,.
\\end{equation}
This works well, as long as the trace is not too close to \\(-1\\), which leads to a numerical inaccuracy, or an undefined result when it is exactly \\(-1\\). Here comes branching for the rescue. Whenever the trace is, for example, negative, one could just take the trace expression and negate two out of the three diagonal elements, making the whole expression positive. From this new, positive, expression, a different coefficient (\\(x\\), \\(y\\), or \\(z\\)) could be algebraically extracted. Then, the off-diagonal elements are manipulated accordingly to extract the rest of the parameters. You can find the full algorithm online with a simple search, so it is not explicitly presented here.

&nbsp;&nbsp;&nbsp;&nbsp;The discussion above is too algebraic though. Can we treat it in a more geometric way, and give meaning to the algebraic manipulations? The answer, of course, is positive. The expression for the quaternion in terms of the rotation angle, Eq.&nbsp;\\eqref{eq:QuaterniEuler's Formula Theta}, gives us the relation
\\begin{equation}
	w = \\cos\\!\\left(\\frac{\\theta}{2}\\right)\\,.
\\end{equation}
We thus deduce that when[^18][^19]
\\begin{equation}
	\\label{eq:Branching Condition}
	\\left|\\theta\\right|\\mod \\tau < 2 \\arccos\\!\\left(\\frac{1}{2}\\right) = \\frac{1}{3} \\tau\\,,
\\end{equation}
the classic algorithm branches, as the trace can not be used reliably anymore. Branching thus generically happens one third of the time. Can we eliminate the branches entirely? Also here, the answer is positive! As we show in what follows, the underlying computation would be the same as in the classic algorithm. However, we will be able to find patterns that combine all of the branching paths into one.

&nbsp;&nbsp;&nbsp;&nbsp;So, under the assumption that Eq.&nbsp;\\eqref{eq:Branching Condition} is not satisfied, we would have to do something else. The (yet unknown) axis of rotation, presented in Eq.&nbsp;\\eqref{eq:QuaterniEuler's Formula Theta}, is
\\begin{equation}
	\\hat{n} = \\frac{1}{\\sqrt{x^{2} + y^{2} + z^{2}}} \\begin{pmatrix} x \\\\ y \\\\ z \\end{pmatrix}\\,.
\\end{equation}
The key observation is that multiplying \\(O\\) by a certain transformation would result in a positive trace. This transformation is a rotation of \\(180^{\\circ}\\) around the Cartesian axis that is "close enough" to \\(\\hat{n}\\). It is important to understand that what we do is *not* a change of basis. We feed the algorithm a new input matrix that has a positive trace - eliminating the branch in an artificial way. The hand-wavy reason for why this works is that it affects \\(\\hat{n}\\) in a minimal way, and most of the effect is in a change of \\(\\theta\\), such that the shifted angle now satisfies the condition of Eq.&nbsp;\\eqref{eq:Branching Condition}.

&nbsp;&nbsp;&nbsp;&nbsp;Of course, one of the problems in constructing the quaternion is finding \\(\\hat{n}\\), thus we do not know which axis is "close enough"! Let us consider a special case, which would allow us to understand the strategy later on. We ask ourselves: what effect will a \\(180^{\\circ}\\) rotation around one of the Cartesian axes have? Without loss of generality, consider a rotation around the \\(\\hat{z}\\) direction. The rotation matrix would be
\\begin{equation}
	R\_{z} = \\begin{pmatrix} -1 & 0 & 0 \\\\ 0 & -1 & 0 \\\\ 0 & 0 & 1 \\end{pmatrix}\\,,
\\end{equation}
and the transformed input matrix is, surprise surprise,
\\begin{equation}
	\\label{eq:Transformed O}
	\\tilde{O} = R\_{z} O = \\begin{pmatrix} -O\_{00} & -O\_{01} & -O\_{02} \\\\ -O\_{10} & -O\_{11} & -O\_{12} \\\\ O\_{20} & O\_{21} & O\_{22} \\end{pmatrix}\\,.
\\end{equation}
The trace of the transformed input matrix is
\\begin{equation}
	\\label{eq:Transformed O Trace}
	\\text{Tr}\\!\\left[\\tilde{O}\\right] = 4 \\tilde{w}^{2} - 1 \\quad\\Longleftrightarrow\\quad \\text{Tr}\\!\\left[R\_{z} O\\right] = O\_{22} - O\_{00} - O\_{11} = 4 z^{2} - 1\\,.
\\end{equation}
The right hand side of Eq.&nbsp;\\eqref{eq:Transformed O Trace} is the exact same expression computed by one of the classic algorithm's branches! We see then that the algebraic approach actually "applies" a rotation of the input matrix. We considered here only a rotation around the \\(\\hat{z}\\) direction, however the discussion applies also for the other directions - each corresponds to a different branch path. Replacing \\(O\\) in Eq.&nbsp;\\eqref{eq:Off-Diagonal Manipulation} by the new \\(\\tilde{O}\\) of Eq.&nbsp;\\eqref{eq:Transformed O} would result in the other quaternion's coefficients: \\(\\tilde{x}\\), \\(\\tilde{y}\\), and \\(\\tilde{z}\\).

We could thus forget about different *expressions* (*i.e.*, whether we add or subtract elements), and think of different *transformations* (we have the same expressions to evaluate, but feed it with different input parameters). This is a way of thinking which we like in programming, mostly because it allows us to avoid code duplication.

&nbsp;&nbsp;&nbsp;&nbsp;Now comes the last crucial part. Assume we are given an input matrix \\(O\\), and we apply (or not) a transformation to it, to make its trace positive. We then perform the classic algorithm with the transformed matrix, \\(\\tilde{O}\\), getting back a quaternion. This output quaternion, though, represents \\(\\tilde{O}\\), and it should still be modified with the inverse transformation, to get the quaternion that represents \\(O\\). Luckily for us, the transformation (and its inverse) is a multiplication by one of the basis elements! In the example above, it would be a multiplication by \\(\\underline{k}\\). The multiplication table of the basis elements (or the \\(Q\_{8}\\) group, presented in Eq.&nbsp;[\\(\\left(7.8\\right)\\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#mjx-eqn%3Aeq%3AQuaternion_Group_Definition)), is easy to master, and a pattern can be easily retrieved. This transformation is just a permutation of the quaternion coefficients, up to a sign (which also follows a pattern).

&nbsp;&nbsp;&nbsp;&nbsp;Before a representative implementation of the algorithm is shown, let us outline the branchless algorithm:
1. Determine the needed transformation, and apply it to the input matrix.
2. Feed the classic algorithm with the new matrix. It would not branch!
3. Apply the inverse transformation to the output quaternion which was received from the classic algorithm.

Of course, this is highly open to interpretation, and could be implemented in numerous ways. However, the (potential) branching is now moved to Step&nbsp;\\(1\\) and Step&nbsp;\\(3\\), and it is (y)our job to implement the above in a branchless manner.

&nbsp;&nbsp;&nbsp;&nbsp;The following piece of code realizes the ideas of this section. It extracts the quaternion, up to a global sign. This global sign is important in case one would like to treat the quaternion not as a group element, but rather as a vector (*i.e.*, for linear interpolation purposes), and can be easily taken into account. The presented implementation is *not* the most efficient out of the ones I could come up with. I was trying to keep it somewhat readable (hence the use of the ternary operator), while showing the potential of bit-wise operations (which may or may not help performance). I noticed that performance highly depends on the compiler in use. Sometimes the disassembly written by the compiler was not as optimized as I would have hoped, and there is a considerable variance between compilers. I am looking forward to be amazed by the community, and the cleverness of fellow programmers!

```c++
struct Quaternion
{
	// It is easier, in this example, to place w at the end of the struct.
	float x, y, z, w;
};

struct Matrix
{
	float m00, m01, m02;
	float m10, m11, m12;
	float m20, m21, m22;
};

Quaternion ToQuaternion(const Matrix& O)
{
    Quaternion q;
    q.x = + O.m00 - O.m11 - O.m22; // Tr[i * O]
    q.y = - O.m00 + O.m11 - O.m22; // Tr[j * O]
    q.z = - O.m00 - O.m11 + O.m22; // Tr[k * O]
    q.w = + O.m00 + O.m11 + O.m22; // Tr[1 * O]

    // Determine the needed transformation, according to the sign of the
    // "trace". These values would make sense in the next instruction.
    const unsigned int index0 = q.w > 0 ? 0b11 : 0b00;
    const unsigned int index1 = q.x > 0 ? 0b00 : 0b11;
    const unsigned int index2 = q.y > 0 ? 0b01 : 0b11;
    const unsigned int index3 = q.z > 0 ? 0b11 : 0b11;

    // i describes which transformation is applied. It is also the index
    // of "w tilde" - the parameter we extract out of the diagonal.
    const unsigned int i = index0 | (((index1 & index2 & index3) + 1) / 2);

    float* const p = &q.x;
    // Extracting "w tilde".
    p[i] = std::sqrt(1.0f + p[i]);
    const float normalization = 0.5f / p[i];
    p[i] *= 0.5f;

    // Determine the signs of the off-diagonal elements, according to the
    // value of i.
    const int sign01 = (i & 0b10) - 1;
    const int sign20 = ((i & 0b01) << 1) - 1;
    const int sign12 = sign01 * sign20;

    // There is a pattern to the permutation of quaternion elements in
    // their multiplication table. It is incorporated in index manipulations.

    // i ^ 0b10 is the transformation 0 <-> 2 and 1 <-> 3.
    p[i ^ 0b10] = normalization * (O.m02 - sign20 * O.m20);

    // i ^ 0b01 is the transformation 0 <-> 1 and 2 <-> 3.
    p[i ^ 0b01] = normalization * (O.m10 - sign01 * O.m01);

    // i ^ 0b11 is the transformation 0 <-> 3 and 1 <-> 2.
    p[i ^ 0b11] = normalization * (O.m21 - sign12 * O.m12);

    return q;
}
```
<br><br>

---
<br>

To the previous part: [\\(\\text{IV}\\ \\) The Connection To \\(3D\\) Rotations](https://07U.github.io/Quaternions/TheConnectionTo3DRotations).
<br><br>

# Discussion

Any comments or questions related to this part can be posted in the [dedicated LinkedIn post](https://www.linkedin.com/posts/oz-davidi_proud-8-months-ago-i-challenged-myself-activity-7226104655049588738-L1Jc).
<br><br>

---
<br>

[^17]: This section is mostly about the algorithm, with a \\(C\\text{++}\\) example given at the end of it. Hence, we use zero-based indices.
[^18]: Robert Palais. \\(\\pi\\) is wrong! *The Mathematical Intelligencer*, 23(3):7–8, 2001. [doi:10.1007/BF03026846](https://doi.org/10.1007/BF03026846).
[^19]: Michael Hartl. The Tau Manifesto. URL: [http://tauday.com/tau-manifesto](http://tauday.com/tau-manifesto).
