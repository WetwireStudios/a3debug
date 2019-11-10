# Arma 3 Basic Scripts


  * [Utility](#utility)
    + [Delete Object.](#delete-object)
    + [Skip Time](#skip-time)
    + [Remove Fog](#remove-fog)
    + [Creating Vehicles](#creating-vehicles)
    + [Arsenal](#arsenal)
      - [On cursor](#on-cursor)
      - [On selected object (Zeus or Eden)](#on-selected-object--zeus-or-eden-)
    + [Map teleport (Alt-Click)](#map-teleport--alt-click-)
    + [God Mode](#god-mode)
    + [Upgrade Vehicles Speed (Hold shift) (Targets vehicle currently occupying) (Use Responsibly)](#upgrade-vehicles-speed--hold-shift---targets-vehicle-currently-occupying---use-responsibly-)
    + [Kills @ Cursor](#kills---cursor)
    + [Heals @ Cursor](#heals---cursor)
    + [Heals Self and Surrounding Players](#heals-self-and-surrounding-players)
    + [Disarms @ Cursor](#disarms---cursor)
    + [Disable fatique](#disable-fatique)
    + [Repair Vehicle](#repair-vehicle)
  * [Fun commands](#fun-commands)
    + [Pet!](#pet-)
    + [Teleport player, or player(s) into the air.](#teleport-player--or-player-s--into-the-air)
    + [Shotgun Upgrade (Works on vehicles too!)](#shotgun-upgrade--works-on-vehicles-too--)
    + [Rocket Propelled Bullets](#rocket-propelled-bullets)
    + [Infinite Ammo](#infinite-ammo)
    + [Rooster Head.](#rooster-head)
    + [Box Bullets.](#box-bullets)
    + [Human Cannon.](#human-cannon)



## Utility
### Delete Object.
```sqf
// Will delete any object, or Vechicle your crosshair is at.
deleteVehicle cursorObject
```
### Skip Time
```sqf
// Skip time per hour. "5" = Hours (Server side)
skipTime 5;
```
### Remove Fog
```sqf
// This will remove the fog from Arma completely, visually nice but will effect performance.
0 setFog 0;
 forceWeatherChange;
 999999 setFog 0;
```
### Creating Vehicles
```sqf
// Will spawn vechicle at player, or player(s) location. "C_Offroad" = cfg name.
_veh
```
### Arsenal
#### On cursor
```sqf
["AmmoboxInit",[cursorObject,true]] call BIS_fnc_arsenal;
```

#### On selected object (Zeus or Eden)
```sqf
["AmmoboxInit",[this,true]] call BIS_fnc_arsenal;
```
### Map teleport (Alt-Click)
```sqf
player onMapSingleClick "if (_alt) then {player setPosATL _pos}";
```
### God Mode
```sqf 
player allowdamage false;
```
### Upgrade Vehicles Speed (Hold shift) (Targets vehicle currently occupying) (Use Responsibly)
```sqf
fn_Turbo = { _veh = vehicle player;
 _speed = speed _veh;
 _velXM = velocityModelSpace _veh select 0;
 _velYM = velocityModelSpace _veh select 1;
 if(_speed <= 1 || _speed >= 200 || _velXM > _velYM) exitWith {};
 _speedBoost = 0.1;
 _curVMS = velocityModelSpace _veh;
 _newVMS = _curVMS vectorAdd [0, _speedBoost, 0];
 _veh setVelocityModelSpace _newVMS;
 };
 dokeyDown={ private ["_handled","_key_delay"] ;
 _key_delay = 0.01;
 _handled = false ;
 if (player getvariable["key",true] and (_this select 1) == 46) exitwith { player setvariable["key",false];
 [_key_delay] spawn {sleep (_this select 0);
player setvariable["key",true];
 };
 _handled };
 if ((_this select 1) == 42 and speed player >1) then { if(vehicle player != player && vehicle player isKindOf "LandVehicle" && isTouchingGround vehicle player && driver vehicle player == player) then { call fn_Turbo;
 _handled=true;
 };
 };
 _handled;
 };
 waituntil {!(IsNull (findDisplay 46))};
 if ( !(isNil "_keydownEventHandler") ) then { (findDisplay 46) displayRemoveEventHandler ["KeyDown", _keydownEventHandler];
 };
 _keydownEventHandler = (FindDisplay 46) displayAddEventHandler ["keydown","_this call dokeyDown"];
  ```

### Kills @ Cursor
```sqf
// Kills object, player, or player(s)
cursorObject setdamage 1
```
### Heals @ Cursor
```sqf
// Heals yourself, or all players.
cursorObject setDamage 0;
```
### Heals Self and Surrounding Players
```sqf
player setdamage 0.0;
 src = player;
 {_x setDamage 0;
} forEach (src nearEntities ["Man", 25]);
```

### Disarms @ Cursor
```sqf
// Removes player, or player(s) Weapons.
removeAllWeapons cursorObject;
```
### Disable fatique

```sqf
// Disable now
player enableFatigue false;
// Disable on respawn
player addEventhandler ["Respawn", {player enableFatigue false}];
```
### Repair Vehicle
```sqf
_timeForRepair = 0;
 _vehicle = vehicle player;
 hint format ["Please wait %1 seconds for repair/flip",_timeForRepair];
 sleep _timeForRepair;
 if (_vehicle == player) then {_vehicle = cursorObject;
};
 _vehicle setfuel 1;
 _vehicle setdamage 0;
 _vehicle = nil;
 vehicle = this select 0;
 _vehicle setvectorup [0,0,1];
```


## Fun commands

### Pet!
```sqf
SF_petFollow = { params["_src", "_animalType"];
 private["_animalClassname"];
 if ( _animalType == "Dog" ) then { _animalClassname = "Fin_random_F";
 };
 if ( _animalType == "Sheep" ) then { _animalClassname = "Sheep_random_F";
 };
 if ( _animalType == "Goat" ) then { _animalClassname = "Goat_random_F";
 };
 if ( _animalType == "Rabbit" ) then { _animalClassname = "Rabbit_F";
 };
 if ( _animalType == "Hen" ) then { _animalClassname = "Hen_random_F";
 };
 if ( _animalType == "Snake" ) then { _animalClassname = "Snake_random_F";
 };
 _animal = createAgent [_animalClassname, getPos _src, [], 5, "CAN_COLLIDE"];
 _animal setVariable ["BIS_fnc_animalBehaviour_disable", true];
 nul = [_src, _animal, _animalType] spawn { params["_src", "_animal", "_animalType"];
 _animalGoMove = _animalType + "_Run";
 _animalIdleMove = _animalType + "_Idle_Stop";
 if ( _animalType == "Dog" ) then { _animalGoMove = "Dog_Sprint";
 };
 if ( _animalType == "Rabbit" ) then { _animalGoMove = "Rabbit_Hop";
 };
 if ( _animalType == "Hen" ) then { _animalGoMove = "Hen_Walk";
 };
 if ( _animalType == "Snake" ) then { _animalGoMove = "Snakes_Move";
 };
 _animalMoving = true;
 _moveDist = 5;
 while {alive _animal} do { if (_animal distance _src > _moveDist) then { if ( !_animalMoving ) then { _animal playMove _animalGoMove;
 _animalMoving = true;
 };
 } else { if ( _animalMoving ) then { _animal playMove _animalIdleMove;
 _animalMoving = false;
 };
 };
 if ( _animalMoving ) then { _animal moveTo getPos _src;
 };
 sleep 0.5;
 };
 };
 };
 [player, "Dog"] call SF_petFollow;
 [player, "Sheep"] call SF_petFollow;
 [player, "Goat"] call SF_petFollow;
 [player, "Rabbit"] call SF_petFollow;
 [player, "Hen"] call SF_petFollow;
 [player, "Snake"] call SF_petFollow;
```


### Teleport player, or player(s) into the air.
```sqf
_pos = getPosATL player;
 _pos set [2, 700];
 player setPosATL _pos;
 player spawn bis_fnc_halo;
```

### Shotgun Upgrade (Works on vehicles too!)

```sqf
if ( !(isNil "FEH_shotgunPlayer") ) then { player removeeventhandler["fired", FEH_shotgunPlayer];
};
 FEH_shotgunPlayer = player addeventhandler ["fired", { _numBullets = 6;
 _angle = 0;
 while {_angle < _degreeStep * _numBullets} do { _radius = _startRadius + (_angle * 0.0003);
 _offsetX = _radius * ( cos _angle );
 _offsetZ = _radius * ( sin _angle );
 _offset = [_offsetX, _distanceOut, _offsetZ];
 _angleRadius = _angle / 360;
 _angleX = _spread * (cos _angle) * _angleRadius;
 _rndAngleX = _rndAngle/2 - random(_rndAngle);
 _angleZ = _spread * (sin _angle) * _angleRadius;
 _rndAngleZ = _rndAngle/2 - random(_rndAngle);
 _angles = [_angleX + _rndAngleX, _angleZ + _rndAngleZ];
 _bulletInfo pushBack [_offset, _angles];
 _angle = _angle + _degreeStep;
 };
 // get bullet info _bullet = nearestObject [_this select 0,_this select 4];
 _bulletType = typeOf _bullet;
 _bulletpos = getPos _bullet;
 _weapdir = player weaponDirection currentWeapon player;
 _up = vectorUp _bullet;
 _bulletPitchBank = _bullet call BIS_fnc_getPitchBank;
 _bulletPitch = _bulletPitchBank select 0;
 _bulletBank = _bulletPitchBank select 1;
 _bulletDir = getDir _bullet;
 // spawn bullets { _o = createVehicle [_bulletType, [0,0,0], [], 0, "CAN_COLLIDE"];
 _o setVectorDirAndUp[_weapdir,_up];
 _offset = _x select 0;
 _vecToAdd = (_o modelToWorld _offset);
 _bulletPos2 = _bulletPos vectorAdd _vecToAdd;
 _o setPos _bulletPos2;
 _angles = _x select 1;
 _dir = _angles select 0;
 _pitch = _angles select 1;
 _o setDir _bulletDir + _dir;
 [_o, _bulletPitch + _pitch, _bulletBank] call BIS_fnc_setPitchBank;
 _o setVelocityModelSpace [0, vectorMagnitude (velocity _bullet), 0];
 } forEach _bulletInfo;
 }];
```
### Rocket Propelled Bullets
```sqf
player removeeventhandler["fired", FEH_missile];
 FEH_missile = player addeventhandler ["fired", { _bullet = nearestObject [_this select 0,_this select 4];
 _bulletpos = getPosASL _bullet;
 _o = "R_PG7_F" createVehicle _bulletpos;
 _weapdir = player weaponDirection currentWeapon player;
 _dist = 11;
 _o setPosASL [ (_bulletpos select 0) + (_weapdir select 0)*_dist, (_bulletpos select 1) + (_weapdir select 1)*_dist, (_bulletpos select 2) + (_weapdir select 2)*_dist ];
 _up = vectorUp _bullet;
 _o setVectorDirAndUp[_weapdir,_up];
 _o setVelocity velocity _bullet;
 }];
```
which can be any of the following

> "R_PG7_F"
> "M_NLAW_AT_F"
> "R_PG32V_F"
> "R_TBG32V_F"
> "M_TITAN_AT"
> "M_TITAN_AP"
> "Bo_GBU12_LGB"
> "BombCluster_01_Ammo_F"
### Infinite Ammo
```sqf
player removeeventhandler["fired", FEH_playerAmmo];
 FEH_playerAmmo = player addeventhandler ["fired", {(_this select 0) setvehicleammo 1}];
```

### Rooster Head.
```sqf
// Attach "Cock" to player, or players head
 _expl1 = "Cock_random_F" createVehicle position player;
 _expl1 attachTo [player, [-0.1, 0.1, 0.15], "Head"];
 _expl1 setVectorDirAndUp [ [0.5, 0.5, 0], [-0.5, 0.5, 0] ];
```

### Box Bullets.
```sqf
// Shoots boxes out of your gun.
if (isNil "B0X_CANN0N_T0GGLE") then { B0X_CANN0N_T0GGLE = 0;
 };
 if (B0X_CANN0N_T0GGLE == 0) then { B0X_CANN0N_T0GGLE = 1;
 hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>";
 ["TaskSucceeded", ["", "Box Cannon Activated"]] call BIS_fnc_showNotification;
 player addEventHandler ["Fired", { _null = _this spawn { _missile = _this select 6;
 _VEH = "Land_CargoBox_V1_F" createVehicle position player;
 waitUntil { _VEH attachto [_missile,[0,0,0]];
 };
 };
 }];
 } else { B0X_CANN0N_T0GGLE = 0;
 ["TaskFailed", ["", "Box Cannon Removed"]] call BIS_fnc_showNotification;
 { deleteVehicle _x;
 } forEach (position player nearObjects ["Land_CargoBox_V1_F",1000]);
 player removeEventHandler ["Fired", 0] };
```
### Human Cannon.
```sqf
// Shoots players around you out of your gun.
if (isNil "PL4YER_CANN0N_T0GGLE") then { PL4YER_CANN0N_T0GGLE = 0;
 };
 if (PL4YER_CANN0N_T0GGLE == 0) then { PL4YER_CANN0N_T0GGLE = 1;
 ["TaskSucceeded", ["", "Player Cannon Activated"]] call BIS_fnc_showNotification;
 hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>";
 player addEventHandler ["Fired", { _null = _this spawn { _missile = _this select 6;
 _unit = allUnits select floor(random count allUnits);
 waitUntil { if !(name _unit == name player) then { _unit attachto [_missile,[0,0,0]];
 _unit allowDamage false;
 };
 };
 };
 }];
 } else { PL4YER_CANN0N_T0GGLE = 0;
 ["TaskFailed", ["", "Player Cannon Removed"]] call BIS_fnc_showNotification;
 player removeEventHandler ["Fired", 0] };
``