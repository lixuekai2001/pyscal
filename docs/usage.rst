Usage
=====

Pyscal is meant to be used directly by end users by its Python
API. Additionally there are end-user scripts where parameter
collection are inputted through Excel worksheets.

Basic example
-------------

To generate SWOF input for Eclipse or flow (OPM) with certain
saturation endpoints and certain relative permeability endpoints, you
may run the following code:

.. code-block:: python

    from pyscal import WaterOil
    wo = WaterOil(swl=0.05, sorw=0.03, h=0.1)
    wo.add_corey_water(nw=2.1, krwend=0.6)
    wo.add_corey_oil(now=2.5, kroend=0.9)
    wo.add_simple_J()
    print(wo.SWOF())

which will print a table that can be included in an Eclipse
simulation. There are more parameters to adjust, check the
corresponding API. Instead of corey, you can find a corresponding
function for a LET-parametrization, or perhaps another capillary
pressure function. Also adjust the parameter ``h`` to obtain a finer
resolution on the saturation scale.

The output from the code above:

.. code-block:: console

    SWOF
    --
    -- Sw Krw Krow Pc
    -- swirr=0 swl=0.05 swcr=0.05 sorw=0.03
    -- Corey krw, nw=2.1, krwend=0.6, krwmax=1
    -- Corey krow, now=2.5, kroend=0.9, kromax=1
    -- krw = krow @ sw=0.52365
    -- Simplified J function for Pc;
    --   a=5, b=-1.5, poro_ref=0.25, perm_ref=100 mD, drho=300 kg/m³, g=9.81 m/s²
    0.0500000 0.0000000 0.9000000 0.6580748
    0.1500000 0.0056780 0.6750059 0.1266466
    0.2500000 0.0243422 0.4876455 0.0588600
    0.3500000 0.0570363 0.3355461 0.0355327
    0.4500000 0.1043573 0.2161630 0.0243731
    0.5500000 0.1667377 0.1267349 0.0180379
    0.6500000 0.2445200 0.0642167 0.0140398
    0.7500000 0.3379891 0.0251669 0.0113276
    0.8500000 0.4473895 0.0055300 0.0093886
    0.9500000 0.5729360 0.0000627 0.0079459
    0.9700000 0.6000000 0.0000000 0.0077015
    1.0000000 1.0000000 0.0000000 0.0073575
    /


Instead of ``SWOF()``, you may ask for ``SWFN()`` or similar. Both
family 1 and 2 of Eclipse keywords are supported.  For the Nexus
simulator, you can use the function ``WOTABLE()``