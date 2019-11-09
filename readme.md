# arma3-debug-commands
## Object spawning

### Delete Object.
```sqf
// Will delete any object, or Vechicle your crosshair is at.
deleteVehicle cursorTarget
```

## Entity spawning

### Creating Vehicles
```sqf
// Will spawn vechicle at player, or player(s) location. "C_Offroad" = cfg name.
_veh = "C_Offroad_01_F" createVehicle position player;
```

## Weather and time

### Skip Time
```sqf
// Skip time per hour. "5" = Hours (Server side)
skipTime 5; 
```
### Remove Fog
```sqf
// This will remove the fog from Arma completely, visually nice but will effect performance.
0 setFog 0; forceWeatherChange; 999999 setFog 0;
```

## Utility

### Map teleport
```sqf
// This will teleport you around the map freely by alt then left clicking.
player onMapSingleClick "if (_alt) then {player setPosATL _pos}";
```
### God Mode
```sqf
// You will take damage, however you will not die. 
player allowdamage false;
```
### Upgrade Vehicles Speed
```sqf
fn_Turbo = { _veh = vehicle player; _speed = speed _veh; _velXM = velocityModelSpace _veh select 0; _velYM = velocityModelSpace _veh select 1; if(_speed <= 1 || _speed >= 180 || _velXM > _velYM) exitWith {}; _speedBoost = 0.1; _curVMS = velocityModelSpace _veh; _newVMS = _curVMS vectorAdd [0, _speedBoost, 0]; _veh setVelocityModelSpace _newVMS; }; dokeyDown={ private ["_handled","_key_delay"] ; _key_delay = 0.01; _handled = false ; if (player getvariable["key",true] and (_this select 1) == 46) exitwith { player setvariable["key",false]; [_key_delay] spawn {sleep (_this select 0);player setvariable["key",true]; }; _handled }; if ((_this select 1) == 42 and speed player >1) then { if(vehicle player != player && vehicle player isKindOf "LandVehicle" && isTouchingGround vehicle player && driver vehicle player == player) then { call fn_Turbo; _handled=true; }; }; _handled; }; waituntil {!(IsNull (findDisplay 46))}; if ( !(isNil "_keydownEventHandler") ) then { (findDisplay 46) displayRemoveEventHandler ["KeyDown", _keydownEventHandler]; }; _keydownEventHandler = (FindDisplay 46) displayAddEventHandler ["keydown","_this call dokeyDown"];
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
player setdamage 0.0; src = player; {_x setDamage 0;} forEach (src nearEntities ["Man", 25]);
```

### Disarms @ Cursor
```sqf
// Removes player, or player(s) Weapons.
removeAllWeapons cursorObject;
```
### Disable fatique (without ACE loaded)

```sqf
// Disable now
player enableFatigue false;
// Disable on next spawn
player addEventhandler ["Respawn", {player enableFatigue false}];
```
### Repair Vehicle
```sqf
// Will repair any Vechicle you're currently in.
_timeForRepair = 0; _vehicle = vehicle player; hint format ["Please wait %1 seconds for repair/flip",_timeForRepair]; sleep _timeForRepair; if (_vehicle == player) then {_vehicle = cursorTarget;}; _vehicle setfuel 1; _vehicle setdamage 0; _vehicle = nil; vehicle = this select 0; _vehicle setvectorup [0,0,1];
```
### See all people on the map
```sqf
// Display ALL players and spawned units on the map.
if(stealthMarkerToggle == 1) exitWith {stealthMarkerToggle = 0; onEachFrame {}; {deleteMarkerLocal _x;} forEach markerList; hint "Markers disabled";}; stealthMarkerToggle = 1; markerList = []; markerUnits = []; hint "Markers enabled - Check map!"; while {true} do { if(stealthMarkerToggle == 0) exitWith {}; { _unit = _x; markerUnits = markerUnits + [_x]; _markerName = str(format ["%1",name _x]); _mName = "m" + _markerName; //player sidechat format ["%1",_markerName]; if(side _x == side player) then { _mName = createMarkerLocal [_markerName, position _x]; _mName setMarkerSizeLocal [0.6, 0.9]; _mName setMarkerShapeLocal "ICON"; _mName setMarkerTypeLocal "mil_triangle"; _mName setMarkerColorLocal "ColorBlue"; _mName setMarkerTextLocal _markerName; _mName setMarkerDirLocal (direction _x); markerList = markerList + [_mName]; } else { _unit = _x; markerUnits = markerUnits + [_x]; _mName setMarkerSizeLocal [0.6, 0.9]; _mName = createMarkerLocal [_markerName, position _x]; _mName setMarkerShapeLocal "ICON"; _mName setMarkerTypeLocal "mil_triangle"; _mName setMarkerColorLocal "ColorRed"; _mName setMarkerTextLocal _markerName; _mName setMarkerDirLocal (direction _x); markerList = markerList + [_mName]; }; //hint format ["%1",_mName]; } forEach allUnits; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {_x setMarkerPosLocal getPos (markerUnits select (markerList find _mName)); _x setMarkerDirLocal getDir(markerUnits select (markerList find _mName));} forEach markerList; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {_x setMarkerPosLocal getPos (markerUnits select (markerList find _mName)); _x setMarkerDirLocal getDir(markerUnits select (markerList find _mName));} forEach markerList; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {_x setMarkerPosLocal getPos (markerUnits select (markerList find _mName)); _x setMarkerDirLocal getDir(markerUnits select (markerList find _mName));} forEach markerList; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {_x setMarkerPosLocal getPos (markerUnits select (markerList find _mName)); _x setMarkerDirLocal getDir(markerUnits select (markerList find _mName));} forEach markerList; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {deleteMarkerLocal _x;} forEach markerList; markerUnits = []; markerList = []; };
```
### ESP
```sqf
// Visually show lines to where all players and units are while on foot.
if (isnil ("WookieESP")) then {WookieESP = 0;}; if (WookieESP==0) then {WookieESP=1;cutText [format["Esp On"], "PLAIN DOWN"];hint "Esp On";}else{WookieESP=0;cutText [format["Esp Off"], "PLAIN DOWN"];hint "Esp Off";}; if (WookieESP==1) then { oneachframe { _nigs = nearestobjects [player,["CAManBase"],1400]; { if((side _x != side player) && (getPlayerUID _x != "") && ((player distance _x) < 1400)) then { drawIcon3D ["", [1,0,0,0.7], GetPosATL _x, 0.1, 0.1, 45, (format ["%2 : %1m",round(player distance _x), name _x]), 1, 0.03, "default"] } else { if((getPlayerUID _x != "") && ((player distance _x) < 1000)) then { drawIcon3D ["", [0,1,0.5,0.4], GetPosATL _x, 0.1, 0.1, 45, (format ["%2 : %1m",round(player distance _x), name _x]), 1, 0.03, "default"] }; }; } foreach playableUnits; _noobs = nearestobjects [player,["CAManBase"],100]; { if(((alive _x)) && ((player distance _x) < 100)) then { if((side _x != side player) && ((player distance _x) < 100)) then { if(player distance _x < 10 && _x iskindof "CAManBase" && side _x != civilian) then { drawLine3D [[getposatl player select 0, getposatl player select 1, getposatl player select 2], _x, [1,0,0,(abs((((player distance _x)) - 100)/100))]] }; } else { drawLine3D [[getposatl player select 0, getposatl player select 1, getposatl player select 2], _x, [0,1,0,(abs((((player distance _x)) - 100)/100))]] }; }; } foreach playableUnits; }; } else { oneachframe {nil}; };
```
### Show all Vehicles on the map with markers.
```sqf
// Show ALL spawned Vechicles on the map. (Need testing if it updates in real time)
if (isnil "ggggggggggggggggggg" ) then {ggggggggggggggggggg=0};

if (ggggggggggggggggggg==0) then
{
hint "Adding Vehicle Markers";
ggggggggggggggggggg=1;
VL = vehicles;
j = count VL;
i = 0;
MV = true;

while {MV} do
{
VL = vehicles;
j = count VL;
i = 0;

for "i" from 0 to j do
{
veh = VL select i;
deleteMarkerLocal ("VM"+ (str i));
mk2 = "VM" + (str i);
mk2 = createMarkerLocal [mk2,getPos veh];
mk2 setMarkerTypeLocal "waypoint";
mk2 setMarkerPosLocal (getPos veh);
mk2 setMarkerColorLocal("ColorGreen");
mk2 setMarkerTextLocal format ["%1",typeOf veh];
};
sleep 0.5;
};
}
else
{
hint "VM Stopping";
i = 0;
MV = false;
ggggggggggggggggggg=0;

for "i" from 0 to j do
{
veh = VL select i;
deleteMarkerLocal ("VM"+ (str i));
};
```

## Fun commands

### Pet!
```sqf
SF_petFollow = { params["_src", "_animalType"]; private["_animalClassname"]; if ( _animalType == "Dog" ) then { _animalClassname = "Fin_random_F"; }; if ( _animalType == "Sheep" ) then { _animalClassname = "Sheep_random_F"; }; if ( _animalType == "Goat" ) then { _animalClassname = "Goat_random_F"; }; if ( _animalType == "Rabbit" ) then { _animalClassname = "Rabbit_F"; }; if ( _animalType == "Hen" ) then { _animalClassname = "Hen_random_F"; }; if ( _animalType == "Snake" ) then { _animalClassname = "Snake_random_F"; }; _animal = createAgent [_animalClassname, getPos _src, [], 5, "CAN_COLLIDE"]; _animal setVariable ["BIS_fnc_animalBehaviour_disable", true]; nul = [_src, _animal, _animalType] spawn { params["_src", "_animal", "_animalType"]; _animalGoMove = _animalType + "_Run"; _animalIdleMove = _animalType + "_Idle_Stop"; if ( _animalType == "Dog" ) then { _animalGoMove = "Dog_Sprint"; }; if ( _animalType == "Rabbit" ) then { _animalGoMove = "Rabbit_Hop"; }; if ( _animalType == "Hen" ) then { _animalGoMove = "Hen_Walk"; }; if ( _animalType == "Snake" ) then { _animalGoMove = "Snakes_Move"; }; _animalMoving = true; _moveDist = 5; while {alive _animal} do { if (_animal distance _src > _moveDist) then { if ( !_animalMoving ) then { _animal playMove _animalGoMove; _animalMoving = true; }; } else { if ( _animalMoving ) then { _animal playMove _animalIdleMove; _animalMoving = false; }; }; if ( _animalMoving ) then { _animal moveTo getPos _src; }; sleep 0.5; }; }; }; [player, "Dog"] call SF_petFollow; [player, "Sheep"] call SF_petFollow; [player, "Goat"] call SF_petFollow; [player, "Rabbit"] call SF_petFollow; [player, "Hen"] call SF_petFollow; [player, "Snake"] call SF_petFollow;
```


### Teleport player, or player(s) into the air.
```sqf
// Teleport player, or all active players into the air based on set number.
_pos = getPosATL player; _pos set [2, 700]; player setPosATL _pos; player spawn bis_fnc_halo;
```

### Shotgun Upgrade (Works on vehicles too!)

```sqf
if ( !(isNil "FEH_shotgunPlayer") ) then { player removeeventhandler["fired", FEH_shotgunPlayer];}; FEH_shotgunPlayer = player addeventhandler ["fired", { _numBullets = 6; // # bullets added to each bullet fired _spread = 1; // bullets spread angle _rndAngle = 0.5; // max random angle added to spread _startRadius = 0.0; // distance sideways bullets appear from original _distanceOut = 0.75; // distance forward bullets appear from original _bulletsPerCircle = 6; // # bullets per each revolution of spiral _degreeStep = 360/_bulletsPerCircle; // populate offsets array _bulletInfo = []; _angle = 0; while {_angle < _degreeStep * _numBullets} do { _radius = _startRadius + (_angle * 0.0003); _offsetX = _radius * ( cos _angle ); _offsetZ = _radius * ( sin _angle ); _offset = [_offsetX, _distanceOut, _offsetZ]; _angleRadius = _angle / 360; _angleX = _spread * (cos _angle) * _angleRadius; _rndAngleX = _rndAngle/2 - random(_rndAngle); _angleZ = _spread * (sin _angle) * _angleRadius; _rndAngleZ = _rndAngle/2 - random(_rndAngle); _angles = [_angleX + _rndAngleX, _angleZ + _rndAngleZ]; _bulletInfo pushBack [_offset, _angles]; _angle = _angle + _degreeStep; }; // get bullet info _bullet = nearestObject [_this select 0,_this select 4]; _bulletType = typeOf _bullet; _bulletpos = getPos _bullet; _weapdir = player weaponDirection currentWeapon player; _up = vectorUp _bullet; _bulletPitchBank = _bullet call BIS_fnc_getPitchBank; _bulletPitch = _bulletPitchBank select 0; _bulletBank = _bulletPitchBank select 1; _bulletDir = getDir _bullet; // spawn bullets { _o = createVehicle [_bulletType, [0,0,0], [], 0, "CAN_COLLIDE"]; _o setVectorDirAndUp[_weapdir,_up]; _offset = _x select 0; _vecToAdd = (_o modelToWorld _offset); _bulletPos2 = _bulletPos vectorAdd _vecToAdd; _o setPos _bulletPos2; _angles = _x select 1; _dir = _angles select 0; _pitch = _angles select 1; _o setDir _bulletDir + _dir; [_o, _bulletPitch + _pitch, _bulletBank] call BIS_fnc_setPitchBank; _o setVelocityModelSpace [0, vectorMagnitude (velocity _bullet), 0]; } forEach _bulletInfo; }];
```

### Rocket Propelled Bullets
```sqf
player removeeventhandler["fired", FEH_missile]; FEH_missile = player addeventhandler ["fired", { _bullet = nearestObject [_this select 0,_this select 4]; _bulletpos = getPosASL _bullet; _o = "R_PG7_F" createVehicle _bulletpos; _weapdir = player weaponDirection currentWeapon player; _dist = 11; _o setPosASL [ (_bulletpos select 0) + (_weapdir select 0)*_dist, (_bulletpos select 1) + (_weapdir select 1)*_dist, (_bulletpos select 2) + (_weapdir select 2)*_dist ]; _up = vectorUp _bullet; _o setVectorDirAndUp[_weapdir,_up]; _o setVelocity velocity _bullet; }];
```
which can be any of the following

> "R_PG7_F", 
> "M_NLAW_AT_F", 
> "R_PG32V_F", 
> "R_TBG32V_F", 
> "M_TITAN_AT",
> "M_TITAN_AP", 
> "Bo_GBU12_LGB", 
> "BombCluster_01_Ammo_F"

### Infinite Ammo
```sqf
player removeeventhandler["fired", FEH_playerAmmo]; FEH_playerAmmo = player addeventhandler ["fired", {(_this select 0) setvehicleammo 1}];
```

### Rooster Head.
```sqf
// Attach "Cock" to player, or players head
 _expl1 = "Cock_random_F" createVehicle position player; _expl1 attachTo [player, [-0.1, 0.1, 0.15], "Head"]; _expl1 setVectorDirAndUp [ [0.5, 0.5, 0], [-0.5, 0.5, 0] ]; 
 ```
### Karate Moves. 
 ```sqf 
// Force player, or players to do "sick moves" - Karate animation
[] spawn { player playMove "AmovPercMstpSnonWnonDnon_exerciseKata"; sleep 30; player playMove ""; }; 
```
### Create Dogs.
```sqf
// Create group of Dogs at player or players locations.
_dog = createAgent ["Fin_random_F", getPos player, [], 5, "CAN_COLLIDE"];
```
### Create Sea Turtles.
```sqf
// Creates Sea Turtle at player or players location.
" Turtle_F" createVehicle position player;
```
### Attaches GBU to Players.
```sqf
// Attach bombs to player, or players. (Not tested if they explode)
_expl1 = "Bo_GBU12_LGB" createVehicle position player; _expl1 attachTo [player, [-0.1, 0.1, 0.15], "Pelvis"]; _expl1 setVectorDirAndUp [ [0.5, 0.5, 0], [-0.5, 0.5, 0] ]; _expl2 = "Bo_GBU12_LGB" createVehicle position player; _expl2 attachTo [player, [0, 0.15, 0.15], "Pelvis"]; _expl2 setVectorDirAndUp [ [1, 0, 0], [0, 1, 0] ]; _expl3 = "Bo_GBU12_LGB" createVehicle position player; _expl3 attachTo [player, [0.1, 0.1, 0.15], "Pelvis"]; _expl3 setVectorDirAndUp [ [0.5, -0.5, 0], [0.5, 0.5, 0] ];
```
### Camera Shake.
```sqf
// Forced player or players camera to shake.
addCamShake [100, 5, 25];
```
### Rainbow Army.
```sqf
[] spawn { hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; ["TaskSucceeded", ["", "Rainbow Army Incoming"]] call BIS_fnc_showNotification; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["B_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["O_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["I_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["C_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; };
```
### Zeus Menu
[Link](https://pastebin.com/E0vAisYw)

### Box Bullets.
```sqf
// Shoots boxes out of your gun.
if (isNil "B0X_CANN0N_T0GGLE") then { B0X_CANN0N_T0GGLE = 0; }; if (B0X_CANN0N_T0GGLE == 0) then { B0X_CANN0N_T0GGLE = 1; hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; ["TaskSucceeded", ["", "Box Cannon Activated"]] call BIS_fnc_showNotification; player addEventHandler ["Fired", { _null = _this spawn { _missile = _this select 6; _VEH = "Land_CargoBox_V1_F" createVehicle position player; waitUntil { _VEH attachto [_missile,[0,0,0]]; }; }; }]; } else { B0X_CANN0N_T0GGLE = 0; ["TaskFailed", ["", "Box Cannon Removed"]] call BIS_fnc_showNotification; { deleteVehicle _x; } forEach (position player nearObjects ["Land_CargoBox_V1_F",1000]); player removeEventHandler ["Fired", 0] };
```
### Human Cannon.
```sqf
// Shoots players around you out of your gun.
if (isNil "PL4YER_CANN0N_T0GGLE") then { PL4YER_CANN0N_T0GGLE = 0; }; if (PL4YER_CANN0N_T0GGLE == 0) then { PL4YER_CANN0N_T0GGLE = 1; ["TaskSucceeded", ["", "Player Cannon Activated"]] call BIS_fnc_showNotification; hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; player addEventHandler ["Fired", { _null = _this spawn { _missile = _this select 6; _unit = allUnits select floor(random count allUnits); waitUntil { if !(name _unit == name player) then { _unit attachto [_missile,[0,0,0]]; _unit allowDamage false; }; }; }; }]; } else { PL4YER_CANN0N_T0GGLE = 0; ["TaskFailed", ["", "Player Cannon Removed"]] call BIS_fnc_showNotification; player removeEventHandler ["Fired", 0] };
```
```
### SUPER EVIL COMMAND !!
```sqf
// Freeze players game
disableUserinput true
```
