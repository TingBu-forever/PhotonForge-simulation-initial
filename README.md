# PhotonForge-simulation-startup
The note is to created to have quick access to photonforge simulation for new leaners. The materials below are from the user guides and my experience.

## 1: Installation
1) install Tidy3D, and run an example provided in the [website](https://docs.flexcompute.com/projects/tidy3d/en/latest/)
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
Specifically, we can define our own ports specs by 
```
xxx=pf.PortSpec("XXXX", width=x,limits=[x,x],num_modes=x,target_neff=x,path_profiles={})
#the path profiles contain the (width, offset,layer) for the cladding and core.
````
1) Add a port
   ```
   port0 = pf.Port(center=(0, 0), input_direction=0, spec="Slot")
   #"Slot" can be changed to the name of your customized name like slot, slot= pf.PortSpec(.....);
   #input_direction: the input direction of the light entering the system
   # Set the port name to "P0"
   connection.add_port(port0, "P0")
   ```
2) Auto-detection of ports
   ```
   detected_ports = connection.detect_ports(["Slot"])
   detected_ports
   connection.add_port(detected_ports[0], "P1")
   ```
### Load components
   1) load the componnet from PDK:
      ```
      pf.config.default_technology = siepic.ebeam()
      siepic.component_names# check all the components name
      the_component=siepic.component("the_name_of_component")

###  Custom Parametric Components
It is useful to change the internally-used instances by using "update"function in the customized parametric components
#### the angle setting for path.arc 
the plot are different when the second angle are set to -90 and 270 degree.
When it is -90:
```
path=pf.Path((0, 0), 0.5)
path.arc(0, -90, 5, euler_fraction=0.5)
```

<img width="150" alt="Screenshot 2025-03-28 at 3 48 49 PM" src="https://github.com/user-attachments/assets/dd4c5840-3c16-40f8-8cdd-5d786bcd2154" />

```
when it is 270:
path=pf.Path((0, 0), 0.5)
path.arc(0, 270, 5, euler_fraction=0.5)
```

<img width="150" alt="Screenshot 2025-03-28 at 3 49 04 PM" src="https://github.com/user-attachments/assets/0d929193-43fe-4033-bde7-cdc0867eeaac" />




