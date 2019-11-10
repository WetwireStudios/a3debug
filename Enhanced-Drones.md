### Choose what vehicle to use ("veh")

> MQ-12 FALCON - 'B_T_UAV_03_F' 
> 
> UGV RCWS STOMPER - 'B_UGV_01_rcws_F' 
> 
> AR-2 DARTER - 'B_UAV_01_F' 

### Script : Replace 'B_UGV_01_rcws_F' with your desired vehicle classname

```sqf
vehx  =  'B_UGV_01_rcws_F' createvehicle (screenToWorld [0.0,0.5]);

  

_crewman  = (group player) createUnit ["B_UAV_AI",position vehicle player,[],0,"CAN_COLLIDE"];

[_crewman] joinSilent creategroup west;

[_crewman] joinSilent (group player);

_crewman moveInAny  vehx;

  

_crewman  = (group player) createUnit ["B_UAV_AI",position vehicle player,[],0,"CAN_COLLIDE"];

[_crewman] joinSilent creategroup west;

[_crewman] joinSilent (group player);

_crewman moveInAny  vehx;

  

_x  = 0;

for  "_x" from  -1 to 2 do {

vehx  addWeaponTurret ['cannon_125mm', [_x]];

vehx  addMagazineTurret ["12Rnd_125mm_HE_T_Green", [_x]];

vehx  addMagazineTurret ["12Rnd_125mm_HEAT_T_Red", [_x]];

vehx  addMagazineTurret ["24Rnd_125mm_APFSDS", [_x]];

vehx  addWeaponTurret ['cannon_125mm', [_x]];

vehx  addMagazineTurret ["Laserbatteries", [_x]];

vehx  addWeaponTurret ['Laserdesignator_mounted', [_x]];

vehx  addWeaponTurret ["missiles_SCALPEL",[_x]];

vehx  addMagazineTurret ["8Rnd_LG_scalpel",[_x]];

vehx  addMagazineTurret ["8Rnd_LG_scalpel",[_x]];

vehx  addMagazineTurret ["8Rnd_LG_scalpel",[_x]];

vehx  addMagazineTurret ["8Rnd_LG_scalpel",[_x]];

vehx  addMagazineTurret ["8Rnd_LG_scalpel",[_x]];

vehx  addMagazineTurret ["8Rnd_LG_scalpel",[_x]];

vehx  addMagazineTurret ["8Rnd_LG_scalpel",[_x]];

vehx  addMagazineTurret ["8Rnd_LG_scalpel",[_x]];

vehx  addWeaponTurret ["Gatling_30mm_Plane_CAS_01_F",[_x]];

vehx  addMagazineTurret ["1000Rnd_Gatling_30mm_Plane_CAS_01_F",[_x]];

vehx  addMagazineTurret ["1000Rnd_Gatling_30mm_Plane_CAS_01_F",[_x]];

vehx  addMagazineTurret ["1000Rnd_Gatling_30mm_Plane_CAS_01_F",[_x]];

vehx  addMagazineTurret ["1000Rnd_Gatling_30mm_Plane_CAS_01_F",[_x]];

vehx  addMagazineTurret ["1000Rnd_Gatling_30mm_Plane_CAS_01_F",[_x]];

vehx  addWeaponTurret ["autocannon_40mm_CTWS",[_x]];

vehx  addMagazineTurret ["60Rnd_40mm_GPR_shells",[_x]];

vehx  addMagazineTurret ["40Rnd_40mm_APFSDS_shells",[_x]];

vehx  addMagazineTurret ["60Rnd_40mm_GPR_shells",[_x]];

vehx  addMagazineTurret ["40Rnd_40mm_APFSDS_shells",[_x]];

vehx  addMagazineTurret ["60Rnd_40mm_GPR_shells",[_x]];

vehx  addMagazineTurret ["40Rnd_40mm_APFSDS_shells",[_x]];

vehx  addWeaponTurret ["autocannon_30mm_RCWS",[_x]];

vehx  addMagazineTurret ["60Rnd_30mm_MP_shells_Tracer_Green",[_x]];

vehx  addMagazineTurret ["60Rnd_30mm_MP_shells_Tracer_Green",[_x]];

vehx  addMagazineTurret ["60Rnd_30mm_MP_shells_Tracer_Green",[_x]];

vehx  addWeaponTurret ["missiles_titan",[_x]];

vehx  addMagazineTurret ["5Rnd_GAT_missiles",[_x]];

vehx  addMagazineTurret ["4Rnd_GAA_missiles",[_x]];

vehx  addMagazineTurret ["4Rnd_Titan_long_missiles",[_x]];

vehx  addMagazineTurret ["5Rnd_GAT_missiles",[_x]];

vehx  addMagazineTurret ["4Rnd_GAA_missiles",[_x]];

vehx  addMagazineTurret ["4Rnd_Titan_long_missiles",[_x]];

vehx  addMagazineTurret ["5Rnd_GAT_missiles",[_x]];

vehx  addMagazineTurret ["4Rnd_GAA_missiles",[_x]];

vehx  addMagazineTurret ["4Rnd_Titan_long_missiles",[_x]];

vehx  addMagazineTurret ["magazine_Missile_rim116_x21", [_x]];

vehx  addMagazineTurret ["magazine_Missile_rim162_x8", [_x]];

vehx  addMagazineTurret ["magazine_Missile_rim162_x8", [_x]];

vehx  addMagazineTurret ["magazine_Missile_rim116_x21", [_x]];

vehx  addMagazineTurret ["magazine_Missile_rim162_x8", [_x]];

vehx  addMagazineTurret ["magazine_Missile_rim162_x8", [_x]];

vehx  addMagazineTurret ["magazine_Missile_rim116_x21", [_x]];

vehx  addMagazineTurret ["magazine_Missile_rim162_x8", [_x]];

vehx  addMagazineTurret ["magazine_Missile_rim162_x8", [_x]];

vehx  addWeaponTurret ['weapon_rim116Launcher', [_x]];

vehx  addWeaponTurret ['weapon_rim162Launcher', [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [_x]];

vehx  addWeaponTurret ['weapon_Cannon_Phalanx', [_x]];

};
```
