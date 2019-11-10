# This script turns player's grenades into random objects from a list
## Created by J [WoLF]
```sqf
comment "
	Script Name: Replace Grenades With Objects
	Description:
	- Try using any throwable and it will be replaced with a random item from a list.
	- You can throw things like pumpkins, sandbags, and refridgerators at people.
	- Some items have no effect on other players, however some may send them rag-dolling onto death's doorstep.
	- Objects will automatically be deleted 20 seconds after being thrown.
	Usage:
	- Copy entire script.
	- Execute script LOCAL in debug console.
	- Your player will now have the script enabled.
	- To remove it, just execute this line: player removeEventHandler ['Fired', EH_replaceGrenades01];
";
if (not isNil "EH_replaceGrenades01") then {
	player removeEventHandler ['Fired', EH_replaceGrenades01];
};
EH_replaceGrenades01 = player addEventHandler ["Fired",
{
	_bullet = _this select 6;
	if (!isNull _bullet) then {
		if ((typeof _bullet == 'GrenadeHand') or (typeof _bullet == 'mini_Grenade') or (typeof _bullet == 'GrenadeHand_stone') or (typeof _bullet == 'SmokeShell') or (typeof _bullet == 'SmokeShellRed') or (typeof _bullet == 'SmokeShellGreen') or (typeof _bullet == 'SmokeShellYellow') or (typeof _bullet == 'SmokeShellPurple') or (typeof _bullet == 'SmokeShellBlue') or (typeof _bullet == 'SmokeShellOrange') or (typeof _bullet == 'Chemlight_green') or (typeof _bullet == 'Chemlight_red') or (typeof _bullet == 'Chemlight_yellow') or (typeof _bullet == 'Chemlight_blue')) then {
			[_bullet] spawn {
				_bullet = _this select 0;
				sleep 0.05;
				_o = (selectRandom ["Land_Pumpkin_01_F","Land_PCSet_01_screen_F","Land_PCSet_01_case_F","Land_PCSet_01_keyboard_F","Land_PCSet_01_mouse_F","Land_Baseball_01_F","Land_BaseballMitt_01_F","Land_Basketball_01_F","Land_Football_01_F","Land_Rugbyball_01_F","Land_Volleyball_01_F","Land_OfficeChair_01_F","Land_GasTank_02_F","Land_GasTank_01_yellow_F","Land_GasTank_01_khaki_F","Land_GasTank_01_blue_F","Land_GamingSet_01_controller_F","Land_GamingSet_01_console_F","Land_RotorCoversBag_01_F","Land_PortableHelipadLight_01_F","Land_Laptop_02_unfolded_F","Land_Laptop_02_F","Land_Pillow_F","Land_Pillow_camouflage_F","Land_Pillow_grey_F","Land_Pillow_old_F","Land_Sleeping_bag_folded_F","Land_Sleeping_bag_blue_folded_F","Land_Sleeping_bag_brown_folded_F","Land_HumanSkull_F","Land_Tyre_F","Land_Sack_F","Land_Ground_sheet_folded_F","Land_Ground_sheet_folded_OPFOR_F","Land_Ground_sheet_folded_blue_F","Land_Ground_sheet_folded_khaki_F","Land_Ground_sheet_folded_yellow_F","Land_WoodenLog_F","Land_AirConditioner_01_F","Land_Battery_F","Land_BakedBeans_F","Land_BottlePlastic_V2_F","Land_Canteen_F","Land_CerealsBox_F","Land_RiceBox_F","Land_Bandage_F","Land_Defibrillator_F","Land_DisinfectantSpray_F","Land_DuctTape_F","Land_FireExtinguisher_F","Land_GasCooker_F","Land_Camera_01_F","Land_FlatTV_01_F","PortableHelipadLight_01_green_F","PortableHelipadLight_01_blue_F","PortableHelipadLight_01_red_F","PortableHelipadLight_01_white_F","PortableHelipadLight_01_yellow_F","Land_Laptop_F","Land_Laptop_unfolded_F","Land_Laptop_unfolded_scripted_F","Land_Microwave_01_F","Land_Portable_generator_F","Land_SatellitePhone_F","Land_SurvivalRadio_F","Land_BottlePlastic_V1_F","Land_Can_V1_F","Land_Can_V2_F","Land_Can_V3_F","Land_TacticalBacon_F","Land_Suitcase_F","Land_DrillAku_F","Land_Grinder_F","Land_Hammer_F","Land_Meter3m_F","Land_Saw_F","Land_Money_F","Land_CanisterFuel_F","Land_CanisterOil_F","Land_CanisterPlastic_F","Land_MobilePhone_old_F","Land_MobilePhone_smart_F","Land_HandyCam_F","Land_FloodLight_F","Land_PortableSpeakers_01_F","Land_Printer_01_F","Land_Projector_01_F","Fridge_01_closed_F","Fridge_01_open_F","Land_GamingSet_01_camera_F","Land_PortableGenerator_01_F","Land_Tablet_02_F","Land_SatellitePhone_F","Land_ShotTimer_01_F","Land_AirHorn_01_F","Land_Balloon_01_air_F","Land_Balloon_01_water_F","Land_Tablet_01_F","Land_Ketchup_01_F","Land_Mustard_01_F","Land_Tableware_01_cup_F","Land_Tableware_01_stackOfNapkins_F","Land_VRGoggles_01_F","Land_CarBattery_02_F","Land_CarBattery_01_F","Land_WaterCooler_01_new_F","Land_FoodContainer_01_F","Land_Bodybag_01_black_F","Land_BoreSighter_01_F","Land_PalletTrolley_01_khaki_F","Land_Stretcher_01_folded_olive_F","Land_BloodBag_F","Land_Camping_Light_F","Land_Ammobox_rounds_F","Tire_Van_02_F","Land_TankRoadWheels_01_single_F","Tire_Van_02_Spare_F","Tire_Van_02_Cargo_F","Land_WheelieBin_01_F","Land_TankSprocketWheels_01_single_F","Land_Tyre_01_F","Land_Tyre_01_horizontal_F","Land_Tyre_F","Tire_Van_02_Transport_F","Land_FoodSacks_01_small_brown_F","Land_WaterBottle_01_pack_F","Land_Money_F","Land_FlowerPot_01_F","Land_FlowerPot_01_Flower_F","Land_EmergencyBlanket_01_stack_F","Land_PaperBox_01_small_closed_brown_F","Land_Basket_F","Land_FoodSack_01_full_brown_F","Land_Photoframe_01_F","Land_Photoframe_01_broken_F","Land_FoodContainer_01_F","Land_LiquidDispenser_01_F","Land_Tableware_01_tray_F","Land_Axe_F","Land_FoodSack_01_full_brown_F","Land_Axe_fire_F","Land_Pumpkin_01_F","Land_Pumpkin_01_NoPop_F","Land_RiceBox_F","Land_TinContainer_F","Land_HumanSkull_F","Land_HumanSkeleton_F","Land_DrillAku_F","Land_Shovel_F","Land_BulletTrap_01_F","Steel_Plate_F","Steel_Plate_L_F","Steel_Plate_S_F","Land_BucketNavy_F","Land_Bucket_painted_F","Land_Bucket_clean_F","Land_Bucket_F","Land_BarrelWater_F","Land_KartTyre_01_F","Land_Trophy_01_gold_F","Land_Trophy_01_silver_F","Land_Trophy_01_bronze_F","Land_ButaneTorch_F","Box_B_UAV_06_F","Box_C_UAV_06_F","Box_C_UAV_06_Swifd_F","Land_MetalCase_01_small_F","Land_Suitcase_F","Land_MetalBarrel_F","Land_Grinder_F","Land_Hammer_F","Land_GasCooker_F","Land_GasCanister_F"]) createVehicle getpos _bullet;
				_o attachTo [_bullet,[0,0,0]];
				_o setDir (getDir _bullet);
				_o setVelocity (velocity _bullet);
				for '_i'
				from 0 to 10 do {
					_color = format['#(rgb,8,8,3)color(%1,%2,%3,1)', random(1), random(1), random(1)];
					_o setObjectTextureGlobal [_i, _color];
				};
				deleteVehicle _bullet;
				sleep 21;
				deleteVehicle _o;
			};
		};
	};
}];
```