## How to implemenet new archteypes 

The following text describes the integration of Archetypes into TEASER exmaplary based on the IWU [https://github.com/IWUGERMANY/Nichtwohngebaeude-Typologie-Deutschland](IWU Typologie der Nichtwohngebäude in Deutschland ) (IWU). 

1. Create a folder in [teaser\logic\archetypebuildings](archetypebuildings) with the name of the typology, e.g. iwu. For each of the Archetype building categories create a python file, e.g.: "oad.py". 

2. Set up the respective file. Copy paste the import for Non-Residential: 

´import math
import collections
from teaser.logic.archetypebuildings.nonresidential import NonResidential
from teaser.logic.buildingobjects.useconditions import UseConditions as UseCond
from teaser.logic.buildingobjects.buildingphysics.ceiling import Ceiling
from teaser.logic.buildingobjects.buildingphysics.floor import Floor
from teaser.logic.buildingobjects.buildingphysics.groundfloor import GroundFloor
from teaser.logic.buildingobjects.buildingphysics.innerwall import InnerWall
from teaser.logic.buildingobjects.buildingphysics.outerwall import OuterWall
from teaser.logic.buildingobjects.buildingphysics.rooftop import Rooftop
from teaser.logic.buildingobjects.buildingphysics.window import Window
from teaser.logic.buildingobjects.thermalzone import ThermalZone
´

for Residential: 

´from teaser.logic.archetypebuildings.residential import Residential
from teaser.logic.buildingobjects.useconditions import UseConditions as UseCond
from teaser.logic.buildingobjects.buildingphysics.ceiling import Ceiling
from teaser.logic.buildingobjects.buildingphysics.floor import Floor
from teaser.logic.buildingobjects.buildingphysics.groundfloor import GroundFloor
from teaser.logic.buildingobjects.buildingphysics.innerwall import InnerWall
from teaser.logic.buildingobjects.buildingphysics.outerwall import OuterWall
from teaser.logic.buildingobjects.buildingphysics.rooftop import Rooftop
from teaser.logic.buildingobjects.buildingphysics.window import Window
from teaser.logic.buildingobjects.thermalzone import ThermalZone
´

3. Create a class, that inherits from Residential or Non-Residential, e.g. Oad. 

4. Set the minimum attributes according to the parent class, e.g. year of construction. Are there any specialities/characteristics from the typology, that are not impelemented in the parent class? For example the layout or size of zones. 

5. Create an input data json in (teaser\data\input\inputdata)[Inputdata] and add the attributes that can be represented, e.g., Outerwall, Door, Window, Rooftop, InnerWall, Ceiling, Floor. See the examplary input for the IWU OAD: 

´ 
{
    "version": "",
    "OuterWall_[0, 1978]_iwu_oad": {
        "building_age_group": [
            0,
            1978
        ],
        "construction_type": "iwu_oad",
        "inner_radiation": 5.0,
        "inner_convection": 2.7,
        "outer_radiation": 5.0,
        "outer_convection": 20.0,
        "layer": {
            "0": {
                "thickness": 0.2,
                "material": {
                    "name": "lightweight_concrete_Vermiculit_1100",
                    "material_id": "570be3be-3a43-11e7-b769-2cd444b2e704"
                }
            }
            }
        },
    "GroundFloor_[0, 1978]_iwu_oad": {
        "building_age_group": [
            0,
            1978
        ],
        "construction_type": "iwu_oad",
        "inner_radiation": 5.0,
        "inner_convection": 1.7,
        "layer": {
            "0": {
                "thickness": 0.03,
                "material": {
                    "name": "oak_old",
                    "material_id": "25b5d680-3a43-11e7-ba46-2cd444b2e704"
                }
            }
        }
    },
    "Window_[0, 1978]_iwu_oad": {
        "building_age_group": [
            0, 
            1978
        ],
        "construction_type": "iwu_oad",
        "inner_radiation": 5.0,
        "inner_convection": 2.7,
        "outer_radiation": 5.0,
        "outer_convection": 20.0,
        "g_value": 0.6,
        "a_conv": 0.02,
        "shading_g_total": 1.0,
        "shading_max_irr": 100.0,
        "layer": {
            "0": {
                "thickness": 0.5617090909090908,
                "material": {
                    "name": "glas_generic",
                    "material_id": "0abbb19a-83ff-11e6-bacd-2cd444b2e704"
                }
            }
        }
    }
}
´


6. Get Material data, based on the U-values. For this go to: https://www.ubakus.de/ and add layers to the respective input data. Add the respective materials to "teaser\data\input\inputdata\MaterialTemplates.json" 

7. Get 