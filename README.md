# LatticeEftData
Generated finite-volume spectrum, matrix elements, and fitted scattering amplitude for Lattice EFT for project in ArXiv:2602.20373

Contains a json and txt file, calculations for fixed mass (M=50) and various box sizes (L^3) and couplings (c).
Errors are includes with mean values as quantity = mean value (error)
All parametrizations for scattering amplitude are using ERE -> pcotd = a + b * p2,
  provided with a,b with error
boosts used are  (0,0,0), (0,0,1), (1,1,0), (1,1,1)
Format:
1. first section is calq, which contains single L,c,boost data for analysis
calq (calculated spectrum input) {
  Lattice siz(int) {
    coupling (float) {
      boost (tuple) {
        p2 (float): c.o.m. momentum from finite volume spectrum
        p2_QC (float): c.o.m. momentum from parametrization for scattering amplitude using Lüscher [actual input to formalism]
        Ecm (float): c.o.m. energy from p2_QC
        Elab (float): lab frame energy from Ecm
        Pvec (tuple): 2pi/L times the boost
        Pmu (4-vector): Elab with the Pvec 
        LL (float): Lellouch-Lüscher factor using parametrization }
      }
    }
2. Results
Results contains the formalism-specific calculation going from
boost a -> boost b
where we fix boost a to be (0,0,0)
Format:
Errors included as pm on the mean value, ie quantity= mean value +- error
All quantities done for the mu=0 (timelike) component.
All quantities have be redefined to absort bare scattering amplitude dependence
Result for L=latt_size, c=coupling
{ boost_a :
  { boost_b:
    {
       A_22 (float): short-distance function obtained by combining matrix element with LL factor and triangle function inputs.
       G_inf_scalar (complex): infinite-volume scalar G factor depending on P_i^mu, P_f^mu
       G_inf_vector (complex):  infinite-volume scalar G factor depending on P_i^mu, P_f^mu
       G_scalar (complex): finite-volume scalar G factor depending on P_i^mu, P_f^mu, L
       G_vector (complex): finite-volume mu=0 G factor depending on P_i^mu, P_f^mu, L
       ME (float): finite-volume matrix element
       Q2 (float): Q^2 = - (P_f - P_i)^2
       W_Ldf (float): intermediate value of calculation, ME/ LL_factor_i*LL_factor_f
       W_df (float): intermediate value of calculation, W_Ldf with finite-volume G function contribution subtracted
3. Fit Parameters
Results for fitting parametrization of phase shift data using the finite-volume spectrum with Lüscher,
using data for coupling with three different lattice sizes (6,8,10) for a simulataneous fit
with each boost considered.
Format:
*Note: fir parameters for same coupling, different lattice size are identical
** parametrization: a + b * q^2
Fit parameters for L=latt_size, c=coupling
[ a pm error, b pm error ]

