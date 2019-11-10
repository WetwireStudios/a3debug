[Home](readme.md)
## Textures
### ARGB
```sqf
BLACK:
cursorObject setObjectTextureGlobal [0, "#(argb,8,8,3)color(0,0,0,1)"];

OLIVE:
cursorObject setObjectTextureGlobal [0, "#(argb,8,8,3)color(0.33,0.31,0.24,0.3)"];

SAND:
cursorObject setObjectTextureGlobal [0, "#(argb,8,8,3)color(0.26,0.24,0.17,0.54)"];

ORANGE:
cursorObject setObjectTextureGlobal [0, "#(argb,8,8,3)color(1,0.4,0.1,0.3)"];
```
### Re-texture
#### Only works on vehicles that have the specified texture in vanilla files
```sqf
BLACK:
[cursorObject,["black",1]] call BIS_fnc_initVehicle;

OLIVE:
[cursorObject,["olive",1]] call BIS_fnc_initVehicle;

SAND:
[cursorObject,["sand",1]] call BIS_fnc_initVehicle;
```

### Specific Vehicles (Cursor Target)
#### V-44 Blackfish (Navy Blue)
```sqf
cursorObject setObjectTextureGlobal [0,'\A3\Air_F_exp\VTOL_01\Data\VTOL_01_EXT01_blue_CO.paa'];
cursorObject setObjectTextureGlobal [1,'\A3\Air_F_exp\VTOL_01\Data\VTOL_01_EXT02_blue_CO.paa'];
cursorObject setObjectTextureGlobal [2,'\A3\Air_F_exp\VTOL_01\Data\VTOL_01_EXT03_blue_CO.paa'];
cursorObject setObjectTextureGlobal [3,'\A3\Air_F_exp\VTOL_01\Data\VTOL_01_EXT04_blue_CO.paa'];
```

#### UH-80 Ghost Hawk (Olive)
```sqf
cursorObject setObjectTextureGlobal [0,'\A3\air_f_beta\Heli_Transport_01\Data\Heli_Transport_01_ext01_BLUFOR_CO.paa'];
cursorObject setObjectTextureGlobal [1,'\A3\air_f_beta\Heli_Transport_01\Data\Heli_Transport_01_ext02_BLUFOR_CO.paa'];
```
#### NATO Strider (Sand)
```sqf
cursorObject setObjectTextureGlobal [0,'\A3\soft_f_beta\mrap_03\data\mrap_03_ext_co.paa'];
cursorObject setObjectTextureGlobal [1,'\A3\data_f\vehicles\turret_co.paa'];
```
#### NATO Prowler
##### Olive
```sqf
cursorObject setObjectTextureGlobal [0,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_01_olive_CO.paa'];
cursorObject setObjectTextureGlobal [1,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_02_olive_CO.paa'];
cursorObject setObjectTextureGlobal [2,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_03_olive_CO.paa'];
cursorObject setObjectTextureGlobal [3,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_Adds_olive_CO.paa'];
```
##### Sand
```sqf
cursorObject setObjectTextureGlobal [0,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_01_sand_CO.paa'];
cursorObject setObjectTextureGlobal [1,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_02_sand_CO.paa'];
cursorObject setObjectTextureGlobal [2,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_03_sand_CO.paa'];
cursorObject setObjectTextureGlobal [3,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_Adds_sand_CO.paa'];
```
##### Black
```sqf
cursorObject setObjectTextureGlobal [0,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_01_black_CO.paa'];
cursorObject setObjectTextureGlobal [1,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_02_black_CO.paa'];
cursorObject setObjectTextureGlobal [2,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_03_black_CO.paa'];
cursorObject setObjectTextureGlobal [3,'\A3\soft_f_exp\LSV_01\Data\NATO_LSV_Adds_black_CO.paa'];
```

#### NATO Gorgon (Sand)
```
cursorObject setObjectTextureGlobal [0, "A3\Armor_F_Gamma\APC_Wheeled_03\Data\apc_wheeled_03_ext_co.paa"];
cursorObject setObjectTextureGlobal [1, "A3\Armor_F_Gamma\APC_Wheeled_03\Data\apc_wheeled_03_ext2_co.paa"];
cursorObject setObjectTextureGlobal [2, "A3\Armor_F_Gamma\APC_Wheeled_03\Data\rcws30_co.paa"];
cursorObject setObjectTextureGlobal [3, "A3\Armor_F_Gamma\APC_Wheeled_03\Data\apc_wheeled_03_ext_alpha_co.paa"];
```
####  Pawnee / Hummingbird
##### Black
```sqf
cursorObject setObjectTextureGlobal [0, "\a3\air_f\Heli_Light_01\Data\heli_light_01_ext_ion_co.paa"];
```
##### AAF
```sqf
cursorObject setObjectTextureGlobal [0, "A3\Air_F\Heli_Light_01\Data\heli_light_01_ext_indp_co.paa"];
```
#### AAF Orca (Digi)
```sqf
cursorObject setObjectTextureGlobal [0, "\a3\air_f\Heli_Light_02\Data\heli_light_02_ext_indp_co.paa"];
```
#### Civilian Orca (Black and Yellow)
```sqf
cursorObject setObjectTextureGlobal [0, "\a3\air_f\Heli_Light_02\Data\heli_light_02_ext_civilian_co.paa"];
```

#### Civilian Mohawk
```sqf
cursorObject setObjectTextureGlobal [0,"a3\air_f_beta\Heli_Transport_02\Data\Skins\heli_transport_02_1_dahoman_co.paa"];
cursorObject setObjectTextureGlobal [1,"a3\air_f_beta\Heli_Transport_02\Data\Skins\heli_transport_02_2_dahoman_co.paa"];
cursorObject setObjectTextureGlobal [2,"a3\air_f_beta\Heli_Transport_02\Data\Skins\heli_transport_02_3_dahoman_co.paa"];
```
#### ION Mohawk
```sqf
cursorObject setObjectTextureGlobal [0,"a3\air_f_beta\Heli_Transport_02\Data\Skins\heli_transport_02_1_ion_co.paa"];
cursorObject setObjectTextureGlobal [1,"a3\air_f_beta\Heli_Transport_02\Data\Skins\heli_transport_02_2_ion_co.paa"];
cursorObject setObjectTextureGlobal [2,"a3\air_f_beta\Heli_Transport_02\Data\Skins\heli_transport_02_3_ion_co.paa"];
```
#### CSAT Buzzard
```sqf
cursorObject setObjectTextureGlobal [0,"a3\Air_F_Gamma\Plane_Fighter_03\Data\Plane_Fighter_03_body_1_brownhex_CO.paa"];  
cursorObject setObjectTextureGlobal [1,"a3\Air_F_Gamma\Plane_Fighter_03\Data\Plane_Fighter_03_body_2_brownhex_CO.paa"];
```
#### CSAT Buzzard (Gray)
```sqf
cursorObject setObjectTextureGlobal [0,"a3\Air_F_Gamma\Plane_Fighter_03\Data\Plane_Fighter_03_body_1_greyhex_CO.paa"];  
cursorObject setObjectTextureGlobal [1,"a3\Air_F_Gamma\Plane_Fighter_03\Data\Plane_Fighter_03_body_2_greyhex_CO.paa"];
```
#### Y-32 Xi'an (Reskin)
```sqf
_obj = cursorObject;
_tex = "A3\Air_F_Exp\Heli_Transport_01\Data\Heli_Transport_01_ext01_tropic_CO.paa";
_obj setObjectTextureGlobal[0,_tex];
_obj setObjectTextureGlobal[1,_tex];
_obj setObjectTextureGlobal[2,_tex];
_obj setObjectTextureGlobal[3,_tex];
```

## Flags (Executed on cursor)
### Single Color Flags
```sqf
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_red_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_green_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_blue_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_white_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_fd_red_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_fd_green_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_fd_blue_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_fd_orange_CO.paa";
```
### Country Flags
```sqf
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_uk_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_us_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_AAF_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_Altis_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_CSAT_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_FIA_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_AltisColonial_CO.paa";
```
### Organizations and Groups
```sqf
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_armex_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_bis_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_ion_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_larkin_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_nato_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_quontrol_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_uno_CO.paa";
cursorObject forceFlagTexture "\A3\Data_F\Flags\flag_vrana_CO.paa";
```
### Medical
```sqf
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_rcrystal_CO.paa";
```
### Misc
```sqf
cursorObject forceFlagTexture "\A3\Data_F\Flags\Flag_pow_CO.paa";
cursorObject forceFlagTexture "\A3\Signs_F\SignSpecial\data\checker_flag_co.paa";
```
### Remove Flag
```sqf
this forceFlagTexture "";
```
