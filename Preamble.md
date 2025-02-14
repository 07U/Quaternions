<script src="load-mathjax.js" async></script>

## \\(\\text{I}\\ \\) Preamble

### \\(1\\ \\) Introduction
<div style="display:none">\(\setSection{1}\)</div>

This document was written to serve several purposes. The first is my urge to write. There is a nice feeling in sharing knowledge with others, initiating a discussion, or just revisiting intreresting ideas. I had this urge to write, especially on a topic very close to my heart, for a few years now - even before I started working in the video games industry - and finally I took the time to fulfill it. I am very pleased, because it allowed me to better understand things I thought I understand, but apparently I had missed some subtleties. I recommend you to do the same with a simple topic - you will be surprised!

&nbsp;&nbsp;&nbsp;&nbsp;Speaking of the video games industry, the second purpose for writing this text is to allow video game programmers to better understand the concept of quaternions. Be it new developers who do not have years of experience with this mathematical structure, and look for an explanation to why they "work"; or be it experienced engineers that use it as a black box, because someone already wrote the math library in the previous century, and anyway the code is unreadable.

&nbsp;&nbsp;&nbsp;&nbsp;A lot of people try to understand (and explain) quaternions in \\(4D\\). As an excellent former lecturer of mine describes it (in the context of black holes, though) - our brain was designed to make us run away from lions in the Savanna, and not for comprehending the \\(4^{\\text{th}}\\) dimension. I would like to show that although quaternions are \\(4\\)-dimensional objects, we do not need the \\(4^{\\text{th}}\\) dimension in order to understand, hopefully in a very intuitive way, how they rotate \\(3D\\) spaces.

&nbsp;&nbsp;&nbsp;&nbsp;Okay, but why is it presented here? Well, I wanted to "publish" the text somewhere, and the concepts that are going to be reviewed here are well known in the scientific community. However, in a practical industry like the video games one, some of the concepts covered here may not be familiar to most. I would have liked to allow for a potential discussion about the subjects presented here, and a social media such as LinkedIn looks like a good platform to have one with other professionals. Unfortunately, LinkedIn is not a friendly platform for technical articles, so I had to drop the idea of publishing the text there. This was how I ended up with this hybrid model - GitHub is responsible for presenting the text, while the potential discussion is done in dedicated posts on LinkedIn. Keeping LinkedIn as a medium would hopefully also allow this document to get more exposure.
<br><br>

### \\(2\\ \\) Prerequisites And Goals
<div style="display:none">\(\setSection{2}\)</div>

This text does not serve as an introduction to [Linear Algebra](https://en.wikipedia.org/wiki/Linear_algebra), [Complex Numbers](https://en.wikipedia.org/wiki/Complex_number), [Group Theory](https://en.wikipedia.org/wiki/Group_theory), [Representation Theory](https://en.wikipedia.org/wiki/Representation_theory), or even [Quaternions](https://en.wikipedia.org/wiki/Quaternion). The assumption is that the reader is familiar at least with linear algebra and complex numbers, and could understand new ideas as they are presented or used. Explicit derivations are not shown, and in order to arrive to the end result, one needs to know the theory behind the [Taylor series](https://en.wikipedia.org/wiki/Taylor_series), especially the [expansion of the exponential function](https://en.wikipedia.org/wiki/Exponential_function#Formal_definition), as well as the properties of the basic [trigonometric functions](https://en.wikipedia.org/wiki/Trigonometric_functions). There is an attempt referring to external sources, mostly Wikipedia (as is done in this paragraph), for further reading in case one of the terms is not known to the reader.

&nbsp;&nbsp;&nbsp;&nbsp;The text is also not going to cover the more general subject of [Geometric Algebra](https://en.wikipedia.org/wiki/Geometric_algebra). If one wants to gain a complete picture on the algebraic representation of geometric objects, how to transform them (in any number of dimensions!), and how this can be implemented in a video game engine - this is not the place. There are good sources for material on this huge subject online. One which I really recommend is [biVector.net](https://bivector.net/) - I found the documents a little bit harder to understand for beginners, but the videos are highly recommended![^1]

&nbsp;&nbsp;&nbsp;&nbsp;This was about what the text expects of you, and what you should not expect of it. The main goal of this text is to place the quaternions inside a fictional MRI machine, and see into their mechanism for rotations. As a reminder, with this mechanism, a vector \\(\\vec{v} \\in \\mathbb{R}^{3}\\) is rotated by defining the purely imaginary quaternion
\\begin{equation}
	\\label{eq:The Vector Quaternion Association}
	\\vec{v} = \\begin{pmatrix}x \\\\ y \\\\ z\\end{pmatrix} \\quad\\longleftrightarrow\\quad v = x i + y j + z k\\,,
\\end{equation}
and applying the sandwich product
\\begin{equation}
	v \\longmapsto q v q^{-1}\\,,
\\end{equation}
with some quaternion \\(q\\) - the rotating quaternion. Don't worry, we will go over the definition of quaternion multiplications again. I would like to state at this stage, though, that because, by definition,
\\begin{equation}
	q q^{-1} = 1\\,,
\\end{equation}
the global scale does not play any role. It is thus customary and makes total sense to consider only unit-quaternions, *i.e.* those that satisfy
\\begin{equation}
	\\left|q\\right|^{2} = q q^{\\ast} = 1 \\quad\\longleftrightarrow\\quad q^{-1} = q^{\\ast}\\,,
\\end{equation}
with the conjugation operation, \\(\\ast\\), negating \\(i\\), \\(j\\), and \\(k\\). Hence, our MRI machine should reveal to us the matrix-code that runs[^2]
\\begin{equation}
	\\label{eq:Unit Quaternion Transformation}
	v \\longmapsto q v q^{\\ast}\\,.
\\end{equation}

&nbsp;&nbsp;&nbsp;&nbsp;By considering unit-quaternions, we have eliminated one dimension from their description. However, it is a dimension in the wrong direction. I would like to show you the "natural" \\(3\\) dimensions of unit-quaternions. This would allow us to clarify how and why quaternions rotate \\(3\\)-dimensional vectors, and how and why they relate to \\(3 \\times 3\\) rotation matrices the way they do.

&nbsp;&nbsp;&nbsp;&nbsp;By the end of this document, I hope you would also be able to: understand the potential issues with quaternion linear interpolation (without even performing one!); be able to criticize any text or video on this subject (even this one!); and if you are going to really pay attention, understand what determines the direction of rotation (which seems to always be done according to the right-hand rule[^3]). This last point is extremely subtle, and I know I did not quite understand the technicalities until now.

&nbsp;&nbsp;&nbsp;&nbsp;I hope this text will provide a refreshing point of view to some readers, and help others. Again, derivations are not rigorous, as I hope the small details skipped are easily reproducible by the reader, but also because I wanted to release the text at some point. With that said, this is the internet - if anything is missing, or a jump is too big, please write to me and I will make sure the text gets improved and things get clarified. Although most of the information here is not new, in the last section of this text, a branchless algorithm is presented. I am not aware of a similar algorithm, so I hope this could be considered as a new contribution that may be helpful for other developers, even if just on the conceptual level.
<br><br>

### \\(3\\ \\) Overview
<div style="display:none">\(\setSection{3}\)</div>

Part&nbsp;[\\(\\text{II}\\)](https://07U.github.io/Quaternions/Intuition) serves as an appetizer for what is yet to come, and builds new concepts on top of previous knowledge. In Section&nbsp;[\\(5\\)](https://07U.github.io/Quaternions/Intuition#5--rotations-with-complex-numbers) we review complex numbers and their relation to \\(2D\\) rotations. We then make a small leap, in Section&nbsp;[\\(6\\)](https://07U.github.io/Quaternions/Intuition#6--a-glimpse-into-the-future), and use the complex numbers example to define an extremely important concept - the *representation* - which would allow us to look at quaternions with new and powerful glasses.

&nbsp;&nbsp;&nbsp;&nbsp;Part&nbsp;[\\(\\text{III}\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts) starts in Section&nbsp;[\\(7\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#7--groups), where we introduce the *group*. In Section&nbsp;[\\(8\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#8--fun-with-quaternions), we repeat the process which was applied to complex numbers, but now with quaternions. Unfortunately, it is not as easy as with complex numbers, as it does not directly connect quaternions to rotations, but to some weird transformations in \\(4\\) dimensions. However, it reveals an interesting and somewhat hidden role of the imaginary part of quaternions. Closing remarks are made in Section&nbsp;[\\(9\\)](https://07U.github.io/Quaternions/EstablishingBasicConcepts#9--closing-remarks).

&nbsp;&nbsp;&nbsp;&nbsp;Part&nbsp;[\\(\\text{IV}\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations) goes almost till the end, where we establish the first connection between quaternions and rotations in \\(3\\)-dimensional space. It is the most technical part, and it starts with a bang. Section&nbsp;[\\(10\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#10--representations) dives into more details about *representations*. Section&nbsp;[\\(11\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#11--the-suleft2right-algebra-and-generators) clarifies this above-mentioned hidden role of imaginary quaternions, where we briefly mention the concepts of an *algebra* and *generators*. In Section&nbsp;[\\(12\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#12--the-connection-between-suleft2right-and-soleft3right) we finally derive an implicit connection between quaternions and \\(3D\\) rotations. Section&nbsp;[\\(13\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#13--summary) summarizes.

&nbsp;&nbsp;&nbsp;&nbsp;But we are not done yet! Part&nbsp;[\\(\\text{V}\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation) serves as the ultimate part. Section&nbsp;[\\(14\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation#14--deriving-the-explicit-rotation-matrix-form) applies all the knowledge we have gained, showing explicitly how a \\(3\\)-dimensional rotation matrix emerges out of a quaternion. Section&nbsp;[\\(15\\)](https://07U.github.io/Quaternions/OnTheAdjointRepresentation#15--a-branchless-matrix-to-quaternion-translation) discusses the inverse process of extracting a quaternion out of a rotation matrix, and presents a branchless implementation for doing this.
<br><br>

### \\(4\\ \\) Acknowledgments
<div style="display:none">\(\setSection{4}\)</div>

Want your LinkedIn profile to appear here? Please join the conversation and contribute! At the end of each part, there is a reference to the post on LinkedIn regarding that part. Please add your comments and insights there. You could also write to me directly in my [LinkedIn profile](https://www.linkedin.com/in/Oz-Davidi/).
<br><br>

---
<br>

To the next part: [\\(\\text{II}\\ \\) Intuition](https://07U.github.io/Quaternions/Intuition).
<br><br>

# Discussion

Any comments or questions related to this part can be posted in the [dedicated LinkedIn post](
https://www.linkedin.com/posts/oz-davidi_dear-network-and-community-in-the-past-activity-7209858721005400064-t-XS).
<br><br>

---
<br>

[^1]: Please check it after you read this text, as it makes the text obsolete in some sense 😅
[^2]: Pun was not intended.
[^3]: There are claims on the internet that a quaternion with a negative real part performs a rotation according to the left-hand rule, but that is not quite accurate.
