# PhotonForge-simulation-startup

## 1: Installation
1) install Tidy3D, and run an example provided in the (website)[https://docs.flexcompute.com/projects/tidy3d/en/latest/]
2) 
   ```
   pip install "photonforge[live_viewer]"
   ```
5) install some PDKs like
   ```
   pip install siepic-forge
   ```
   and
   ```
   pip install luxtelligence-lnoi400-forge
   ```

## 2: Tips from the tuitorials:
### Process Design Kit(PDK)
1) Check the parameters in a specific PDK that can be changed Take siepic_forge as an example. Type ```siepic_forge.ebeam? ``` will return the parameters.
2) The definition of the inported PDK, Given ```pf.config.default_technology=siepic_forge.ebeam()```, we can look at its defitions for layers/ extrusion specs/ ports/ background medium by ```pf.config.default_technology.layers```.etc.
3) Let ```tech=siepic.ebeam()``` and ```pf.config.default_technology=tech```. We can
      a) create the component by definding a ```shape ``` and use the codes ```component=pf.Component(name="xxx")```, ```component.add(###layer_name or layer_number###,shape)```
      b) the color of the layer can be changed by ```tech.layers[###the_layer###].color="#XXXXXXXX"``` with 8 hex digits.
      c) add a layer by defining its layer number, description, color and patter, ```new_layer=pf.LayerSpec(layer=(X,X),description="XXXX",color=(204,255,204,1),pattern="XX")``` and ```tech.addlayer("###your layer name###",new_layer)```. Delete the layer by ```tech.remove_layer("###your layer name###")```
### Ports
Similar to the PDK, we can check the ports by ```tech.ports```. Check the [link](https://docs.flexcompute.com/projects/photonforge/en/latest/_autosummary/photonforge.PortSpec.html#photonforge.PortSpec.polarization) for more information of the parameters for the port.
   
