```sqf
fnc_createSelectionMenu = {
	sleep 3;
	createDialog "RscDisplayEmpty";
	
	_ctrl = findDisplay -1 ctrlCreate ["RscPicture",1000];
	_ctrl ctrlSetText "#(argb,8,8,3)color(1,1,1,1)";
	_ctrl ctrlSetTextColor [0,0,0,0.5];
	_ctrl ctrlSetPosition [0.2625,0.42,0.475,0.22];
	_ctrl ctrlCommit 0;
	
	_ctrl = findDisplay -1 ctrlCreate ["RscPicture",1000];
	_ctrl ctrlSetText "#(argb,8,8,3)color(1,1,1,1)";
	_ctrl ctrlSetTextColor [0.1,0.1,0.1,0.75];
	_ctrl ctrlSetPosition [0.275,0.46,0.45,0.16];
	_ctrl ctrlCommit 0;
	
	_ctrl = findDisplay -1 ctrlCreate ["RscText",1000];
	_ctrl ctrlSetText "Zeus Essentials Player Selection";
	_ctrl ctrlSetPosition [0.275,0.42,0.3,0.04];
	_ctrl ctrlCommit 0;
	
	_ctrl = findDisplay -1 ctrlCreate ["RscCombo",1001];
	_ctrl ctrlSetPosition [0.2875,0.48,0.3125,0.04];
	_ctrl ctrlCommit 0;
	
	{
		_name = name _x;
		if(_x in call BIS_fnc_listCuratorPlayers) then 
		{
			systemChat (_name + " is a curator");
			_index = _ctrl lbAdd _name;
		};
	} foreach allPlayers;
	
	_ctrl = findDisplay -1 ctrlCreate ["RscButtonMenu",1000];
	_ctrl ctrlSetText "Confirm";
	_ctrl ctrlSetPosition [0.6,0.48,0.1125,0.04];
	_ctrl ctrlCommit 0;
	_ctrl ctrlAddEventHandler ["ButtonDown", 
	{
		_combo = ((findDisplay -1) displayCtrl 1001);
		_tgtIndex = lbCurSel _combo;
		_name = _combo lbText _tgtIndex;
		
		missionNameSpace setVariable ["targetNameForAccess", _name, true];
		
		call fnc_loadSystem;
		closeDialog 1;
		(_name + " now has access to the Zeus Essentials Menu") remoteExec["systemChat"];
		playSound "hint";
	}];
};
[] spawn fnc_createSelectionMenu;

fnc_displayAd = {
	{
		adEvent = player addMPEventHandler["MPRespawn",
		{
			_ad = findDisplay 0 getVariable "_ad";
			if(!isNil "_ad") then {ctrlDelete _ad;};
			disableSerialization;
			_ctrl = findDisplay 12 ctrlCreate ["RscStructuredText", -1]; 
			_ctrl ctrlSetPosition [0.6885,0.72,0.42,0.1]; 
			_ctrl ctrlCommit 0; 
			_ctrl ctrlSetStructuredText parseText "<a size='0.95' href='https://pastebin.com/JuP2DG1j'>Zeus Essentials Menu for Public Zeus Link</a>";
			findDisplay 0 setVariable ["_ad", _ctrl];
			player removeMPEventHandler ["MPRespawn", adEvent];
		}];
	} remoteExec["BIS_fnc_call",-2,"zeusEssentialsAd"];
};

fnc_loadSystem = {
	{
		create_menu = {
		
			disableSerialization;
			
			[] spawn
			{
				firstTimeStartup = true;
				missionNamespace setVariable ["_version", "v0.1"];
				"Initializing..." remoteExec["systemChat"];
			};
			
			load_start = 
			{
				if(firstTimeStartup) then 
				{
					firstTimeStartup = false;
					
					systemChat "Load completed...";
					systemChat ("Zeus Essentials " + (missionNamespace getVariable "_version")); 
					
					i = 0; 
					while {i < 1} do  
					{ 
						i = i +1; 
						playSound "Transition2";
					}; 
				};
			};
			
			DisplayNumber = 312;
			xOffset = 0;
			yOffset = 0;
			ySpawn = 1.5;
			
			findDisplay 0 setVariable ["background_1",0];
			background_1_Pos = [0.625+xOffset,0+yOffset,0.375,0.66];
			background_1_Spawn_Pos = [0.625+xOffset,ySpawn,0.375,0.66];
			
			findDisplay 0 setVariable ["background_2",0];
			background_2_Pos = [0.6375+xOffset,0.04+yOffset,0.35,0.58];
			background_2_Spawn_Pos = [0.6375+xOffset,ySpawn,0.35,0.58];
			
			findDisplay 0 setVariable ["background_3",0];
			background_3_Pos = [0.65+xOffset,0.06+yOffset,0.325,0.08];
			background_3_Spawn_Pos = [0.65+xOffset,ySpawn,0.325,0.08];
			
			findDisplay 0 setVariable ["listBox",0];
			listBox_Pos = [0.65+xOffset,0.16+yOffset,0.325,0.44];
			listBox_Spawn_Pos = [0.65+xOffset,ySpawn,0.325,0.44];
					
			findDisplay 0 setVariable ["title",0];
			title_Pos = [0.6375+xOffset,0+yOffset,0.1875,0.04];
			title_Spawn_Pos = [0.6375+xOffset,ySpawn,0.1875,0.04];
			
			findDisplay 0 setVariable ["creditText",0];
			creditText_Pos = [0.8875+xOffset,0.62+yOffset,0.15,0.04];
			creditText_Spawn_Pos = [0.8875+xOffset,ySpawn,0.15,0.04];
			
			findDisplay 0 setVariable ["checkbox",0];
			checkbox_Pos = [0.958+xOffset,0+yOffset,0.035,0.04];
			checkbox_Spawn_Pos = [0.958+xOffset,0+ySpawn,0.035,0.04];
			
			findDisplay 0 setVariable ["cat_button_1",0];
			cat_button_1_Pos = [0.65+xOffset,0.06+yOffset,0.1375,0.04];
			cat_button_1_Spawn_Pos = [0.65+xOffset,ySpawn,0.1375,0.04];
			
			findDisplay 0 setVariable ["cat_button_2",0];
			cat_button_2_Pos = [0.7875+xOffset,0.06+yOffset,0.1,0.04];
			cat_button_2_Spawn_Pos = [0.7875+xOffset,ySpawn,0.1,0.04];
			
			findDisplay 0 setVariable ["cat_button_3",0];
			cat_button_3_Pos = [0.8875+xOffset,0.06+yOffset,0.0875,0.04];
			cat_button_3_Spawn_Pos = [0.8875+xOffset,ySpawn,0.0875,0.04];
			
			findDisplay 0 setVariable ["cat_button_4",0];
			cat_button_4_Pos = [0.65+xOffset,0.1+yOffset,0.0875,0.04];
			cat_button_4_Spawn_Pos = [0.65+xOffset,ySpawn,0.0875,0.04];
			
			findDisplay 0 setVariable ["cat_button_5",0];
			cat_button_5_Pos = [0.7375+xOffset,0.1+yOffset,0.0875,0.04];
			cat_button_5_Spawn_Pos = [0.7375+xOffset,ySpawn,0.0875,0.04];
			
			findDisplay 0 setVariable ["cat_button_6",0];
			cat_button_6_Pos = [0.825+xOffset,0.1+yOffset,0.075,0.04];
			cat_button_6_Spawn_Pos = [0.825+xOffset,ySpawn,0.075,0.04];
			
			input_text = "";
			
			findDisplay 0 setVariable ["input_box",0];
			input_box_Pos = [0.625,0.66,0.3,0.04];
			
			findDisplay 0 setVariable ["execute_button",0];
			execute_button_Pos = [0.925,0.66,0.075,0.04];
			
			findDisplay 0 setVariable ["blufor_button",0];
			blufor_button_Pos = [0.625,0.7,0.1,0.02];
			
			findDisplay 0 setVariable ["opfor_button",0];
			opfor_button_Pos = [0.725,0.7,0.0875,0.02];
			
			findDisplay 0 setVariable ["independent_button",0];
			independent_button_Pos = [0.8125,0.7,0.0875,0.02];
			
			findDisplay 0 setVariable ["civilian_button",0];
			civilian_button_Pos = [0.9,0.7,0.1,0.02];
			
			primary_color = [1,1,1,1];
			secondary_color = [1,1,1,1];
			primary_color_hex = "#ffffff";
			secondary_color_hex = "#ffffff";
			active_color = [0,1,0,1];
			inactive_color = [1,1,1,1];
			
			blufor_color = [0,0.4,0.7,1];
			blufor_color_hex = blufor_color call BIS_fnc_colorRGBAtoHTML;
			
			last_color = blufor_color;
			last_color_hex = blufor_color_hex;
		
			opfor_color = [0.5,0,0,1];
			opfor_color_hex = opfor_color call BIS_fnc_colorRGBAtoHTML;
			
			independent_color = [0,0.5,0,1];
			independent_color_hex = independent_color call BIS_fnc_colorRGBAtoHTML;
			
			civilian_color = [0.686,0.2,0.807,1];
			civilian_color_hex = civilian_color call BIS_fnc_colorRGBAtoHTML;
			
			_color_white	= [1,1,1,1];
			_color_red 		= [1,0,0,1];
			_color_green 	= [0,0.5,0.1,1];
			_color_blue 	= [0,0.25,1,1];
			_color_cyan 	= [0,0.75,1,1];
			_color_yellow 	= [1,1,0,1];
			_color_orange 	= [1,0.45,0,1];
			_color_violet	= [0.5,0,1,1];
			_color_pink		= [1,0.375,0.9,1];
			
			allColors = [
				_color_white,	
				_color_red 	,	
				_color_green,	
				_color_blue ,	
				_color_cyan ,	
				_color_yellow ,	
				_color_orange ,	
				_color_violet ,
				_color_pink		
			];
			color_index = 1;
			
			isMenuExisting = true;
			isMenuLoopAllowedToRun = true;
			isSideMuted = false;
			isGlobalMuted = false;
			isRespawnArsenalEnabled = false;
			isModeratorDisabled = false;
					
			load_backgrounds = {
				disableSerialization;
				
				call load_start;
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscPicture",1000];
				_ctrl ctrlSetText "#(argb,8,8,3)color(1,1,1,1)";
				_ctrl ctrlSetTextColor [0,0,0,0.5];
				_ctrl ctrlSetPosition background_1_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition background_1_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 2.5;
				findDisplay 0 setVariable ["background_1", _ctrl];
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscPicture",1000];
				_ctrl ctrlSetText "#(argb,8,8,3)color(1,1,1,1)";
				_ctrl ctrlSetTextColor [0.1,0.1,0.1,0.75];
				_ctrl ctrlSetPosition background_2_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition background_2_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 2.75;
				findDisplay 0 setVariable ["background_2", _ctrl];
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscPicture",1000];
				_ctrl ctrlSetText "#(argb,8,8,3)color(1,1,1,1)";
				_ctrl ctrlSetTextColor [0.05,0.05,0.05,1];
				_ctrl ctrlSetPosition background_3_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition background_3_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 3;
				findDisplay 0 setVariable ["background_3", _ctrl];
			};
			
			load_titles = {
				disableSerialization;
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscStructuredText",1000];
				_ctrl ctrlSetStructuredText parseText ("<t size='1' color='"+primary_color_hex+"'>Zeus Essentials</t>");
				_ctrl ctrlSetTooltip "v0.1";
				_ctrl ctrlSetPosition title_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition title_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 2.5;
				findDisplay 0 setVariable ["title", _ctrl];
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscStructuredText",1000];
				_ctrl ctrlSetStructuredText parseText ("<t size='0.75' color='"+primary_color_hex+"'>By Capt. Chris</t>");
				_ctrl ctrlSetPosition creditText_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition creditText_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 2.5;
				findDisplay 0 setVariable ["creditText", _ctrl];
			};
			
			load_checkBox = {
				disableSerialization;
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscCheckbox",1001];
				_ctrl ctrlSetPosition checkbox_Spawn_Pos;
				_ctrl ctrlSetTooltip "Hide/Show";
				_ctrl cbSetChecked true;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition checkbox_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 2.5;
				findDisplay 0 setVariable ["checkbox", _ctrl];
				_ctrl ctrlAddEventHandler ["CheckedChanged", 
				{
					if(cbChecked ((findDisplay DisplayNumber) displayCtrl 1001)) then
					{
						{ 
							_x ctrlShow true;
						} foreach (findDisplay 0 getVariable "_allGUI");
						playSound "zoomin";
					}
					else 
					{
						{ 
							_x ctrlShow false;
						} foreach (findDisplay 0 getVariable "_allGUI");
						playSound "zoomout";
					};
				}];
			};
			
			load_listBox = {
				disableSerialization;
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscListbox",1002];
				_ctrl ctrlSetPosition listBox_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition listBox_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 2.75;
				findDisplay 0 setVariable ["listBox", _ctrl];
				_ctrl ctrlAddEventHandler ["LBDblClick", 
				{
					_lb = ((findDisplay DisplayNumber) displayCtrl 1002);
					_index = lbCurSel _lb;
					_array = missionNamespace getVariable "_allLBFuncs";
					[_index] call (_array select _index);
					
					i = 0; 
					while {i < 3} do  
					{ 
						i = i +1; 
						playSound "Beep_Target";
					}; 
				}];
			};
			
			load_catagories = {
				disableSerialization;
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetText "Messages";
				_ctrl ctrlSetTooltip "Special Zeus messages";
				_ctrl ctrlSetTextColor primary_color;
				_ctrl ctrlSetPosition cat_button_1_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition cat_button_1_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 3;
				findDisplay 0 setVariable ["cat_button_1", _ctrl];
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{
					_lb = ((findDisplay DisplayNumber) displayCtrl 1002); 
					if(!(isNull _lb)) then 
					{
						lbClear _lb; 
						_array = [];
						missionNamespace setVariable ["_allLBFuncs", _array];
						
						
						_index = _lb lbAdd "High Command Message";
						_lb lbSetTooltip [_index, "Send a message in the High Command format"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_HighCommand";
						_array pushBack _func;
						
						_index = _lb lbAdd "Mission Name Message";
						_lb lbSetTooltip [_index, "Send a message in the Mission Name format"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_MissionName";
						_array pushBack _func;
						
						_index = _lb lbAdd "Story Message";
						_lb lbSetTooltip [_index, "Send a message in the Story format"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_StoryMessage";
						_array pushBack _func;
						
						_index = _lb lbAdd "Objective Complete Event";
						_lb lbSetTooltip [_index, "Display objective complete event"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_ObjectiveComplete";
						_array pushBack _func;
						
						_index = _lb lbAdd "Objective Failed Event";
						_lb lbSetTooltip [_index, "Display objective failed event"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_ObjectiveFailed";
						_array pushBack _func;
						
						missionNamespace setVariable ["_allLBFuncs", _array];
					}
					else
					{
						systemChat "ERROR: UNABLE TO FIND LIST BOX";
						"ERROR: UNABLE TO FIND LIST BOX" call BIS_fnc_errorMsg;
					};
				}];
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetText "Delete";
				_ctrl ctrlSetTooltip "Various delete options";
				_ctrl ctrlSetTextColor primary_color;
				_ctrl ctrlSetPosition cat_button_2_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition cat_button_2_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 3;
				findDisplay 0 setVariable ["cat_button_2", _ctrl];
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{
					_lb = ((findDisplay DisplayNumber) displayCtrl 1002); 
					if(!(isNull _lb)) then 
					{
						lbClear _lb;
						_array = [];
						missionNamespace setVariable ["_allLBFuncs", _array];
											
						_index = _lb lbAdd "Delete all Dead";
						_lb lbSetTooltip [_index, "Delete all dead infantry and vehicles"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_deleteAllDead";
						_array pushBack _func;
						
						_index = _lb lbAdd "Delete empty vehicles";
						_lb lbSetTooltip [_index, "Delete all of the empty vehicles"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_deleteEmptyVehicles";
						_array pushBack _func;
						
						_index = _lb lbAdd "Delete guns and gear";
						_lb lbSetTooltip [_index, "Delete all of the guns and equipment on the ground"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_deleteGunsAndEquipment";
						_array pushBack _func;
						
						_index = _lb lbAdd "Delete all NATO AI";
						_lb lbSetTooltip [_index, "Delete all NATO AI infantry and vehicles"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_deleteNATO";
						_array pushBack _func;
						
						_index = _lb lbAdd "Delete all CSAT AI";
						_lb lbSetTooltip [_index, "Delete all CSAT AI infantry and vehicles"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_deleteCSAT";
						_array pushBack _func;
						
						_index = _lb lbAdd "Delete all Independent AI";
						_lb lbSetTooltip [_index, "Delete all Independent AI infantry and vehicles"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_deleteIndependent";
						_array pushBack _func;
						
						_index = _lb lbAdd "Delete all Civilian AI";
						_lb lbSetTooltip [_index, "Delete all Civilian AI infantry and vehicles"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_deleteCivilian";
						_array pushBack _func;
						
						_index = _lb lbAdd "Delete all of the above";
						_lb lbSetTooltip [_index, "Call every function above this one"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_deleteAll";
						_array pushBack _func;
						
						missionNamespace setVariable ["_allLBFuncs", _array];
					}
					else
					{
						systemChat "ERROR: UNABLE TO FIND LIST BOX";
						"ERROR: UNABLE TO FIND LIST BOX" call BIS_fnc_errorMsg;
					};
				}];
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetText "Tools";
				_ctrl ctrlSetTooltip "Various utility scripts";
				_ctrl ctrlSetTextColor primary_color;
				_ctrl ctrlSetPosition cat_button_3_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition cat_button_3_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 3;
				findDisplay 0 setVariable ["cat_button_3", _ctrl];
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{
					_lb = ((findDisplay DisplayNumber) displayCtrl 1002); 
					if(!(isNull _lb)) then 
					{
						lbClear _lb; 
						_array = [];
						missionNamespace setVariable ["_allLBFuncs", _array];
						
						_index = _lb lbAdd "Kill all players";
						_lb lbSetTooltip [_index, "Force respawn every player"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_killPlayers";
						_array pushBack _func;
						
						_index = _lb lbAdd "Listen to side channel";
						_lb lbSetTooltip [_index, "Listen to NATO side channel (NATO only)"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_listenSide";
						_array pushBack _func;
						
						_index = _lb lbAdd "Add more objects to interface";
						_lb lbSetTooltip [_index, "Cant select something? Try this!"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_addObjectsToInterface";
						_array pushBack _func;
						
						_index = _lb lbAdd "Mute side channel";
						_lb lbSetTooltip [_index, "Mute the side channel,\nalso affects JIP"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_manageSideChannel";
						_array pushBack _func;
						if(isSideMuted) then 
						{
							_lb lbSetColor [_index,active_color];
						};
						
						_index = _lb lbAdd "Mute global channel";
						_lb lbSetTooltip [_index, "Mute the global channel except for zeus,\nalso affects JIP"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_manageGlobalChannel";
						_array pushBack _func;
						if(isGlobalMuted) then 
						{
							_lb lbSetColor [_index,active_color];
						};
						
						_index = _lb lbAdd "Respawn Arsenal";
						_lb lbSetTooltip [_index, "Allow all players to open an arsenal on respawn,\nalso affects JIP"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_ArsenalOnRrespawn";
						_array pushBack _func;
						if(isRespawnArsenalEnabled) then 
						{
							_lb lbSetColor [_index,active_color];
						};
						
						_index = _lb lbAdd "Disable Moderator";
						_lb lbSetTooltip [_index, "Disable the other zeus user by killing them forever"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_DisableModerator";
						_array pushBack _func;
						if(isModeratorDisabled) then 
						{
							_lb lbSetColor [_index,active_color];
						};
											
						missionNamespace setVariable ["_allLBFuncs", _array];
					}
					else
					{
						systemChat "ERROR: UNABLE TO FIND LIST BOX";
						"ERROR: UNABLE TO FIND LIST BOX" call BIS_fnc_errorMsg;
					};
				}];
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetText "Color";
				_ctrl ctrlSetTooltip "Menu color customization";
				_ctrl ctrlSetTextColor primary_color;			
				_ctrl ctrlSetPosition cat_button_4_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition cat_button_4_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 3;
				findDisplay 0 setVariable ["cat_button_4", _ctrl];
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{
					_lb = ((findDisplay DisplayNumber) displayCtrl 1002); 
					if(!(isNull _lb)) then 
					{
						lbClear _lb; 
						_array = [];
						missionNamespace setVariable ["_allLBFuncs", _array];
						
						_index = _lb lbAdd "Switch primary color";
						_lb lbSetTooltip [_index, "Click to switch between\nall available colors"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_primaryColor";
						_array pushBack _func;
						
						_index = _lb lbAdd "Switch secondary color";
						_lb lbSetTooltip [_index, "Click to switch between\nall available colors"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_secondaryColor";
						_array pushBack _func;
						
						_index = _lb lbAdd "Switch active color";
						_lb lbSetTooltip [_index, "Click to switch between\nall available colors\n\nActive color is when\na script is actively running"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_activeColor";
						_array pushBack _func;
						
						_index = _lb lbAdd "Reset all colors";
						_lb lbSetTooltip [_index, "Reset all of the colors back to white"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_ResetColor";
						_array pushBack _func;
						
						_index = _lb lbAdd "Active Example";
						_lb lbSetTooltip [_index, "Just an example\nthis does nothing"];
						_lb lbSetColor [_index, active_color];
						
						missionNamespace setVariable ["_allLBFuncs", _array];
					}
					else
					{
						systemChat "ERROR: UNABLE TO FIND LIST BOX";
						"ERROR: UNABLE TO FIND LIST BOX" call BIS_fnc_errorMsg;
					};
				}];
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetText "Extra";
				_ctrl ctrlSetTooltip "Unrelated scripts and stuff";
				_ctrl ctrlSetTextColor primary_color;
				_ctrl ctrlSetPosition cat_button_5_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition cat_button_5_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 3;
				findDisplay 0 setVariable ["cat_button_5", _ctrl];
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{
					_lb = ((findDisplay DisplayNumber) displayCtrl 1002); 
					if(!(isNull _lb)) then 
					{
						lbClear _lb; 
						_array = [];
						missionNamespace setVariable ["_allLBFuncs", _array];
					
						_index = _lb lbAdd "Credits";
						_lb lbSetTooltip [_index, "Roll the credits!"];
						_lb lbSetColor [_index,secondary_color];
						_func = findDisplay 0 getVariable "fnc_credits";
						_array pushBack _func;
					}
					else
					{
						systemChat "ERROR: UNABLE TO FIND LIST BOX";
						"ERROR: UNABLE TO FIND LIST BOX" call BIS_fnc_errorMsg;
					};
				}];
				
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetText "Help";
				_ctrl ctrlSetTooltip "FAQ";
				_ctrl ctrlSetTextColor primary_color;
				_ctrl ctrlSetPosition cat_button_6_Spawn_Pos;
				_ctrl ctrlSetFade 1;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetPosition cat_button_6_Pos;
				_ctrl ctrlSetFade 0;
				_ctrl ctrlCommit 3;
				findDisplay 0 setVariable ["cat_button_6", _ctrl];
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{
					_lb = ((findDisplay DisplayNumber) displayCtrl 1002); 
					if(!(isNull _lb)) then 
					{
						lbClear _lb;
						_array = [{},{},{},{},{},{},{},{},{},{},{}];
						missionNamespace setVariable ["_allLBFuncs", _array];
						
						_index = _lb lbAdd "How do I use these scripts?";
						_lb lbSetTooltip [_index, "First click a tab at the top,\nthen double click on the text to activate that script"];
						_lb lbSetColor [_index,secondary_color];
						_index = _lb lbAdd "What do the green ones mean?";
						_lb lbSetTooltip [_index, "If a script is green, that means its\nactive until you deactivate it"];
						_lb lbSetColor [_index,secondary_color];
						_index = _lb lbAdd "How do I hide this menu?";
						_lb lbSetTooltip [_index, "Click the little white box\nat the top of this menu"];
						_lb lbSetColor [_index,secondary_color];
						_index = _lb lbAdd "What is JIP?";
						_lb lbSetTooltip [_index, "JIP: Join in progress. Its when\na player joins the server AFTER it has started"];
						_lb lbSetColor [_index,secondary_color];
						_index = _lb lbAdd "Can I have this menu script?";
						_lb lbSetTooltip [_index, "Yeah sure, its available on Steam Arma 3 Guides"];
						_lb lbSetColor [_index,secondary_color];
						_index = _lb lbAdd "Can I trust these scripts?";
						_lb lbSetTooltip [_index, "Sure why not?\nMaybe.\nNothing is guaranteed to work all the time"];
						_lb lbSetColor [_index,secondary_color];
					}
					else
					{
						systemChat "ERROR: UNABLE TO FIND LIST BOX";
						"ERROR: UNABLE TO FIND LIST BOX" call BIS_fnc_errorMsg;
					};
				}];
			};
			
			fnc_HighCommand = {
				disableSerialization;
				
				run_HighCommand = {
					[] spawn {
						"hint" remoteExec["playSound"];
						_fadeTime = 1.375;
						_par = "''";
						if(last_color_hex == civilian_color_hex) then 
						{
							_title = "[NEWS REPORT]";
							msg = ("<t color='"+last_color_hex+"' font='RobotoCondensed' size='2'>"+_title+"</t><br/>"+_par+input_text+_par);
						}
						else 
						{
							_title = "[HIGH COMMAND]";
							msg = ("<t color='"+last_color_hex+"' font='RobotoCondensed' size='2'>"+_title+"</t><br/>"+_par+input_text+_par);
						};
						[2,[msg, "PLAIN DOWN", _fadeTime, true, true]] remoteExec ["cutText"];
					};
				};
			
				_ok = createDialog "RscDisplayEmpty";
				_dialog = findDisplay -1;
				
				call load_color_buttons;
				
				_ctrl = _dialog ctrlCreate ["RscEdit",1001];
				_ctrl ctrlSetPosition input_box_Pos;
				_ctrl ctrlSetText "Type here";
				_ctrl ctrlSetTextColor last_color;
				_ctrl ctrlSetBackgroundColor [0,0,0,0.5];
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Press Escape to cancel";
				
				_ctrl = _dialog ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetPosition execute_button_Pos;
				_ctrl ctrlSetText "Exec";
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Execute";
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{	
					_inputBox = ((findDisplay -1) displayCtrl 1001);
					_text = ctrlText _inputBox;		
					input_text = _text;
					call run_HighCommand;
					closeDialog 1;
				}];
			}; findDisplay 0 setVariable ["fnc_HighCommand",fnc_HighCommand];
			
			fnc_MissionName = {
				disableSerialization;
				
				run_MissionName = {
					[] spawn 
					{
						_fadeTime = 1.75;
						_msg = ("<t color='"+last_color_hex+"' font='PuristaSemiBold' size='5'>"+input_text+"</t><br/>
						____________________________________________________________________________________________________________________");
						
						[1,[_msg, "PLAIN", _fadeTime, true, true]] remoteExec ["cutText"];
						"hint" remoteExec["playSound"];
					};
				};
							
				_ok = createDialog "RscDisplayEmpty";
				_dialog = findDisplay -1;
				
				call load_color_buttons;
				
				_ctrl = _dialog ctrlCreate ["RscEdit",1001];
				_ctrl ctrlSetPosition input_box_Pos;
				_ctrl ctrlSetText "Type here";
				_ctrl ctrlSetTextColor last_color;
				_ctrl ctrlSetBackgroundColor [0,0,0,0.5];
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Press Escape to cancel";
				
				_ctrl = _dialog ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetPosition execute_button_Pos;
				_ctrl ctrlSetText "Exec";
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Execute";
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{	
					_inputBox = ((findDisplay -1) displayCtrl 1001);
					_text = ctrlText _inputBox;		
					input_text = _text;
					call run_MissionName;
					closeDialog 1;
				}];
			}; findDisplay 0 setVariable ["fnc_MissionName",fnc_MissionName];
			
			fnc_StoryMessage = {
				disableSerialization;
				
				run_StoryMessage = {
					[] spawn 
					{
						_fadeTime = 1.75;
						_msg = ("<t font='PuristaSemiBold' size='1.5'>"+input_text+"</t><br/>");
						
						[1,[_msg, "PLAIN", _fadeTime, true, true]] remoteExec ["cutText"];
						"hint" remoteExec["playSound"];
					};
				};
							
				_ok = createDialog "RscDisplayEmpty";
				_dialog = findDisplay -1;
				
				_ctrl = _dialog ctrlCreate ["RscEdit",1001];
				_ctrl ctrlSetPosition input_box_Pos;
				_ctrl ctrlSetText "Type here";
				_ctrl ctrlSetTextColor last_color;
				_ctrl ctrlSetBackgroundColor [0,0,0,0.5];
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Press Escape to cancel";
				
				_ctrl = _dialog ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetPosition execute_button_Pos;
				_ctrl ctrlSetText "Exec";
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Execute";
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{	
					_inputBox = ((findDisplay -1) displayCtrl 1001);
					_text = ctrlText _inputBox;		
					input_text = _text;
					call run_StoryMessage;
					closeDialog 1;
				}];
			}; findDisplay 0 setVariable ["fnc_StoryMessage",fnc_StoryMessage];
			
			load_color_buttons = {
				disableSerialization;
				
				_ctrl = findDisplay -1 ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetPosition blufor_button_Pos;
				_ctrl ctrlsetbackgroundcolor blufor_color;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "BLUFOR Color";
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{	
					_inputBox = ((findDisplay -1) displayCtrl 1001);
					_inputBox ctrlSetTextColor blufor_color;
					last_color = blufor_color;
					last_color_hex = blufor_color_hex;
				}];
				
				_ctrl = findDisplay -1 ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetPosition opfor_button_Pos;
				_ctrl ctrlsetbackgroundcolor opfor_color;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "OPFOR Color";
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{	
					_inputBox = ((findDisplay -1) displayCtrl 1001);
					_inputBox ctrlSetTextColor opfor_color;
					last_color = opfor_color;
					last_color_hex = opfor_color_hex;
				}];
				
				_ctrl = findDisplay -1 ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetPosition independent_button_Pos;
				_ctrl ctrlsetbackgroundcolor independent_color;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Independent Color";
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{	
					_inputBox = ((findDisplay -1) displayCtrl 1001);
					_inputBox ctrlSetTextColor independent_color;
					last_color = independent_color;
					last_color_hex = independent_color_hex;
				}];
				
				_ctrl = findDisplay -1 ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetPosition civilian_button_Pos;
				_ctrl ctrlsetbackgroundcolor civilian_color;
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Civilian Color";
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{	
					_inputBox = ((findDisplay -1) displayCtrl 1001);
					_inputBox ctrlSetTextColor civilian_color;
					last_color = civilian_color;
					last_color_hex = civilian_color_hex;
				}];
			};
			
			fnc_ObjectiveComplete = {
				[] spawn 
				{
					_fadeTime = 1.65;
					_msg = "<t color='#00ff19' font='PuristaMedium' size='5'>OBJECTIVE COMPLETE";
					[1,[_msg, "PLAIN", _fadeTime, true, true]] remoteExec ["cutText"];
					"EventTrack02b_F_EPC" remoteExec["playMusic"];
				};
			}; findDisplay 0 setVariable ["fnc_ObjectiveComplete",fnc_ObjectiveComplete];
			
			fnc_ObjectiveFailed = {
				[] spawn
				{
					_fadeTime = 1.35;
					_msg = "<t color='#ff0000' font='PuristaMedium' size='5'>OBJECTIVE FAILED";
					[1,[_msg, "PLAIN", _fadeTime, true, true]] remoteExec ["cutText"];
					"EventTrack02_F_EPB" remoteExec["playMusic"];
				};
			}; findDisplay 0 setVariable ["fnc_ObjectiveFailed",fnc_ObjectiveFailed];
			
			fnc_deleteAllDead = {
				{ deleteVehicle _x; } forEach allDead;
			}; findDisplay 0 setVariable ["fnc_deleteAllDead",fnc_deleteAllDead];
			
			fnc_deleteEmptyVehicles = {
				_vehicles = nearestObjects [getPos player, ["AllVehicles"], 10000];
				{
					if (count crew vehicle _x == 0) then {deleteVehicle _x};
				} forEach _vehicles;			
			}; findDisplay 0 setVariable ["fnc_deleteEmptyVehicles",fnc_deleteEmptyVehicles];
			
			fnc_deleteGunsAndEquipment = {
				{ 
					deleteVehicle _x; 
				} forEach nearestObjects [getpos player,["WeaponHolder","GroundWeaponHolder"],10000]
			}; findDisplay 0 setVariable ["fnc_deleteGunsAndEquipment",fnc_deleteGunsAndEquipment];
			
			fnc_deleteNATO = {
				{
					if(side _x == west && !(_x in allPlayers)) then 
					{
						_run = true;
						_veh = vehicle _x;
						{
							if(_x in allPlayers) then {_run = false;};
						} foreach crew _veh;
						
						if(_run) then 
						{
							deleteVehicle _veh;
						};
						deleteVehicle _x;
					};
				} foreach allUnits;
			}; findDisplay 0 setVariable ["fnc_deleteNATO",fnc_deleteNATO];
			
			fnc_deleteCSAT = {
				{
					if(side _x == east && !(_x in allPlayers)) then 
					{
						_run = true;
						_veh = vehicle _x;
						{
							if(_x in allPlayers) then {_run = false;};
						} foreach crew _veh;
						
						if(_run) then 
						{
							deleteVehicle _veh;
						};
						deleteVehicle _x;
					};
				} foreach allUnits;
			}; findDisplay 0 setVariable ["fnc_deleteCSAT",fnc_deleteCSAT];
			
			fnc_deleteIndependent = {
				{
					if(side _x == resistance && !(_x in allPlayers)) then 
					{
						_run = true;
						_veh = vehicle _x;
						{
							if(_x in allPlayers) then {_run = false;};
						} foreach crew _veh;
						
						if(_run) then 
						{
							deleteVehicle _veh;
						};
						deleteVehicle _x;
					};
				} foreach allUnits;
			}; findDisplay 0 setVariable ["fnc_deleteIndependent",fnc_deleteIndependent];
			
			fnc_deleteCivilian = {
				{
					if(side _x == civilian && !(_x in allPlayers)) then 
					{
						_run = true;
						_veh = vehicle _x;
						{
							if(_x in allPlayers) then {_run = false;};
						} foreach crew _veh;
						
						if(_run) then 
						{
							deleteVehicle _veh;
						};
						deleteVehicle _x;
					};
				} foreach allUnits;
			}; findDisplay 0 setVariable ["fnc_deleteCivilian",fnc_deleteCivilian];
			
			fnc_deleteAll = {
				call fnc_deleteAllDead;
				call fnc_deleteEmptyVehicles;
				call fnc_deleteGunsAndEquipment;
				call fnc_deleteNATO;
				call fnc_deleteCSAT;
				call fnc_deleteIndependent;
				call fnc_deleteCivilian;
				
				"vr_shutdown" remoteExec["playSound"];
				
				_start = diag_tickTime;
				(format ["Server cleanup took %1 seconds",diag_tickTime - _start]) remoteExec["systemChat"];
			}; findDisplay 0 setVariable ["fnc_deleteAll",fnc_deleteAll];
			
			fnc_killPlayers = {
				{
					if(!(_x in call BIS_fnc_listCuratorPlayers)) then {_x setDamage 1;};
				} foreach allPlayers;
			}; findDisplay 0 setVariable ["fnc_killPlayers",fnc_killPlayers];
			
			fnc_listenSide = {
				{
					_grpName = createGroup west;
					[call BIS_fnc_listCuratorPlayers select 0] joinSilent _grpName;
					[call BIS_fnc_listCuratorPlayers select 1] joinSilent _grpName;
				} remoteExec ["BIS_fnc_call",2];
			}; findDisplay 0 setVariable ["fnc_ListenSide",fnc_ListenSide];
			
			fnc_addObjectsToInterface = {
				{
					{
						_x addCuratorEditableObjects [allUnits,true];
						_x addCuratorEditableObjects [vehicles,true];
					} forEach allCurators;
				} remoteExec ["bis_fnc_call", 2];
			}; findDisplay 0 setVariable ["fnc_addObjectsToInterface",fnc_addObjectsToInterface];
			
			fnc_manageSideChannel = {
				params["_index"];
			
				if (!isSideMuted) then 
				{
					{
						1 enableChannel [true,false];
					} remoteExec ["bis_fnc_call", 0, "muteSide"]; 
					
					_listBox = findDisplay 0 getVariable "listBox";
					_listBox lbSetColor [_index,active_color];
				}
				else 
				{
					{
						1 enableChannel [true,true];
					} remoteExec ["bis_fnc_call", 0, "muteSide"]; 
					
					_listBox = findDisplay 0 getVariable "listBox";
					_listBox lbSetColor [_index,secondary_color];
				};
				isSideMuted = !isSideMuted;
			}; findDisplay 0 setVariable ["fnc_manageSideChannel",fnc_manageSideChannel];
			
			fnc_manageGlobalChannel = {
				params["_index"];
			
				if (!isGlobalMuted) then 
				{
					{
						if(!(player in call BIS_fnc_listCuratorPlayers)) then 
						{
							0 enableChannel [true,false];
						}
					} remoteExec ["bis_fnc_call", 0, "muteGlobal"]; 
					
					
					_listBox = findDisplay 0 getVariable "listBox";
					_listBox lbSetColor [_index,active_color];
				}
				else 
				{
					{
						0 enableChannel [true,true];
					} remoteExec ["bis_fnc_call", 0, "muteGlobal"]; 
					
					_listBox = findDisplay 0 getVariable "listBox";
					_listBox lbSetColor [_index,secondary_color];
				};
				isGlobalMuted = !isGlobalMuted; 
			}; findDisplay 0 setVariable ["fnc_manageGlobalChannel",fnc_manageGlobalChannel];
			
			fnc_ArsenalOnRrespawn = {
				params["_index"];
			
				if (!isRespawnArsenalEnabled) then 
				{
					{
						arsenalEventIndex =	player addMPEventHandler ["MPRespawn", 
						{
							open_Arsenal = 
							{
								["Open",true] spawn BIS_fnc_arsenal;
								removeAllActions player;
							};
							player addAction ["<t color='#ff0000'>Open Arsenal</t>", {call open_Arsenal;}];
						}];
					} remoteExec ["bis_fnc_call", 0, "respawnArsenal"]; 
					
					_listBox = findDisplay 0 getVariable "listBox";
					_listBox lbSetColor [_index,active_color];
				}
				else 
				{
					{
						player removeMPEventHandler ["MPRespawn", arsenalEventIndex]; 
					} remoteExec ["bis_fnc_call", 0, "respawnArsenal"]; 
					
					_listBox = findDisplay 0 getVariable "listBox";
					_listBox lbSetColor [_index,secondary_color];
				};
				isRespawnArsenalEnabled = !isRespawnArsenalEnabled; 
			}; findDisplay 0 setVariable ["fnc_ArsenalOnRrespawn",fnc_ArsenalOnRrespawn];
			
			
			
			fnc_DisableModerator = {
				params["_index"];
			
				if (!isModeratorDisabled) then 
				{
					findDisplay 0 setVariable ['_modLoop', true]; 
					[] spawn 
					{	
						while { (findDisplay 0 getVariable '_modloop'); } do 
						{	
							_curators = call BIS_fnc_listCuratorPlayers;
							{
								if(_x != player) then 
								{ 
									_x setDamage 1;
								}
							} foreach _curators;
							
							sleep 2.75;
						};
					};
					
					_listBox = findDisplay 0 getVariable "listBox";
					_listBox lbSetColor [_index,active_color];
				}
				else
				{
					{
						findDisplay 0 setVariable ['_modLoop', false]; 
					} remoteExec ["bis_fnc_call", 0, "respawnArsenal"]; 
					
					_listBox = findDisplay 0 getVariable "listBox";
					_listBox lbSetColor [_index,secondary_color];
				};
				isModeratorDisabled = !isModeratorDisabled;
			}; findDisplay 0 setVariable ["fnc_DisableModerator",fnc_DisableModerator];
			
			fnc_credits = {
				{
					[] spawn 
					{	
						run_credits = {
							params["_num"];
							
							disableSerialization;
							
							_delay = 1.5;
							_delay_2 = 0.65;
							
							_speed = 20;
							
							_startY = 1.5;
							_endY = -0.5;
							
							_titlePos = [0.3,_startY,0.6,0.12];
							_subTitlePos = [0.4,_startY,0.425,0.12];
							_namePos = [0.325,_startY,0.875,0.04];
							
							_titlePos_2 = [0.3,_endY,0.6,0.12];
							_subTitlePos_2 = [0.4,_endY,0.425,0.12];
							_namePos_2 = [0.325,_endY,0.875,0.04];
								
							
							_ctrl = findDisplay _num ctrlCreate ["RscStructuredText",1000];
							_ctrl ctrlSetStructuredText parseText ("<t size='2.75'>Zeus Essentials</t>");
							_ctrl ctrlSetTooltip "v0.1";
							_ctrl ctrlSetPosition _titlePos;
							_ctrl ctrlCommit 0;
							_ctrl ctrlSetPosition _titlePos_2;
							_ctrl ctrlCommit _speed;
							
							sleep (_delay+0.5);
							
							_ctrl = findDisplay _num ctrlCreate ["RscStructuredText",1000];
							_ctrl ctrlSetStructuredText parseText ("<t size='1.5'>Created by Capt. Chris</t>");
							_ctrl ctrlSetTooltip "praise me!";
							_ctrl ctrlSetPosition [0.35,_startY,0.425,0.12];
							_ctrl ctrlCommit 0;
							_ctrl ctrlSetPosition [0.35,_endY,0.425,0.12];
							_ctrl ctrlCommit _speed;
							
							sleep _delay;
							
							_ctrl = findDisplay _num ctrlCreate ["RscStructuredText",1000];
							_ctrl ctrlSetStructuredText parseText ("<t size='1.5'>Special Thanks:</t>");
							_ctrl ctrlSetTooltip "Thanks guys! You da best!";
							_ctrl ctrlSetPosition _subTitlePos;
							_ctrl ctrlCommit 0;
							_ctrl ctrlSetPosition _subTitlePos_2;
							_ctrl ctrlCommit _speed;
							
							sleep _delay_2;
							
							_ctrl = findDisplay _num ctrlCreate ["RscStructuredText",1000];
							_ctrl ctrlSetStructuredText parseText ("<t size='1'>Sergeant Hades | Co-Creator and stuff</t>");
							_ctrl ctrlSetTooltip "Thanks for the name!";
							_ctrl ctrlSetPosition _namePos;
							_ctrl ctrlCommit 0;
							_ctrl ctrlSetPosition _namePos_2;
							_ctrl ctrlCommit _speed;
						};
						312 call run_credits;
						46 call run_credits;
						systemChat "The credits are rolling!";
					};
				} remoteExec ["BIS_fnc_call",0];
			}; findDisplay 0 setVariable ["fnc_credits",fnc_credits];
			
			fnc_primaryColor = {
				if(color_index > 8) then 
				{
					color_index = 0;
				};
				
				primary_color = allColors select color_index;
				primary_color_hex = primary_color call BIS_fnc_colorRGBAtoHTML;
				
				(findDisplay 0 getVariable "cat_button_1" ) ctrlSetTextColor primary_color;
				(findDisplay 0 getVariable "cat_button_2" ) ctrlSetTextColor primary_color;
				(findDisplay 0 getVariable "cat_button_3" ) ctrlSetTextColor primary_color;
				(findDisplay 0 getVariable "cat_button_4" ) ctrlSetTextColor primary_color;
				(findDisplay 0 getVariable "cat_button_5" ) ctrlSetTextColor primary_color;
				(findDisplay 0 getVariable "cat_button_6" ) ctrlSetTextColor primary_color;
				(findDisplay 0 getVariable "title"        ) ctrlSetStructuredText parseText ("<t size='1' color='"+primary_color_hex+"'>Zeus Essentials</t>");
				(findDisplay 0 getVariable "creditText"   )	ctrlSetStructuredText parseText ("<t size='0.75' color='"+primary_color_hex+"'>By Capt. Chris</t>");
				
				color_index = (color_index + 1);
			}; findDisplay 0 setVariable ["fnc_primaryColor",fnc_primaryColor];
			
			fnc_secondaryColor = {
				if(color_index > 8) then 
				{
					color_index = 0;
				};
				
				secondary_color = allColors select color_index;
				secondary_color_hex = secondary_color call BIS_fnc_colorRGBAtoHTML;
				
				_lb = (findDisplay 0 getVariable "listBox");
				_size = lbSize _lb;
				for "i" from 0 to _size do 
				{
					_lb lbSetColor [i,secondary_color];
				};
				
				color_index = (color_index + 1);
			}; findDisplay 0 setVariable ["fnc_secondaryColor",fnc_secondaryColor];
			
			fnc_activeColor = {
				if(color_index > 8) then 
				{
					color_index = 0;
				};
				active_color = allColors select color_index;
				color_index = (color_index + 1);
				
				_lb = (findDisplay 0 getVariable "listBox");
				_lb lbSetColor[4, active_color];
				
			}; findDisplay 0 setVariable ["fnc_activeColor",fnc_activeColor];
			
			fnc_ResetColor = {
				color_index = 0;
				systemChat str color_index;
				call fnc_primaryColor;
				color_index = 0;
				call fnc_secondaryColor;
				color_index = 0;
				call fnc_activeColor;
				active_color = [0,1,0,1];
			}; findDisplay 0 setVariable ["fnc_ResetColor",fnc_ResetColor];
			
			delete_global = {
				{
					i = 0;
					while {i < 100} do 
					{
						i = i + 1;
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1000);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1001);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1002);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1003);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1004);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1005);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1006);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1007);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1008);
						ctrlDelete ((findDisplay DisplayNumber) displayCtrl 1009);
						isCreated = nil;
						isMenuLoopAllowedToRun = false;
					};
				} remoteExec ["bis_fnc_call", 0]; 
			};
			missionNamespace setVariable ["_delete", delete_global];
			
			load_delete = 
			{
				_ctrl = findDisplay DisplayNumber ctrlCreate ["RscButtonMenu",1000];
				_ctrl ctrlSetPosition [0.8,1,0.1,0.05];
				_ctrl ctrlSetText "Delete";
				_ctrl ctrlCommit 0;
				_ctrl ctrlSetTooltip "Delete the menu";
				_ctrl ctrlAddEventHandler ["ButtonDown", 
				{
					_func = missionNamespace getVariable "_delete";
					call _func;
				}];
			};
			
			while {isMenuLoopAllowedToRun} do 
			{
				_ui = ((findDisplay DisplayNumber) displayCtrl 1000);
				if(isNull _ui) then 
				{
					[] spawn
					{
						sleep 1.25;
						call load_backgrounds;
						call load_titles;
						call load_checkBox;
						call load_listBox;
						call load_catagories;
						
						allGUI = 
						[
							findDisplay 0 getVariable "background_1",
							findDisplay 0 getVariable "background_2",
							findDisplay 0 getVariable "background_3",
							findDisplay 0 getVariable "listBox",
							findDisplay 0 getVariable "title",
							findDisplay 0 getVariable "creditText",
							findDisplay 0 getVariable "cat_button_1",
							findDisplay 0 getVariable "cat_button_2",
							findDisplay 0 getVariable "cat_button_3",
							findDisplay 0 getVariable "cat_button_4",
							findDisplay 0 getVariable "cat_button_5",
							findDisplay 0 getVariable "cat_button_6"
						];
						
						findDisplay 0 setVariable ["_allGUI", allGUI];
						missionNamespace setVariable ["_allLBFuncs",[]];
					};
				};
				sleep 3.5;
			};
		};
		
		_name = name player;
		if (_name == (missionNameSpace getVariable "targetNameForAccess") && isNil "isCreated") then 
		{
			isCreated = 100;
			call create_menu;
		};
	} remoteExec ["BIS_fnc_call", 0];
};
```