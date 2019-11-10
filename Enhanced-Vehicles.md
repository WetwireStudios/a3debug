[Home](readme.md)
### Choose what vehicle to use

> Hummingbird - B_Heli_Light_01_F
> 
> Pawnee - B_Heli_Light_01_armed_F
> 
> Blackfish Inf. - B_T_VTOL_01_infantry_F
> 
> Huron - B_Heli_Transport_03_F
> 
> Gorgon - B_APC_Wheeled_03_cannon_F
> 
> Blackfoot - B_Heli_Attack_01_F
> 
> Marshall - B_APC_Wheeled_01_cannon_F
> 
> Wipeout - B_Plane_CAS_01_F

### Script : Replace 'B_Heli_Light_01_armed_F' with your desired vehicle classname

```sqf
vehx  =  'B_Heli_Light_01_armed_F' createvehicle (screenToWorld [0.0,0.5]); 

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
