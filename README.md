README
======

Supporting data for the paper

    New lower bounds for kissing numbers in dimensions 25–29 and 31
    Rustem Takhanov and Stanislav Yun

This directory contains coordinate files and saved numerical-search outputs
supporting the constructions reported in the paper.

A kissing configuration in R^d is represented by an N x d NumPy array whose
rows are unit vectors.  The kissing condition is

    x_i^T x_j <= 1/2   for all i != j.

The constructions start from the Leech-lifting configurations used by
PackingStar and modify them as described in the paper.


1. MAIN RESULTS REPRESENTED IN THIS DIRECTORY
---------------------------------------------

Dimension   Starting size   Size supplied here   Modification
---------   -------------   ------------------   -------------------------------
25          197056          197058               modified lifting height;
                                                add the antipodal poles +/-e_25
26          198550          198552               rotate lifted+auxiliary block;
                                                add an antipodal pair
27          200044          200046               rotate lifted+auxiliary block;
                                                add an antipodal pair
28          204520          204522               rotate lifted+auxiliary block;
                                                add an antipodal pair
29          209496          209497               rotate lifted+auxiliary block;
                                                add one point
30          220440          220440               no improvement reported
31          238350          238354               rotate only the seven
                                                additional coordinates of the
                                                lifted vectors; add four points

Thus the coordinate files support the bounds

    tau_25 >= 197058,
    tau_26 >= 198552,
    tau_27 >= 200046,
    tau_28 >= 204522,
    tau_29 >= 209497,
    tau_31 >= 238354.

No improvement in dimension 30 is claimed.


2. FINAL COORDINATE FILES
-------------------------

Each ZIP archive below contains one float64 NumPy .npy array.  Rows are the
points of the corresponding spherical code.

    kissing_r25_197058_float64.zip
        kissing_r25_197058.npy
        shape: (197058, 25)

    kissing26_coord.zip
        kissing26_coord.npy
        shape: (198552, 26)

    kissing27_coord.zip
        kissing27_coord.npy
        shape: (200046, 27)

    kissing28_coord.zip
        kissing28_coord.npy
        shape: (204522, 28)

    kissing29_coord.zip
        kissing29_coord.npy
        shape: (209497, 29)

    kissing_r31_238354.zip
        kissing_r31_238354.npy
        shape: (238354, 31)

The maximum observed row-norm error in these stored float64 arrays is below
8e-16.

SHA-256 hashes of the inner .npy files:

    kissing_r25_197058.npy
        f4ac93575c536ff839738034a30d8a91fba2af329da5ead3c7720af076c53a79

    kissing26_coord.npy
        3f00fe093cc5b66f4458fcbe6e90bdb27932e1bc8400bda11db1436cd20c69be

    kissing27_coord.npy
        5cc217a675901681f9d73691d0c68c0b49da653bac4a84927f09b58001e761dd

    kissing28_coord.npy
        a09fb683f51508bc8f165f9af8696e893e2043a536428e2bb99ddcddfc4510c4

    kissing29_coord.npy
        0f0b2f1dc1149b460e8333229453325ce2222217ed1096f9518359864cb60490

    kissing_r31_238354.npy
        4a49815d0deb2289ad49577daa57890e56fa4109fdbcbaa9b6a1da4f28f933ba


3. SAVED SEARCH RUNS: run25.tar.gz THROUGH run31.tar.gz
------------------------------------------------------

The archives run25.tar.gz, ..., run31.tar.gz are saved outputs of the
joint rotation/hole search described in the paper.  In this search the
unlifted bulk B_d is fixed and the block

    M_d = (lifted vectors) union (auxiliary vectors)

is rotated by a common orthogonal matrix Q, while a candidate hole x is
optimized simultaneously.

Typical contents of runXX.tar.gz include:

    runXX/run_info.json
        Dimension, input sizes, source member, hashes, and decomposition of
        the original PackingStar configuration.

    runXX/result.json
        Final status of the run and information about accepted added points.

    runXX/certificate.json
        Numerical/certified bounds for the saved configuration and rotation.

    runXX/base_certificate.json
        Verification information for the rotated base configuration.

    runXX/configuration.npy
        The configuration produced by this particular rigid-block-rotation
        run.

    runXX/Q.npy, runXX/Q.txt
        Saved rotation matrix.

    runXX/x.npy
        Saved candidate hole.

    runXX/added.npy, runXX/added.txt
        Points actually added by that run.  These are empty in runs for which
        the generic rigid-block search produced no certified extension.

    runXX/solution.npz
        Compact saved solution data.

    runXX/joint/
        Optimizer state, progress log, arguments, checkpoint, best rotation,
        and best candidate point.

    runXX/saturation/
        For dimensions where points were added, additional searches attempting
        to find further holes.  Failure to find another point within these
        budgets is not a proof of saturation or global optimality.

The rigid-block runs yield the extensions in dimensions 26, 27, 28, and 29.
Their certified added-point counts are respectively 2, 2, 2, and 1.

The saved generic rigid-block searches in dimensions 25, 30, and 31 did not
find a certified first hole.  This is not a nonexistence result.

IMPORTANT:
The final d=25 and d=31 records are obtained by different constructions and
must not be confused with run25/configuration.npy or run31/configuration.npy.

For d=25 the paper changes the lifting height to h=1/2 and then adds +/-e_25.
For d=31 the paper rotates only the seven additional coordinates of the
lifted vectors while keeping the bulk and the auxiliary block fixed.


4. DIMENSION 31 CERTIFICATE DATA
--------------------------------

    certificate_D31.zip

contains:

    certificate_D31/kissing_r31_238354.zip
        The full 238354 x 31 float64 coordinate array.  This is identical to
        the root-level kissing_r31_238354.zip.

    certificate_D31/rotation_matrix_R.txt
        The 7 x 7 rotation R applied to the additional coordinates of all
        lifted vectors.

    certificate_D31/u1_and_u2_vectors.txt
        Two unit vectors u_1,u_2 in R^24 used to define the four added points.

The d=31 construction is the one described in the paper as follows.  The
126 auxiliary directions form a normalized E_7 root configuration.  For two
antipodal deepest-hole directions

    v_1 = -(1/sqrt(3), 0, 0, 0, 0, 0, sqrt(2/3)),
    v_2 = -v_1,

the four added points are

    z_j^+ = ( +(1/2) u_j, (sqrt(3)/2) v_j ),
    z_j^- = ( -(1/2) u_j, (sqrt(3)/2) v_j ),     j=1,2.

The final configuration is

    B_31 union L_31(R) union F_31 union
    {z_1^+, z_1^-, z_2^+, z_2^-},

with block sizes

    |B_31| = 175728,
    |L_31| = 62496,
    |F_31| = 126,

and total size 238354.

The paper gives rigorous upper bounds for all changed classes of inner
products, including

    m(L_31(R), F_31) <= 0.499868403188,
    m(L_31(R), Z)    <= 0.499383903054,

while the remaining relevant classes are bounded by 1/2 (or, for the
cross-pairs between the two hole families, by -1/2).

The text files in certificate_D31.zip are compact numerical data defining
this construction.  The rigorous certification in the paper interprets the
stored decimal rotation through its orthogonal polar factor and accounts for
normalization and numerical representation by outward-rounded bounds.


5. DIMENSION 25 SPECIAL CONSTRUCTION
------------------------------------

The d=25 record in

    kissing_r25_197058_float64.zip

does not come from the generic run25 rigid-block rotation search.

Let S_1 be the 496-point Leech subset used by the starting construction.
The lifted vectors are moved to height h=1/2:

    l_epsilon(u) = ( (sqrt(3)/2) u, epsilon/2 ),
    epsilon in {-1,+1}.

At this height the two poles +/-e_25 can be added.  The resulting size is

    (196560 - 496) + 2*496 + 2 = 197058.


6. QUICKLY LOADING A COORDINATE FILE
------------------------------------

Example:

    import numpy as np

    X = np.load("kissing_r31_238354.npy", allow_pickle=False)
    print(X.shape)                       # (238354, 31)
    print(np.max(np.abs(
        np.linalg.norm(X, axis=1) - 1
    )))

For another dimension, replace the file name accordingly.

A direct full Gram matrix is unnecessary and can require substantial memory.
For numerical checking, process row blocks and exclude the diagonal when
computing the maximum off-diagonal inner product.


7. INTERPRETATION OF NUMERICAL FILES
------------------------------------

The .npy files are convenient floating-point coordinate realizations.
They should not be confused with an exact symbolic representation.

The proofs in the paper use the algebraic structure of Leech lifting together
with explicit error bounds for the numerically changed parts.  In particular,
the numerical search output alone is not intended as a proof of global
optimality, and unsuccessful searches in dimensions 25, 30, or 31 do not
establish that no other extension exists.

The results claimed here are lower bounds obtained from explicit kissing
configurations.


8. PROVENANCE
-------------

The starting configurations in dimensions 25 through 31 are the
Leech-lifting configurations produced by PackingStar.  The saved run metadata
records the source member names and SHA-256 hashes used in the computations.

The present repository contains the derived coordinate files, rotations,
candidate points, certificates, and saved optimizer output needed to document
the computations reported in the paper.


9. CITATION
-----------

If you use these files, please cite the accompanying paper:

    Rustem Takhanov and Stanislav Yun,
    "New lower bounds for kissing numbers in dimensions 25–29 and 31",
    2026.

Please also cite the original PackingStar work for the starting
Leech-lifting configurations, as referenced in the paper.
