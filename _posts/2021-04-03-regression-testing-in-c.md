---
layout: post
title:  "Regression testing in C"
---

# Alternatives to unit tests

While working on my numerical model for [Elastic Fibre Networks][RFN], I became more interested in testing and methods for building more confidence in software projects.

For reasons of efficiency and compatibility with the PETSc library, I was writing the model in C, which gave me few choices when considering unit testing. While there are some options out there, the procedural nature of C combined with my limited experience at the time led me to look into some *homemade* alternatives.

After reading a bit more into the idea behind regression tests, to test for unexpected changes, I decided this could be a nice fit for software in a research domain, where I didn't necessarily know what was definitively correct, but I did want to be made aware when code modifications had changed my results unexpectedly.

To do this, I hacked together a shell script which ran the model for a series of small test cases and compared the output model with previously run and stored results.

In simplified form, this was

`mpiexec -n 1 ./model <params> > output.txt`

followed by

`diff output.txt prev_results.txt`

where the result of the `diff` can be checked with 

`if [ $? != 0 ]; then`...

[RFN]: https://github.com/M-R-Houghton/petsc_model/wiki

