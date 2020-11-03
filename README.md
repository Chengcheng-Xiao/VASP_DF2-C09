# VASP_DF2-C09
This patch adds the ability to use `vdW-DF2-C09` exchange correlation functional to VASP (v.5.4.4)

<!-- __NOTE: This is a unstable branch, results still needs testing.__ -->

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

To use DF2-C09, simply add the following tags to your `INCAR` file:

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

Also, don't forget the `vdw_kernel.bindat` file.

## Validation
The correctness of this patch was checked by comparing the lattice constants of GaSe to the [reported results](https://www.sciencedirect.com/science/article/abs/pii/S0022459615301535). The calculation was performed with the following parameters:

- ENCUT  = 680
- EDIFFG = -0.002
- EDIFF  = 1E-6
- KPOINTS= gamma centered 12x12x2

| Literature  | a (\AA)    | c (\AA)   |   This implementation   | a (\AA)  | c (\AA)  |
|-------------|-------|--------|-------------|-------|--------|
| LDA         | 3.719 | 15.611 | LDA         | 3.717 | 15.647 |
| PBE         | 3.823 | 17.848 | PBE         | 3.817 | 18.145 |
| vdw-DF2     | 3.946 | 16.511 | vdw-DF2     | 3.959 | 16.577 |
| rev-vdW-DF2 | 3.788 | 16.073 | rev-vdW-DF2 | 3.792 | 16.028 |
| vdW-DF2-C09 | 3.761 | 15.943 | vdW-DF2-C09 | 3.767 | 15.901 |
| PBE-D2      | 3.749 | 15.931 | PBE-D2      | 3.745 | 15.927 |






## Disclamer
Any result obtained by this patch should be carefully checked by the user.
