[Home](readme.md)
## This script opens a UI prompting to assign a curator.
### Created by J [WoLF] and M9-SD.
```sqf
comment "Script Title:

	Curator Creator (Create and Assign New Zeuses).

	< Current Version: 1.0 >
	
";
comment "Credits:
	Created by J [WoLF] and M9-SD.
";
comment "Description:
	- Creates new unique zeus module for specified players.
	- Assigns unique Zeus module to specified clients.
	- Automatically updates zeus interface with new objects.
	- Re-assigns zeus to player every respawn.
	- Re-assigns zeus to player upon reconnecting to the session.
	- JIP (join-in-progress) compatible.
";
comment "Usage:
	- Copy entire script. Paste in debug console.
	- Execute on local client.
	- Exit the pause menu if open.
	- Wait for GUI to appear.
	- Select recipients of the Zeus Interface.
	- Choose to remove or add interface. 
	- The selected players will now either be assigned or unassigned their unique Zeus module.
";
comment "Distribution:
	- You may share this script with anyone you want. 
	- Don't give this to trolls, please.
	- Give credit where it is due.
	- Enjoy :)
";

[] spawn 
{

	comment "-----------------------------------------------";
	if (!hasInterface) exitWith {};
	waitUntil { !isNil { player } && { !isNull player } };
	waitUntil { !isNull (findDisplay 46) };
	comment "-----------------------------------------------";
	
	systemChat "[JAM] >>> Zeus Helper >>> Initializing Curator Creator...";
	
	JAM_fnc_createAndAssignZeus = 
	{
	
		if (typeOf getAssignedCuratorLogic player != "") then {
		
			comment "do nothing";
			systemChat "[JAM] >>> Zeus Helper >>> You already have a zeus interface.";
			
		} else {

			JAM_fnc_createAssignCurator = 
			{
				comment "-----------------------------------------------";
				if (!hasInterface) exitWith {};
				waitUntil { !isNil { player } && { !isNull player } };
				waitUntil { !isNull (findDisplay 46) };
				comment "-----------------------------------------------";
				
				_myPlayer = _this # 0;
				
				_myCuratorPlayer = _myPlayer;
				
				JAM_addZeus_UID = getPlayerUID _myPlayer;
				
				JAM_addZeus_superCuratorVar = ("JAM_" + JAM_addZeus_UID + "_superCurator");
				
				JAM_addZeus_superCuratorPlayerAttributesVar = ("JAM_" + JAM_addZeus_UID + "_superCuratorPlayerAttributes");
				
				_JAM_my_curatorInitText = 
				("" + 
					"if (isNil """ + JAM_addZeus_superCuratorVar + """) then {" + 
						JAM_addZeus_superCuratorVar + " = JAM_superCurator_group createUnit ['ModuleCurator_F', [0, 90, 90],[],0.5,'NONE'];" + 
						JAM_addZeus_superCuratorVar + " setVehicleVarName '" + JAM_addZeus_superCuratorVar + "';" + 
						JAM_addZeus_superCuratorVar + " setVariable ['text','" + JAM_addZeus_superCuratorVar + "'];" + 
						JAM_addZeus_superCuratorVar + " setVariable ['Addons',3,true];" + 
						JAM_addZeus_superCuratorVar + " setVariable ['owner','objnull'];" + 
						JAM_addZeus_superCuratorVar + " setVariable ['vehicleinit',""
							_this setVariable ['Addons',3,true];
							_this setVariable ['owner','objnull'];
						""];" + 
						"unassignCurator " + JAM_addZeus_superCuratorVar + ";" + 
						"objnull assignCurator " + JAM_addZeus_superCuratorVar + ";" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " = JAM_superCurator_group createUnit ['ModuleCuratorSetAttributesPlayer_F', [2, 91, 91],[],0.5,'NONE'];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['curator','" + JAM_addZeus_superCuratorVar + "'];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['unitpos',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['fuel',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['respawnposition',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['respawnvehicle',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['skill',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['rank',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['damage',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['exec',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['lock',true];" + 
						JAM_addZeus_superCuratorPlayerAttributesVar + " setVariable ['vehicleinit',""
							_this setVariable ['curator','" + JAM_addZeus_superCuratorVar + "'];
							_this setVariable ['unitpos',true];
							_this setVariable ['fuel',true];
							_this setVariable ['respawnposition',true];
							_this setVariable ['respawnvehicle',true];
							_this setVariable ['skill',true];
							_this setVariable ['rank',true];
							_this setVariable ['damage',true];
							_this setVariable ['exec',true];
							_this setVariable ['lock',true];
						""];" + 
						"[" + JAM_addZeus_superCuratorVar + ",[-2,-1,0,1]] spawn BIS_fnc_setCuratorVisionModes;" + 
						"JAM_" + JAM_addZeus_UID + "_updateSuperCuratorEditableObjects = true;" + 
						"[] spawn {while {(JAM_" + JAM_addZeus_UID + "_updateSuperCuratorEditableObjects" + ")} do { if ( ((getAssignedCuratorUnit " + JAM_addZeus_superCuratorVar + ") != objNull) && (alive (getAssignedCuratorUnit " + JAM_addZeus_superCuratorVar + "))) then { " + JAM_addZeus_superCuratorVar + " addCuratorEditableObjects [([] call JAM_fnc_getEditableObjects),true]; }; sleep 30;}; };" + 
					"}; "
				+ "");
				
				[_JAM_my_curatorInitText,{
				
					_initText = _this;
					_initCode = compile _initText;
					
					if (isNil "JAM_blacklistedObjectsArray_01") then {
						JAM_blacklistedObjectsArray_01 = [
							"ModuleCurator_F",
							"ModuleCuratorSetCamera_F",
							"Logic",
							"ModuleHQ_F",
							"VirtualCurator_F",
							"ModuleCuratorSetModuleCosts_F",
							"ModuleCuratorAddPoints_F",
							"ModuleCuratorSetObjectCosts_F",
							"ModuleCuratorSetCosts_F",
							"ModuleCuratorSetCoefs_F",
							"ModuleCuratorSetDefaultCosts_F",
							"ModuleCuratorAddEditingAreaPlayers_F",
							"ModuleMPTypeGameMaster_F",
							"ModuleRadioChannelCreate_F",
							"ModuleCuratorSetAttributesPlayer_F"
						];
					};
					
					if (isNil "JAM_fnc_getEditableObjects") then {
						JAM_fnc_getEditableObjects = 
						{
							_allObjs = allMissionObjects 'all';
							_editableObjs = [];
							{
								if ( ( not ( ( typeOf _x ) in JAM_blacklistedObjectsArray_01 ) ) && ( not ( _x isKindOf "Logic" ) ) ) then {
									_editableObjs pushBackUnique _x;
								};
							} forEach _allObjs;
							_editableObjs;
						};
					};
					
					if (isNil "JAM_superCurator_group") then {
						JAM_superCurator_group = createGroup sideLogic;
					};
					
					[] spawn _initCode;
					
				}] remoteExec ['spawn',2];
				
				comment "JIP";
				
				[[JAM_addZeus_UID,JAM_addZeus_superCuratorVar],
				{
					comment "-----------------------------------------------";
					if (!hasInterface) exitWith {};
					waitUntil { !isNil { player } && { !isNull player } };
					waitUntil { !isNull (findDisplay 46) };
					comment "-----------------------------------------------";
					_curatorUID = _this # 0;
					_curatorVarStr = _this # 1;
					if (getPlayerUID player == _curatorUID) then {
						_curatorPlayer = player;
						JAM_my_curatorInitText = 
						("" + 
							"waitUntil {(not isNil """ + _curatorVarStr + """)}; " + 
							"_curatorVar = " + _curatorVarStr + "; " + 
							"_curatorPlayer = _this select 0; " + 
							"[_curatorVar,_curatorPlayer] spawn {
								_curatorVar = _this # 0;
								_curatorPlayer = _this # 1;
								while {((getAssignedCuratorLogic _curatorPlayer) != _curatorVar)} do {
									unassignCurator _curatorVar;
									objnull assignCurator _curatorVar;
									unassignCurator _curatorVar;
									_curatorPlayer assignCurator _curatorVar;
									sleep 3.5;
								};
							};" + 
							"JAM_" + _curatorUID + "_updateSuperCuratorEditableObjects = true;" + 
							"_curatorPlayer = _this select 0;
							'[JAM] >>> Zeus Helper >>> You were given Zeus interface. To open, press [Y].' remoteExec ['systemChat', _curatorPlayer];" + 
						"");
						[[JAM_my_curatorInitText,_curatorPlayer],{
							_initText = _this # 0;
							_curatorPlayer = _this # 1;
							_initCode = compile _initText;
							[_curatorPlayer] spawn _initCode;
						}] remoteExec ['spawn',2];
						
						comment "re-assign upon death/respawn";
						
						JAM_keepGivingMeZeus = true;
						
						if (!isNil "JAM_EH_autoReassignCuratorUponDeath") then {
							player removeEventHandler ["Respawn",JAM_EH_autoReassignCuratorUponDeath];
						};
						
						waitUntil {(alive _curatorPlayer)};
						
						JAM_EH_autoReassignCuratorUponDeath = player addEventHandler ["Respawn",{
							if (JAM_keepGivingMeZeus) then {
								[] spawn {
									waitUntil {(alive player)};
									sleep 3.5;
									[[JAM_my_curatorInitText,player],{
										_initText = _this # 0;
										_curatorPlayer = _this # 1;
										_initCode = compile _initText;
										[_curatorPlayer] spawn _initCode;
									}] remoteExec ['spawn',2];
								};
							};
						}];
						
						
					};
				}] remoteExec ['spawn',0,JAM_addZeus_superCuratorVar];

			};

			_target = player;

			[_target] spawn JAM_fnc_createAssignCurator;
			
		};
	};
	
	JAM_fnc_deleteAndUnassignZeus = 
	{
		if (typeOf getAssignedCuratorLogic player == "") then {
			comment "do nothing";
			systemChat "[JAM] >>> Zeus Helper >>> You already do not have a zeus interface.";
		} else {
			JAM_fnc_deleteUnassignCurator = 
			{
				comment "-----------------------------------------------";
				if (!hasInterface) exitWith {};
				waitUntil { !isNil { player } && { !isNull player } };
				waitUntil { !isNull (findDisplay 46) };
				comment "-----------------------------------------------";
				_myPlayer = _this # 0;
				_myCuratorPlayer = _myPlayer;
				JAM_addZeus_UID = getPlayerUID _myPlayer;
				JAM_addZeus_superCuratorVar = ("JAM_" + JAM_addZeus_UID + "_superCurator");
				JAM_addZeus_superCuratorPlayerAttributesVar = ("JAM_" + JAM_addZeus_UID + "_superCuratorPlayerAttributes");
				_JAM_my_curatorInitText = 
				("" + 
					"if (!isNil """ + JAM_addZeus_superCuratorVar + """) then {" + 
						"JAM_" + JAM_addZeus_UID + "_updateSuperCuratorEditableObjects = false;" + 
						"unassignCurator " + JAM_addZeus_superCuratorVar + ";" + 
						"objnull assignCurator " + JAM_addZeus_superCuratorVar + ";" + 
						"unassignCurator " + JAM_addZeus_superCuratorVar + "; sleep 0.1;" + 
						"comment 'deleteVehicle " + JAM_addZeus_superCuratorVar + ";';" + 
					"};" + 
					"if (!isNil """ + JAM_addZeus_superCuratorPlayerAttributesVar + """) then {" + 
						"comment 'deleteVehicle " + JAM_addZeus_superCuratorPlayerAttributesVar + ";';" + 
					"};" + 
				"");
				[_JAM_my_curatorInitText,{
					_initText = _this;
					_initCode = compile _initText;
					[] spawn _initCode;
				}] remoteExec ['spawn',2];
				comment "remove JIP";
				[[JAM_addZeus_UID,JAM_addZeus_superCuratorVar],
				{
					comment "-----------------------------------------------";
					if (!hasInterface) exitWith {};
					waitUntil { !isNil { player } && { !isNull player } };
					waitUntil { !isNull (findDisplay 46) };
					comment "-----------------------------------------------";
					_curatorUID = _this # 0;
					_curatorVarStr = _this # 1;
					if (getPlayerUID player == _curatorUID) then {
						_curatorPlayer = player;
						JAM_my_curatorInitText = 
						("" + 
							"_curatorPlayer = _this select 0;
							'[JAM] >>> Zeus Helper >>> Zeus Interface was removed from your client.' remoteExec ['systemChat', _curatorPlayer];"
						+ "");
						[[JAM_my_curatorInitText,_curatorPlayer],{
							_initText = _this # 0;
							_curatorPlayer = _this # 1;
							_initCode = compile _initText;
							[_curatorPlayer] spawn _initCode;
						}] remoteExec ['spawn',2];
						JAM_keepGivingMeZeus = false;
						[] spawn {
							if (not (isNull (findDisplay 312))) then {
								(findDisplay 312) closeDisplay 0;
							};
							waitUntil {(not (isNull (findDisplay 312)))};
							if (not JAM_keepGivingMeZeus) then {
								if (not (isNull (findDisplay 312))) then {
									(findDisplay 312) closeDisplay 0;
								};
							};
						};
						if (!isNil "JAM_EH_autoReassignCuratorUponDeath") then {
							player removeEventHandler ["Respawn",JAM_EH_autoReassignCuratorUponDeath];
						};
					};
				}] remoteExec ['spawn',0];
				[[],{}] remoteExec ['spawn',0,JAM_addZeus_superCuratorVar];
			};
			_target = player;
			[_target] spawn JAM_fnc_deleteUnassignCurator;
		};
	};
	
	JAM_curator_recipients = [];

	comment "check if player is Zeus";

	if (isNil "JAM_fnc_getDisplay46or312") then {
		JAM_fnc_getDisplay46or312 = {
			comment "default";
			_displayNumber = 46;
			if ((isNull (findDisplay 312)) && (not isNull (findDisplay 46))) then {
				_displayNumber = 46;
			};
			if (not isNull (findDisplay 312)) then {
				_displayNumber = 312;
			};
			comment "return value (display number)";
			_displayNumber
		};
	};

	comment "
		- Define critical variables.
			> JAM_txtSizeNum
			> JAM_txtSizeStr
	";
	JAM_txtSizeNum = 0.5 * safezoneH;
	JAM_txtSizeStr = str JAM_txtSizeNum;
	with uiNamespace do {
		JAM_txtSizeNum = 0.5 * safezoneH;
		JAM_txtSizeStr = str JAM_txtSizeNum;
	};
	with missionNamespace do {
		JAM_txtSizeNum = 0.5 * safezoneH;
		JAM_txtSizeStr = str JAM_txtSizeNum;
	};
	comment "
		...Variables Defined.
	";

	JAM_open_selectJAMZeusRecipients = 
	{
		JAM_curator_recipients = [];
		_centerScreenPos = [0.494844 * safezoneW + safezoneX,0.489 * safezoneH + safezoneY,0.004125 * safezoneW,0.0055 * safezoneH];
		disableSerialization;
		d_selectJAMZeusRecipients = (findDisplay ([] call JAM_fnc_getDisplay46or312)) createDisplay "RscDisplayEmpty";
		showChat true;

		_ctrl_selectJAMZeusRecipientsTitle = d_selectJAMZeusRecipients ctrlCreate ["RscStructuredText", -1];
		_ctrl_selectJAMZeusRecipientsTitle ctrlSetStructuredText parseText ("<t valign='middle' align='center' size='" + (str (JAM_txtSizeNum * 0.8)) + "'>ZEUS HELPER >>> CURATOR CREATOR<br/><t size='" + (str (JAM_txtSizeNum * 0.7)) + "'>(Create and Assign New Zeuses)<t/>");
		_ctrl_selectJAMZeusRecipientsTitle ctrlSetBackgroundColor [0,0,0,0.77];
		_ctrl_selectJAMZeusRecipientsTitle ctrlSetPosition _centerScreenPos;
		_ctrl_selectJAMZeusRecipientsTitle ctrlSetFade 1;
		_ctrl_selectJAMZeusRecipientsTitle ctrlCommit 0;
		_ctrl_selectJAMZeusRecipientsTitle ctrlSetPosition [0.427812 * safezoneW + safezoneX,0.313 * safezoneH + safezoneY,0.128906 * safezoneW,0.033 * safezoneH];
		_ctrl_selectJAMZeusRecipientsTitle ctrlSetFade 0;
		_ctrl_selectJAMZeusRecipientsTitle ctrlCommit 0.5;
		
		ctrl_sJr_PlayerList = d_selectJAMZeusRecipients ctrlCreate ["RscListBox", -1];
		{ _pL_index = ctrl_sJr_PlayerList lbAdd name _x; } forEach allPlayers;
		ctrl_sJr_PlayerList ctrlSetPosition _centerScreenPos;
		ctrl_sJr_PlayerList ctrlSetFade 1;
		ctrl_sJr_PlayerList ctrlCommit 0;
		ctrl_sJr_PlayerList ctrlSetPosition [0.427812 * safezoneW + safezoneX,0.379 * safezoneH + safezoneY,0.061875 * safezoneW,0.22 * safezoneH];
		ctrl_sJr_PlayerList ctrlSetFade 0;
		ctrl_sJr_PlayerList ctrlCommit 0.5;
		
		ctrl_sJr_recipientList = d_selectJAMZeusRecipients ctrlCreate ["RscListBox", -1];
		ctrl_sJr_recipientList ctrlSetPosition _centerScreenPos;
		ctrl_sJr_recipientList ctrlSetFade 1;
		ctrl_sJr_recipientList ctrlCommit 0;
		ctrl_sJr_recipientList ctrlSetPosition [0.494844 * safezoneW + safezoneX,0.379 * safezoneH + safezoneY,0.061875 * safezoneW,0.22 * safezoneH];
		ctrl_sJr_recipientList ctrlSetFade 0;
		ctrl_sJr_recipientList ctrlCommit 0.5;
		
		_ctrl_cancel = d_selectJAMZeusRecipients ctrlCreate ["RscButtonMenu", -1];
		_ctrl_cancel ctrlSetStructuredText parseText ("<t valign='middle' align='center' size='" + JAM_txtSizeStr + "'>CLOSE<t/>");
		_ctrl_cancel ctrlSetTooltip "Cancel the script and close this menu.";
		_ctrl_cancel ctrladdEventHandler ["ButtonClick",{
			d_selectJAMZeusRecipients closeDisplay 0;
			JAM_curator_recipients = [];
		}];
		_ctrl_cancel ctrlSetFade 1;
		_ctrl_cancel ctrlSetPosition _centerScreenPos;
		_ctrl_cancel ctrlCommit 0;
		_ctrl_cancel ctrlSetPosition [0.469063 * safezoneW + safezoneX,0.698 * safezoneH + safezoneY, 0.0464063 * safezoneW,0.022 * safezoneH];
		_ctrl_cancel ctrlSetFade 0;
		_ctrl_cancel ctrlCommit 0.5;

		_ctrl_removeJAMZeusbutton = d_selectJAMZeusRecipients ctrlCreate ["RscButtonMenu", -1];
		_ctrl_removeJAMZeusbutton ctrlSetStructuredText parseText ("<t valign='middle' align='center' size='" + JAM_txtSizeStr + "'>---------REMOVE ZEUS---------<t/>");
		_ctrl_removeJAMZeusbutton ctrlSetTooltip "Delete and unassign unique zeus module for each player on the right-hand list.";
		_ctrl_removeJAMZeusbutton ctrlSetBackgroundColor [0.5,0.2,0,0.6];
		_ctrl_removeJAMZeusbutton ctrladdEventHandler ["ButtonClick",{
			if (count JAM_curator_recipients != 0) then {
				d_selectJAMZeusRecipients closeDisplay 0;
				{
					_recipientName = _x;
					systemChat ("[JAM] >>> Zeus Helper >>> Removing Zeus from " + (_recipientName) + "...");
					{
						if ((name _x) == (_recipientName)) then {
							[JAM_fnc_deleteAndUnassignZeus,{
								_code = _this;
								[] spawn _code;
							}] remoteExec ['spawn',_x];
						};
					} forEach allPlayers;
				} forEach JAM_curator_recipients;
				comment "[] call JAM_init;";
			} else {
				hint "[JAM] : ERROR : You have not selected any players; Array is empty.";
				systemChat "[JAM] : ERROR : You have not selected any players; Array is empty.";
			};
		}];
		_ctrl_removeJAMZeusbutton ctrlSetPosition _centerScreenPos;
		_ctrl_removeJAMZeusbutton ctrlSetFade 1;
		_ctrl_removeJAMZeusbutton ctrlCommit 0;
		_ctrl_removeJAMZeusbutton ctrlSetPosition [0.432969 * safezoneW + safezoneX,0.654 * safezoneH + safezoneY,0.118594 * safezoneW,0.033 * safezoneH];
		_ctrl_removeJAMZeusbutton ctrlSetFade 0;
		_ctrl_removeJAMZeusbutton ctrlCommit 0.5;
		
		_ctrl_addBtn = d_selectJAMZeusRecipients ctrlCreate ["RscButtonMenu", -1];
		_ctrl_addBtn ctrlSetStructuredText parseText ("<t valign='middle' align='center' size='" + JAM_txtSizeStr + "'>Add<t/>");
		_ctrl_addBtn ctrlSetTooltip "Add selected player to the target list.";
		_ctrl_addBtn ctrlSetBackgroundColor [-1,0.5,-1,0.6];
		_ctrl_addBtn ctrladdEventHandler ["ButtonClick",{
			_selectedItem = lbCurSel ctrl_sJr_PlayerList;
			_playerName = ctrl_sJr_PlayerList lbText _selectedItem;
			if (JAM_curator_recipients find _playerName == -1) then {
				JAM_curator_recipients pushBackUnique _playerName;
				ctrl_sJr_recipientList lbAdd _playerName;
			};
		}];
		_ctrl_addBtn ctrlSetPosition _centerScreenPos;
		_ctrl_addBtn ctrlSetFade 1;
		_ctrl_addBtn ctrlCommit 0;
		_ctrl_addBtn ctrlSetPosition [0.427812 * safezoneW + safezoneX,0.357 * safezoneH + safezoneY,0.061875 * safezoneW,0.022 * safezoneH];
		_ctrl_addBtn ctrlSetFade 0;
		_ctrl_addBtn ctrlCommit 0.5;
		
		_ctrl_removeBtn = d_selectJAMZeusRecipients ctrlCreate ["RscButtonMenu", -1];
		_ctrl_removeBtn ctrlSetStructuredText parseText ("<t valign='middle' align='center' size='" + JAM_txtSizeStr + "'>Remove<t/>");
		_ctrl_removeBtn ctrlSetTooltip "Remove selected player from the target list.";
		_ctrl_removeBtn ctrlSetBackgroundColor [0.5,-1,-1,0.6];
		_ctrl_removeBtn ctrladdEventHandler ["ButtonClick",{
			_selectedItem = lbCurSel ctrl_sJr_recipientList;
			_playerName = ctrl_sJr_recipientList lbText _selectedItem;
			if (JAM_curator_recipients find _playerName > -1) then {
				_idx = JAM_curator_recipients find _playerName;
				JAM_curator_recipients deleteAt _idx;
				ctrl_sJr_recipientList lbDelete _selectedItem;
			};
		}];
		_ctrl_removeBtn ctrlSetPosition _centerScreenPos;
		_ctrl_removeBtn ctrlSetFade 1;
		_ctrl_removeBtn ctrlCommit 0;
		_ctrl_removeBtn ctrlSetPosition [0.494844 * safezoneW + safezoneX,0.357 * safezoneH + safezoneY,0.061875 * safezoneW,0.022 * safezoneH];
		_ctrl_removeBtn ctrlSetFade 0;
		_ctrl_removeBtn ctrlCommit 0.5;
		
		_ctrl_giveJAMZeusbutton = d_selectJAMZeusRecipients ctrlCreate ["RscButtonMenu", -1];
		_ctrl_giveJAMZeusbutton ctrlSetStructuredText parseText ("<t valign='middle' align='center' size='" + JAM_txtSizeStr + "'>------------GIVE ZEUS------------<t/>");
		_ctrl_giveJAMZeusbutton ctrlSetTooltip "Create and assign unique zeus module for each player on the right-hand list.";
		_ctrl_giveJAMZeusbutton ctrlSetBackgroundColor [-1,-1,0.4,0.6];
		_ctrl_giveJAMZeusbutton ctrladdEventHandler ["ButtonClick",{
			if (count JAM_curator_recipients != 0) then {
				d_selectJAMZeusRecipients closeDisplay 0;
				comment "[] call JAM_init;";
				{
					_recipientName = _x;
					systemChat ("[JAM] >>> Zeus Helper >>> Giving Zeus to " + (_recipientName) + "...");
					{
						if ((name _x) == (_recipientName)) then {
							[JAM_fnc_createAndAssignZeus,{
								_code = _this;
								[] spawn _code;
							}] remoteExec ['spawn',_x];
						};
					} forEach allPlayers;
				} forEach JAM_curator_recipients;
			} else {
				hint "[JAM] : ERROR : You have not selected any players; Array is empty.";
				systemChat "[JAM] : ERROR : You have not selected any players; Array is empty.";
			};
		}];
		_ctrl_giveJAMZeusbutton ctrlSetFade 1;
		_ctrl_giveJAMZeusbutton ctrlSetPosition _centerScreenPos;
		_ctrl_giveJAMZeusbutton ctrlCommit 0;
		_ctrl_giveJAMZeusbutton ctrlSetPosition [0.432969 * safezoneW + safezoneX,0.61 * safezoneH + safezoneY,0.118594 * safezoneW,0.033 * safezoneH];
		_ctrl_giveJAMZeusbutton ctrlSetFade 0;
		_ctrl_giveJAMZeusbutton ctrlCommit 0.5;
		
		systemChat "[JAM] >>> Zeus Helper >>> Select players to give or remove Zeus Interface.";
	};
	
	comment "close debug console";

	if ( not (isNull (findDisplay 49)) ) then {
		(findDisplay 49) closeDisplay 0;
	};
	
	waitUntil { isNull (findDisplay 49) };
	sleep 0.1;
	
	systemChat "[JAM] >>> Zeus Helper >>> Spawning GUI...";
	
	[] spawn JAM_open_selectJAMZeusRecipients;
	
};
```
