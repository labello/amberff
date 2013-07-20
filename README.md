amberff
=======

These module files provide the complete parameters sets for the popular 
Amber force fields as Python modules.

How to use these modules
========================

Import the module into your code.

    >>> import gaffparams

Access the parameters of an atom, bond, torsion or non-bonded atom.

    >>> gaffparams.Atoms
    >>> mycarbon = gaffparams.Atoms['c']
    >>> mycarbon.mass
    12.01
    >>> mycarbon.comment
    'Sp2 C carbonyl group' 

    >>> carbon_oxygen_bond = gaffparams.Bonds['c-o']
    >>> carbon_oxygen_bond.k
    648.0
    >>> carbon_oxygen_bond.r0
    1.214


AMBER94
-------

*A Second Generation Force Field for the Simulation of Proteins, Nucleic Acids,
and Organic Molecules*
http://ffamber.cnsm.csulb.edu/pdfs/cornell_amber94_1995jacs.pdf

GAFF
----

*Development and Testing of a General Amber Force Field*
http://ambermd.org/antechamber/gaff.pdf

About Amber parameters and units
--------------------------------

**Atoms**

* Mass of atoms (mass) is recorded in Atomic Mass Units

**Bonds**

* The bond stretch force constant (k) is stored in kcal/(mol * A^2)
* The idealized bond length (r0) is in Angstroms

**Angles**

* The angle force constant (k) is stored in kcal/(mol * radian^2)
* The idealized angle (theta0) is stored in degrees

**Torsions**

* The torsion bond path (bondpaths) parameter is the number of bond paths that the total
  Vn/2 is dividied into.  This is equal to the product of the number of bonds
  leading into the middle two atoms.  For example, since X-C-CA-X has 4 bond
  paths, each of them has a Vn/2 of 14.5/4 kcal/mol assigned to it

* The magnitude of the torsion, Vn/2 (stored as Vn2) is in kcal/mol

* (gamma) is the ideal phase offset of the torsion in degrees

* (period) is the periodicity of the torsion

**VdW**

* (R) is the Van der Waals radius for the given atom in Angstroms.
  The value used in eq 1 for an interaction of atom i and atom j
  is Rij* = Ri* + Rj*

* Epsilon (epsilon) is the Van der Waals well depth in kcal/mol


