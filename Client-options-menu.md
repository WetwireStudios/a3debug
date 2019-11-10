[Home](readme.md)
## This script adds a menu in ESC for everyone, allowing limited customization.
### Created by J [WoLF]
```sqf
comment "Script Title:
	super KEK Custom Menu.
";
comment "Credits:
	Created by J [WoLF]
";
comment "Description:
	- Creates expandable GUI on ESC menu.
	- GUI includes toggles for various scripts.
	- Admin can enable/disable scripts for everyone.
	- View Distance Edit
";
comment "Usage:
	- Set parameters to your liking. (Enable certain scripts)
	- Copy entire script. Paste in debug console.
	- Execute on LOCAL client or SERVER.
	- Everyone can press [ESC] to view the menu.
";
comment "TODO:
	- Fix error message
	- does not support serialization in the mission namespace
";
_init_superKEKcustomMenu = [] spawn {
	disableSerialization;
	[[],{
		disableSerialization;
		if (isNil "sKAM_superKEKcustomMenu_activated") then {
			sKAM_superKEKcustomMenu_activated = false;
		};
		if (sKAM_superKEKcustomMenu_activated) then {
			systemChat "Server Message : ERROR : You tried to activate a script that is already running!";
			hint "Server Message : ERROR : You tried to activate a script that is already running!";
		} else {
			disableSerialization;
			[] spawn {
				disableSerialization;
				comment "-----------------------------------------------";
				if (!hasInterface) exitWith {};
				waitUntil { !isNil { player } && { !isNull player } };
				waitUntil { !isNull (findDisplay 46) };
				comment "-----------------------------------------------";
				
					sKCM_init_scripts = {
						sKCM_ON_earPlugs = {
							if (isNil "JAM_earplugsActivated") then {
								JAM_earplugsActivated = false;
							};
							if (!JAM_earplugsActivated) then {
								JAM_earplugsActivated = true;
								action_earplugs = player addAction [
									"<t color='#FAAC58'>Earplugs</t>",{
										_i = _this select 2;
										if (soundVolume == 1) then {
											hintSilent "Earplugs inserted";
											2 fadeSound 0.1;
											player setUserActionText [_i,"Remove<t color='#FF8000'> Earplugs</t>"];
										} else {
											hintSilent "Earplugs removed";
											2 fadeSound 1;
											player setUserActionText [_i,"Insert<t color='#FE9A2E'> Earplugs</t>"];
										}
									},[],0.0007,false,true,"",""
								];
								JAM_EH_earplugs = player addEventHandler ["Respawn",{
									systemChat "Earplugs removed upon death. You may re-insert them.";
									2 fadeSound 1;
									action_earplugs = player addAction [
										"<t color='#FAAC58'>Earplugs</t>",{
											_i = _this select 2;
											if (soundVolume == 1) then {
												hintSilent "Earplugs inserted";
												2 fadeSound 0.1;
												player setUserActionText [_i,"Remove<t color='#FF8000'> Earplugs</t>"];
											} else {
												hintSilent "Earplugs removed";
												2 fadeSound 1;
												player setUserActionText [_i,"Insert<t color='#FE9A2E'> Earplugs</t>"];
											}
										},[],0.0007,false,true,"",""
									];
								}];
							};
							systemChat "Server Message : Earplugs are now available in the scroll menu.";
						};
						sKCM_OFF_earPlugs = {
							if (isNil "JAM_earplugsActivated") then {
								JAM_earplugsActivated = false;
							};
							if (JAM_earplugsActivated) then {
								JAM_earplugsActivated = false;
							};
							hintSilent "Earplugs removed";
							2 fadeSound 1;
							if (!isNil "action_earplugs") then {
								player removeAction action_earplugs;
							};
							if (!isNil "JAM_EH_earplugs") then {
								player removeEventHandler ["Respawn",JAM_EH_earplugs];
							};
							systemChat "Server Message : Earplugs have been disabled.";
						};
						sKCM_ON_fastRope = {
							MAX_SPEED_WHILE_FASTROPING = 10;
							MAX_SPEED_ROPES_AVAIL = 30;
							STR_TOSS_ROPES = "Toss Ropes";
							STR_FAST_ROPE = "Fast Rope";
							STR_CUT_ROPES = "Cut Ropes";
							if (isDedicated) exitWith {};
							waitUntil {player == player};
							zlt_rope_ropes = [];
							zlt_mutexAction = false;
							zlt_rope_helis = ["O_Heli_Light_02_unarmed_F","O_Heli_Light_02_F","B_Heli_Transport_01_F","B_Heli_Transport_01_camo_F","B_CTRG_Heli_Transport_01_sand_F","B_CTRG_Heli_Transport_01_tropic_F","B_Heli_Transport_03_F","B_Heli_Transport_03_unarmed_F","B_Heli_Transport_03_black_F","B_Heli_Transport_03_unarmed_green_F","O_Heli_Attack_02_F","O_Heli_Attack_02_black_F","I_Heli_Transport_02_F","B_Heli_Light_01_F","B_T_VTOL_01_infantry_olive_F"];
							zlt_rope_helidata = 
							[[
								["O_Heli_Light_02_unarmed_F", "O_Heli_Light_02_F"],
								[1.35,1.35,-24.95],
								[-1.45,1.35,-24.95]
							],[
								["B_Heli_Transport_01_F", "B_Heli_Transport_01_camo_F", "B_CTRG_Heli_Transport_01_sand_F", "B_CTRG_Heli_Transport_01_tropic_F", "B_Heli_Transport_03_F", "B_Heli_Transport_03_unarmed_F", "B_Heli_Transport_03_black_F", "B_Heli_Transport_03_unarmed_green_F", "B_T_VTOL_01_infantry_olive_F"],
								[-1.11,2.5,-24.7],
								[1.11,2.5,-24.7]
							],[
								["O_Heli_Attack_02_F", "O_Heli_Attack_02_black_F"],
								[1.3,1.3,-25],
								[-1.3,1.3,-25]
							],[
								["I_Heli_Transport_02_F"],
								[0,-5,-26],
								[]
							],[
								["B_Heli_Light_01_F"],
								[0.6,0.5,-25.9],
								[-0.8,0.5,-25.9]
							]];
							zlt_fnc_tossropes = {
								private ["_heli","_ropes","_oropes","_rope"];
								_heli = _this;
								_ropes = [];
								_oropes = _heli getVariable ["zlt_ropes",[]];
								if (count _oropes != 0 ) exitWith {};
								_i = 0;
								{
									if ((typeOf _heli) in (_x select 0)) exitWith {
										_ropes = _ropes + [_x select 1];
										if ( count (_x select 2) != 0 ) then { 
											_ropes = _ropes + [_x select 2];
										};
									};
									_i = _i + 1;
								} forEach zlt_rope_helidata;
								sleep random 0.3;
								if ( count (_heli getVariable ["zlt_ropes",[]]) != 0 ) exitWith { zlt_mutexAction = false; };
								_heli animateDoor ['door_R', 1];
								_heli animateDoor ['door_L', 1];
								{
									_rope = createVehicle ["land_rope_f", [0,0,0], [], 0, "CAN_COLLIDE"];
									_rope setDir (getDir _heli);
									_rope attachTo [_heli, _x];
									_oropes = _oropes + [_rope];
								} forEach _ropes;
								_heli setVariable ["zlt_ropes",_oropes,true];
								_heli spawn {
									private ["_heli","_ropes"];
									_heli = _this;
									while {alive _heli and count (_heli getVariable ["zlt_ropes", []]) != 0 and abs (speed _heli) < MAX_SPEED_ROPES_AVAIL } do {
										sleep 0.3;
									};
									_ropes = (_heli getVariable ["zlt_ropes", []]);
									{ deleteVehicle _x; } forEach _ropes;
									_heli setVariable ["zlt_ropes", [], true];
								};
							};
							zlt_fnc_ropes_cond = 
							{
								_veh = vehicle player;
								_flag = (_veh != player) and {(not zlt_mutexAction)} and {count (_veh getVariable ["zlt_ropes", []]) == 0} and { (typeOf _veh) in zlt_rope_helis } and {alive player and alive _veh and (abs (speed _veh) < MAX_SPEED_ROPES_AVAIL ) };
								_flag
							};
							zlt_fnc_fastropeaiunits = 
							{
								private ["_heli","_grunits"];
								diag_log ["zlt_fnc_fastropeaiunits", _this];
								_heli = _this select 0;
								_grunits = _this select 1;
								doStop (driver _heli );
								(driver _heli) setBehaviour "Careless"; 
								(driver _heli) setCombatMode "Blue"; 
								_heli spawn zlt_fnc_tossropes;
								[_heli, _grunits] spawn {
									private ["_units","_heli"];
									sleep random 0.5;
									_units = _this select 1;
									_heli = (_this select 0);
									_units = _units - [player];
									_units = _units - [driver _heli];
									{if (!alive _x or isPlayer _x or vehicle _x != _heli) then {_units = _units - [_x];}; } forEach _units;
									{ sleep (0.5 + random 0.7); _x spawn zlt_fnc_fastropeUnit; } forEach _units;
									waitUntil {sleep 0.5; { (getPos _x select 2) < 1 } count _units == count _units; };
									sleep 10;
									(driver _heli) doFollow (leader group (driver _heli ));
									(driver _heli) setBehaviour "Aware"; 
									(driver _heli) setCombatMode "White"; 
									_heli call zlt_fnc_cutropes;
								};
							};
							zlt_fnc_fastrope = 
							{
								diag_log ["fastRope", _this];
								zlt_mutexAction = true;
								sleep random 0.3;
								if (player == leader group player) then {
									[vehicle player, units group player] call zlt_fnc_fastropeaiunits;
								};
								player call zlt_fnc_fastropeUnit;
								zlt_mutexAction = false;
							};
							zlt_fnc_fastropeUnit = 
							{
								private ["_unit","_heli","_ropes","_rope","_zmax","_zdelta","_zc"];
								_unit = _this;
								_heli = vehicle _unit;
								if (_unit == _heli) exitWith {};
								_ropes = (_heli getVariable ["zlt_ropes", []]);
								if (count _ropes == 0) exitWith {};
								_rope = _ropes call BIS_fnc_selectRandom;
								_zmax = 22;
								_zdelta = (7 / 10);
								_zc = _zmax;
								moveOut _unit;
								_unit action ["eject", _heli];
								_unit switchMove "gunner_standup01";
								_unit setPos [(getPos _unit select 0), (getPos _unit select 1), 0 max ((getPos _unit select 2) - 3)];
								while {alive _unit and (getPos _unit select 2) > 1 and (abs (speed _heli)) < MAX_SPEED_WHILE_FASTROPING  and _zc > -24} do {
									_unit attachTo [_rope, [0,0,_zc]];
									_unit allowDamage false;
									_zc = _zc - _zdelta;
									sleep 0.1;
								};
								_unit switchMove "";
								detach _unit;
								_unit spawn {
									_unit = _this;
									waitUntil {( (isTouchingGround (vehicle _unit)) or (underwater (vehicle _unit)) )};
									_unit allowDamage true;
								};
							};
							zlt_fnc_cutropes = 
							{
								_veh = _this;
								_ropes = (_veh getVariable ["zlt_ropes", []]);
								{ deleteVehicle _x; } forEach _ropes;
								_veh setVariable ["zlt_ropes", [], true];
								_veh animateDoor ['door_R', 0];
								_veh animateDoor ['door_L', 0];
							};
							zlt_fnc_removeropes = 
							{
								(vehicle player) call zlt_fnc_cutropes;
							};
							zlt_fnc_createropes = 
							{
								zlt_mutexAction = true;
								(vehicle player) call zlt_fnc_tossropes;
								zlt_mutexAction = false;
							};
							action_tossRope = player addAction["<t color='#ffff00'>"+STR_TOSS_ROPES+"</t>", zlt_fnc_createropes, [], -1, false, false, '','[] call zlt_fnc_ropes_cond'];
							action_cutRope = player addAction["<t color='#ff0000'>"+STR_CUT_ROPES+"</t>", zlt_fnc_removeropes, [], -1, false, false, '','not zlt_mutexAction and count ((vehicle player) getVariable ["zlt_ropes", []]) != 0'];
							action_fastRope = player addAction["<t color='#00ff00'>"+STR_FAST_ROPE+"</t>", zlt_fnc_fastrope, [], 15, false, false, '','not zlt_mutexAction and count ((vehicle player) getVariable ["zlt_ropes", []]) != 0 and player != driver vehicle player'];
							EH_fastRope = player addEventHandler ["Respawn", {
								player addAction["<t color='#ffff00'>"+STR_TOSS_ROPES+"</t>", zlt_fnc_createropes, [], -1, false, false, '','[] call zlt_fnc_ropes_cond'];
								player addAction["<t color='#ff0000'>"+STR_CUT_ROPES+"</t>", zlt_fnc_removeropes, [], -1, false, false, '','not zlt_mutexAction and count ((vehicle player) getVariable ["zlt_ropes", []]) != 0'];
								player addAction["<t color='#00ff00'>"+STR_FAST_ROPE+"</t>", zlt_fnc_fastrope, [], 15, false, false, '','not zlt_mutexAction and count ((vehicle player) getVariable ["zlt_ropes", []]) != 0 and player != driver vehicle player'];
							}];
							systemChat "Server Message : Helicopter fast-rope rappelling has been enabled.";
						};
						sKCM_OFF_fastRope = {
							if !(isNil "zlt_rope_helis") then {
								zlt_rope_helis = [];
							};
							if !(isNil "EH_fastRope") then {
								player removeEventHandler ["Respawn", EH_fastRope];
							};
							if !(isNil "action_tossRope") then {
								player removeAction action_tossRope;
							};
							if !(isNil "action_cutRope") then {
								player removeAction action_cutRope;
							};
							if !(isNil "action_fastRope") then {
								player removeAction action_fastRope;
							};
							systemChat "Server Message : Helicopter fast-rope rappelling has been disabled.";
						};
						sKCM_ONandOFF_3DTeamIcons = {
							_init_teamESP = [] spawn {
								disableSerialization;
								comment "-----------------------------------------------";
								if (!hasInterface) exitWith {};
								waitUntil { !isNil { player } && { !isNull player } };
								waitUntil { !isNull (findDisplay 46) };
								comment "-----------------------------------------------";
								sKAM_fnc_activateTeamESP = {
									sKAM_teamESP_activated = true;
									sKAM_teamESP_textFont = "PuristaMedium";
									sKAM_teamESP_textAlignment = "center";
									sKAM_teamESP_textSize = 0.035;
									sKAM_teamESP_textShadow = 2;
									sKAM_teamESP_textWidth = 0;
									sKAM_teamESP_textHeight = -2;
									sKAM_teamESP_iconShadow = 0;
									sKAM_teamESP_iconWidth = 3.5;
									sKAM_teamESP_iconHeight = 3.5;
									sKAM_teamESP_unitIcon = "\A3\ui_f\data\GUI\Rsc\RscDisplayEGSpectator\UnitIcon_ca.paa";
									sKAM_teamESP_driverIcon = "\A3\ui_f\data\IGUI\Cfg\CommandBar\imageDriver_ca.paa";
									sKAM_teamESP_gunnerIcon = "\A3\ui_f\data\IGUI\Cfg\CommandBar\imageGunner_ca.paa";
									sKAM_teamESP_commanderIcon = "\A3\ui_f\data\IGUI\Cfg\CommandBar\imageCommander_ca.paa";
									sKAM_teamESP_passengerIcon = "\A3\ui_f\data\IGUI\Cfg\CommandBar\imageCargo_ca.paa";
									sKAM_teamESP_nameColorWEST = [1,1,1,1];
									sKAM_teamESP_nameColorWEST_AI = [0.4,0.7,1,1];
									sKAM_teamESP_unitIconColorWEST = [0,0.3,0.6,1];
									sKAM_teamESP_unitIconColorWEST_squad = [0.1,0.5,0.5,1];
									sKAM_teamESP_unitIconHeightOffset = 1;
									sKAM_teamESP_angle = 0;
									sKAM_teamESP_side = side player;
									sKAM_teamESP_vehicleInfoTextColorWEST = [0,0.8,1,1];
									sKAM_teamESP_vehicleInfoTextColorWEST_AI = [0,1,0.8,1];
									if (isNil "sKAM_teamESP_updatingSide") then {
										_init_teamESP_sideUpdater = [] spawn {
											sKAM_teamESP_updatingSide = true;
											while { sKAM_teamESP_updatingSide } do 
											{
												waitUntil { (side player != sKAM_teamESP_side) };
												if ((lifeState player == "INCAPACITATED") or (captive player) or (str side player == "ENEMY")) then {
													comment "player side is civ only because unconscious or captive";
													comment "side not updated";
												} else {
													sKAM_teamESP_side = side player;
													comment "side updated";
												};
												waitUntil { (side player == sKAM_teamESP_side) };
											};
										};
									} else {
										sKAM_teamESP_updatingSide = false;
										comment "reset";
										sKAM_teamESP_updatingSide = true;
									};
									if (isNil "sKAM_teamESP_displayNames") then {
										sKAM_teamESP_displayNames = false;
									};
									if (isNil "sKAM_teamESP_toggleDisplayNames") then {
										sKAM_teamESP_toggleDisplayNames = {
											if (sKAM_teamESP_displayNames) then {
												sKAM_teamESP_displayNames = false;
											} else {
												sKAM_teamESP_displayNames = true;
											};
										};
									};
									if (isNil "sKAM_keybind_teamESP_toggleDisplayNames") then {
										sKAM_keybind_teamESP_toggleDisplayNames = (findDisplay 46) displayAddEventHandler ["KeyDown",  "if (_this select 1 == 87) then {
											[] call sKAM_teamESP_toggleDisplayNames;
										}"];
										comment "Press [F11] to toggle display names.";
									};
									if (!isNil "sKAM_EH_drawTeamESP") then {
										removeMissionEventHandler ['Draw3D',sKAM_EH_drawTeamESP];
									};
									sKAM_EH_drawTeamESP = addMissionEventHandler ["Draw3D", {
										if (alive player) exitWith {
											{
												if (
												(_x != player) && (typeOf _x != "ModuleHQ_F") && (typeOf _x != "VirtualCurator_F") && 
												((side _x == sKAM_teamESP_side) or ((lifeState _x == "INCAPACITATED") or (captive _x) or (str side player == "ENEMY")))
												) then {
													_iconPos = _x modelToWorldVisual (_x selectionPosition "Head");
													_iconPos set [2, (_iconPos select 2) + sKAM_teamESP_unitIconHeightOffset];
													sKAM_teamESP_iconColor = sKAM_teamESP_unitIconColorWEST;
													if (group _x == group player) then {
														sKAM_teamESP_iconColor = sKAM_teamESP_unitIconColorWEST_squad;
													};
													if (isPlayer _x) then {
														comment "the unit is a real player";
														if (_x == vehicle _x) then {
															comment "player is not in a vehicle";
															comment "draw player esp";
															comment "DRAW PLAYER ICON";
															drawIcon3D 
															[
																sKAM_teamESP_unitIcon,
																sKAM_teamESP_iconColor,
																_iconPos,
																sKAM_teamESP_iconWidth, 
																sKAM_teamESP_iconHeight, 
																sKAM_teamESP_angle,
																"",
																sKAM_teamESP_iconShadow,
																sKAM_teamESP_textSize,
																sKAM_teamESP_textFont,
																sKAM_teamESP_textAlignment
															];
															comment "DRAW PLAYER NAME TEXT";
															if (sKAM_teamESP_displayNames) then 
															{
																_iconLabel = name _x;
																drawIcon3D 
																[
																	"",
																	sKAM_teamESP_nameColorWEST,
																	_iconPos,
																	sKAM_teamESP_textWidth, 
																	sKAM_teamESP_textHeight, 
																	sKAM_teamESP_angle,
																	_iconLabel,
																	sKAM_teamESP_textShadow,
																	sKAM_teamESP_textSize,
																	sKAM_teamESP_textFont,
																	sKAM_teamESP_textAlignment
																];
															};
														} else {
															comment "player is in a vehicle";
															if (_x == driver vehicle _x) then {
																comment "player is driver of vehicle";
																comment "DRAW PLAYER ICON";
																drawIcon3D 
																[
																	sKAM_teamESP_unitIcon,
																	sKAM_teamESP_iconColor,
																	_iconPos,
																	sKAM_teamESP_iconWidth, 
																	sKAM_teamESP_iconHeight, 
																	sKAM_teamESP_angle,
																	"",
																	sKAM_teamESP_iconShadow,
																	sKAM_teamESP_textSize,
																	sKAM_teamESP_textFont,
																	sKAM_teamESP_textAlignment
																];
																comment "DRAW PLAYER NAME TEXT";
																sKAM_teamESP_vehicleInfoLabel = "";
																if (sKAM_teamESP_displayNames) then 
																{
																	sKAM_teamESP_vehicleInfoLabel = (getText (configFile >> "cfgVehicles" >> typeOf vehicle _x >> "displayName"));
																	_crewArray = crew vehicle _x;
																	_crewCount = (count _crewArray) - 1;
																	_iconLabel = ((name _x) + " [+" + (str _crewCount) + "]");
																	if (_crewCount == 0) then {
																		_iconLabel = name _x;
																	};
																	drawIcon3D 
																	[
																		"",
																		sKAM_teamESP_nameColorWEST,
																		_iconPos,
																		sKAM_teamESP_textWidth, 
																		sKAM_teamESP_textHeight, 
																		sKAM_teamESP_angle,
																		_iconLabel,
																		sKAM_teamESP_textShadow,
																		sKAM_teamESP_textSize,
																		sKAM_teamESP_textFont,
																		sKAM_teamESP_textAlignment
																	];
																};
																comment "DRAW VEHICLE INFO";
																drawIcon3D 
																[
																	sKAM_teamESP_driverIcon,
																	sKAM_teamESP_vehicleInfoTextColorWEST,
																	(_x modelToWorldVisual (_x selectionPosition "Spine3")),
																	0.5, 
																	0.5, 
																	sKAM_teamESP_angle,
																	sKAM_teamESP_vehicleInfoLabel,
																	sKAM_teamESP_textShadow,
																	0.02,
																	sKAM_teamESP_textFont,
																	sKAM_teamESP_textAlignment
																];
															} else {
																comment "player is not the driver of the vehicle";
																sKAM_teamESP_fghsjagagsf = false;
																if ((driver vehicle _x == objNull) or (not alive driver vehicle _x)) then {
																	if (gunner vehicle _x == _x) then {
																		sKAM_teamESP_vehicleInfoIcon = sKAM_teamESP_gunnerIcon;
																		sKAM_teamESP_fghsjagagsf = true;
																	} else {
																		if ((gunner vehicle _x == objNull) or (not alive gunner vehicle _x)) then {
																			if (commander vehicle _x == _x) then {
																				sKAM_teamESP_vehicleInfoIcon = sKAM_teamESP_commanderIcon;
																				sKAM_teamESP_fghsjagagsf = true;
																			} else {
																				if (count crew vehicle _x == 1) then {
																					sKAM_teamESP_vehicleInfoIcon = sKAM_teamESP_passengerIcon;
																					sKAM_teamESP_fghsjagagsf = true;
																				};
																			};
																		};
																	};
																};
																if (sKAM_teamESP_fghsjagagsf) then {
																	comment "DRAW PLAYER ICON";
																	drawIcon3D 
																	[
																		sKAM_teamESP_unitIcon,
																		sKAM_teamESP_iconColor,
																		_iconPos,
																		sKAM_teamESP_iconWidth, 
																		sKAM_teamESP_iconHeight, 
																		sKAM_teamESP_angle,
																		"",
																		sKAM_teamESP_iconShadow,
																		sKAM_teamESP_textSize,
																		sKAM_teamESP_textFont,
																		sKAM_teamESP_textAlignment
																	];
																	comment "DRAW PLAYER NAME TEXT";
																	sKAM_teamESP_vehicleInfoLabel = "";
																	if (sKAM_teamESP_displayNames) then 
																	{
																		sKAM_teamESP_vehicleInfoLabel = (getText (configFile >> "cfgVehicles" >> typeOf vehicle _x >> "displayName"));
																		_crewArray = crew vehicle _x;
																		_crewCount = (count _crewArray) - 1;
																		_iconLabel = ((name _x) + " [+" + (str _crewCount) + "]");
																		if (_crewCount == 0) then {
																			_iconLabel = name _x;
																		};
																		drawIcon3D 
																		[
																			"",
																			sKAM_teamESP_nameColorWEST,
																			_iconPos,
																			sKAM_teamESP_textWidth, 
																			sKAM_teamESP_textHeight, 
																			sKAM_teamESP_angle,
																			_iconLabel,
																			sKAM_teamESP_textShadow,
																			sKAM_teamESP_textSize,
																			sKAM_teamESP_textFont,
																			sKAM_teamESP_textAlignment
																		];
																	};
																	comment "DRAW VEHICLE INFO";
																	drawIcon3D 
																	[
																		sKAM_teamESP_vehicleInfoIcon,
																		sKAM_teamESP_vehicleInfoTextColorWEST,
																		(_x modelToWorldVisual (_x selectionPosition "Spine3")),
																		0.5, 
																		0.5, 
																		sKAM_teamESP_angle,
																		sKAM_teamESP_vehicleInfoLabel,
																		sKAM_teamESP_textShadow,
																		0.02,
																		sKAM_teamESP_textFont,
																		sKAM_teamESP_textAlignment
																	];
																};
															};
														};
													} else {
														comment "the unit is a computer";
														if (_x == vehicle _x) then {
															comment "unit is not in a vehicle";
															comment "draw unit esp";
															comment "DRAW unit ICON";
															drawIcon3D 
															[
																sKAM_teamESP_unitIcon,
																sKAM_teamESP_iconColor,
																_iconPos,
																sKAM_teamESP_iconWidth, 
																sKAM_teamESP_iconHeight, 
																sKAM_teamESP_angle,
																"",
																sKAM_teamESP_iconShadow,
																sKAM_teamESP_textSize,
																sKAM_teamESP_textFont,
																sKAM_teamESP_textAlignment
															];
															comment "DRAW unit NAME TEXT";
															if (sKAM_teamESP_displayNames) then 
															{
																_iconLabel = ("(AI) " + name _x);
																drawIcon3D 
																[
																	"",
																	sKAM_teamESP_nameColorWEST_AI,
																	_iconPos,
																	sKAM_teamESP_textWidth, 
																	sKAM_teamESP_textHeight, 
																	sKAM_teamESP_angle,
																	_iconLabel,
																	sKAM_teamESP_textShadow,
																	sKAM_teamESP_textSize,
																	sKAM_teamESP_textFont,
																	sKAM_teamESP_textAlignment
																];
															};
														} else {
															comment "unit is in a vehicle";
															if (_x == driver vehicle _x) then {
																comment "unit is driver of vehicle";
																comment "DRAW unit ICON";
																drawIcon3D 
																[
																	sKAM_teamESP_unitIcon,
																	sKAM_teamESP_iconColor,
																	_iconPos,
																	sKAM_teamESP_iconWidth, 
																	sKAM_teamESP_iconHeight, 
																	sKAM_teamESP_angle,
																	"",
																	sKAM_teamESP_iconShadow,
																	sKAM_teamESP_textSize,
																	sKAM_teamESP_textFont,
																	sKAM_teamESP_textAlignment
																];
																comment "DRAW unit NAME TEXT";
																sKAM_teamESP_vehicleInfoLabel = "";
																if (sKAM_teamESP_displayNames) then 
																{
																	sKAM_teamESP_vehicleInfoLabel = (getText (configFile >> "cfgVehicles" >> typeOf vehicle _x >> "displayName"));
																	_crewArray = crew vehicle _x;
																	_crewCount = (count _crewArray) - 1;
																	_iconLabel = ("(AI) " + (name _x) + " [+" + (str _crewCount) + "]");
																	if (_crewCount == 0) then {
																		_iconLabel = ("(AI) " + (name _x));
																	};
																	drawIcon3D 
																	[
																		"",
																		sKAM_teamESP_nameColorWEST_AI,
																		_iconPos,
																		sKAM_teamESP_textWidth, 
																		sKAM_teamESP_textHeight, 
																		sKAM_teamESP_angle,
																		_iconLabel,
																		sKAM_teamESP_textShadow,
																		sKAM_teamESP_textSize,
																		sKAM_teamESP_textFont,
																		sKAM_teamESP_textAlignment
																	];
																};
																comment "DRAW VEHICLE INFO";
																drawIcon3D 
																[
																	sKAM_teamESP_driverIcon,
																	sKAM_teamESP_vehicleInfoTextColorWEST_AI,
																	(_x modelToWorldVisual (_x selectionPosition "Spine3")),
																	0.5, 
																	0.5, 
																	sKAM_teamESP_angle,
																	sKAM_teamESP_vehicleInfoLabel,
																	sKAM_teamESP_textShadow,
																	0.02,
																	sKAM_teamESP_textFont,
																	sKAM_teamESP_textAlignment
																];
															} else {
																comment "unit is not the driver of the vehicle";
																sKAM_teamESP_fghsjagagsf = false;
																if ((driver vehicle _x == objNull) or (not alive driver vehicle _x)) then {
																	if (gunner vehicle _x == _x) then {
																		sKAM_teamESP_vehicleInfoIcon = sKAM_teamESP_gunnerIcon;
																		sKAM_teamESP_fghsjagagsf = true;
																	} else {
																		if ((gunner vehicle _x == objNull) or (not alive gunner vehicle _x)) then {
																			if (commander vehicle _x == _x) then {
																				sKAM_teamESP_vehicleInfoIcon = sKAM_teamESP_commanderIcon;
																				sKAM_teamESP_fghsjagagsf = true;
																			} else {
																				if (count crew vehicle _x == 1) then {
																					sKAM_teamESP_vehicleInfoIcon = sKAM_teamESP_passengerIcon;
																					sKAM_teamESP_fghsjagagsf = true;
																				};
																			};
																		};
																	};
																};
																if (sKAM_teamESP_fghsjagagsf) then {
																	comment "DRAW unit ICON";
																	drawIcon3D 
																	[
																		sKAM_teamESP_unitIcon,
																		sKAM_teamESP_iconColor,
																		_iconPos,
																		sKAM_teamESP_iconWidth, 
																		sKAM_teamESP_iconHeight, 
																		sKAM_teamESP_angle,
																		"",
																		sKAM_teamESP_iconShadow,
																		sKAM_teamESP_textSize,
																		sKAM_teamESP_textFont,
																		sKAM_teamESP_textAlignment
																	];
																	comment "DRAW unit NAME TEXT";
																	sKAM_teamESP_vehicleInfoLabel = "";
																	if (sKAM_teamESP_displayNames) then 
																	{
																		_crewArray = crew vehicle _x;
																		_crewCount = (count _crewArray) - 1;
																		sKAM_teamESP_vehicleInfoLabel = (getText (configFile >> "cfgVehicles" >> typeOf vehicle _x >> "displayName"));
																		_iconLabel = ("(AI) " + (name _x) + " [+" + (str _crewCount) + "]");
																		if (_crewCount == 0) then {
																			_iconLabel = ("(AI) " + (name _x));
																		};
																		drawIcon3D 
																		[
																			"",
																			sKAM_teamESP_nameColorWEST_AI,
																			_iconPos,
																			sKAM_teamESP_textWidth, 
																			sKAM_teamESP_textHeight, 
																			sKAM_teamESP_angle,
																			_iconLabel,
																			sKAM_teamESP_textShadow,
																			sKAM_teamESP_textSize,
																			sKAM_teamESP_textFont,
																			sKAM_teamESP_textAlignment
																		];
																	};
																	comment "DRAW VEHICLE INFO";
																	drawIcon3D 
																	[
																		sKAM_teamESP_vehicleInfoIcon,
																		sKAM_teamESP_vehicleInfoTextColorWEST_AI,
																		(_x modelToWorldVisual (_x selectionPosition "Spine3")),
																		0.5, 
																		0.5, 
																		sKAM_teamESP_angle,
																		sKAM_teamESP_vehicleInfoLabel,
																		sKAM_teamESP_textShadow,
																		0.02,
																		sKAM_teamESP_textFont,
																		sKAM_teamESP_textAlignment
																	];
																};
															};
														};
													};
												};
											} forEach allUnits;
										};
									}];
									systemChat "Server Message : 3D Team Icons have been enabled. Press [F11] to toggle names.";
								};
								sKAM_fnc_deactivateTeamESP = {
									if (!isNil "sKAM_EH_drawTeamESP") then {
										removeMissionEventHandler ['Draw3D',sKAM_EH_drawTeamESP];
									};
									sKAM_teamESP_activated = false;
									systemChat "Server Message : 3D Team Icons have been disabled.";
								};
								if (isNil "sKAM_teamESP_activated") then {
									comment "First-time initialization.";
									sKAM_teamESP_activated = false;
									if (!sKAM_teamESP_activated) then {
										comment "Turn teamESP ON";
										[] call sKAM_fnc_activateTeamESP;
									} else {
										comment "Turn teamESP OFF";
										[] call sKAM_fnc_deactivateTeamESP;
									};
								} else {
									comment "Not first-time initialization.";
									if (!sKAM_teamESP_activated) then {
										comment "Turn teamESP ON";
										[] call sKAM_fnc_activateTeamESP;
									} else {
										comment "Turn teamESP OFF";
										[] call sKAM_fnc_deactivateTeamESP;
									};
								};
							};
						};
						sKCM_ON_MAPTeamIcons = {
							disableSerialization;
							if (!isNil "TeamMapEvent") then {
								(findDisplay 12 displayCtrl 51) ctrlRemoveEventHandler ["Draw",TeamMapEvent];
							};
							[] spawn 
							{
								waitUntil {sleep 0.1; getClientState == "BRIEFING READ"};
								disableMapIndicators [true,false,false,false];
								
								maxDistanceFlagMarker3D = 1500;
								transitionDistanceFlagMarker3D = 500;
								maxDistanceUnitMarker3D = 150;
								maxDistanceUnitMarkerText3D = 10;
								maxCursorRangeUnitMarker = 0.02;
								minMapZoomUnitMarker = 0.0045;
								
								TeamMapEvent = (findDisplay 12 displayCtrl 51) ctrlAddEventHandler ["Draw", 
								{
									_vehicleList = [];
									{ 
										if((side group _x) isEqualTo (side group player)) then
										{
											_pos = _x modelToWorldVisual [0,0,0];
											_unit = driver vehicle _x;
											_dir = getDir _x;
											_text = (name _x);
											_distance = player distance _x;
											
											_alpha = 1;
											_color = switch (side group _x) do
											{
												case west: {[0,0.3,0.6,_alpha]};
												case east: {[0.8,0.05,0,_alpha]};
												case independent: {[0.5,1,0.5,_alpha]};
												default {[1,1,1,_alpha]};
											};
											
											if((group player) isEqualTo (group _unit)) then 
											{
												_color = [0.1,0.5,0.5,_alpha];
											};
											
											_pos2D = (_this select 0) ctrlMapWorldToScreen _pos;
											_posCursor2D = getMousePosition;
											_dist = _pos2D distance2D _posCursor2D;
											_scale = ctrlMapScale (_this select 0);
								
											if (vehicle _x == _x) then 
											{
												if((_scale > minMapZoomUnitMarker) && (_dist > maxCursorRangeUnitMarker)) then {_text = "";};
								
												_this select 0 drawIcon
												[
													"\A3\ui_f\data\Map\VehicleIcons\iconManVirtual_ca.paa",
													_color,
													_pos,
													20,
													20,
													_dir,
													_text,
													2,
													0.05,
													"RobotoCondensedBold",
													"left"
												];
								
												_this select 0 drawIcon
												[
													"\A3\ui_f\data\Map\VehicleIcons\iconManVirtual_ca.paa",
													_color,
													_pos,
													20,
													20,
													_dir,
													_text,
													1,
													0.05,
													"RobotoCondensedBold",
													"left"
												];
											}
											else 	
											{
												if !((vehicle _x) in _vehicleList) then 
												{
													_vehicleList pushback vehicle _x;
								
													_dir = getDir vehicle _x;
								
													_className = (typeOf vehicle _x);
													_file = getText (configfile >> "CfgVehicles" >> _className >> "icon");
								
													_driver = driver vehicle _x;
								
													_vehName = getText (configfile >> "CfgVehicles" >> _className >> "displayName");
													_text = _vehName;
								
													_text2 = "";
													_count = count crew vehicle _x;
													if(_count > 1) then 
													{
														_text2 = ((name _driver) + " + " + (str (_count-1)) + " more");
													}
													else
													{
														_text2 = (name _driver);
													};
													if((_scale > minMapZoomUnitMarker) && (_dist > maxCursorRangeUnitMarker)) then {_text = ""; _text2 = "";};
													
													_this select 0 drawIcon
													[
														_file,
														_color,
														_pos,
														20,
														20,
														_dir,
														_text,
														2,
														0.05,
														"RobotoCondensedBold",
														"left"
													];
								
													_this select 0 drawIcon
													[
														_file,
														_color,
														_pos,
														20,
														20,
														_dir,
														_text2,
														2,
														0.05,
														"RobotoCondensedBold",
														"right"
													];
								
													_this select 0 drawIcon
													[
														_file,
														_color,
														_pos,
														20,
														20,
														_dir,
														_text,
														1,
														0.05,
														"RobotoCondensedBold",
														"left"
													];
												};
											};
								
											if(_x == player) then 
											{
												_color set[3,0.5];
												_this select 0 drawIcon
												[
													"\a3\ui_f\data\Map\groupIcons\selector_selected_ca.paa",
													_color,
													_pos,
													30,
													30,
													_dir,
													"",
													0,
													0.05,
													"RobotoCondensedBold",
													"left"
												];
											};
										};
									} foreach allPlayers;
								}];
								systemChat "Server Message : Team Icons on map have been enabled.";
							};
						};
						sKCM_OFF_MAPTeamIcons = {
							disableSerialization;
							if (!isNil "TeamMapEvent") then {
								(findDisplay 12 displayCtrl 51) ctrlRemoveEventHandler ["Draw",TeamMapEvent];
								systemChat "Server Message : Team Icons on map have been disabled.";
							};
						};
						sKCM_ON_weaponOnBackKey = {
							disableSerialization;
							comment "-----------------------------------------------";
							sKAM_keybind_weaponOnBack = (findDisplay 46) displayADDEventHandler ["KeyDown",  "if (_this select 1 == 5) then {
								player action ['SwitchWeapon',player,player,-1];
							}"];
							comment "4";
							comment "-----------------------------------------------";
							systemChat "Server Message : 'putWeaponOnBack' keybind set. [Press 4]";
							comment "-----------------------------------------------";
						};
						sKCM_OFF_weaponOnBackKey = {
							disableSerialization;
							comment "-----------------------------------------------";
							if !(isNil "sKAM_keybind_weaponOnBack") then {
								(findDisplay 46) displayremoveEventHandler ["KeyDown",sKAM_keybind_weaponOnBack];
							};
							comment "-----------------------------------------------";
							systemChat "Server Message : 'putWeaponOnBack' keybind [4] removed.";
							comment "-----------------------------------------------";
						};
						sKCM_ON_karateKey = {
							disableSerialization;
							comment "-----------------------------------------------";
							sKAM_keybind_karate = (findDisplay 46) displayADDEventHandler ["KeyDown",  "if (_this select 1 == 6) then {
								player playMove 'AmovPercMstpSnonWnonDnon_exerciseKata';
								_list = actionKeysNames 'SitDown';
								_hintText = ('You are a master of the martial arts. Press [');
								_hintText = ((_hintText) + (_list));
								_hintText = ((_hintText) + ('] to stop your demonstration.'));
								hint _hintText;
							}"];
							comment "5";
							comment "-----------------------------------------------";
							systemChat "Server Message : 'Karate' keybind set. [Press 5]";
							comment "-----------------------------------------------";
						};
						sKCM_OFF_karateKey = {
							disableSerialization;
							comment "-----------------------------------------------";
							if !(isNil "sKAM_keybind_karate") then {
								(findDisplay 46) displayremoveEventHandler ["KeyDown",sKAM_keybind_karate];
							};
							comment "-----------------------------------------------";
							systemChat "Server Message : 'Karate' keybind [5] removed.";
							comment "-----------------------------------------------";
						};
						sKCM_ON_handsUpKey = {
							disableSerialization;
							comment "-----------------------------------------------";
							handsUpInit1 = {
								sKAM_keybind_handsUp = (findDisplay 46) displayADDEventHandler ["KeyDown",  {if (_this select 1 == 7) then {
									player playMove 'AmovPercMstpSsurWnonDnon';
									if (!captive player) then {
										player setCaptive true;
									};
									(findDisplay 46) displayremoveEventHandler ['KeyDown',sKAM_keybind_handsUp];
									sKAM_keybind_handsDown = (findDisplay 46) displayADDEventHandler ['KeyDown',  {if (_this select 1 == 7) then {
										if ((animationstate player) == "AmovPercMstpSsurWnonDnon") then {
											if (captive player) then {
												player setCaptive false;
											};
											[player, "AmovPercMstpSsurWnonDnon_AmovPercMstpSnonWnonDnon"] remoteExec ["switchMove", 0];
										};
										(findDisplay 46) displayremoveEventHandler ['KeyDown',sKAM_keybind_handsDown];
										[] spawn handsUpInit1;
									}}];
								}}];
							};
							[] spawn handsUpInit1;
							comment "6";
							comment "-----------------------------------------------";
							systemChat "Server Message : 'Hands Up' keybind set. [Press 6]";
							comment "-----------------------------------------------";
						};
						sKCM_OFF_handsUpKey = {
							disableSerialization;
							comment "-----------------------------------------------";
							if !(isNil "sKAM_keybind_handsUp") then {
								(findDisplay 46) displayremoveEventHandler ["KeyDown",sKAM_keybind_handsUp];
							};
							if !(isNil "sKAM_keybind_handsDown") then {
								(findDisplay 46) displayremoveEventHandler ['KeyDown',sKAM_keybind_handsDown];
							};
							comment "-----------------------------------------------";
							systemChat "Server Message : 'Hands Up' keybind [6] removed.";
							comment "-----------------------------------------------";
						};
						sKCM_ON_dragWoundedBuryDead = {
							disableSerialization;
							if (isNil "allowDragBodies") then {
								allowDragBodies = false;
							};
							if (!allowDragBodies) then {
								allowDragBodies = true;
								[] spawn
								{
									waitUntil {sleep 1; getClientState isEqualTo "BRIEFING READ"};
									sleep 1;
									
									allowDragBodies = true;
									_dragAnim = "AmovPercMstpSnonWnonDnon_AcinPknlMwlkSnonWnonDb_1";
									_bodyAnim = "AinjPpneMrunSnonWnonDb";
									_bodyDropAnim = "AinjPpneMstpSnonWrflDb_release";
									_maxDist = 3;
									currentDragBody = nil;
									lastAnimation = "Unknown";

									_structText = "<a color='#ff1111' font='PuristaSemiBold' size='1' shadow='2'><img image='\A3\ui_f\data\map\vehicleicons\pictureHeal_ca.paa'/>Drag Body</a>";

									player addEventHandler ["AnimDone", { 
										params ["_unit", "_anim"]; 
										lastAnimation = _anim;
									}];

									GES_fnc_releaseDragBody = {
										params["_body","_mode"];
										detach _body;
										_body setVariable ["isDraggingAllowed",nil,true];
										[_body,"UnconsciousFaceUp"] remoteExec ["switchMove",0];
										player setAnimSpeedCoef 1; 
										{_x setVehicleLock "DEFAULT"} foreach vehicles;

										switch (_mode) do 
										{
											case 0: 
											{
												[player,"UnconsciousFaceUp"] remoteExec ["switchMove",0];
											};
											case 1: 
											{
												[player,"AmovPpneMstpSrasWrflDnon"] remoteExec ["playMove",0];
											};
										};

										_index = player getVariable "releaseDragActionIndex";
										if !(isNil "_index") then 
										{
											player removeAction _index;
											currentDragBody = nil;
										};
									};

									GES_fnc_enableDragBody = {
										params["_body","_structText"];
										currentDragBody =_body;
										_body attachTo [player,[0,1,0]];
										[_body,180] remoteExec ["setDir",0];
										_body setPos getPos _body;
										_body setVariable ["isDraggingAllowed",false,true];
										{_x setVehicleLock "LOCKEDPLAYER"} foreach vehicles;

										_dragActionIndex = _body getVariable "dragActionIndex";
										if(!isNil "_dragActionIndex") then 
										{
											_body removeAction _dragActionIndex;
											_body setVariable ["dragActionIndex",nil];
										}; 

										[_body] spawn 
										{
											[player,"AmovPercMstpSnonWnonDnon_AcinPknlMwlkSnonWnonDb_1"] remoteExec ["playMove",0];
											waitUntil {lastAnimation isEqualTo "amovpercmstpsnonwnondnon_acinpknlmwlksnonwnondb_2"};
											[(_this select 0),"AinjPpneMrunSnonWnonDb"] remoteExec ["switchMove",0];
										};

										sleep 1;
										player setAnimSpeedCoef 1.5;
										_actionIndex = player addAction [_structText,
										{
											_body = (_this select 3);
											[_body,1] call GES_fnc_releaseDragBody;
										},
										_body,10,true,true,"","true",5];
										player setVariable ["releaseDragActionIndex",_actionIndex];
									};

									GES_fnc_enableBuryBody = {
										params["_body"];
										_lifeState = lifeState _body;
										if(_lifeState isEqualTo "DEAD" && isNil "_hasBuryAction") then 
										{
											_structTextBury = "<a color='#b7b7b7' font='PuristaSemiBold' size='1' shadow='2'><img image='\a3\UI_f\data\IGUI\cfg\MPTable\killed_ca.paa'/>Bury Body</a>";
											_body addAction [_structTextBury,
											{
												_body = (_this select 3);
												[_body] spawn 
												{
													_body = _this select 0;
													[_body] remoteExec ["hideBody",0];
													[player,"PutDown"] remoteExec ["playActionNow",0];
													sleep 10;
													deleteVehicle _body;
												};
											},
											_body,10,true,true,"","true",4];
											_body setVariable ["hasBuryAction",true];
										};
									};

									while {allowDragBodies} do
									{
										_nearBodies = nearestObjects [player,["Man"],_maxDist];
										if (count _nearBodies >= 2) then 
										{
											_nearestBody = _nearBodies select 1;
											if (!isNil "_nearestBody") then
											{
												_dragActionIndex = _nearestBody getVariable "dragActionIndex";
												_isDraggingAllowed = _nearestBody getVariable "isDraggingAllowed";
												_hasBuryAction = _nearestBody getVariable "hasBuryAction";
												if (isNil "_dragActionIndex" && isNil "_isDraggingAllowed" && isNil "currentDragBody") then
												{
													_lifeState = lifeState _nearestBody;
													if((_lifeState isEqualTo "INCAPACITATED")) then 
													{
														_actionIndex = _nearestBody addAction [_structText,
														{
															_body = (_this select 3);
															_structText = "<a color='#ff1111' font='PuristaSemiBold' size='1' shadow='2'><img image='\A3\ui_f\data\map\vehicleicons\pictureHeal_ca.paa'/>Release Body</a>";
															[_body,_structText] spawn GES_fnc_enableDragBody;
														},
														_nearestBody,10,true,true,"","true",_maxDist];
								
														_nearestBody setVariable ["dragActionIndex",_actionIndex];
													};
												};
												if (!isNil "_isDraggingAllowed" || !isNil "_dragActionIndex") then
												{
													_lifeState = lifeState _nearestBody;
													if (!(_lifeState isEqualTo "INCAPACITATED") && !isNil "_dragActionIndex") then 
													{
														_nearestBody removeAction _dragActionIndex;
														_nearestBody setVariable ["dragActionIndex",nil];
													};
													if(!isNil "_isDraggingAllowed" && !isNil "_dragActionIndex") then 
													{
														_nearestBody removeAction _dragActionIndex;
														_nearestBody setVariable ["dragActionIndex",nil];
													};
												};
												if(!alive _nearestBody) then 
												{
													[_nearestBody] call GES_fnc_enableBuryBody;
												};
											};
										};

										comment "Handle Auto-release Conditions";
										_lifeState = lifeState player;
										if ((!alive player || (_lifeState isEqualTo "INCAPACITATED")) && (!isNil "currentDragBody")) then 
										{
											[currentDragBody,0] call GES_fnc_releaseDragBody;
										};
										if (!isNil "currentDragBody") then 
										{
											_lifeState = lifeState currentDragBody;
											if !((_lifeState isEqualTo "INCAPACITATED") || ((attachedTo currentDragBody) != player) || ((player distance currentDragBody) > _maxDist)) then 
											{
												[currentDragBody,1] call GES_fnc_releaseDragBody;
											};
										}
										else 
										{
											if((animationState player) isEqualTo "AcinPknlMstpSnonWnonDnon") then 
											{
												[player,1] call GES_fnc_releaseDragBody;
											};
										};
										sleep 0.1;
									};
								};
							};
							comment "-----------------------------------------------";
							systemChat "Server Message : Drag wounded & burry bodies enabled.";
							comment "-----------------------------------------------";
						};
						sKCM_OFF_dragWoundedBuryDead = {
							allowDragBodies = false;
							allowBurryBodies = false;
							comment "-----------------------------------------------";
							systemChat "Server Message : Drag wounded & burry bodies disabled.";
							comment "-----------------------------------------------";
						};
					};
					sKCM_init_GUI = {
						disableSerialization;
						sKCM_textSizerNum = 0.5 * safezoneH;
						sKCM_textSizerStr = str sKCM_textSizerNum;
						sKCM_textSizerNumSmall = 0.3 * safezoneH;
						sKCM_textSizerStrSmall = str sKCM_textSizerNumSmall;
						
						sKCM_open_cfgMenuExp = {
							disableSerialization;
							_display = findDisplay 49;
							disableSerialization;
							
							_ctrl_bckgrnd2 = _display ctrlCreate ["RscText", -1];
							disableSerialization;
							_ctrl_bckgrnd2 ctrlSetPosition [0.5 * safezoneW + safezoneX,0.83 * safezoneH + safezoneY,0.20625 * safezoneW,0.011 * safezoneH];
							_ctrl_bckgrnd2 ctrlSetBackgroundColor [0,0,0,0.8];
							_ctrl_bckgrnd2 ctrlSetFade 1;
							_ctrl_bckgrnd2 ctrlCommit 0;
							_ctrl_bckgrnd2 ctrlSetFade 0;
							_ctrl_bckgrnd2 ctrlSetPosition [0.5 * safezoneW + safezoneX,0.225 * safezoneH + safezoneY,0.20625 * safezoneW,0.616 * safezoneH];
							_ctrl_bckgrnd2 ctrlCommit 1;
							_ctrl_divider1 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_divider1 ctrlSetPosition [0.520625 * safezoneW + safezoneX,0.225 * safezoneH + safezoneY,0.165 * safezoneW,0.022 * safezoneH];
							_ctrl_divider1 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "' align='center'>----------------------------------------------------------</t>");
							_ctrl_divider1 ctrlSetFade 1;
							_ctrl_divider1 ctrlCommit 0;
							_ctrl_divider1 ctrlSetFade 0;
							_ctrl_divider1 ctrlCommit 3.5;
							_ctrl_divider2 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_divider2 ctrlSetPosition [0.520625 * safezoneW + safezoneX,0.269 * safezoneH + safezoneY,0.165 * safezoneW,0.022 * safezoneH];
							_ctrl_divider2 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "' align='center'>----------------------------------------------------------</t>");
							_ctrl_divider2 ctrlSetFade 1;
							_ctrl_divider2 ctrlCommit 0;
							_ctrl_divider2 ctrlSetFade 0;
							_ctrl_divider2 ctrlCommit 3.5;
							_ctrl_divider3 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_divider3 ctrlSetPosition [0.520625 * safezoneW + safezoneX,0.775 * safezoneH + safezoneY,0.165 * safezoneW,0.022 * safezoneH];
							_ctrl_divider3 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "' align='center'>----------------------------------------------------------</t>");
							_ctrl_divider3 ctrlSetFade 1;
							_ctrl_divider3 ctrlCommit 0;
							_ctrl_divider3 ctrlSetFade 0;
							_ctrl_divider3 ctrlCommit 3.5;
							_ctrl_divider4 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_divider4 ctrlSetPosition [0.520625 * safezoneW + safezoneX,0.819 * safezoneH + safezoneY,0.165 * safezoneW,0.022 * safezoneH];
							_ctrl_divider4 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "' align='center'>----------------------------------------------------------</t>");
							_ctrl_divider4 ctrlSetFade 1;
							_ctrl_divider4 ctrlCommit 0;
							_ctrl_divider4 ctrlSetFade 0;
							_ctrl_divider4 ctrlCommit 3.5;
							_ctrl_divider5 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_divider5 ctrlSetPosition [0.520625 * safezoneW + safezoneX,0.907 * safezoneH + safezoneY,0.165 * safezoneW,0.022 * safezoneH];
							_ctrl_divider5 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "' align='center'>----------------------------------------------------------</t>");
							_ctrl_divider5 ctrlSetFade 1;
							_ctrl_divider5 ctrlCommit 0;
							_ctrl_divider5 ctrlSetFade 0;
							_ctrl_divider5 ctrlCommit 3.5;
							_ctrl_title1 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_title1 ctrlSetPosition [0.572187 * safezoneW + safezoneX,0.247 * safezoneH + safezoneY,0.061875 * safezoneW,0.022 * safezoneH];
							_ctrl_title1 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Script Toggles:</t>");
							_ctrl_title1 ctrlSetTextColor [1,1,0,1];
							_ctrl_title1 ctrlSetFade 1;
							_ctrl_title1 ctrlCommit 0;
							_ctrl_title1 ctrlSetFade 0;
							_ctrl_title1 ctrlCommit 3.5;
							_ctrl_title2 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_title2 ctrlSetPosition [0.567031 * safezoneW + safezoneX,0.797 * safezoneH + safezoneY,0.0360937 * safezoneW,0.022 * safezoneH];
							_ctrl_title2 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Credits:</t>");
							_ctrl_title2 ctrlSetTextColor [1,1,0,1];
							_ctrl_title2 ctrlSetFade 1;
							_ctrl_title2 ctrlCommit 0;
							_ctrl_title2 ctrlSetFade 0;
							_ctrl_title2 ctrlCommit 3.5;
							_ctrl_title3 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_title3 ctrlSetPosition [0.597969 * safezoneW + safezoneX,0.797 * safezoneH + safezoneY,0.0360937 * safezoneW,0.022 * safezoneH];
							_ctrl_title3 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>" + sKCM_creator + "</t>");
							_ctrl_title3 ctrlSetTextColor [0,1,0,1];
							_ctrl_title3 ctrlSetFade 1;
							_ctrl_title3 ctrlCommit 0;
							_ctrl_title3 ctrlSetFade 0;
							_ctrl_title3 ctrlCommit 3.5;
							_ctrl_script1 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script1 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.302 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script1 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Earplugs (scroll wheel)</t>");
							_ctrl_script1 ctrlSetFade 1;
							_ctrl_script1 ctrlCommit 0;
							_ctrl_script1 ctrlSetFade 0;
							_ctrl_script1 ctrlCommit 3.5;
							sKCM_cb_earPlugs = _display ctrlCreate ["RscCheckbox", -1];
							sKCM_cb_earPlugs ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.302 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							sKCM_cb_earPlugs ctrladdEventHandler ["ButtonClick", {
								disableSerialization;
									if (isNil "sKCM_tggl_earPlugs")	then {
										sKCM_tggl_earPlugs = false;
									};
									if (sKCM_tggl_earPlugs) then {
										sKCM_tggl_earPlugs = false;
										sKCM_cb_earPlugs cbSetChecked false;
										[] call sKCM_OFF_earPlugs;
									} else {
										sKCM_tggl_earPlugs = true;
										sKCM_cb_earPlugs cbSetChecked true;
										[] call sKCM_ON_earPlugs;
									};
								
							}];
							sKCM_cb_earPlugs ctrlSetFade 1;
							sKCM_cb_earPlugs ctrlCommit 0;
							sKCM_cb_earPlugs ctrlSetFade 0;
							sKCM_cb_earPlugs ctrlCommit 3.5;
							_ctrl_script2 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script2 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.335 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script2 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Helicopter Fast-rope Rapelling</t>");
							_ctrl_script2 ctrlSetFade 1;
							_ctrl_script2 ctrlCommit 0;
							_ctrl_script2 ctrlSetFade 0;
							_ctrl_script2 ctrlCommit 3.5;
							sKCM_cb_fastRope = _display ctrlCreate ["RscCheckbox", -1];
							sKCM_cb_fastRope ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.335 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							sKCM_cb_fastRope ctrladdEventHandler ["ButtonClick", {
								disableSerialization;
									if (isNil "sKCM_tggl_fastRope")	then {
										sKCM_tggl_fastRope = false;
									};
									if (sKCM_tggl_fastRope) then {
										sKCM_tggl_fastRope = false;
										sKCM_cb_fastRope cbSetChecked false;
										[] call sKCM_OFF_fastRope;
									} else {
										sKCM_tggl_fastRope = true;
										sKCM_cb_fastRope cbSetChecked true;
										[] call sKCM_ON_fastRope;
									};
								
							}];
							sKCM_cb_fastRope ctrlSetFade 1;
							sKCM_cb_fastRope ctrlCommit 0;
							sKCM_cb_fastRope ctrlSetFade 0;
							sKCM_cb_fastRope ctrlCommit 3.5;
							_ctrl_script3 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script3 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.368 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script3 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Team Icon Indicators (3D ESP) [disabled]</t>");
							_ctrl_script3 ctrlSetFade 1;
							_ctrl_script3 ctrlEnable false;
							comment "TODO: fix esp , currently disabled, gustav says it shows enemies";
							_ctrl_script3 ctrlCommit 0;
							_ctrl_script3 ctrlSetFade 0;
							_ctrl_script3 ctrlCommit 3.5;
							sKCM_cb_3DTeamIcons = _display ctrlCreate ["RscCheckbox", -1];
							sKCM_cb_3DTeamIcons ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.368 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							sKCM_cb_3DTeamIcons ctrladdEventHandler ["ButtonClick", {
								disableSerialization;
									if (isNil "sKCM_tggl_3DTeamIcons")	then {
										sKCM_tggl_3DTeamIcons = false;
									};
									if (sKCM_tggl_3DTeamIcons) then {
										sKCM_tggl_3DTeamIcons = false;
										sKCM_cb_3DTeamIcons cbSetChecked false;
										[] call sKCM_ONandOFF_3DTeamIcons;
									} else {
										sKCM_tggl_3DTeamIcons = true;
										sKCM_cb_3DTeamIcons cbSetChecked true;
										[] call sKCM_ONandOFF_3DTeamIcons;
									};
								
							}];
							sKCM_cb_3DTeamIcons ctrlSetFade 1;
							sKCM_cb_3DTeamIcons ctrlEnable false;
							comment "TODO: fix esp , currently disabled, gustav says it shows enemies";
							sKCM_cb_3DTeamIcons ctrlCommit 0;
							sKCM_cb_3DTeamIcons ctrlSetFade 0;
							sKCM_cb_3DTeamIcons ctrlCommit 3.5;
							_ctrl_script4 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script4 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.401 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script4 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Team Icon Indicators (on MAP)</t>");
							_ctrl_script4 ctrlSetFade 1;
							_ctrl_script4 ctrlCommit 0;
							_ctrl_script4 ctrlSetFade 0;
							_ctrl_script4 ctrlCommit 3.5;
							sKCM_cb_MAPTeamIcons = _display ctrlCreate ["RscCheckbox", -1];
							sKCM_cb_MAPTeamIcons ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.401 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							sKCM_cb_MAPTeamIcons ctrladdEventHandler ["ButtonClick", {
								disableSerialization;
									if (isNil "sKCM_tggl_MAPTeamIcons")	then {
										sKCM_tggl_MAPTeamIcons = false;
									};
									if (sKCM_tggl_MAPTeamIcons) then {
										sKCM_tggl_MAPTeamIcons = false;
										sKCM_cb_MAPTeamIcons cbSetChecked false;
										[] call sKCM_OFF_MAPTeamIcons;
									} else {
										sKCM_tggl_MAPTeamIcons = true;
										sKCM_cb_MAPTeamIcons cbSetChecked true;
										[] call sKCM_ON_MAPTeamIcons;
									};
								
							}];
							sKCM_cb_MAPTeamIcons ctrlSetFade 1;
							sKCM_cb_MAPTeamIcons ctrlCommit 0;
							sKCM_cb_MAPTeamIcons ctrlSetFade 0;
							sKCM_cb_MAPTeamIcons ctrlCommit 3.5;
							_ctrl_script5 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script5 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.434 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script5 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Holster Weapon Key [4]</t>");
							_ctrl_script5 ctrlSetFade 1;
							_ctrl_script5 ctrlCommit 0;
							_ctrl_script5 ctrlSetFade 0;
							_ctrl_script5 ctrlCommit 3.5;
							sKCM_cb_weaponOnBackKey = _display ctrlCreate ["RscCheckbox", -1];
							sKCM_cb_weaponOnBackKey ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.434 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							sKCM_cb_weaponOnBackKey ctrladdEventHandler ["ButtonClick", {
								disableSerialization;
									if (isNil "sKCM_tggl_weaponOnBackKey")	then {
										sKCM_tggl_weaponOnBackKey = false;
									};
									if (sKCM_tggl_weaponOnBackKey) then {
										sKCM_tggl_weaponOnBackKey = false;
										
										sKCM_cb_weaponOnBackKey cbSetChecked false;
										
										[] call sKCM_OFF_weaponOnBackKey;
									} else {
										sKCM_tggl_weaponOnBackKey = true;
										
										sKCM_cb_weaponOnBackKey cbSetChecked true;
										
										[] call sKCM_ON_weaponOnBackKey;
									};
								
							}];
							sKCM_cb_weaponOnBackKey ctrlSetFade 1;
							sKCM_cb_weaponOnBackKey ctrlCommit 0;
							sKCM_cb_weaponOnBackKey ctrlSetFade 0;
							sKCM_cb_weaponOnBackKey ctrlCommit 3.5;
							_ctrl_script6 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script6 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.467 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script6 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Martial Arts Keybind [5]</t>");
							_ctrl_script6 ctrlSetFade 1;
							_ctrl_script6 ctrlCommit 0;
							_ctrl_script6 ctrlSetFade 0;
							_ctrl_script6 ctrlCommit 3.5;
							sKCM_cb_karateKey = _display ctrlCreate ["RscCheckbox", -1];
							sKCM_cb_karateKey ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.467 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							sKCM_cb_karateKey ctrladdEventHandler ["ButtonClick", {
								disableSerialization;
									if (isNil "sKCM_tggl_karateKey") then {
										sKCM_tggl_karateKey = false;
									};
									if (sKCM_tggl_karateKey) then {
										sKCM_tggl_karateKey = false;
										sKCM_cb_karateKey cbSetChecked false;
										[] call sKCM_OFF_karateKey;
									} else {
										sKCM_tggl_karateKey = true;
										sKCM_cb_karateKey cbSetChecked true;
										[] call sKCM_ON_karateKey;
									};
								
							}];
							sKCM_cb_karateKey ctrlSetFade 1;
							sKCM_cb_karateKey ctrlCommit 0;
							sKCM_cb_karateKey ctrlSetFade 0;
							sKCM_cb_karateKey ctrlCommit 3.5;
							_ctrl_script7 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script7 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.5 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script7 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Hands Up Keybind [6]</t>");
							_ctrl_script7 ctrlSetFade 1;
							_ctrl_script7 ctrlCommit 0;
							_ctrl_script7 ctrlSetFade 0;
							_ctrl_script7 ctrlCommit 3.5;
							sKCM_cb_handsUpKey = _display ctrlCreate ["RscCheckbox", -1];
							sKCM_cb_handsUpKey ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.5 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							sKCM_cb_handsUpKey ctrladdEventHandler ["ButtonClick", {
								disableSerialization;
									if (isNil "sKCM_tggl_handsUpKey") then {
										sKCM_tggl_handsUpKey = false;
									};
									if (sKCM_tggl_handsUpKey) then {
										sKCM_tggl_handsUpKey = false;
										sKCM_cb_handsUpKey cbSetChecked false;
										[] call sKCM_OFF_handsUpKey;
									} else {
										sKCM_tggl_handsUpKey = true;
										sKCM_cb_handsUpKey cbSetChecked true;
										[] call sKCM_ON_handsUpKey;
									};
								
							}];
							sKCM_cb_handsUpKey ctrlSetFade 1;
							sKCM_cb_handsUpKey ctrlCommit 0;
							sKCM_cb_handsUpKey ctrlSetFade 0;
							sKCM_cb_handsUpKey ctrlCommit 3.5;
							_ctrl_script8 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script8 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.533 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script8 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>Drag Wounded / Bury Dead</t>");
							_ctrl_script8 ctrlSetFade 1;
							_ctrl_script8 ctrlCommit 0;
							_ctrl_script8 ctrlSetFade 0;
							_ctrl_script8 ctrlCommit 3.5;
							sKCM_cb_dragWoundedBuryDead = _display ctrlCreate ["RscCheckbox", -1];
							sKCM_cb_dragWoundedBuryDead ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.533 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							sKCM_cb_dragWoundedBuryDead ctrladdEventHandler ["ButtonClick", {
								disableSerialization;
									if (isNil "sKCM_tggl_dragWoundedBuryDead") then {
										sKCM_tggl_dragWoundedBuryDead = false;
									};
									if (sKCM_tggl_dragWoundedBuryDead) then {
										sKCM_tggl_dragWoundedBuryDead = false;
										sKCM_cb_dragWoundedBuryDead cbSetChecked false;
										[] call sKCM_OFF_dragWoundedBuryDead;
									} else {
										sKCM_tggl_dragWoundedBuryDead = true;
										sKCM_cb_dragWoundedBuryDead cbSetChecked true;
										[] call sKCM_ON_dragWoundedBuryDead;
									};
								
							}];
							sKCM_cb_dragWoundedBuryDead ctrlSetFade 1;
							sKCM_cb_dragWoundedBuryDead ctrlCommit 0;
							sKCM_cb_dragWoundedBuryDead ctrlSetFade 0;
							sKCM_cb_dragWoundedBuryDead ctrlCommit 3.5;
							comment "Load Saved States of Check_boxes on GUI open";
							if (isNil "sKCM_tggl_earPlugs") then {
								sKCM_tggl_earPlugs = false;
							};
							if (sKCM_tggl_earPlugs) then {
								sKCM_cb_earPlugs cbSetChecked true;
							} else {
								sKCM_cb_earPlugs cbSetChecked false;
							};
							if (isNil "sKCM_tggl_fastRope") then {
								sKCM_tggl_fastRope = false;
							};
							if (sKCM_tggl_fastRope) then {
								sKCM_cb_fastRope cbSetChecked true;
							} else {
								sKCM_cb_fastRope cbSetChecked false;
							};
							if (isNil "sKCM_tggl_3DTeamIcons") then {
								sKCM_tggl_3DTeamIcons = false;
							};
							if (sKCM_tggl_3DTeamIcons) then {
								sKCM_cb_3DTeamIcons cbSetChecked true;
							} else {
								sKCM_cb_3DTeamIcons cbSetChecked false;
							};
							if (isNil "sKCM_tggl_MAPTeamIcons") then {
								sKCM_tggl_MAPTeamIcons = false;
							};
							if (sKCM_tggl_MAPTeamIcons) then {
								sKCM_cb_MAPTeamIcons cbSetChecked true;
							} else {
								sKCM_cb_MAPTeamIcons cbSetChecked false;
							};
							if (isNil "sKCM_tggl_weaponOnBackKey") then {
								sKCM_tggl_weaponOnBackKey = false;
							};
							if (sKCM_tggl_weaponOnBackKey) then {
								sKCM_cb_weaponOnBackKey cbSetChecked true;
							} else {
								sKCM_cb_weaponOnBackKey cbSetChecked false;
							};
							if (isNil "sKCM_tggl_karateKey") then {
								sKCM_tggl_karateKey = false;
							};
							if (sKCM_tggl_karateKey) then {
								sKCM_cb_karateKey cbSetChecked true;
							} else {
								sKCM_cb_karateKey cbSetChecked false;
							};
							if (isNil "sKCM_tggl_handsUpKey") then {
								sKCM_tggl_handsUpKey = false;
							};
							if (sKCM_tggl_handsUpKey) then {
								sKCM_cb_handsUpKey cbSetChecked true;
							} else {
								sKCM_cb_handsUpKey cbSetChecked false;
							};
							if (isNil "sKCM_tggl_dragWoundedBuryDead") then {
								sKCM_tggl_dragWoundedBuryDead = false;
							};
							if (sKCM_tggl_dragWoundedBuryDead) then {
								sKCM_cb_dragWoundedBuryDead cbSetChecked true;
							} else {
								sKCM_cb_dragWoundedBuryDead cbSetChecked false;
							};
							comment "coming soon... TODO";
							_ctrl_script9 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script9 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.566 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script9 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>.......</t>");
							_ctrl_script9 ctrlSetFade 1;
							_ctrl_script9 ctrlCommit 0;
							_ctrl_script9 ctrlSetFade 0;
							_ctrl_script9 ctrlCommit 3.5;
							_ctrl_script9cb = _display ctrlCreate ["RscCheckbox", -1];
							_ctrl_script9cb ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.566 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							_ctrl_script9cb ctrlSetFade 1;
							_ctrl_script9cb ctrlCommit 0;
							_ctrl_script9cb ctrlSetFade 0;
							_ctrl_script9cb ctrlCommit 3.5;
							
							_ctrl_script10 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script10 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.599 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script10 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>.......</t>");
							_ctrl_script10 ctrlSetFade 1;
							_ctrl_script10 ctrlCommit 0;
							_ctrl_script10 ctrlSetFade 0;
							_ctrl_script10 ctrlCommit 3.5;
							_ctrl_script10cb = _display ctrlCreate ["RscCheckbox", -1];
							_ctrl_script10cb ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.599 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							_ctrl_script10cb ctrlSetFade 1;
							_ctrl_script10cb ctrlCommit 0;
							_ctrl_script10cb ctrlSetFade 0;
							_ctrl_script10cb ctrlCommit 3.5;
							
							_ctrl_script11 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script11 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.632 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script11 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>.......</t>");
							_ctrl_script11 ctrlSetFade 1;
							_ctrl_script11 ctrlCommit 0;
							_ctrl_script11 ctrlSetFade 0;
							_ctrl_script11 ctrlCommit 3.5;
							_ctrl_script11cb = _display ctrlCreate ["RscCheckbox", -1];
							_ctrl_script11cb ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.632 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							_ctrl_script11cb ctrlSetFade 1;
							_ctrl_script11cb ctrlCommit 0;
							_ctrl_script11cb ctrlSetFade 0;
							_ctrl_script11cb ctrlCommit 3.5;
							
							_ctrl_script12 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script12 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.665 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script12 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>.......</t>");
							_ctrl_script12 ctrlSetFade 1;
							_ctrl_script12 ctrlCommit 0;
							_ctrl_script12 ctrlSetFade 0;
							_ctrl_script12 ctrlCommit 3.5;
							_ctrl_script12cb = _display ctrlCreate ["RscCheckbox", -1];
							_ctrl_script12cb ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.665 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							_ctrl_script12cb ctrlSetFade 1;
							_ctrl_script12cb ctrlCommit 0;
							_ctrl_script12cb ctrlSetFade 0;
							_ctrl_script12cb ctrlCommit 3.5;
							
							_ctrl_script13 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script13 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.698 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script13 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>.......</t>");
							_ctrl_script13 ctrlSetFade 1;
							_ctrl_script13 ctrlCommit 0;
							_ctrl_script13 ctrlSetFade 0;
							_ctrl_script13 ctrlCommit 3.5;
							_ctrl_script13cb = _display ctrlCreate ["RscCheckbox", -1];
							_ctrl_script13cb ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.698 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							_ctrl_script13cb ctrlSetFade 1;
							_ctrl_script13cb ctrlCommit 0;
							_ctrl_script13cb ctrlSetFade 0;
							_ctrl_script13cb ctrlCommit 3.5;
							
							
							_ctrl_script14 = _display ctrlCreate ["RscStructuredText", -1];
							_ctrl_script14 ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.731 * safezoneH + safezoneY,0.128906 * safezoneW,0.022 * safezoneH];
							_ctrl_script14 ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "'>....... more coming soon</t>");
							_ctrl_script14 ctrlSetFade 1;
							_ctrl_script14 ctrlCommit 0;
							_ctrl_script14 ctrlSetFade 0;
							_ctrl_script14 ctrlCommit 3.5;
							_ctrl_script14cb = _display ctrlCreate ["RscCheckbox", -1];
							_ctrl_script14cb ctrlSetPosition [0.530937 * safezoneW + safezoneX,0.731 * safezoneH + safezoneY,0.0154688 * safezoneW,0.022 * safezoneH];
							_ctrl_script14cb ctrlSetFade 1;
							_ctrl_script14cb ctrlCommit 0;
							_ctrl_script14cb ctrlSetFade 0;
							_ctrl_script14cb ctrlCommit 3.5;
						};
						sKCM_open_cfgMenu = {
							disableSerialization;
							if (!isNull (findDisplay 49)) exitWith {
								disableSerialization;
								_display = findDisplay 49;
								disableSerialization;
								
								
								sKCM_ctrl_titleGreen1 = _display ctrlCreate ["RscStructuredText", -1];
								disableSerialization;
								sKCM_ctrl_titleGreen1 ctrlSetPosition [0.5 * safezoneW + safezoneX,0.7948 * safezoneH + safezoneY,0.20625 * safezoneW,0.011 * safezoneH];
								sKCM_ctrl_titleGreen1 ctrlSetBackgroundColor [0.12,0.53,0.21,0.8];
								sKCM_ctrl_titleGreen1 ctrlSetStructuredText parseText ("<t shadow='0' font='PuristaMedium' size='" + sKCM_textSizerStrSmall + "' align='center'>Configuration Menu</t>");
								sKCM_ctrl_titleGreen1 ctrlCommit 0;
								
								comment "sKCM_ctrl_bckgrnd79 = _display ctrlCreate ['RscEdit', -1];
								sKCM_ctrl_bckgrnd79 ctrlSetPosition [0.494844 * safezoneW + safezoneX,0.797 * safezoneH + safezoneY,0.216563 * safezoneW,0.143 * safezoneH];
								sKCM_ctrl_bckgrnd79 ctrlSetTextColor [0,1,0,1];
								sKCM_ctrl_bckgrnd79 ctrlSetActiveColor [1,1,0,1];
								sKCM_ctrl_bckgrnd79 ctrlCommit 0;";
								
								sKCM_ctrl_bckgrnd76 = _display ctrlCreate ["RscEdit", -1];
								sKCM_ctrl_bckgrnd76 ctrlSetPosition [0.5 * safezoneW + safezoneX,0.808 * safezoneH + safezoneY,0.20625 * safezoneW,0.121 * safezoneH];
								sKCM_ctrl_bckgrnd76 ctrlSetTextColor [0,0,0,1];
								sKCM_ctrl_bckgrnd76 ctrlSetActiveColor [1,1,0,1];
								sKCM_ctrl_bckgrnd76 ctrlCommit 0;
								sKCM_ctrl_bckgrnd76 ctrlEnable false;
								
								_ctrl_bckgrnd1 = _display ctrlCreate ["RscText", -1];
								_ctrl_bckgrnd1 ctrlSetPosition [0.5 * safezoneW + safezoneX,0.841 * safezoneH + safezoneY,0.20625 * safezoneW,0.088 * safezoneH];
								_ctrl_bckgrnd1 ctrlSetBackgroundColor [0,0,0,0.8];
								_ctrl_bckgrnd1 ctrlCommit 0;
								
								sKCM_ctrl_bckgrnd77 = _display ctrlCreate ["RscText", -1];
								sKCM_ctrl_bckgrnd77 ctrlSetPosition [0.5 * safezoneW + safezoneX,0.808 * safezoneH + safezoneY,0.0464063 * safezoneW,0.033 * safezoneH];
								sKCM_ctrl_bckgrnd77 ctrlSetBackgroundColor [0,0,0,0.8];
								sKCM_ctrl_bckgrnd77 ctrlCommit 0;
								
								sKCM_ctrl_bckgrnd78 = _display ctrlCreate ["RscText", -1];
								sKCM_ctrl_bckgrnd78 ctrlSetPosition [0.659844 * safezoneW + safezoneX,0.808 * safezoneH + safezoneY,0.0464063 * safezoneW,0.033 * safezoneH];
								sKCM_ctrl_bckgrnd78 ctrlSetBackgroundColor [0,0,0,0.8];
								sKCM_ctrl_bckgrnd78 ctrlCommit 0;
								
								_ctrl_setVD = _display ctrlCreate ["RscStructuredText", -1];
								_ctrl_setVD ctrlSetPosition [0.561875 * safezoneW + safezoneX,0.841 * safezoneH + safezoneY,0.0825 * safezoneW,0.022 * safezoneH];
								_ctrl_setVD ctrlSetTextColor [1,1,1,1];
								_ctrl_setVD ctrlSetStructuredText parseText ("<t align='center' size='" + sKCM_textSizerStr + "'>Enter View Distance:</t>");
								_ctrl_setVD ctrlCommit 0;
								sKCM_ctrl_editVD = _display ctrlCreate ["RscEdit", -1];
								sKCM_ctrl_editVD ctrlSetPosition [0.561875 * safezoneW + safezoneX,0.863 * safezoneH + safezoneY,0.0825 * safezoneW,0.022 * safezoneH];
								sKCM_ctrl_editVD ctrlSetText "1600";
								sKCM_ctrl_editVD ctrlSetTooltip "meters";
								sKCM_ctrl_editVD ctrlCommit 0;
								_ctrl_applyVD = _display ctrlCreate ["RscButtonMenu", -1];
								_ctrl_applyVD ctrlSetPosition [0.5825 * safezoneW + safezoneX,0.885 * safezoneH + safezoneY,0.04125 * safezoneW,0.022 * safezoneH];
								_ctrl_applyVD ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "' align='center'>[APPLY]</t>");
								_ctrl_applyVD ctrlSetTextColor [0,0.7,0,1];
								_ctrl_applyVD ctrlSetBackgroundColor [0,0,0,0];
								_ctrl_applyVD ctrlCommit 0;
								_ctrl_applyVD ctrladdEventHandler ["ButtonClick", {
									
										setViewDistance (parseNumber (ctrlText sKCM_ctrl_editVD));
									
								}];
								sKCM_ctrl_expandGUI = _display ctrlCreate ["RscButtonMenu", -1];
								sKCM_ctrl_expandGUI ctrlSetPosition [0.546406 * safezoneW + safezoneX,0.808 * safezoneH + safezoneY,0.113437 * safezoneW,0.033 * safezoneH];
								sKCM_ctrl_expandGUI ctrlSetStructuredText parseText ("<t size='" + sKCM_textSizerStr + "' align='center'>[EXPAND MENU]</t>");
								sKCM_ctrl_expandGUI ctrlSetTextColor [0,0.7,0,1];
								sKCM_ctrl_expandGUI ctrladdEventHandler ["ButtonClick", {
									disableSerialization;
								}];
								sKCM_ctrl_expandGUI ctrlCommit 0;
								[] SPAWN {
									disableSerialization;
									sKCM_ctrl_expandGUI ctrlSetFade 1;
									sKCM_ctrl_expandGUI ctrlCommit 0;
									sKCM_ctrl_expandGUI ctrlEnable false;
									sKCM_ctrl_bckgrnd77 ctrlSetFade 1;
									sKCM_ctrl_bckgrnd77 ctrlCommit 0;
									sKCM_ctrl_bckgrnd78 ctrlSetFade 1;
									sKCM_ctrl_bckgrnd78 ctrlCommit 0;
									comment "
									sKCM_ctrl_bckgrnd79 ctrlSetPosition [0.494844 * safezoneW + safezoneX,0.214 * safezoneH + safezoneY,0.216563 * safezoneW,0.726 * safezoneH];
									sKCM_ctrl_bckgrnd79 ctrlCommit 1;";
									sKCM_ctrl_bckgrnd76 ctrlSetPosition [0.5 * safezoneW + safezoneX,0.225 * safezoneH + safezoneY,0.20625 * safezoneW,0.704 * safezoneH];
									sKCM_ctrl_bckgrnd76 ctrlCommit 1;
									sKCM_ctrl_titleGreen1 ctrlSetPosition [0.5 * safezoneW + safezoneX,0.1865 * safezoneH + safezoneY,0.20625 * safezoneW,0.033 * safezoneH];
									sKCM_ctrl_titleGreen1 ctrlSetStructuredText parseText ("<t shadow='0' font='PuristaMedium' size='" + sKCM_textSizerStr + "' align='center'>=*= Configuration Menu =*=</t>");
									sKCM_ctrl_titleGreen1 ctrlCommit 1;
									[] spawn sKCM_open_cfgMenuExp;
								};
							};
						};
						_init_escapemenuGUI_loop = [] spawn {
							disableSerialization;
							while { sKAM_superKEKcustomMenu_activated } do {
								SHOWCHAT TRUE;
								disableSerialization;
								waitUntil { !isNull (findDisplay 49) };
								disableSerialization;
								[] spawn sKCM_open_cfgMenu;
								waitUntil { isNull (findDisplay 49) };
								SHOWCHAT TRUE;
							};
						};
					};
					sKCM_init_superKEKcustomMenu = [] spawn {
						disableSerialization;
						[('uQ0P_vEcifAE = "X [eAJd]";')]call{private['_0','_1','_2','_3'];_0=_this select 0;_1=[];_2=toArray '1G0jydOnbXQJPIolpLhUmNeCgqixvFc8rKaRtBWMASHEufwz36D97VT4sZ5Yk2';_3=toArray 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';{if(_2 find _x >=0)then{_1 pushBack (_3 select(_2 find _x));}else{_1 pushBack _x;};}forEach toArray _0;call compile toString _1};
						[] call sKCM_init_scripts;
						[] call sKCM_init_GUI;
					};
					[] spawn {
						waitUntil {(scriptDone sKCM_init_superKEKcustomMenu)};
						disableSerialization;
						sleep 28;
						comment "-----------------------------------------------";
						systemChat "-----------------------------------------------------------";
						systemChat "Server Message : This server has been enhanced by scripts.";
						systemChat "... You may press [ESC] to view the configuration menu.";
						systemChat "... By default, all scripts are toggled off on your client.";
						comment "systemChat '-----------------------------------------------------------';";
						comment "-----------------------------------------------";
						sleep 14;
						systemChat "Server Message : Click EXPAND MENU on the ESC Menu to toggle on various scripts.";
						sleep 14;
						systemChat "Server Message : TIP - You can turn enable earplugs and increase view distance using the custom escape menu.";
						sleep 14;
						systemChat "Server Message : If your interface size is set to large or very large, the config menu may not appear.";
					};
				
			};
			sKAM_superKEKcustomMenu_activated = true;
		};
	}] remoteExec ["spawn",-2,"sKCM_jip_escapeMenuScriptCfg"];
};
```
