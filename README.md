In this repository, I have recreated work for pristine CsV3Sb5 under pressure of 15 GPa, where I have calculated bands and phonons. The corresponding plots are placed here as bands.pdf and 15gpa.pdf. The purpose of these calculations is to learn DFT simulation using Quantum Espresso (QE). The steps are :
1) first fully relax the structure using vc-relax calculations implemented in QE with pressure = 0 Kbar.
2) perform a vc-relax calculation with optimized lattice parameters and atomic positions with the pressure that we are interested. ( 10 Kbar = 1 GPa ) ( press = 150 for 15 GPa)
3) Perform SCF calculation with optimized parameters after pressure is implied. ( pw.x )
3) perform bands calculation for band structure with respective high-symmetry points. ( G-M-K-G-A-L-H-A)
4) perform another calculation for getting plotable band structure data. ( bands.x )
5) perform phonon calculation:
 i) ph.x calculation can be performed to compute the dynamical matrix.
 ii) q2r.x calculation uses these dynamical matrices and Fourier transforms them and creates a file with Interatomic Force Constants (IFC) in real space.
iii) matdyn.x uses IFC as input and produces phonon modes and frequencies at within given high-symmetry path.
   note: tr2_ph should be considered carefully.
6) electron-phonon interaction can be calculated by including electron-phonon='interpolated' in elph.in file. But, we first need to calculate a scf calculation for a dense K-point grid with la2f = .true., followed by a normal scf with normal K points. Then run elph.in file with ph.x for calculating electron-phonon calculations. We include the file name in fildvscf where first-order variation of potential will be stored and we use several values for Gaussian broadening values in el_ph_sigma.
i) We then compute q2r.in, matdyn.in, and lambda.x to get phonon bands, Eliashberg spectral function,  E-P coefficients and an estimate of superconducting critical temperature with Allen-dynes modified Mc-Millan formula for superconducting critical temperature. These calculations are so heavy and I do not have access to HPC with lots of nodes, so I have only included here calculations with normal K-mesh and small q-grid.
