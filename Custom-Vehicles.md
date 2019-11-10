## Vehicle Inits
### These can be run on cursorObject, when pointing @ the first vehicle (the vehicle to be attached to)
#### Pawnee w/ Black Wasp
```sqf
_blackwasp = createVehicle ["B_Plane_Fighter_01_F",getPosATL cursorObject,[],0,"GROUND"]; 
_blackwasp attachTo [cursorObject, [0,0,-1.79]];
```
#### A-164 Wipeout w/ Raised Mk30 HMG .50 & Mk32 GMG 20 mm (on wings)
```sqf
_gmg = createVehicle ["B_GMG_01_high_F",getPosATL player,[],0,"GROUND"]; 
_gmg attachTo [cursorObject, [4.3,0,1.6]];_hmg = createVehicle ["B_HMG_01_high_F",getPosATL player,[],0,"GROUND"]; 
_hmg attachTo [cursorObject, [-3.9,0.15,1.6]];
```
#### Quad Bike w/ Mk30 HMG .50:
```sqf
_turret = createVehicle ["B_HMG_01_F",getPosATL cursorObject,[],0,"GROUND"]; 
_turret attachTo [cursorObject, [0.1,0,0.6]];
```
#### Quad Bike w/ Mk32 GMG 20 mm: 
```sqf
_turret = createVehicle ["B_GMG_01_F",getPosATL cursorObject,[],0,"GROUND"]; 
_turret attachTo [cursorObject, [0.1,0,0.6]];
```
#### Offroad w/ Mortar: 
```sqf
_mortar = createVehicle ["B_T_Mortar_01_F",getPosATL cursorObject,[],0,"GROUND"]; 
_mortar attachTo [cursorObject, [0,-2,0]];
```
#### Offroad w/ Mk30 HMG .50 (Raised): 
```sqf
_hmgturret = createVehicle ["B_HMG_01_high_F",getPosATL player,[],0,"GROUND"]; 
_hmgturret attachTo [cursorObject, [0.2,-2,1]];
```
#### Offroad w/ Mk32 GMG 20 mm (Raised): 
```sqf
_gmgturret = createVehicle ["B_GMG_01_high_F",getPosATL player,[],0,"GROUND"]; 
_gmgturret attachTo [cursorObject, [0.2,-2,1]];
```
#### Hunter w/ Static Titan Launcher (AT): 
```sqf
_titanAT = createVehicle ["B_static_AT_F",getPosATL player,[],0,"GROUND"]; 
_titanAT attachTo [cursorObject, [0,-2.65,1.6]];
```
#### Hunter w/ Static Titan Launcher (AA): 
```sqf
_titanAA = createVehicle ["B_static_AA_F",getPosATL player,[],0,"GROUND"]; 
_titanAA attachTo [cursorObject, [0,-2.65,1.6]];
```
#### RHIB Boat w/ Mk30 HMG .50 (Raised): 
```sqf
_hmg = createVehicle ["B_HMG_01_high_F",getPosATL player,[],0,"GROUND"]; 
_hmg attachTo [cursorObject, [0.25,1.5,1]];
```
#### RHIB Boat w/ Mk32 GMG 20 mm (Raised): 
```sqf
_gmg = createVehicle ["B_GMG_01_high_F",getPosATL player,[],0,"GROUND"]; 
_gmg attachTo [cursorObject, [0.25,1.5,1]];
```
 
