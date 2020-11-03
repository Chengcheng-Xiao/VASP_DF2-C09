# VASP_DF2-C09
This patch adds the ability to calculate `vdW-DF2-C09` exchange correlation functional to VASP (v.5.4.4)

__NOTE: This is a unstable branch, results still needs testing.__

## Installation

1. [Download](http://cms.mpi.univie.ac.at/patches/patch.5.4.4.16052018.gz) and apply the official patch for version-5.4.4.16052018.
```
patch -p0 < patch.5.4.4.16052018
```

2. Apply patch provided by this repo `DF2_C09.patch`:
```
patch -p0 < DF2_C09.patch
```

3. Compile VASP as usual.

## Usage

Add following tags to your `INCAR` file:

```
GGA      = C9
LUSE_VDW = .TRUE.
PARAM1   = 0.0617
PARAM2   = 1.245
PARAM3   = 0.0483
Zab_vdW  = -1.8867
AGGAC    = 0.0000
LASPH = .TRUE.
```

Here, `PARAM1` is `\mu`, `PARAM2` is `\kappa` and `PARAM3` is `\alpha` in equation 3 in [this paper](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.81.161104).

# Disclamer
This is a trial patch, any result obtained by this patch should be carefully checked.
