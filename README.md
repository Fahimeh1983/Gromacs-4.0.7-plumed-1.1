# Installing Gromacs-4.0.7 and plumed-1.1

In this repository, you can find gromacs-4.0.7.tar and plumed-28mar.tar (this is plumed version 1.1). This plumed directory includes all the collective variables used in the following articles:

1) http://pubs.acs.org/doi/abs/10.1021/ja210826a

2) http://journals.aps.org/prl/abstract/10.1103/PhysRevLett.110.168103

The implementation of the collective variables can be find in the following directory:

plumed-28mar/common_files

The collective variables used in the first article are the following:

a) restraint_frontal_antibeta_8VAL.c

b) restraint_lateral_antibeta_8VAL.c 

c) restraint_lateral_parabeta_8VAL.c

The collective variables used in the second article are the following:

a) restraint_lateral_antibeta_MVGGVV.c

b) restraint_lateral_parabeta_MVGGVV.c

c) restraint_frontal_antibeta_MVGGVV_MET_MET.c

d) restraint_frontal_antibeta_MVGGVV_MET_VAL.c

e) restraint_frontal_antibeta_general.c

f) restraint_frontal_parabeta_general.c

To install plumed and gromacs, I suggest to first install gromacs itself to make sure that everything is working fine. 

## Installing gromacs

1) download gromacs-4.0.7.tar to your local computer, lets assume your working directory is dir=/home/username/workdir. From here after, we use $dir environmental variable to point to this working directory. 

2) Untar the gromacs-4.0.7.tar:

tar -xvf gromacs-4.0.7.tar

3) Rename the gromacs-4.0.7 to gromacs-4.0.7-noplumed

mv gromacs-4.0.7 gromacs-4.0.7-noplumed

4) Enter gromacs-4.0.7-noplumed  directory:

cd $dir/gromacs-4.0.7-noplumed

5) Run configure:

./configure

6) Install gromacs:

make

If everything works without any error, then you can excecute mdrun as the following:

$dir/gromacs-4.0.7-noplumed/src/kernel/mdrun

This version of gromacs does not have plumed installed (mdrun does not have the -plumed option)

## Installing gromacs with plumed

Now that we are sure that we were able to install gromacs without plumed without any problem, it is time to patch the plumed to gromacs and install it both together. Follow the steps below:

1) Untar the gromacs-4.0.7.tar and plumed-28mar.tar:

tar -xvf gromacs-4.0.7.tar

tar -xvf plumed-28mar.tar

3) Rename the gromacs-4.0.7 to gromacs-4.0.7-plumed

mv gromacs-4.0.7 gromacs-4.0.7-plumed

4) Enter gromacs-4.0.7-plumed directory:

cd $dir/gromacs-4.0.7-plumed

5) Run configure:

./configure

6) Enter plumed-28mar directory and find the right patch for the gromacs version, for gromacs-4.0.7, plumed patch version 4.0.4 is good enough:

cd $dir/plumed-28mar/patches

7) Open the patch that you have chosen:

vi plumedpatch_gromacs_4.0.4.sh

8) Change the line on top of the file which is representing the plumed directory to your plumed directory: plumedir=$dir/plumed-28mar (You should type you exact path)

9) Save and close this file

10) Enter your gromacs directory and copy that plumed patch to your gromacs directory:

cd $dir/gromacs-4.0.7-plumed

cp $dir/plumed-28mar/patches/plumedpatch_gromacs_4.0.4.sh .

11) Patch plumed to gromacs:

./plumedpatch_gromacs_4.0.4.sh -patch

If everything works fine, it should congratulate you on patching correctly. 

12) Now install gromacs with plumed:

make

If everything works without any error, you should be able to excecute mdrun and this time see that there is -plumed flag available. 

NOTE: If you wish to install the parallel version of gromacs with plumed, everything is the same but you should include mpi flags at step 5 (configure)

GOOD LUCK 
