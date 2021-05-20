Ipopt
=====

# You are looking at **Ipopt 3.14 BETA**. For Ipopt 3.13, checkout branch stable/3.13 or [release 3.13.4](https://github.com/coin-or/Ipopt/releases/tag/releases/3.13.4).

Introduction
------------

Ipopt (Interior Point OPTimizer, pronounced eye-pea-Opt) is a software package for large-scale [nonlinear optimization](http://wiki.mcs.anl.gov/NEOS/index.php/Nonlinear_Programming_FAQ).
It is designed to find (local) solutions of mathematical optimization problems of the form

```
   min     f(x)
  x ∈ Rⁿ

s.t.       g_L ≤ g(x) ≤ g_U
           x_L ≤  x   ≤ x_U
```
where ```f(x): Rⁿ --> R``` is the objective function, and ```g(x): Rⁿ --> Rᵐ```
are the constraint functions.  The vectors `g_L` and `g_U` denote the lower and upper bounds on the constraints, and the vectors `x_L` and `x_U` are the bounds on the variables `x`.
The functions `f(x)` and `g(x)` can be nonlinear and nonconvex, but should be twice continuously differentiable.
Note that equality constraints can be formulated in the above formulation by setting the corresponding components of `g_L` and `g_U` to the same value.

Ipopt is part of the [COIN-OR Initiative](http://www.coin-or.org).
The Ipopt project webpage is <https://github.com/coin-or/Ipopt>.


Background
----------

Ipopt is written in C++ and is released as open source code under the [Eclipse Public License (EPL)](LICENSE).
The code has been written by [Andreas Wächter](http://www.mccormick.northwestern.edu/directory/profiles/Andreas-Waechter.html) and [Carl Laird](http://allthingsoptimal.com/biography/).
The COIN-OR project managers for Ipopt are [Andreas Wächter](http://users.iems.northwestern.edu/~andreasw) und [Stefan Vigerske](https://www.gams.com/~stefan).
For a list of **all contributors**, see the [AUTHORS file](AUTHORS).

The C++ version has first been [released on Aug 26, 2005](http://list.coin-or.org/pipermail/ipopt/2005-August/000331.html) as version 3.0.0.
The previously released [pre-3.0 Fortran version](https://github.com/coin-or/Ipopt/tree/stable/2.3) is no longer maintained.


The Ipopt distribution can be used to generate a library that can be linked to one's own C++, C, Fortran, or Java code, as well as a solver executable for the [AMPL](http://www.ampl.com) modeling environment.
The package includes an interface to the [R](http://www.r-project.org/) programming environment.
IPOPT can be used on Linux/UNIX, macOS, and Windows platforms.

As open source software, the source code for Ipopt is provided without charge.
You are free to use it, also for commercial purposes.
You are also free to modify the source code (with the restriction that you need to make your changes public if you decide to distribute your version in any way, e.g. as an executable); for details see the EPL license.
And we are certainly very keen on feedback from users, including contributions!

In order to compile Ipopt, certain third party code is required (such as some linear algebra routines).
Those are available under different conditions/licenses.

If you want to learn more about Ipopt, you can find references in the [bibliography of the documentation](https://coin-or.github.io/Ipopt/citelist.html) and this ["Papers about Ipopt" page](https://github.com/coin-or/Ipopt/wiki/IpoptPapers).

For information on projects that use Ipopt, refer to the [Success Stories page](https://github.com/coin-or/Ipopt/wiki/SuccessStories).


Getting Started
---------------

Please consult the [detailed installation instructions](https://coin-or.github.io/Ipopt/INSTALL.html)
in the Ipopt documentation. In the following, we only summarize some main points.

### Dependencies

Ipopt requires at least one of the following solvers for systems of linear equations:
- MA27, MA57, HSL_MA77, HSL_MA86, or HSL_MA97 from the [Harwell Subroutines Library](http://hsl.rl.ac.uk) (HSL).
  It is recommended to use project [ThirdParty-HSL](https://github.com/coin-or-tools/ThirdParty-HSL) to build a HSL library for use by Ipopt.
- [Parallel Sparse Direct Linear Solver](http://www.pardiso-project.org) (Pardiso).
  Note, that the Intel Math Kernel Library (MKL) also includes a version of Pardiso, but the one from Pardiso Project often offers better performance.
- [Sparse Parallel Robust Algorithms Library](https://github.com/ralna/spral) (SPRAL).
- [MUltifrontal Massively Parallel sparse direct Solver](http://mumps.enseeiht.fr/) (MUMPS).
  It is highly recommended to use project [ThirdParty-Mumps](https://github.com/coin-or-tools/ThirdParty-Mumps) to build a MUMPS library for use by Ipopt.
- [Watson Sparse Matrix Package](http://www.research.ibm.com/projects/wsmp)

A fast implementation of BLAS and LAPACK is required by Ipopt.

To build the AMPL interface of Ipopt, the AMPL Solver Library (ASL) is required.
It is recommended to use project [ThirdParty-ASL](https://github.com/coin-or-tools/ThirdParty-ASL) to build a ASL library for use by Ipopt.

### Build

After installation of dependencies, an Ipopt build and installation follows these 4 steps:

1. Run `./configure`. Use `./configure --help` to see available options.

2. Run `make` to build the Ipopt libraries. If ASL was made available, also Ipopt executables will be build.

3. Run `make test` to test the Ipopt build.

4. Run `make install` to install Ipopt (libraries, executables, and header files).

It is suggested to use the same installation prefix (`--prefix` option of `configure`)
when configuring the build of ThirdParty-ASL, ThirdParty-HSL, ThirdParty-MUMPS, and Ipopt.

### Using coinbrew

An alternative to the above steps is to use the `coinbrew` script from
https://coin-or.github.io/coinbrew/.
`coinbrew` automates the download of the source code for ASL, MUMPS, and Ipopt
and the sequential build and installation of these three packages.

After obtaining the `coinbrew` script, run

    /path/to/coinbrew fetch Ipopt --no-prompt
    /path/to/coinbrew build Ipopt --prefix=/dir/to/install --test --no-prompt --verbosity=3
    /path/to/coinbrew install Ipopt --no-prompt

More details on using coinbrew can be found at the instructions on
[Getting Started with the COIN-OR Optimization Suite](https://coin-or.github.io/user_introduction).

### Precompiled binaries

Some precompiled binaries of Ipopt are also available:

- **[Ipopt releases page](https://github.com/coin-or/Ipopt/releases)** provides libraries and executables
- **[JuliaBinaryWrappers](https://github.com/JuliaBinaryWrappers/Ipopt_jll.jl/releases)** provides libraries and executables
- **[IDEAS](https://github.com/IDAES/idaes-ext/releases)** provides executables; these executables include HSL solvers
- **[AMPL](http://ampl.com/products/solvers/open-source/#ipopt)** provides executables
- **[Pardiso project](https://pardiso-project.org/index.html#binaries)** provides libraries for using Ipopt with Pardiso through Matlab (Matpower)

Getting Help
------------

 * **[Ipopt Documentation](https://coin-or.github.io/Ipopt/)** with installation instructions, options reference, and more
 * **[Issue tracking system](https://github.com/coin-or/Ipopt/issues/)**: If you believe you found a **bug** in the code, please use the issue tracking system.
   Please include as much information as possible, and if possible some (ideally simple) example code so that we can reproduce the error.
 * **[Discussions](https://github.com/coin-or/Ipopt/discussions)**: ask questions, share ideas, engage with the Ipopt community
 * **[Mailing list archive](http://list.coin-or.org/pipermail/ipopt/)** (2002-2020): predecessor of Discussions
 * **[Ipopt Wiki](https://github.com/coin-or/Ipopt/wiki)** with hints and tricks
 * External resources:
   * [short Ipopt tutorial](http://drops.dagstuhl.de/volltexte/2009/2089/pdf/09061.WaechterAndreas.Paper.2089.pdf)
   * [build Ipopt on Windows step-by-step](https://github.com/Ishanki/IPOPT-Installation-on-Windows-10)

Please Cite Us
--------------

We provide this program in the hope that it may be useful to others, and we would very much like to hear about your experience with it.
If you found it helpful and are using it within our software, we encourage you to add your feedback to the [Success Stories page](https://github.com/coin-or/Ipopt/wiki/SuccessStories).

Since a lot of time and effort has gone into Ipopt's development, **please cite the following publication if you are using Ipopt for your own research**:

* A. Wächter and L. T. Biegler, **[On the Implementation of a Primal-Dual Interior Point Filter Line Search Algorithm for Large-Scale Nonlinear Programming](http://dx.doi.org/10.1007/s10107-004-0559-y)**, _Mathematical Programming_ 106(1), pp. 25-57, 2006
  ([preprint](http://www.optimization-online.org/DB_HTML/2004/03/836.html))
