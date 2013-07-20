amberff
=======

These module files provide parameter sets for the popular 
Amber force fields as Python modules. See the original references, 
linked below, for an explanation of these paramters. 

How to use these modules
========================

Each module contains four dictionaries: 
* Atoms
* Bonds
* Torsions
* VdWs  

The dictionary **keys** correspond to the identifiers used in the reference 
paramter files. This amounts to the atom type, or the hyphen-separated
atom types for angles and torsions. Spaces are removed.  


Here are a few lines from parm94.dat,
for example:

    BR 79.90                !            bromine
    C  12.01                             sp2 C carbonyl group
    ...
    C -CA  469.0    1.409       JCC,7,(1986),230; TYR
    C -CB  447.0    1.419       JCC,7,(1986),230; GUA
    ...
    CB-C -NA    70.0      111.30    NA
    CB-C -O     80.0      128.80
    ...
    X -C -CA-X    4   14.50        180.0             2.         intrpol.bsd.on C6H6
    X -C -CB-X    4   12.00        180.0             2.         intrpol.bsd.on C6H6

Each **value** in the dictionary is a *namedtuple* with fields for each type of
parameter associated with the entity.  

Atoms:    mass, comment
Bonds:    k, r0, comment
Angle:    k, theta0, comment
Torsion:  bondpaths, Vn2, gamma, period, comment
Improper: Vn2, gamma, period, comment
Vdw:      R, epsilon, comment



Import the module into your code.

    >>> import amber94params 

    >>> mycarbon = gaffparams.Atoms['C']
    >>> mycarbon.mass
    12.01
    >>> mycarbon.comment
    'Sp2 C carbonyl group' 

    >>> c_ca_bond = amber94params.Bonds['C-CA']
    >>> c_ca_bond.k 
    469.0 
    >>> c_ca_bond.r0
    1.409

    >>> x_c_ca_x = amber94params.Torsions['X-C-CA-X']
    >>> x_c_ca_x.gamma
    180.0


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


