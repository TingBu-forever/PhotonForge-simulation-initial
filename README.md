# PhotonForge-simulation-startup

## 1: Installation
1) install Tidy3D, and run an example in  https://docs.flexcompute.com/projects/tidy3d/en/latest/
2) install
   '''ruby
   pip install "photonforge[live_viewer]"
   '''
5) install some PDKs [**pip install siepic-forge**] and [**pip install luxtelligence-lnoi400-forge**]

## 2: Tips from the tuitorials:
1) Check the parameters in a specific PDK that can be changed Take siepic_forge as an example. Type [**siepic_forge.ebeam?**] will return the parameters.
2) The definition of the inported PDK, Given **pf.config.default_technology=siepic_forge.ebeam()**, we can look at its defitions for layers/ extrusion specs/ ports/ background medium by **pf.config.default_technology.layers**...
