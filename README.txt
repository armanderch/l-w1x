----- Background -----
For more information on the L-W1X methods, see:
Assessment of DLPNO-CCSD(T)-F12 and its use for the formulation of the low-cost and reliable L-W1X composite method.
Chan, B.; Karton, A. J. Comput. Chem. 2022, 43, 1394.
https://doi.org/10.1002/jcc.26892

----- General -----
A set of ".cmp" files is included in the "cmp-files" folder. Put them in a convenient location on your system. In your ORCA input, include the full path to the chosen .cmp file. The L-W1X energy is printed at the end of the output under the COMPOUND BLOCK.

----- Variations -----
For a collection of neutral species with only light elements, using the lw1x.cmp would be ideal.

For systems with heavy elements, use the lw1x-p34.cmp file; it mimics the W1-P34 method. The lw1x-p34.cmp file incorporates basis-set and ECP options for the heavy elements, and the DKH component is calculated separately from the inner-valence-correlation component. For this reason, it would be (very) slightly more expensive than the use of lw1x.cmp.

When some of the species of interest are anionic, the use of larger sets of diffuse functions might be desirable. In these cases, the use of the lw1x-jun.cmp and lw1x-p34-jun.cmp protocols may be more appropriate.

For some systems (e.g., polycyclic aromatic hydrocarbons), the use of diffuse functions on carbon leads to basis-set linear dependency. To avoid this issue, the lw1x-no-diffuse-on-c.cmp file assigns non-augmented basis sets for carbon; it is otherwise identical to lw1x.cmp.

----- Examples -----
(1) h2o-addition:

This folder contains input and output files for lw1x.cmp and lw1x-p34.cmp calculations for the species in the reaction:

H2O + CH2=CH2 -> CH3-CH2-OH

The results are shown below, with total energies in hartree (with 5 decimal places) and relative energies in kJ/mol (with 1 decimal place).
         W2X      L-W1X  L-W1X-P34  diff
H2O           -76.47026  -76.47307  -7.4
C2H4          -78.59086  -78.59187  -2.7
C2H5OH       -155.08407 -155.08787 -10.0
rxn E  -61.2      -60.2      -60.2   0.1

The difference in treatments in lw1x.cmp and lw1x-p34.cmp results in different total energies, but there is little difference in the relative energies. In comparison, the W2X reaction energy is -61.2 kJ/mol.

(2) ch3i-ionization:

This example illustrates the use of lw1x-p34.cmp for a heavy-element system, namely the ionization of CH3I:

CH3I -> CH3I+

For this reaction, we have obtained the following energies:
      W1-P34   L-W1X-P34
CH3I         -7151.70495
CH3I+        -7151.34250
rxn E  952.7       951.6

They give a reaction energy of 951.6 kJ/mol, which is in reasonable agreement with the W1-P34 value of 952.7 kJ/mol.

(3) sn2-reaction:

Here, we demonstrate the effect of using larger sets of diffuse functions (lw1x-jun.cmp and lw1x-p34-jun.cmp, vs lw1x.cmp and lw1x-p34.cmp) for which it may be advantageous. Specifically, we use the SN2 reactions:

OH- + CH3-F -> CH3-OH + F-
OH- + CH3-I -> CH3-OH + I-
 
The calculated energies and the resulting reaction energies are:
         W2      L-W1X  L-W1X-jun  diff
OH-          -75.83330  -75.83856 -13.4
CH3F        -139.81458 -139.81698  -6.3
F-           -99.91691  -99.92190 -13.1
CH3OH       -115.76349 -115.76532  -4.8
rxn E -84.3      -85.4      -83.2   2.2
   
      W2-P34   L-W1X-P34 L-W1X-P34-jun  diff
OH-            -75.83607     -75.84118 -13.4
CH3I         -7151.70495   -7151.70645  -4.0
I-           -7111.88374   -7111.88636  -6.9
CH3OH         -115.76672    -115.76856  -4.8
rxn E -281.7      -287.3        -281.7   5.7

For the fluorine reaction, both methods yield comparable results. However, for the iodine reaction, the use of the "jun" method leads to a notably better agreement with the W2-P34 reference. This is due to, with lw1x-p34.cmp, poorer cancelation of errors between the energies for the "hard" OH- and the "soft" I- anions.

(4) isodesmic:

In this last example, we use lw1x.cmp and lw1x-no-diffuse-on-c.cmp for the reaction:

naphthalene + CH2=CH2 -> 2 benzene

This gives the following results (L-W1X* refers to lw1x-no-diffuse-on-c.cmp):
      W1X-1      L-W1X     L-W1X* diff
C2H4         -78.59088  -78.59071  0.4
C6H6        -232.25924 -232.25896  0.8
C10H8       -385.91267 -385.91258  0.2
rxn E -39.0      -39.2      -38.4  0.9

For comparison, the W1X-1 energy is -39.0 kJ/mol. Thus, both lw1x.cmp and lw1x-no-diffuse-on-c.cmp results are in good agreement with the reference. Note that, for these hydrocarbon species, the omission of diffuse functions on carbon causes little changes in the total energies.

For larger aromatic hydrocarbons, such as chrysene, the use of lw1x.cmp leads to basis-set linear dependency issues. In this case, the calculation crashed during the integration step of the second component calculation [DefGrid3 RIJCOSX TightPNO DLPNO-CCSD(T1)-F12]. In comparison, the lw1x-no-diffuse-on-c.cmp computation finished normally.
