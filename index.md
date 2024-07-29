<script src="load-mathjax.js" async></script>

<h1>
  <p align = "center">Author: Oz Davidi</p>
</h1>
<h3>
  <p align = "center"><a href = "https://www.linkedin.com/in/Oz-Davidi/">https://www.linkedin.com/in/Oz-Davidi</a></p>
</h3>
<br>

In this text, the theory that relates quaternions and \\(3\\)-dimensional rotations - represented as \\(3 \\times 3\\) matrices - is reviewd. At the end of it, a branchless algorithm for extracting the quaternion parameters out of a rotation matrix is presented, accompanied by a possible implementation.
<br><br>

# [\\(\\text{I}\\ \\) Preamble](https://07U.github.io/Quaternions/Preamble)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(1\\ \\) Introduction](https://07U.github.io/Quaternions/Preamble#1--introduction)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(2\\ \\) Prerequisites And Goals](https://07U.github.io/Quaternions/Preamble#2--prerequisites-and-goals)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(3\\ \\) Overview](https://07U.github.io/Quaternions/Preamble#3--overview)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(4\\ \\) Acknowledgments](https://07U.github.io/Quaternions/Preamble#4--acknowledgments)

# [\\(\\text{II}\\ \\) Intuition](https://07U.github.io/Quaternions/Intuition)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(5\\ \\) Rotations With Complex Numbers](https://07U.github.io/Quaternions/Intuition#5--rotations-with-complex-numbers)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(6\\ \\) A Glimpse Into The Future](https://07U.github.io/Quaternions/Intuition#6--a-glimpse-into-the-future)

# [\\(\\text{III}\\ \\) Establishing Basic Concepts](https://07U.github.io/Quaternions/EstablishingBasicConcepts)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(7\\ \\) Groups](https://07U.github.io/Quaternions/EstablishingBasicConcepts#7--groups)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(8\\ \\) Fun With Quaternions](https://07U.github.io/Quaternions/EstablishingBasicConcepts#8--fun-with-quaternions)
### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(8.1\\ \\) Intuition?](https://07U.github.io/Quaternions/EstablishingBasicConcepts#81--intuition)
### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(8.2\\ \\) Quaternions As Matrices](https://07U.github.io/Quaternions/EstablishingBasicConcepts#82--quaternions-as-matrices)
### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(8.3\\ \\) What Is A Quaternion Exponentiation?](https://07U.github.io/Quaternions/EstablishingBasicConcepts#83--what-is-a-quaternion-exponentiation)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(9\\ \\) Closing Remarks](https://07U.github.io/Quaternions/EstablishingBasicConcepts#9--closing-remarks)

# [\\(\\text{IV}\\ \\) The Connection To \\(3D\\) Rotations](https://07U.github.io/Quaternions/TheConnectionTo3DRotations)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(10\\ \\) Representations](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#10--representations)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(11\\ \\) The \\(SU\\!\\left(2\\right)\\) Algebra And Generators](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#11--the-suleft2right-algebra-and-generators)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(12\\ \\) The Connection Between \\(SU\\!\\left(2\\right)\\) And \\(SO\\!\\left(3\\right)\\)](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#12--the-connection-between-suleft2right-and-soleft3right)
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\\(13\\ \\) Summary](https://07U.github.io/Quaternions/TheConnectionTo3DRotations#13--summary)
