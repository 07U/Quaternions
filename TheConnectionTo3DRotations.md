<script src="load-mathjax.js" async></script>

## \\(\\text{IV}\\ \\) The Connection To \\(3D\\) Rotations

In Part&nbsp;[\\(\\text{II}\\)](https://07U.github.io/Quaternions/Intuition), we had established a connection between the imaginary complex number and the elements of \\(SO\\!\\left(2\\right)\\). In Part&nbsp;[\\(\\text{III}\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts), a connection between imaginary quaternions and the \\(SU\\!\\left(2\\right)\\) group was established: we first chose a matrix *representation* for the quaternion base elements, and then inserted it in the [exponential map](https://en.wikipedia.org/wiki/Exponential_map_(Lie_theory)) to get a \\(2 \\times 2\\) \\(SU\\!\\left(2\\right)\\) matrix. I was teasing you that the imaginary quaternions, \\(\\underline{i}\\), \\(\\underline{j}\\) and \\(\\underline{k}\\), are the *generators* of \\(SU\\!\\left(2\\right)\\), hopefully not leaving you too confused.

&nbsp;&nbsp;&nbsp;&nbsp;In this part we are going to finally dive into the world of [Lie Algebras](https://en.wikipedia.org/wiki/Lie_algebra), [generators](https://en.wikipedia.org/wiki/Lie_algebra#Generators_and_dimension), and representations, however on an extremely high level. In order to *fully* understand what is going on behind the scenes, one needs to read a book on the subject or take a dedicated course. Because the goal of this text is for you not to do so, some things are being swept under the rug (I hope you have a big one). This part of the text contains a lot of definitions, and is going to be technically challenging. However, we should stay focused and do not let some jargon confuse us - as long as the examples are understandable, the path toward the end should remain clear.

&nbsp;&nbsp;&nbsp;&nbsp;What we called the Fundamental representation of \\(SO\\!\\left(2\\right)\\), Eq.&nbsp;[\\(\\left(6.3\\right)\\)](https://07U.github.io/Quaternions/Intuition#mjx-eqn%3Aeq%3Ai_Fundamental_Representation), is what connects the complex numbers to rotations in \\(2\\) dimensions. The representation for quaternions in Eq.&nbsp;[\\(\\left(8.5\\right)\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#mjx-eqn%3Aeq%3A2D_Quaternion_Representation) connects them to \\(2 \\times 2\\) \\(SU\\!\\left(2\\right)\\) matrices. This later representation is also "fundamental". In Section&nbsp;[\\(10\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#10--representations) we define the Fundamental representation in more details, and introduce even more representations. Section&nbsp;[\\(11\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#11--the-suleft2right-algebra-and-generators) introduces the \\(3\\)-dimensional Euclidean space that hides inside \\(SU\\!\\left(2\\right)\\). Section&nbsp;[\\(12\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#12--the-connection-between-suleft2right-and-soleft3right) connects rotations in \\(3D\\) space, represented by \\(3 \\times 3\\) \\(SO\\!\\left(3\\right)\\) matrices, to \\(2 \\times 2\\) \\(SU\\!\\left(2\\right)\\) transformations. With the results of Part&nbsp;[\\(\\text{III}\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts), this leads to a direct connection between quaternions and rotations in our physical world. Section&nbsp;[\\(13\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#13--summary) provides a short summary.

&nbsp;&nbsp;&nbsp;&nbsp;We are purely going to deal with matrices from now on, revisiting quaternions only in the next and final part, Part&nbsp;[\\(\\text{V}\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation), where we would see how to extract quaternion coefficients out of a rotation matrix.
<br><br>

### \\(10\\ \\) Representations
<div style="display:none">\(\setSection{10}\)</div>

We have arrived to the most important link of the chain, which may also be one of the most complex to understand - especially without being rigorous. In Section&nbsp;[\\(6\\)](https://07U.github.io/Quaternions/Intuition#6--a-glimpse-into-the-future) we already defined representations, and also met a specific type of representation of \\(SO\\!\\left(2\\right)\\), called the Fundamental. This section elaborates more on the subject of [group representation](https://en.wikipedia.org/wiki/Group_representation) (definitely not in a complete way), and also answers the questions:
1. How could a group element be applied differently on different vectors of the same space?
2. How could a group element be applied to different vector spaces?

&nbsp;&nbsp;&nbsp;&nbsp;Well, the second question was already partially answered in terms of an example. We saw how a \\(2D\\) rotation can act on a \\(2\\)-dimensional Euclidean space, but could also rotate \\(3\\)-, \\(4\\)-, \\(5\\)-,..., dimensional spaces. At least the \\(3D\\) case is very intuitive for us to understand from our day-to-day experience. Mathematically, we achieve that by ignoring all of the "extra" dimensions, and placing the \\(-\\epsilon\\) structure on the rows and columns of the \\(2\\) dimensions we would like to rotate (recall Eq.&nbsp;[\\(\\left(8.4\\right)\\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#mjx-eqn%3Aeq%3ASO(2)_3D_Representation)). But this is the naïve and less interesting way to do so. We would see how to do it in a more "interesting" way (*i.e.*, without ignoring extra dimensions), but let us first shift the focus to the first question.

&nbsp;&nbsp;&nbsp;&nbsp;Remember that \\(U \\in SU\\!\\left(2\\right)\\), as a \\(2 \\times 2\\) matrix, could act on the \\(2\\)-dimensional complex vector space, \\(\\mathbb{C}^{2}\\)? Yes, we still do not care *what* this transformation actually does to the space, but we would like to identify two ways it could act on it. In other words, we would like to find two different representations.[^12] We build them through examples - it is your responsibility to make sure they are proper representations.

&nbsp;&nbsp;&nbsp;&nbsp;Let \\(\\vec{v}, \\vec{w} \\in \\mathbb{C}^{2}\\). We call \\(D\_{\\text{F}}\\!\\left(U\\right)\\) the *Fundamental* representation if it acts on \\(\\vec{v}\\) in the following way
\\begin{equation}
	\\vec{v} \\longmapsto D\_{\\text{F}}\\!\\left(U\\right) \\vec{v} = U \\vec{v}\\,.
\\end{equation}
Just like we had a Fundamental representation for \\(SO\\!\\left(2\\right)\\), the \\(SU\\!\\left(2\\right)\\) Fundamental representation is the identity map.[^13] Although we defined the representation as the function \\(D\\), we will sometime abuse this term. For example, we may say that \\(\\vec{v}\\) transforms under the Fundamental - meaning that under the operation of an \\(SU\\!\\left(2\\right)\\) element, \\(\\vec{v}\\) has the above-mentioned transformation rule.

&nbsp;&nbsp;&nbsp;&nbsp;Apparently, there are other representations that we could have chosen. We call \\(D\_{\\text{AF}}\\!\\left(U\\right)\\) the *Anti-Fundamental* representation if it acts on \\(\\vec{w}\\) in the following way
\\begin{equation}
	\\vec{w} \\longmapsto D\_{\\text{AF}}\\!\\left(U\\right) \\vec{w} = U^{\\ast} \\vec{w}\\,.
\\end{equation}
The Anti-Fundamental representation maps the group element \\(U\\) to its complex-conjugate. \\(\\vec{w}\\) is said to transform under the Anti-Fundamental.

&nbsp;&nbsp;&nbsp;&nbsp;With the Fundamental and Anti-Fundamental representations, we see how an \\(SU\\!\\left(2\\right)\\) element can act differently on the same vector space. Unfortunately, there is no relevant example I can show you for its usefulness, but fortunately, we do not need one. As was mentioned before, the complex space \\(\\mathbb{C}^{2}\\) is not of importance to us. With that said, we would use these two representations in a moment.

&nbsp;&nbsp;&nbsp;&nbsp;It would be much easier to encode the information about the representation in the vector indices. We use an undotted and dotted index notation, and write \\(v\_{\\alpha}\\) and \\(w\_{\\dot{\\alpha}}\\), to say that \\(\\vec{v}\\) and \\(\\vec{w}\\) transform under the Fundamental and Anti-Fundamental, respectively. The transformation rules are then
\\begin{equation}
	v\_{\\alpha} \\longmapsto \\sum\_{\\beta = 1}^{2} U\_{\\alpha \\beta} v\_{\\beta}\\,,\\quad w\_{\\dot{\\alpha}} \\longmapsto \\sum\_{\\dot{\\beta} = 1}^{2} U^{\\ast}\_{\\dot{\\alpha} \\dot{\\beta}} w\_{\\dot{\\beta}}\\,.
\\end{equation}
Let us introduce even more notation, because... why not? We denote the Fundamental representation of \\(SU\\!\\left(2\\right)\\) by \\(\\boldsymbol{2}\\), and the Anti-Fundamental representation by \\(\\boldsymbol{\\overline{2}}\\). We could then alternatively write \\(\\vec{v} \\sim \\boldsymbol{2}\\) and \\(\\vec{w} \\sim \\boldsymbol{\\overline{2}}\\).

&nbsp;&nbsp;&nbsp;&nbsp;With this set of notation, we can compose representations to build the *Tensor* representation. For instance, a tensor \\(T \\sim \\boldsymbol{2} \\otimes \\boldsymbol{\\overline{2}}\\) transforms as
\\begin{equation}
	T\_{\\alpha \\dot{\\alpha}} \\longmapsto \\sum\_{\\beta = 1}^{2} \\sum\_{\\dot{\\beta} = 1}^{2} U\_{\\alpha \\beta} U^{\\ast}\_{\\dot{\\alpha} \\dot{\\beta}} T\_{\\beta \\dot{\\beta}}\\,,
\\end{equation}
and in matrix notation, it reads
\\begin{equation}
	T \\longmapsto \\text{"\\(\\displaystyle{D\_{\\text{T}}\\!\\left(U\\right) T}\\)"} = U T U^{\\dagger}\\,.
\\end{equation}
The matrix-vector multiplication - the expression inside the quotation marks - is properly derived in Part&nbsp;[\\(\\text{V}\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation). One could build any tensor with as many indices in any representation they like. The \\(\\boldsymbol{2} \\otimes \\boldsymbol{\\overline{2}}\\) one is of particular significance to us.

&nbsp;&nbsp;&nbsp;&nbsp;The Tensor representation reveals how an \\(SU\\!\\left(2\\right)\\) element can act on a completely different vector space - namely one which is not \\(\\mathbb{C}^{2}\\). In particular, the \\(\\boldsymbol{2} \\otimes \\boldsymbol{\\overline{2}}\\) representation acts on a \\(2 \\times 2\\) matrices vector space. Could you connect the dots?[^14]
<br><br>

### \\(11\\ \\) The \\(SU\\!\\left(2\\right)\\) Algebra And Generators
<div style="display:none">\(\setSection{11}\)</div>

Both \\(SO\\!\\left(N\\right)\\) and \\(SU\\!\\left(N\\right)\\), that were presented in Section&nbsp;[\\(7\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#7--groups), are [*Lie groups*](https://en.wikipedia.org/wiki/Lie_group). Such groups define their corresponding [*Lie algebra*](https://en.wikipedia.org/wiki/Lie_algebra). The *algebra* of \\(SU\\!\\left(2\\right)\\), denoted \\(\\mathfrak{su}\\!\\left(2\\right)\\), is spanned by the basis matrices[^15]
\\begin{equation}
	\\label{eq:su(2) Basis}
	X\_{1} \\!\\equiv\\! D\\!\\left(\\underline{i}\\right) \\!=\\! \\begin{pmatrix} 0 & i \\\\ i & 0 \\end{pmatrix}\\,,\\  X\_{2} \\!\\equiv\\! D\\!\\left(\\underline{j}\\right) \\!=\\! \\begin{pmatrix} 0 & -1 \\\\ 1 & 0 \\end{pmatrix}\\,,\\  X\_{3} \\!\\equiv\\! D\\!\\left(\\underline{k}\\right) \\!=\\! \\begin{pmatrix} i & 0 \\\\ 0 & -i \\end{pmatrix}\\,.
\\end{equation}
\\(X\_{i}\\) are called the *generators*. The concept of Lie algebras is not going to be covered here. What is important for us, though, is that the algebra is a vector space. The dot-product between two vectors, \\(V,W \\in \\mathfrak{su}\\!\\left(2\\right)\\) is[^16]
\\begin{equation}
	V \\cdot W = \\frac{1}{2} \\mathrm{Tr}\\!\\left[V W^{\\dagger}\\right]\\,.
\\end{equation}
Indeed, \\(X\_{i}\\) form an orthonormal base under this dot-product.

&nbsp;&nbsp;&nbsp;&nbsp;\\(\\mathfrak{su}\\!\\left(2\\right)\\) is a vector space with a property that is of importance to us. Can you identify it? Yes, it is a vector space of size 3! I assume you can see what we wish to do now - treat this space as our Euclidean one. We did a step in the right direction, but there is still some work to be done.

&nbsp;&nbsp;&nbsp;&nbsp;Eq.&nbsp;\\eqref{eq:su(2) Basis} maps the imaginary quaternion part to the generators of \\(SU\\!\\left(2\\right)\\). This explains the claim from Section&nbsp;[\\(9\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#9--closing-remarks), that \\(\\underline{i}\\),  \\(\\underline{j}\\) and \\(\\underline{k}\\) serve as the generators - namely, they serve as the basis of a vector space, \\(\\mathfrak{su}\\!\\left(2\\right)\\).

&nbsp;&nbsp;&nbsp;&nbsp;As a vector space, one could act on \\(\\mathfrak{su}\\!\\left(2\\right)\\), and transform its vectors. When transforming this space, we would like to transform it onto itself. Observing the generators \\(X\_{i}\\), we note that they possess two special properties - they are traceless and [Skew-Hermitian](https://en.wikipedia.org/wiki/Skew-Hermitian_matrix), namely
\\begin{equation}
	\\mathrm{Tr}\\!\\left[X\_{i}\\right] = 0\\,,\\quad X\_{i}^{\\dagger} = -X\_{i}\\,,
\\end{equation}
for \\(i = 1, 2, 3\\). Any other \\(2 \\times 2\\) matrix with these properties can be written as a linear combination of the generators. The only way to preserve these properties is to transform the generators under the \\(\\boldsymbol{2} \\otimes \\boldsymbol{\\overline{2}}\\) Tensor representation.

&nbsp;&nbsp;&nbsp;&nbsp;As a side remark, the representation of \\(SU\\!\\left(2\\right)\\) that acts on its generators has a special name - it is called the *Adjoint*. It differs from the Fundamental and Anti-Fundamental by the fact that it is a map to \\(3 \\times 3\\) matrices. The Adjoint is derived explicitly in Part&nbsp;[\\(\\text{V}\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation). Trust me, it is worth the wait. In the meantime, let us continue the discussion using the Tensor representation, which is larger in some sense, but easier to understand at this point.

&nbsp;&nbsp;&nbsp;&nbsp;We established the fact that a vector \\(V \\in \\mathfrak{su}\\!\\left(2\\right)\\) transforms under \\(V \\sim \\boldsymbol{2} \\otimes \\boldsymbol{\\overline{2}}\\), meaning that an \\(SU\\!\\left(2\\right)\\) element, \\(U\\), acts on it as the sandwich product
\\begin{equation}
	V \\longmapsto\\ U V U^{\\dagger}\\,.
\\end{equation}
The vector \\(V\\) is of the form
\\begin{equation}
	V = v\_{1} X\_{1} + v\_{2} X\_{2} + v\_{3} X\_{3}\\,,
\\end{equation}
where \\(v\_{i}\\) are chosen to be *real*, otherwise \\(V\\) will not be skew-Hermitian. This is to say that \\(\\mathfrak{su}\\!\\left(2\\right)\\) is a real vector space - just like our \\(3D\\) Euclidean space!
<br><br>

### \\(12\\ \\) The Connection Between \\(SU\\!\\left(2\\right)\\) And \\(SO\\!\\left(3\\right)\\)
<div style="display:none">\(\setSection{12}\)</div>

Some of you may already be familiar with what follows, and for others it may be the first time seeing this derivation. In Section&nbsp;[\\(11\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#11--the-suleft2right-algebra-and-generators), we defined the action of \\(SU\\!\\left(2\\right)\\) on its algebra \\(\\mathfrak{su}\\!\\left(2\\right)\\), which is a \\(3\\)-dimensional real vector space. We would like to show now that this action is equivalent to a \\(3\\)-dimensional rotation. First, associate \\(3\\)-dimensional vectors with \\(2 \\times 2\\) traceless and skew-Hermitian matrices by
\\begin{equation}
	\\label{eq:SU(2)-SO(3) Isomorphism}
	\\vec{v} \\longrightarrow V \\equiv \\sum\_{i = 1}^{3} v\_{i} X\_{i} = \\begin{pmatrix} i v\_{3} & -v\_{2} + i v\_{1} \\\\ v\_{2} + i v\_{1} & -i v\_{3} \\end{pmatrix}\\,.
\\end{equation}
This is a \\(1\\)-to-\\(1\\) mapping - the inverse map is obviously given using the dot-product, namely projecting onto the basis vectors
\\begin{equation}
	\\label{eq:SU(2)-SO(3) Isomorphism Inverse}
	V \\longrightarrow v\_{i} = \\frac{1}{2} \\mathrm{Tr}\\!\\left[X\_{i} V^{\\dagger}\\right]\\,.
\\end{equation}

&nbsp;&nbsp;&nbsp;&nbsp;As \\(V \\sim \\boldsymbol{2} \\otimes \\boldsymbol{\\overline{2}}\\), its transformation induces a transformation of \\(3\\)-dimensional real vectors by
\\begin{equation}
	v\_{i} \\longmapsto \\sum\_{j = 1}^{3} O\_{ij} v\_{j}\\,,\\quad O\_{ij} = \\frac{1}{2} \\mathrm{Tr}\\!\\left[X\_{i} U X\_{j}^{\\dagger} U^{\\dagger}\\right]\\,.
\\end{equation}
To get it, just transform \\(V\\) in Eq.&nbsp;\\eqref{eq:SU(2)-SO(3) Isomorphism Inverse}. The claim, which is not proven here, is that \\(O\\) is a rotation matrix. Check this claim!

&nbsp;&nbsp;&nbsp;&nbsp;The construction above defines a mapping function \\(\\phi\\!: SU\\!\\left(2\\right) \\longrightarrow SO\\!\\left(3\\right)\\). The interesting observation is that \\(\\phi\\!\\left(U\\right) = \\phi\\!\\left(-U\\right)\\), so there are two elements in \\(SU\\!\\left(2\\right)\\) which are being mapped to the same element of \\(SO\\!\\left(3\\right)\\). In fact, \\(\\phi\\) is \\(2\\)-to-\\(1\\). We thus say that \\(SU\\!\\left(2\\right)\\) is a double-cover of \\(SO\\!\\left(3\\right)\\).

&nbsp;&nbsp;&nbsp;&nbsp;The association presented in Eq.&nbsp;\\eqref{eq:SU(2)-SO(3) Isomorphism} is similar to the one that we do when we treat the imaginary part of the quaternion as a \\(3\\)-dimensional vector, Eq.&nbsp;[\\(\\left(2.1\\right)\\)](https://07U.github.io/Quaternions/Preamble#mjx-eqn%3Aeq%3AThe_Vector_Quaternion_Association). Now, we know why it indeed transforms as a vector, and even have a name for its vector space! More on this in Part&nbsp;[\\(\\text{V}\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation).
<br><br>

### \\(13\\ \\) Summary
<div style="display:none">\(\setSection{13}\)</div>

This part is the most intense one in this text, and I feel a summary section is necessary. What did we achieve up until this point?
* We mapped the imaginary **quaternions** to a set of matrices we call \\(X\\) that have the same multiplication properties.
	* This was originally done in Eq.&nbsp;[\\(\\left(8.5\\right)\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#mjx-eqn%3Aeq%3A2D_Quaternion_Representation), although we did not call them by name.
* The \\(X\\)s actually serve as the basis of the \\(3\\)-dimensional vector space \\(\\mathfrak{su}\\!\\left(2\\right)\\). Exponentiating an \\(\\mathfrak{su}\\!\\left(2\\right)\\) vector results in an \\(SU\\!\\left(2\\right)\\) element.
	* The exponentiation was discussed in Section&nbsp;[\\(8\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#8--fun-with-quaternions).
* We have presented different representations of the \\(SU\\!\\left(2\\right)\\) group.
	* The different representations are a very important tool, as they allow us to consider a group element, and potentially apply it on new vector spaces.
* We then showed how a Tensor representation could act on an \\(\\mathfrak{su}\\!\\left(2\\right)\\) vector.
	* Combining with the above points, this shows that quaternions can be used to both represent a \\(3\\)-dimensional vector space, and a transformation that acts on it.
* Lastly, without an explicit proof, we derived a translation from the \\(SU\\!\\left(2\\right)\\) Tensor representation to the Fundamental representation of \\(SO\\!\\left(3\\right)\\), which are **rotations** in \\(3D\\) space.

If you understood everything between the two bold words, I am satisfied.

&nbsp;&nbsp;&nbsp;&nbsp;In Part&nbsp;[\\(\\text{V}\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation), the last part of this text, we will derive \\(O\\) explicitly, hopefully closing any loose ends you may have.
<br><br>

---
<br>

To the previous part: [\\(\\text{III}\\ \\) Establishing Basic Concepts](https://07U.github.io/Quaternions/EstablishingBasicConcepts).<br>
To the next part: [\\(\\text{V}\\ \\) On The Adjoint Representation](https://07U.github.io/Quaternions/OnTheAdjointRepresentation).
<br><br>

# Discussion

Any comments or questions related to this part can be posted in the [dedicated LinkedIn post](https://www.linkedin.com/posts/oz-davidi_dear-network-in-the-text-i-wrote-quaternions-activity-7223569852102279169-qXlu).
<br><br>

---
<br>

[^12]: Reminder: a representations is a map of group elements to matrices that operate on a vector space - not the operation itself!
[^13]: It was not shown that the \\(SO\\!\\left(2\\right)\\) Fundamental representation is an identity map, as it was originally presented in Eq.&nbsp;[\\(\\left(6.3\\right)\\\)](https://07U.github.io/Quaternions/Intuition#mjx-eqn%3Aeq%3Ai_Fundamental_Representation) as a map of \\(i\\) and not as a map of the group elements. However, the resulting matrix after exponentiation, Eq.&nbsp;[\\(\\left(6.4\\right)\\\)](https://07U.github.io/Quaternions/Intuition#mjx-eqn%3Aeq%3AFundamental_Representation_of_Euler%E2%80%99s_Formula), was exactly \\(\\rho\\!\\left(\\theta\\right)\\), as defined in Eq.&nbsp;[\\(\\left(5.3\\right)\\\)](https://07U.github.io/Quaternions/Intuition#mjx-eqn%3Aeq%3A2D_Rotation_Matrix). Meaning that, in this setting, \\(D\\!\\left(\\rho\\right) = \\rho\\).
[^14]: Not those above the indices - these are just a cosmetic marks.
[^15]: In the Physics community, where I had spent a decent fraction of my life, it is standard to normalize the basis elements by a multiplicative factor of half. In case I introduce this factor, I would probably have to write a whole section just on its origin. This factor would not play an important role, so my fellow physicists would have to excuse me for omitting it (and for not using [Pauli matrices](https://en.wikipedia.org/wiki/Pauli_matrices)).
[^16]: Make sure you understand why it is a valid dot-product!
