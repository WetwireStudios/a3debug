[Home](readme.md)
# Table of Contents
- [Preface](#weapons)
    + [Syntax](#syntax-)
    + [Vehicle Seat Index](#vehicle-seat-index-)
- [Weapons](#weapons-1)
    + [MG/HMGs](#mg-hmgs)
    + [Dumb Fire Rockets](#dumb-fire-rockets)
    + [Explosives](#explosives)
    + [Large HE Guns / Cannons (Sorted by Caliber)](#large-he-guns---cannons--sorted-by-caliber-)
    + [AG or LG Rockets](#ag-or-lg-rockets)
    + [Bombs](#bombs)
    + [Anti-Air Missiles](#anti-air-missiles)
    + [Special](#special)

## Preface

**Used to add weapons to VEHICLES**
### Syntax:
addWeaponTurret Syntax
> vehicle addWeaponTurret [weaponName, turretPath]


removeWeaponTurret Syntax
> vehicle removeWeaponTurret [weaponName, turretPath]

addMagazineTurret Syntax
> vehicle addMagazineTurret [magazineName, turretPath, ammoCount]

removeMagazinesTurret Syntax
> vehicle removeMagazinesTurret [magazineName, turretPath]
### Vehicle Seat Index (turretPath):
> Driver or Pilot: -1

> Gunner: 0

> Commander or LeftGunner: 1

> RightGunner: 2

#### Example:
This example is intended for use on the AH-9 Pawnee. The standard armaments have been replaced with an array of weapons unlike that of a CAS plane.
```sqf
cursorObject removeWeaponTurret ["M134_minigun", [-1]];
cursorObject removeWeaponTurret ["missiles_DAR", [-1]];
cursorObject addWeaponTurret ["gatling_20mm_VTOL_01", [-1]];
cursorObject addMagazineTurret ["4000Rnd_20mm_Tracer_Red_shells", [-1]];
cursorObject addWeaponTurret ["missiles_DAGR", [-1]];
cursorObject addMagazineTurret ["24Rnd_PG_missiles", [-1]];
cursorObject addWeaponTurret ["Rocket_04_AP_Plane_CAS_01_F", [-1]];
cursorObject addMagazineTurret ["7Rnd_Rocket_04_AP_F", [-1]];
```

Usage:

The object you use these on must be a vehicle.
You can use the following for different situations:

> this (object selected by zeus)

> cursorObject (object player is aimed at)

> vehicle player (vehicle player is in)

## Weapons
#### Examples are in cursorObject and are pointed at the DRIVER.

### MG/HMGs
##### RCWS LMG 6.5 mm
```sqf
cursorObject addWeaponTurret ["LMG_RCWS", [-1]];
cursorObject addWeaponTurret ["LMG_65mm_body", [-1]];
cursorObject addMagazineTurret ["200Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["500Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["1000Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["2000Rnd_65x39_Belt", [-1]];
```
##### M200 LMG 6.5 mm
```sqf
cursorObject addWeaponTurret ["LMG_M200", [-1]];
cursorObject addWeaponTurret ["LMG_M200_body", [-1]];
cursorObject addMagazineTurret ["200Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["500Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["1000Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["2000Rnd_65x39_Belt", [-1]];
```
##### Minigun 6.5 mm
```sqf
cursorObject addWeaponTurret ["LMG_Minigun", [-1]];
cursorObject addWeaponTurret ["LMG_Minigun_heli", [-1]];
cursorObject addMagazineTurret ["200Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["500Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["1000Rnd_65x39_Belt", [-1]];
cursorObject addMagazineTurret ["2000Rnd_65x39_Belt", [-1]];
```
##### RCWS HMG 12.7 mm
```sqf
cursorObject addWeaponTurret ["HMG_127", [-1]];
cursorObject addWeaponTurret ["HMG_127_APC", [-1]];
cursorObject addWeaponTurret ["HMG_127_UGV", [-1]];
cursorObject addWeaponTurret ["HMG_01", [-1]];
cursorObject addWeaponTurret ["HMG_static", [-1]];
cursorObject addMagazineTurret ["200Rnd_127x99_mag", [-1]];
cursorObject addMagazineTurret ["500Rnd_127x99_mag", [-1]];
```
##### Tandem M134 Minigun 7.62 mm
```sqf
cursorObject addWeaponTurret ["M134_minigun", [-1]];
cursorObject addMagazineTurret ["5000Rnd_762x51_Belt", [-1]];
cursorObject addMagazineTurret ["5000Rnd_762x51_Yellow_Belt", [-1]];
```
##### Coaxial MG 7.62 mm
```sqf
cursorObject addWeaponTurret ["LMG_coax", [-1]];
cursorObject addMagazineTurret ["200Rnd_762x51_Belt", [-1]];
cursorObject addMagazineTurret ["1000Rnd_762x51_Belt", [-1]];
cursorObject addMagazineTurret ["2000Rnd_762x51_Belt", [-1]];
```
##### RCWS HMG 12.7 mm
```sqf
cursorObject addWeaponTurret ["HMG_127_MBT", [-1]];
cursorObject addMagazineTurret ["200Rnd_127x99_mag", [-1]];
cursorObject addMagazineTurret ["500Rnd_127x99_mag", [-1]];
```
##### Mk30 HMG .50
```sqf
cursorObject addWeaponTurret ["HMG_127_LSV_01", [-1]];
cursorObject addMagazineTurret ["100Rnd_127x99_mag", [-1]];
cursorObject addMagazineTurret ["200Rnd_127x99_mag", [-1]];
cursorObject addMagazineTurret ["500Rnd_127x99_mag", [-1]];
```
##### SPMG .338
```sqf
cursorObject addWeaponTurret ["MMG_02_vehicle", [-1]];
cursorObject addMagazineTurret ["130Rnd_338_Mag", [-1]];
```
##### M61 Minigun 20 mm
```sqf
cursorObject addWeaponTurret ["weapon_Fighter_Gun20mm_AA", [-1]];
cursorObject addMagazineTurret ["magazine_Fighter04_Gun20mm_AA_x150", [-1]];
cursorObject addMagazineTurret ["magazine_Fighter04_Gun20mm_AA_x250", [-1]];
cursorObject addMagazineTurret ["magazine_Fighter01_Gun20mm_AA_x450", [-1]];
```

### Dumb Fire Rockets
##### (DAR) Direct Attack Rocket
```sqf
cursorObject addWeaponTurret ["missiles_DAR", [-1]];
cursorObject addMagazineTurret ["12Rnd_missiles", [-1]];
cursorObject addMagazineTurret ["24Rnd_missiles", [-1]];
cursorObject addMagazineTurret ["PylonRack_12Rnd_missiles", [-1]];
```
##### Skyfire Rockets
```sqf
cursorObject addWeaponTurret ["rockets_Skyfire", [-1]];
cursorObject addMagazineTurret ["14Rnd_80mm_rockets", [-1]];
cursorObject addMagazineTurret ["38Rnd_80mm_rockets", [-1]];
cursorObject addMagazineTurret ["PylonRack_19Rnd_Rocket_Skyfire", [-1]];
```
##### Shrieker HE
```sqf
cursorObject addWeaponTurret ["Rocket_04_HE_Plane_CAS_01_F", [-1]];
cursorObject addMagazineTurret ["7Rnd_Rocket_04_HE_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_7Rnd_Rocket_04_HE_F", [-1]];
```
##### Shrieker AP
```sqf
cursorObject addWeaponTurret ["Rocket_04_AP_Plane_CAS_01_F", [-1]];
cursorObject addMagazineTurret ["7Rnd_Rocket_04_AP_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_7Rnd_Rocket_04_AP_F", [-1]];
```
##### Tratnyr HE
```sqf
cursorObject addWeaponTurret ["Rocket_03_HE_Plane_CAS_02_F", [-1]];
cursorObject addMagazineTurret ["20Rnd_Rocket_03_HE_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_20Rnd_Rocket_03_HE_F", [-1]];
```
##### Tratnyr AP
```sqf
cursorObject addWeaponTurret ["Rocket_03_AP_Plane_CAS_02_F", [-1]];
cursorObject addMagazineTurret ["20Rnd_Rocket_03_AP_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_20Rnd_Rocket_03_AP_F", [-1]];
```

### Explosives
##### Mortar 82 mm
```sqf
cursorObject addWeaponTurret ["mortar_82mm", [-1]];
cursorObject addMagazineTurret ["8Rnd_82mm_Mo_shells", [-1]];
cursorObject addMagazineTurret ["8Rnd_82mm_Mo_LG", [-1]];
cursorObject addMagazineTurret ["8Rnd_82mm_Mo_guided", [-1]];
cursorObject addMagazineTurret ["8Rnd_82mm_Mo_Smoke_white", [-1]];
cursorObject addMagazineTurret ["8Rnd_82mm_Mo_Flare_white", [-1]];
```
##### Howitzer 155 mm
```sqf
cursorObject addWeaponTurret ["mortar_155mm_AMOS", [-1]];
cursorObject addMagazineTurret ["32Rnd_155mm_Mo_shells", [-1]];
cursorObject addMagazineTurret ["2Rnd_155mm_Mo_LG", [-1]];
cursorObject addMagazineTurret ["2Rnd_155mm_Mo_Cluster", [-1]];
cursorObject addMagazineTurret ["2Rnd_155mm_Mo_guided", [-1]];
cursorObject addMagazineTurret ["6Rnd_155mm_Mo_mine", [-1]];
cursorObject addMagazineTurret ["6Rnd_155mm_Mo_AT_mine", [-1]];
cursorObject addMagazineTurret ["6Rnd_155mm_Mo_smoke", [-1]];
```
##### (Sandstorm Missile) 230 mm Missile
```sqf
cursorObject addWeaponTurret ["rockets_230mm_GAT", [-1]];
cursorObject addMagazineTurret ["12Rnd_230mm_rockets", [-1]];
```
##### Minigun 20 mm
```sqf
cursorObject addWeaponTurret ["gatling_20mm", [-1]];
cursorObject addMagazineTurret ["300Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["1000Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["2000Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["PylonWeapon_300Rnd_20mm_shells", [-1]];
```
##### Cannon Caseless 30 mm
```sqf
cursorObject addWeaponTurret ["gatling_30mm", [-1]];
cursorObject addMagazineTurret ["250Rnd_30mm_HE_shells", [-1]];
cursorObject addMagazineTurret ["250Rnd_30mm_APDS_shells", [-1]];
```

### Large HE Guns / Cannons (Sorted by Caliber)
##### Cannon 125mm
```sqf
cursorObject addWeaponTurret ["cannon_125mm", [-1]];
cursorObject addMagazineTurret ["12Rnd_125mm_HE", [-1]];
cursorObject addMagazineTurret ["12Rnd_125mm_HEAT", [-1]];
cursorObject addMagazineTurret ["24Rnd_125mm_APFSDS", [-1]];
```
##### Cannon 120 mm
```sqf
cursorObject addWeaponTurret ["cannon_120mm", [-1]];
cursorObject addMagazineTurret ["32Rnd_120mm_APFSDS_shells", [-1]];
cursorObject addMagazineTurret ["30Rnd_120mm_HE_shells", [-1]];
```
##### Cannon 120 mm
```sqf
cursorObject addWeaponTurret ["cannon_120mm_long", [-1]];
cursorObject addMagazineTurret ["28Rnd_120mm_APFSDS_shells", [-1]];
cursorObject addMagazineTurret ["14Rnd_120mm_HE_shells", [-1]];
```
##### Cannon 105 mm
```sqf
cursorObject addWeaponTurret ["cannon_105mm_VTOL_01", [-1]];
cursorObject addMagazineTurret ["100Rnd_105mm_HEAT_MP", [-1]];
cursorObject addMagazineTurret ["20Rnd_105mm_HEAT_MP", [-1]];
cursorObject addMagazineTurret ["40Rnd_105mm_APFSDS", [-1]];
```
##### Cannon 105 mm
```sqf
cursorObject addWeaponTurret ["cannon_105mm", [-1]];
cursorObject addMagazineTurret ["20Rnd_105mm_HEAT_MP", [-1]];
cursorObject addMagazineTurret ["40Rnd_105mm_APFSDS", [-1]];
```
##### Cannon 40 mm
```sqf
cursorObject addWeaponTurret ["autocannon_40mm_VTOL_01", [-1]];
cursorObject addMagazineTurret ["240Rnd_40mm_GPR_Tracer_Red_shells", [-1]];
cursorObject addMagazineTurret ["160Rnd_40mm_APFSDS_Tracer_Red_shells", [-1]];
cursorObject addWeaponTurret ["autocannon_40mm_CTWS", [-1]];
cursorObject addMagazineTurret ["60Rnd_40mm_GPR_shells", [-1]];
cursorObject addMagazineTurret ["40Rnd_40mm_APFSDS_shells", [-1]];
```
##### Autocannon 35 mm
```sqf
cursorObject addWeaponTurret ["autocannon_35mm", [-1]];
cursorObject addMagazineTurret ["680Rnd_35mm_AA_shells", [-1]];
```
##### CTWS Cannon 30 mm
```sqf
cursorObject addWeaponTurret ["autocannon_30mm_CTWS", [-1]];
cursorObject addMagazineTurret ["60Rnd_30mm_APFSDS_shells", [-1]];
cursorObject addMagazineTurret ["140Rnd_30mm_MP_shells", [-1]];
```
##### Cannon 30 mm
```sqf
cursorObject addWeaponTurret ["autocannon_30mm", [-1]];
cursorObject addMagazineTurret ["140Rnd_30mm_MP_shells", [-1]];
cursorObject addMagazineTurret ["60Rnd_30mm_APFSDS_shells", [-1]];
```
##### (A-164's Main Cannon) Minigun 30 mm
```sqf
cursorObject addWeaponTurret ["Gatling_30mm_Plane_CAS_01_F", [-1]];
cursorObject addMagazineTurret ["1000Rnd_Gatling_30mm_Plane_CAS_01_F", [-1]];
```
##### Cannon 30 mm
```sqf
cursorObject addWeaponTurret ["Cannon_30mm_Plane_CAS_02_F", [-1]];
cursorObject addMagazineTurret ["500Rnd_Cannon_30mm_Plane_CAS_02_F", [-1]];
```
##### Cannon Caseless 30 mm
```sqf
cursorObject addWeaponTurret ["gatling_30mm_VTOL_02", [-1]];
cursorObject addMagazineTurret ["250Rnd_30mm_HE_shells", [-1]];
cursorObject addMagazineTurret ["250Rnd_30mm_APDS_shells", [-1]];
```
##### Gsh Cannon 30mm
```sqf
cursorObject addWeaponTurret ["weapon_Fighter_Gun_30mm", [-1]];
cursorObject addMagazineTurret ["magazine_Fighter02_Gun30mm_AA_x180", [-1]];
```
##### GAU-12 Cannon 25 mm
```sqf
cursorObject addWeaponTurret ["gatling_25mm", [-1]];
cursorObject addMagazineTurret ["300Rnd_25mm_shells", [-1]];
cursorObject addMagazineTurret ["1000Rnd_25mm_shells", [-1]];
```
##### Gatling Cannon 20mm
```sqf
cursorObject addWeaponTurret ["weapon_Cannon_Phalanx", [-1]];
cursorObject addMagazineTurret ["magazine_Cannon_Phalanx_x1550", [-1]];
```
##### Minigun 20 mm
```sqf
cursorObject addWeaponTurret ["gatling_20mm_VTOL_01", [-1]];
cursorObject addMagazineTurret ["300Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["1000Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["2000Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["4000Rnd_20mm_Tracer_Red_shells", [-1]];
```
##### Twin Cannon 20mm
```sqf
cursorObject addWeaponTurret ["Twin_Cannon_20mm", [-1]];
cursorObject addMagazineTurret ["300Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["1000Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["2000Rnd_20mm_shells", [-1]];
cursorObject addMagazineTurret ["PylonWeapon_300Rnd_20mm_shells", [-1]];
```

### AG or LG Rockets
##### (DAGR) Direct Attack Guided Rocket
```sqf
cursorObject addWeaponTurret ["missiles_DAGR", [-1]];
cursorObject addMagazineTurret ["12Rnd_PG_missiles", [-1]];
cursorObject addMagazineTurret ["24Rnd_PG_missiles", [-1]];
cursorObject addMagazineTurret ["PylonRack_12Rnd_PG_missiles", [-1]];
```
##### Skalpel ATGM
```sqf
cursorObject addWeaponTurret ["missiles_SCALPEL", [-1]];
cursorObject addMagazineTurret ["2Rnd_LG_scalpel", [-1]];
cursorObject addMagazineTurret ["6Rnd_LG_scalpel", [-1]];
cursorObject addMagazineTurret ["8Rnd_LG_scalpel", [-1]];
cursorObject addMagazineTurret ["PylonMissile_1Rnd_LG_scalpel", [-1]];
cursorObject addMagazineTurret ["PylonRack_4Rnd_LG_scalpel", [-1]];
```
##### Titan Missile
```sqf
cursorObject addWeaponTurret ["missiles_titan", [-1]];
cursorObject addMagazineTurret ["2Rnd_GAT_missiles", [-1]];
cursorObject addMagazineTurret ["5Rnd_GAT_missiles", [-1]];
cursorObject addMagazineTurret ["4Rnd_GAA_missiles", [-1]];
cursorObject addMagazineTurret ["4Rnd_Titan_long_missiles", [-1]];
```
##### Macer
```sqf
cursorObject addWeaponTurret ["Missile_AGM_02_Plane_CAS_01_F", [-1]];
cursorObject addMagazineTurret ["6Rnd_Missile_AGM_02_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_1Rnd_Missile_AGM_02_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_3Rnd_Missile_AGM_02_F", [-1]];
```
##### Sharur
```sqf
cursorObject addWeaponTurret ["Missile_AGM_01_Plane_CAS_02_F", [-1]];
cursorObject addMagazineTurret ["4Rnd_Missile_AGM_01_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_1Rnd_Missile_AGM_01_F", [-1]];
```
##### Jian
```sqf
cursorObject addWeaponTurret ["missiles_Jian", [-1]];
cursorObject addMagazineTurret ["4Rnd_LG_Jian", [-1]];
cursorObject addMagazineTurret ["PylonRack_1Rnd_Missile_Jian", [-1]];
```
##### Macer II
```sqf
cursorObject addWeaponTurret ["weapon_AGM_65Launcher", [-1]];
cursorObject addMagazineTurret ["magazine_Missile_AGM_02_x1", [-1]];
```
##### KH25 Kedge
```sqf
cursorObject addWeaponTurret ["weapon_AGM_KH25Launcher", [-1]];
cursorObject addMagazineTurret ["magazine_Missile_AGM_KH25_x1", [-1]];
```

### Bombs
##### GBU-12 1
```sqf
cursorObject addWeaponTurret ["GBU12BombLauncher", [-1]];
cursorObject addWeaponTurret ["GBU12BombLauncher_Plane_Fighter_03_F", [-1]];
cursorObject addMagazineTurret ["2Rnd_GBU12_LGB", [-1]];
cursorObject addMagazineTurret ["2Rnd_GBU12_LGB_MI10", [-1]];
```
##### GBU 12 2
```sqf
cursorObject addWeaponTurret ["weapon_GBU12Launcher", [-1]];
cursorObject addMagazineTurret ["magazine_Bomb_GBU12_x1", [-1]];
cursorObject addMagazineTurret ["PylonMissile_Bomb_GBU12_x1", [-1]];
cursorObject addMagazineTurret ["PylonRack_Bomb_GBU12_x2", [-1]];
```
##### GBU-12 3
```sqf
cursorObject addWeaponTurret ["Bomb_04_Plane_CAS_01_F", [-1]];
cursorObject addWeaponTurret ["4Rnd_Bomb_04_F", [-1]];
cursorObject addMagazineTurret ["PylonMissile_1Rnd_Bomb_04_F", [-1]];
```
##### Mk82
```sqf
cursorObject addWeaponTurret ["Mk82BombLauncher", [-1]];
cursorObject addMagazineTurret ["2Rnd_Mk82", [-1]];
cursorObject addMagazineTurret ["2Rnd_Mk82_MI08", [-1]];
cursorObject addMagazineTurret ["PylonMissile_1Rnd_Mk82_F", [-1]];
```
##### LOM-250G
```sqf
cursorObject addWeaponTurret ["Bomb_03_Plane_CAS_02_F", [-1]];
cursorObject addMagazineTurret ["2Rnd_Bomb_03_F", [-1]];
cursorObject addMagazineTurret ["PylonMissile_1Rnd_Bomb_03_F", [-1]];
```
##### KAB 250
```sqf
cursorObject addWeaponTurret ["weapon_KAB250Launcher", [-1]];
cursorObject addMagazineTurret ["magazine_Bomb_KAB250_x1", [-1]];
```

### Anti-Air Missiles
##### (ASRAAM) Advanced Short Range Air-to-Air Missile
```sqf
cursorObject addWeaponTurret ["missiles_ASRAAM", [-1]];
cursorObject addMagazineTurret ["2Rnd_AAA_missiles", [-1]];
cursorObject addMagazineTurret ["2Rnd_AAA_missiles_MI02", [-1]];
cursorObject addMagazineTurret ["4Rnd_AAA_missiles", [-1]];
cursorObject addMagazineTurret ["4Rnd_AAA_missiles_MI02", [-1]];
cursorObject addMagazineTurret ["PylonRack_1Rnd_AAA_missiles", [-1]];
cursorObject addMagazineTurret ["PylonMissile_1Rnd_AAA_missiles", [-1]];
```
##### Zephyr
```sqf
cursorObject addWeaponTurret ["missiles_Zephyr", [-1]];
cursorObject addMagazineTurret ["4Rnd_GAA_missiles", [-1]];
cursorObject addMagazineTurret ["PylonRack_1Rnd_GAA_missiles", [-1]];
cursorObject addMagazineTurret ["PylonMissile_1Rnd_GAA_missiles", [-1]];
```
##### Falchion-22
```sqf
cursorObject addWeaponTurret ["Missile_AA_04_Plane_CAS_01_F", [-1]];
cursorObject addMagazineTurret ["2Rnd_Missile_AA_04_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_1Rnd_Missile_AA_04_F", [-1]];
cursorObject addMagazineTurret ["PylonMissile_1Rnd_Missile_AA_04_F", [-1]];
```
##### Sahr-3
```sqf
cursorObject addWeaponTurret ["Missile_AA_03_Plane_CAS_02_F", [-1]];
cursorObject addMagazineTurret ["2Rnd_Missile_AA_03_F", [-1]];
cursorObject addMagazineTurret ["PylonRack_1Rnd_Missile_AA_03_F", [-1]];
cursorObject addMagazineTurret ["PylonMissile_1Rnd_Missile_AA_03_F", [-1]];
```
##### RIM 116 Spartan
```sqf
cursorObject addWeaponTurret ["weapon_rim116Launcher", [-1]];
cursorObject addMagazineTurret ["magazine_Missile_rim116_x21", [-1]];
```
##### RIM 162 Centurion
```sqf
cursorObject addWeaponTurret ["weapon_rim162Launcher", [-1]];
cursorObject addMagazineTurret ["magazine_Missile_rim162_x8", [-1]];
```
##### AMRAAM
```sqf
cursorObject addWeaponTurret ["weapon_AMRAAMLauncherr", [-1]];
cursorObject addMagazineTurret ["magazine_Missile_AMRAAM_x1", [-1]];
```
##### BIM 9X
```sqf
cursorObject addWeaponTurret ["weapon_BIM9xLauncher", [-1]];
cursorObject addMagazineTurret ["magazine_Missile_BIM9X_x1", [-1]];
```
##### R73 Archer
```sqf
cursorObject addWeaponTurret ["weapon_R73Launcher", [-1]];
cursorObject addMagazineTurret ["PylonMissile_Missile_AA_R73_x1", [-1]];
cursorObject addMagazineTurret ["magazine_Missile_AA_R73_x1", [-1]];
```
##### R77 Adder
```sqf
cursorObject addWeaponTurret ["weapon_R77Launcher", [-1]];
cursorObject addMagazineTurret ["PylonMissile_Missile_AA_R77_x1", [-1]];
cursorObject addMagazineTurret ["PylonMissile_Missile_AA_R77_INT_x1", [-1]];
cursorObject addMagazineTurret ["magazine_Missile_AA_R77_x1", [-1]];
```

### Special
##### Flares
```sqf
cursorObject addWeaponTurret ["CMFlareLauncher", [-1]];
cursorObject addMagazineTurret ["60Rnd_CMFlare_Chaff_Magazine", [-1]];
cursorObject addMagazineTurret ["120Rnd_CMFlare_Chaff_Magazine", [-1]];
cursorObject addMagazineTurret ["168Rnd_CMFlare_Chaff_Magazine", [-1]];
cursorObject addMagazineTurret ["192Rnd_CMFlare_Chaff_Magazine", [-1]];
cursorObject addMagazineTurret ["240Rnd_CMFlare_Chaff_Magazine", [-1]];
cursorObject addMagazineTurret ["300Rnd_CMFlare_Chaff_Magazine", [-1]];
```
##### Smoke Screen
```sqf
cursorObject addWeaponTurret ["SmokeLauncher", [-1]];
cursorObject addMagazineTurret ["SmokeLauncherMag", [-1]];
cursorObject addMagazineTurret ["SmokeLauncherMag_boat", [-1]];
```
##### Laser Marker
```sqf
cursorObject addWeaponTurret ["Laserdesignator_mounted", [-1]];
cursorObject addWeaponTurret ["Laserdesignator_pilotCamera", [-1]];
cursorObject addMagazineTurret ["Laserbatteries", [-1]];
```
##### Searchlight
