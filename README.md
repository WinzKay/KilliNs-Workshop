# KilliNs-Workshop
import flash.display.MovieClip;
import flash.media.SoundTransform;
import flash.geom.ColorTransform;
import fl.transitions.TweenEvent;
import fl.transitions.Tween;
import fl.transitions.easing.*;

//Tabs
var floatingText:MovieClip = new FloatingText();
var itemsTab:MovieClip = new ItemsTab();
var changelogTab:MovieClip = new ChangelogTab();
var partsPacksTab:MovieClip = new PartsPacksTab();
var paintTab:MovieClip = new PaintTab();
var getOpponentTab:MovieClip = new GetOpponentTab();
var battleInfoTab:MovieClip = new BattleInfoTab();
var importExportTab:MovieClip = new ImportExportTab();

//Stats
var isKg:KgB = new KgB();
var isHp:HpB = new HpB();
var isDmg:DmgB = new DmgB();
var isHeatDmg:HeatDmgB = new HeatDmgB();
var isEneDmg:EneDmgB = new EneDmgB();
var isResDmg:ResDmgB = new ResDmgB();
var isHeat:HeatB = new HeatB();
var isCool:CoolB = new CoolB ();
var isEne:EneB = new EneB();
var isReg:RegB = new RegB();
var isPhyRes:PhyResB = new PhyResB();
var isExpRes:ExpResB = new ExpResB();
var isEleRes:EleResB = new EleResB();
var isHeatCapDmg:HeatCapDmgB = new HeatCapDmgB();
var isCoolDmg:CoolDmgB = new CoolDmgB();
var isEneCapDmg:EneCapDmgB = new EneCapDmgB();
var isRegDmg:RegDmgB = new RegDmgB();
var isPush:PushB = new PushB();
var isPull:PullB = new PullB();
var isRange:RangeB = new RangeB();
var isWalk:WalkB = new WalkB();
var isJump:JumpB = new JumpB();
var isUses:UsesB = new UsesB();
var isEneCost:EneCostB = new EneCostB();
var isHeatGen:HeatGenB = new HeatGenB();

//Sounds
var generalVol:SoundTransform = new SoundTransform(.3);
var overButtonMp3 = new OverButtonMp3();
var floatingTextMp3 = new FloatingTextMp3();
var stompMp3:StompMp3 = new StompMp3();
var shutdownMp3:ShutdownMp3 = new ShutdownMp3();
var mechStepMp3:MechStepMp3 = new MechStepMp3();
var heavyImpactMp3:HeavyImpactMp3 = new HeavyImpactMp3();
var grapplingHookMp3:GrapplingHookMp3 = new GrapplingHookMp3();

//Colors
var blank:ColorTransform = new ColorTransform(1,1,1,1,0,0,0);
var white:ColorTransform = new ColorTransform(1,1,1,1,50,50,50);
var red:ColorTransform = new ColorTransform(1,0,0,1,0,0,0);
var green:ColorTransform = new ColorTransform(0,1,0,1,0,0,0);
var customPaint:ColorTransform = new ColorTransform(.5,.5,.5);

//General
var weight:uint = 0;
var health:uint = 0;
var energy:uint = 0;
var regen:uint = 0;
var heat:uint = 0;
var cooling:uint = 0;
var phyRes:uint = 0;
var expRes:uint = 0;
var eleRes:uint = 0;

var arenaBuffs:Boolean = true;
var healthBuff:uint = 300;
var energyBuff:Number = 1.20;
var regenBuff:Number = 1.20;
var heatBuff:Number = 1.20;
var coolingBuff:Number = 1.20;
var phyResBuff:Number = 1.40;
var expResBuff:Number = 1.40;
var eleResBuff:Number = 1.40;

var prevOpTorso:int = -1;
var prevOpLegs:int = -1;
var prevOpSide1:int = -1;
var prevOpSide2:int = -1;
var prevOpSide3:int = -1;
var prevOpSide4:int = -1;
var prevOpTop1:int = -1;
var prevOpTop2:int = -1;
var prevOpDrone:int = -1;
var prevOpCharge:int = -1
var prevOpTele:int = -1;
var prevOpHook:int = -1;
var prevOpMod1:int = -1;
var prevOpMod2:int = -1;
var prevOpMod3:int = -1;
var prevOpMod4:int = -1;
var prevOpMod5:int = -1;
var prevOpMod6:int = -1;
var prevOpMod7:int = -1;
var prevOpMod8:int = -1;
var prevOpPaint:ColorTransform = null;
var prevPlPaint:ColorTransform = null;

var onTabItems:Array = new Array();
var slot:Array = new Array();
var itemDB:Array = new Array();
var getOfficialItems:Boolean = true;
var getFanMadeItems:Boolean = false;
var getSpecialItems:Boolean = false;
var initWorkshop:Boolean = true;
var hasPreviousOpponent:Boolean = false;
var currentSlot:Object = null;
var floatingTextCount:int = 0;
var currentItemStats:Array = new Array();
var mechStructure:Array = new Array();
var badWeaponsList:Array = new Array();
var i:int = 0;
var opponentClass:String = "Dumb";
const C:String = "click";
const ver:String = "-";

var workshopMech:Array = new Array();
var playerMech:Array = new Array();
var opponentMech:Array = new Array();

var torso:Array = new Array();
var	legs:Array = new Array();
var	side:Array = new Array();
var	top:Array = new Array();
var	drone:Array = new Array();
var	charge:Array = new Array();
var	teleporter:Array = new Array();
var	hook:Array = new Array();
var	module:Array = new Array();
var itemTypesList:Array = new Array(torso, legs, side, top, drone, charge, teleporter, hook, module);

//Torsos
itemDB.push([Interceptor,0,"Interceptor",1,309,860,0,0,0,0,0,265,80,193,56,16,22,22,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([Archimonde,0,"Archimonde",1,363,1090,0,0,0,0,0,265,76,265,76,22,22,22,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([Avenger,0,"Avenger",1,350,1242,0,0,0,0,0,145,48,193,64,16,22,22,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([Nightmare,0,"Nightmare",2,315,879,0,0,0,0,0,290,96,193,64,22,16,22,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([Brutality,0,"Brutality",2,341,1033,0,0,0,0,0,290,88,217,64,22,16,22,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([Windigo,0,"Windigo",2,345,982,0,0,0,0,0,301,112,217,72,22,16,22,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([Zarkares,0,"Zarkares",2,362,1136,0,0,0,0,0,312,112,193,64,16,24,16,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([MoltenPlatinumVest,0,"Molten Platinum Vest",2,346,982,0,0,0,0,0,267,96,193,64,44,16,22,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([Sith,0,"Sith",3,312,930,0,0,0,0,0,193,64,245,112,22,22,16,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([Naga,0,"Naga",3,335,982,0,0,0,0,0,193,72,279,104,22,22,16,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([GrimReaper,0,"GrimReaper",3,329,879,0,0,0,0,0,193,64,346,112,22,22,16,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([ThunderPlatinumVest,0,"Thunder Platinum Vest",3,346,982,0,0,0,0,0,193,64,267,96,44,22,16,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([DefenseMatrixTorso,0,"Defense Matrix Torso",0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,"Torso used in legacy damage challenge.",""]);
//Legs
itemDB.push([IronBoots,1,"Iron Boots",1,138,472,163,213,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,1,2,0,0,0,0,"","jump"]);
itemDB.push([RollingBeasts,1,"Rolling Beasts",1,134,451,160,242,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,3,0,0,0,0,0,"","roll"]);
itemDB.push([GraveDiggers,1,"Grave Diggers",1,123,287,223,285,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,1,0,1,2,0,0,0,0,"","jmup"]);
itemDB.push([TheClaw,1,"The Claw",1,150,860,79,111,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,"","walk"]);
itemDB.push([TheElephantsFoot,1,"The Elephant's Foot",1,168,628,204,312,0,0,10,0,0,0,0,10,0,0,0,0,0,0,2,0,1,0,1,0,0,0,0,1,"Item made by Xzyckon.","walk"]);
itemDB.push([ScorchingFeet,1,"Scorching Feet",2,120,413,143,187,36,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,1,2,0,0,0,0,"","jump"]);
itemDB.push([DevouringPaws,1,"Devouring Paws",2,119,394,140,220,44,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,1,2,0,0,0,0,"","jump"]);
itemDB.push([DynamiteBoots,1,"Dynamite Boots",2,136,413,133,224,29,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,1,0,1,2,0,0,0,0,"","jump"]);
itemDB.push([ChargedWalkers,1,"Charged Walkers",3,122,413,143,187,0,48,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,1,2,0,0,0,0,"","jump"]);
itemDB.push([DynamicStompers,1,"Dynamic Stompers",3,118,372,154,217,0,58,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,1,2,0,0,0,0,"","jump"]);
itemDB.push([SparkedRunners,1,"Sparked Runners",3,114,363,135,249,0,38,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,3,0,0,0,0,0,"","roll"]);
itemDB.push([LightningSupporters,1,"Lightning Supporters",3,124,413,127,192,0,67,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,1,2,0,0,0,0,"","jump"]);
itemDB.push([RecoilStompers,1,"Recoil Stompers",3,138,413,140,216,0,38,0,0,0,0,0,0,0,0,0,0,0,0,2,0,1,0,1,2,0,0,0,0,"","jump"]);
itemDB.push([DefenseMatrixLegs,1,"Defense Matrix Legs",0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,"Legs used in legacy damage challenge.","subType"]);
//Side Weapons
itemDB.push([BackBreaker,2,"BackBreaker",1,44,0,228,408,0,0,0,0,0,0,0,0,0,0,0,8,0,8,1,0,1,0,0,0,0,31,31,0,"","axe"]);
itemDB.push([WarHammer,2,"War Hammer",1,58,0,237,398,0,0,0,0,0,0,0,0,0,0,15,0,15,0,3,0,1,0,0,0,0,31,31,0,"","hammer"]);
itemDB.push([SeraphBlade,2,"SeraphBlade",1,49,0,234,376,0,0,12,0,0,0,0,0,0,0,0,0,0,0,0,0,1,2,0,0,0,13,50,0,"","sword"]);
itemDB.push([Annihilation,2,"Annihilation",1,65,0,203,341,0,0,15,0,0,0,0,0,0,0,0,0,0,0,0,0,1,2,0,0,3,0,0,0,"","machinegun"]);
itemDB.push([Mercy,2,"Mercy",1,84,0,197,440,0,0,10,0,0,0,0,0,0,0,0,0,0,0,1,0,1,2,0,0,3,0,0,0,"","shotgun"]);
itemDB.push([ArmorAnnihilator,2,"Armor Annihilation",1,17,0,39,52,0,0,40,0,0,0,0,0,0,0,0,0,0,0,0,0,2,4,0,0,1,0,0,0,"","common"]);
itemDB.push([ArmorDissolver,2,"Armor Dissolver",1,18,0,41-55,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,0,2,4,0,0,2,0,62,0,"","common"]);
itemDB.push([Purifier,2,"Purifier",1,49,0,163,213,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,4,0,0,0,0,0,0,"","common"]);
itemDB.push([NightFall,2,"NightFall",1,49,0,248,366,0,0,11,0,0,0,0,0,0,0,0,0,0,0,0,0,2,4,0,0,3,31,31,0,"","machinegun"]);
itemDB.push([BloodWeep,2,"BloodWeep",1,34,0,147,209,0,0,20,0,0,0,0,0,0,0,0,0,0,0,0,0,2,4,0,0,3,31,31,0,"","common"]);
itemDB.push([TerrorCry,2,"Terror Cry",1,46,0,214,331,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,2,4,0,0,3,25,25,0,"","greenade"]);
itemDB.push([Sweetie,2,"Sweetie",1,42,0,169,256,0,0,10,0,0,0,0,0,0,0,0,0,48,0,0,0,3,6,0,0,3,31,31,0,"","bullet"]);
itemDB.push([TerrorBlade,2,"TerrorBlade",2,52,0,244,319,86,0,0,0,0,0,0,0,0,0,32,0,0,0,1,0,1,0,0,0,0,13,50,0,"","axe"]);
itemDB.push([FlamingHammer,2,"Flaming Hammer",2,60,0,211,354,86,0,0,0,0,0,0,0,0,0,0,17,0,0,3,0,1,0,0,0,0,13,50,0,"","hammer"]);
itemDB.push([HeronMark,2,"HeronMark",2,43,0,193,311,78,0,9,0,0,0,0,0,0,0,0,0,0,0,0,0,1,2,0,0,0,13,50,0,"","sword"]);
itemDB.push([ChaosBringer,2,"Chaos Bringer",2,49,0,203,265,71,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,2,0,0,0,16,45,0,"","common"]);
itemDB.push([CrismonRapture,2,"Crismon Rapture",2,52,0,163,213,135,0,0,0,0,0,0,0,0,0,48,0,0,0,0,0,1,2,0,0,3,31,93,0,"","flameThrower"]);
itemDB.push([Reckoning,2,"Reckoning",2,86,0,182,406,50,0,10,0,0,0,0,0,0,0,0,0,0,0,1,0,1,2,0,0,3,0,31,0,"","shotgun"]);
itemDB.push([BassaltDesolver,2,"Bassalt Desolver",2,23,0,32,65,44,0,40,0,0,0,0,0,0,0,0,0,0,0,0,0,2,4,0,0,1,0,0,0,"","common"]);
itemDB.push([MagmaBlast,2,"Magma Blast",2,55,0,243,463,93,0,13,0,0,0,0,0,0,0,30,17,0,0,1,0,2,4,0,0,1,0,31,0,"","heavyRocket"]);
itemDB.push([Sorrow,2,"Sorrow",2,66,0,163,213,93,0,0,0,0,0,0,0,0,0,12,0,0,0,0,0,2,4,0,0,0,0,31,0,"","common"]);
itemDB.push([Abomination,2,"Abomination",2,66,0,212,307,71,0,12,0,0,0,0,0,0,0,0,0,0,0,1,0,2,4,0,0,3,19,44,0,"","rocket"]);
itemDB.push([HeatBomb,2,"Heat Bomb",2,50,0,40,59,393,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,4,0,0,1,0,393,0,"","bomb"]);
itemDB.push([CorruptLight,2,"Corrupt Light",2,51,0,140,236,93,0,0,0,0,0,0,0,0,0,24,0,0,0,0,0,3,6,0,0,0,16,47,0,"","laser"]);
itemDB.push([DawnBlaze,2,"DawnBlaze",2,52,0,203,265,71,0,5,0,0,0,0,0,0,0,0,0,0,0,0,0,3,6,0,0,0,16,47,0,"","common"]);
itemDB.push([Flaminator,2,"Flaminator",2,47,0,148,228,93,0,0,0,0,0,0,0,0,0,24,0,0,0,0,0,3,6,0,0,0,110,0,0,"","common"]);
itemDB.push([StormWeaver,2,"StormWeaver",3,56,0,244,319,0,114,0,0,0,0,0,0,0,0,0,0,32,0,1,0,1,0,0,0,0,50,13,0,"","axe"]);
itemDB.push([VikingHammer,2,"Viking Hammer",3,63,0,211,354,0,114,0,0,0,0,0,0,0,0,0,0,0,17,3,0,1,0,0,0,0,50,13,0,"","hammer"]);
itemDB.push([BrightRoar,2,"BrightRoar",3,45,0,193,311,0,103,9,0,0,0,0,0,0,0,0,0,0,0,0,0,1,2,0,0,0,50,13,0,"","sword"]);
itemDB.push([BigDaddy,2,"BigDaddy",3,53,0,202,265,0,95,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,2,0,0,0,47,16,0,"","regular"]);
itemDB.push([AshCreator,2,"Ash Creator",3,58,0,163,213,0,180,0,0,0,0,0,0,0,0,0,0,44,0,0,0,1,2,0,0,3,93,31,0,"","flameThrower"]);
itemDB.push([BullDog,2,"BullDog",3,73,0,182,406,0,67,10,0,0,0,0,0,0,0,0,0,0,0,1,0,1,2,0,0,3,31,0,0,"","shotgun"]);
itemDB.push([EMP,2,"EMP",3,70,0,37,61,0,334,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,4,0,0,1,393,0,0,"","bomb"]);
itemDB.push([MortalBullet,2,"Mortal Bullet",3,56,0,163,213,0,123,0,0,0,0,0,0,0,0,0,0,12,0,0,0,2,4,0,0,0,31,0,0,"","common"]);
itemDB.push([LastWords,2,"Last Words",3,63,0,185,285,0,95,0,0,0,0,0,0,0,0,0,0,0,13,1,0,2,4,0,0,3,47,16,0,"","greenade"]);
itemDB.push([BunkerShell,2,"Bunker Shell",3,50,0,243,463,0,123,13,0,0,0,0,0,0,0,0,0,30,17,1,0,2,4,0,0,1,31,0,0,"","heavyRocket"]);
itemDB.push([MaliceBeam,2,"Malice Beam",3,55,0,140,236,0,123,0,0,0,0,0,0,0,0,0,0,24,0,0,0,3,6,0,0,0,47,12,0,"","laser"]);
itemDB.push([UltraBright,2,"UltraBright",3,56,0,203,265,0,95,5,0,0,0,0,0,0,0,0,0,0,0,0,0,3,6,0,0,0,47,16,0,"","common"]);
itemDB.push([HotFlash,2,"Hot Flash",3,66,0,148,228,0,123,0,0,0,0,0,0,0,0,0,0,24,0,0,0,3,6,0,0,0,0,110,0,"","common"]);
itemDB.push([DefenseMatrixWeapon,2,"Defense Matrix Weapon",0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,"Weapon used in legacy damage challenge.","common"]);
//Top Weapons
itemDB.push([NighEagle,3,"Night Eagle",1,46,0,209,336,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,3,6,0,0,3,25,25,0,"","greenade"]);
itemDB.push([SpartanCarnage,3,"SpartanCarnage",1,51,0,226,387,0,0,15,0,0,0,0,0,0,0,0,0,0,0,0,0,3,6,0,0,3,31,31,0,"","machinegun"]);
itemDB.push([RecklessBeam,3,"Reckless Beam",1,35,0,188,283,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,4,8,0,0,0,31,31,0,"","laser"]);
itemDB.push([DesertFury,3,"Desert Fury",1,29,0,154,224,0,0,23,0,0,0,0,0,0,0,0,0,0,0,0,0,4,8,0,0,2,16,16,0,"","common"]);
itemDB.push([MightyCannon,3,"Mighty Cannon",1,55,0,226,387,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,4,8,0,0,0,38,38,0,"","orb"]);
itemDB.push([Falcon,3,"Falcon",1,19,0,596,997,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,8,0,0,0,1,22,22,0,"","common"]);
itemDB.push([SupremeCannon,3,"Supreme Cannon",2,66,0,205,315,71,0,11,0,0,0,0,0,0,0,0,0,0,0,1,0,3,6,0,0,3,19,44,0,"","rocket"]);
itemDB.push([VandalRage,3,"Vandal Rage",2,41,0,143,187,44,0,20,0,0,0,0,0,0,0,0,46,0,0,1,0,4,5,0,0,1,0,25,0,"","common"]);
itemDB.push([Desolation,3,"Desolation",2,66,0,210,310,48,0,10,0,0,0,0,0,0,0,0,0,0,0,0,0,4,8,0,0,3,0,81,0,"","aboveRocket"]);
itemDB.push([IronFrenzy,3,"Iron Frenzy",2,52,0,203,265,71,0,5,0,0,0,0,0,0,0,0,0,0,0,0,0,4,8,0,0,0,16,47,0,"","beam"]);
itemDB.push([DesertSnake,3,"Desert Snake",2,63,0,192,329,71,0,0,0,0,0,0,0,0,0,0,7,0,0,0,1,4,8,0,0,0,25,75,0,"","orb"]);
itemDB.push([Savagery,3,"Savagery",2,51,0,150,228,93,0,0,0,0,0,0,0,0,0,24,0,0,0,0,0,4,8,0,0,0,16,47,0,"","laser"]);
itemDB.push([FlamingScope,3,"Flaming Scope",2,21,0,568,741,212,0,15,0,0,0,0,0,0,0,0,0,0,0,0,0,8,0,0,0,1,31,155,0,"","common"]);
itemDB.push([BurningShower,3,"Burning Shower",2,75,0,173,345,86,0,12,0,0,0,0,0,0,0,0,10,0,0,0,2,4,8,0,0,3,0,81,0,"","diagonalRocket"]);
itemDB.push([GrimCobra,3,"Grim Cobra",3,63,0,181,290,0,95,0,0,0,0,0,0,0,0,0,0,0,13,0,1,3,6,0,0,3,47,16,0,"","greenade"]);
itemDB.push([Hysteria,3,"Hysteria",3,55,0,150,228,0,123,0,0,0,0,0,0,0,0,0,0,24,0,0,0,4,8,0,0,0,47,16,0,"","laser"]);
itemDB.push([ValiantSniper,3,"Valiant Sniper",3,51,0,135,196,0,181,17,0,0,0,0,0,0,0,0,0,0,13,0,0,4,8,0,0,2,31,0,0,"","common"]);
itemDB.push([SpineFall,3,"SpineFall",3,67,0,192,329,0,95,0,0,0,0,0,0,0,0,0,0,0,7,0,1,4,8,0,0,0,75,25,0,"","orb"]);
itemDB.push([Delerium,3,"Delerium",3,56,0,203,265,0,95,5,0,0,0,0,0,0,0,0,0,0,0,0,0,4,8,0,0,0,47,16,0,"","beam"]);
itemDB.push([LightningScope,3,"Lightning Scope",3,23,0,568,741,0,283,15,0,0,0,0,0,0,0,0,0,0,0,0,0,8,0,0,0,1,155,31,0,"","common"]);
//Drones
itemDB.push([Void_Drone,4,"Void",1,29,0,143,187,0,0,5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,16,16,0,"","beam"]);
itemDB.push([HurlBat,4,"HurlBat",1,28,0,135,196,0,0,0,0,0,0,0,0,0,0,6,0,6,0,0,0,0,0,0,0,0,16,16,0,"","common"]);
itemDB.push([Greedy,4,"Greedy",1,20,0,72,117,0,0,10,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,16,16,0,"","bullet"]);
itemDB.push([DustMaker,4,"DustMaker",1,29,0,120,213,0,0,0,0,0,0,0,0,0,0,0,4,0,4,0,0,0,0,0,0,0,16,16,0,"","fireball"]);
itemDB.push([BackStabber,4,"BackStabber",1,56,0,138,222,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,16,16,0,"","greenade"]);
itemDB.push([Clash,4,"Clash",2,43,0,103,135,36,0,5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,31,0,"","beam"]);
itemDB.push([Nemo,4,"Nemo",2,43,0,97,141,36,0,0,0,0,0,0,0,0,0,12,0,0,0,0,0,0,0,0,0,0,0,31,0,"","common"]);
itemDB.push([Swoop,4,"Swoop",2,22,0,55,90,58,0,5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,31,31,0,"","bullet"]);
itemDB.push([Murmur,4,"Murmur",2,45,0,86,153,36,0,0,0,0,0,0,0,0,0,0,7,0,0,0,0,0,0,0,0,0,0,31,0,"","fireBall"]);
itemDB.push([FlameWave,4,"FlameWave",2,53,0,84,154,36,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,31,0,"","rocket"]);
itemDB.push([HeatPoint,4,"Heat Point",2,51,0,176,230,68,0,6,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,0,50,0,"","common"]);
itemDB.push([Snack,4,"Snack",3,30,0,103,135,0,48,5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,31,0,0,"","beam"]);
itemDB.push([Torment,4,"Torment",3,29,0,97,141,0,48,0,0,0,0,0,0,0,0,0,0,12,0,0,0,0,0,0,0,0,31,0,0,"","common"]);
itemDB.push([WindForge,4,"WindForge",3,27,0,55,90,0,76,5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,31,0,0,"","bullet"]);
itemDB.push([Anguish,4,"Anguish",3,30,0,86,153,0,48,0,0,0,0,0,0,0,0,0,0,0,7,0,0,0,0,0,0,0,31,0,0,"","fireBall"]);
itemDB.push([Shockwave,4,"Shockwave",3,57,0,103,135,0,48,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,31,0,0,"","fireBall"]);
itemDB.push([FaceShocker,4,"Face Shoker",3,41,0,163,213,0,76,6,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,50,0,0,"","common"]);
//Charges
itemDB.push([ChargeEngine,5,"Charge Engine",1,20,0,132,174,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,"","charge"]);
//Teleporters
itemDB.push([TeleporterMarkI,6,"Teleporter Mark I (Legacy)",3,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,31,0,0,"","teleport"]);
itemDB.push([AdvancedTeleporter,6,"Advanced Teleporter",3,11,0,103,135,0,48,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,31,0,0,"","teleport"]);
itemDB.push([DoubleTeleporter,6,"Double Teleporter",3,26,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,20,0,0,"","teleport"]);
//Hooks
itemDB.push([PlatinumGrapplingHook,7,"Platinum Grappling Hook",1,17,0,143,187,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,"","hook"]);
itemDB.push([FlamingGrapplingHook,7,"Flaming Grappling Hook",2,16,0,111,145,39,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,31,0,"","hook"]);
itemDB.push([ShockingGrapplingHook,7,"Shocking GrapplingHook",3,11,0,103,135,0,48,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,31,0,0,"","hook"]);
//Modules
itemDB.push([IronPlating,8,"Iron Plating",1,40,145,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([PlatinumPlating,8,"Platinum Plating",1,40,315,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([HeatEngine,8,"Heat Engine",2,25,0,0,0,0,0,0,89,42,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([HeatMassBooster,8,"Heat Mass Booster",2,15,0,0,0,0,0,0,0,63,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([HeatStorageUnit,8,"Heat Storage Unit",2,22,0,0,0,0,0,0,134,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([EnergyEngine,8,"Energy Engine",3,25,0,0,0,0,0,0,0,0,89,42,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([EnergyMassBooster,8,"Energy Mass Booster",3,15,0,0,0,0,0,0,0,0,0,63,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([EnergyStorageUnit,8,"Energy Storage Unit",3,22,0,0,0,0,0,0,0,0,134,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([MightyProtector,8,"Mighty Protector",1,28,0,0,0,0,0,0,0,0,0,0,59,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([UltraHotProtector,8,"UltraHot Protector",2,28,0,0,0,0,0,0,0,0,0,0,0,59,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([SuperChargeProtector,8,"SuperCharge Protector",3,28,0,0,0,0,0,0,0,0,0,0,0,0,59,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
itemDB.push([MaximumProtector,8,"Maximum Protector",0,51,0,0,0,0,0,0,0,0,0,0,39,39,39,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"",""]);
//itemDB.push([0Instance,1Type,"2Name",3element,4kg,5hp,6minDmg,7maxDmg,8heatDmg,9eleDmg,10resDmg,11heat,12cool,13ene,14reg,15phyRes,16expRes,17eleRes,18heatCapDmg,19coolDmg,20eneCapDmg,21regDmg,22push,23pull,24range1,25range2,26walk,27jump,28uses,29eneCost,30heatGen,31Pack,32"info",33"subtype"]);

for (i = 0; i < itemDB.length; i ++)
{
	trace(i, itemDB[i][2]);
}

label_txt.text = "V" + ver;

for (i = 0; i < itemDB.length; i++)
{
	itemTypesList[itemDB[i][1]].push(i);
}


var canceledWeapons:uint = 0;
function rngItem(q:*, t:uint): *
{
	var g:uint = itemTypesList[q][Math.floor(Math.random() * itemTypesList[q].length)];
	
	for (i = 0; i < badWeaponsList.length; i ++)
	{
		if (g == badWeaponsList[i])
			return rngItem(q, t);
	}
	
	if (t < 1)
		return g;
	else if (itemDB[g][3] == t)
		return g;
	else
		return rngItem(q, t);
}

function mcToBtn (s:MovieClip): void
{
	s.buttonMode = true;
	
	var q:uint = s.width;
	var w:uint = s.height;
	
	s.addEventListener(MouseEvent.CLICK, function (e:MouseEvent): void
	{
		s.width = q * 1.05;
		s.height = w * 1.05;
		e.currentTarget.transform.colorTransform = new ColorTransform(1,1,1,1,25,25,25);
	});
	s.addEventListener(MouseEvent.MOUSE_DOWN, function (e:MouseEvent): void
	{
		s.width = q;
		s.height = w;
		e.currentTarget.transform.colorTransform = new ColorTransform(1,1,1,1,50,50,50);
	});
	s.addEventListener(MouseEvent.MOUSE_OVER, function (e:MouseEvent): void
	{
		overButtonMp3.play(0,0,generalVol);
		s.width = q * 1.05;
		s.height = w * 1.05;
		e.currentTarget.transform.colorTransform = new ColorTransform(1,1,1,1,25,25,25);
	});
	s.addEventListener(MouseEvent.MOUSE_OUT, function (e:MouseEvent): void
	{
		s.width = q;
		s.height = w;
		e.currentTarget.transform.colorTransform = new ColorTransform(1,1,1,1,0,0,0);
	});
}

function setMechStructure (base:MovieClip, t:int, torso, legs, side1, side2, side3, side4, top1, top2, drone, p): void
{
	if (t == 2)
	{
		prevOpTorso = torso;
		prevOpLegs = legs;
		prevOpSide1 = side1;
		prevOpSide2 = side2;
		prevOpSide3 = side3;
		prevOpSide4 = side4;
		prevOpTop1 = top1;
		prevOpTop2 = top2;
		prevOpDrone = drone;
		prevOpPaint = p;
	}
	
	// Clear previous mech
	while (base.numChildren > 1)
	{
		base.removeChildAt(1);
	}
	while (mechType[t].length > 0)
	{
		mechType[t].shift();
	}
	
	//Build new mech
	if (torso > -1 && legs > -1)
	{
		var b:MovieClip = buildSprite(itemDB[legs][0], 0, 0, false, true);// Right leg
		var o:MovieClip = buildSprite(itemDB[torso][0], 0, 0, false, true);// Torso
		var c:MovieClip = buildSprite(itemDB[legs][0], 0, 0, false, true);// Left leg
		
		b.name = "rightLeg";
		o.name = "torso";
		c.name = "leftLeg";
		
		c.x = o.mcLeg1.x;
		c.y = c.height * -0.5;
		o.x = c.mcTorso.x + c.x - o.mcLeg1.x;
		o.y = c.mcTorso.y + c.y - o.mcLeg1.y;
		b.x = o.mcLeg2.x + o.x - b.mcTorso.x;
		b.y = o.mcLeg2.y + o.y - b.mcTorso.y;
		
		if (side2 > -1)
		{
			var d:MovieClip = buildSprite(itemDB[side2][0], 0, 0, false, true);// Side weapon 2
			d.name = "side2";
			d.x = o.mcSide2.x + o.x - d.mcTorso.x;
			d.y = o.mcSide2.y + o.y - d.mcTorso.y;
			mechType[t].push(d);
			base.addChild(d);
		}
		if (side4 > -1)
		{
			var e:MovieClip = buildSprite(itemDB[side4][0], 0, 0, false, true);// Side weapon 4
			e.name = "side4";
			e.x = o.mcSide4.x + o.x - e.mcTorso.x;
			e.y = o.mcSide4.y + o.y - e.mcTorso.y;
			mechType[t].push(e);
			base.addChild(e);
		}
		if (top2 > -1)
		{
			var f:MovieClip = buildSprite(itemDB[top2][0], 0, 0, false, true);//Top weapon 2
			f.name = "top2";
			f.x = o.mcTop2.x + o.x - f.mcTorso.x;
			f.y = o.mcTop2.y + o.y - f.mcTorso.y;
			mechType[t].push(f);
			base.addChild(f);
		}
		
		mechType[t].push(b);
		mechType[t].push(o);
		mechType[t].push(c);
		
		base.addChild(b);
		base.addChild(o);
		base.addChild(c);
		
		if (side1 > -1)
		{
			var g:MovieClip = buildSprite(itemDB[side1][0], 0, 0, false, true);// side 1
			g.name = "side1";
			g.x = o.mcSide1.x + o.x - g.mcTorso.x;
			g.y = o.mcSide1.y + o.y - g.mcTorso.y;
			mechType[t].push(g);
			base.addChild(g);
		}
		if (side3 > -1)
		{
			var h:MovieClip = buildSprite(itemDB[side3][0], 0, 0, false, true);
			h.name = "side3";
			h.x = o.mcSide3.x + o.x - h.mcTorso.x;
			h.y = o.mcSide3.y + o.y - h.mcTorso.y;
			mechType[t].push(h);
			base.addChild(h);
		}
		if (top1 > -1)
		{
			var j:MovieClip = buildSprite(itemDB[top1][0], 0, 0, false, true);
			j.name = "top1";
			j.x = o.mcTop1.x + o.x - j.mcTorso.x;
			j.y = o.mcTop1.y + o.y - j.mcTorso.y;
			mechType[t].push(j);
			base.addChild(j);
		}
		if (drone > -1 && currentFrame == 3)
		{
			var k:MovieClip = buildSprite(itemDB[drone][0], 0, 0, false, true);
			k.name = "drone";
			k.x = o.mcDrone.x + o.x - k.mcCenter.x;
			k.y = o.mcDrone.y + o.y - k.mcCenter.y;
			mechType[t].push(k);
			base.addChild(k);
		}
	}
	paint(t, p);
}

function paint (t:int, c:ColorTransform): void
{
	for (i = 0; i < mechType[t].length; i ++)
	{
		mechType[t][i].mcColor.transform.colorTransform = c;
		mechType[t][i].mcColor.blendMode = BlendMode.OVERLAY;
		mechType[t][i].mcColor.visible = true;
		mechType[t][i].mcColor.alpha = 1;
	}
}

function getID (t:String):int
{
	for (i = 0; i < itemDB.length; i++)
	{
		if (itemDB[i][2] == t)
			return i;
	}
	
	trace("Could not get ID for " + t);
	return -1;
}

function setSlotListeners (): void
{
	for (i = 0; i < slot.length; i ++)
	{
		addSlotListener(i);
		function addSlotListener (s:uint): void
		{
			slot[s][0].addEventListener(C, function (e:MouseEvent): void
			{
				currentSlot = s;
				displayItemsList(s);
			});
		}
	}
}

gotoAndStop("WORKSHOP");


if (initWorkshop)
{
	initWorkshop = false;
	
	var stats:Array = new Array(
								null,
								null,
								null,
								null,
								itemSummary.isKg,
								itemSummary.isHp,
								itemSummary.isDmg,
								null,
								itemSummary.isHeatDmg,
								itemSummary.isEneDmg,
								itemSummary.isResDmg,
								itemSummary.isHeat,
								itemSummary.isCool,
								itemSummary.isEne,
								itemSummary.isReg,
								itemSummary.isPhyRes,
								itemSummary.isExpRes,
								itemSummary.isEleRes,
								itemSummary.isHeatCapDmg,
								itemSummary.isCoolDmg,
								itemSummary.isEneCapDmg,
								itemSummary.isRegDmg,
								itemSummary.isPush,
								itemSummary.isPull,
								itemSummary.isRange,
								null,
								itemSummary.isWalk,
								itemSummary.isJump,
								itemSummary.isUses,
								itemSummary.isEneCost,
								itemSummary.isHeatGen
								);
	var mechType:Array = new Array(workshopMech, playerMech, opponentMech);
	
	slot.push([slotTorso, 0, null, -1]);
	slot.push([slotLegs, 1, null, -1]);
	slot.push([slotSide1, 2, null, -1]);
	slot.push([slotSide2, 2, null, -1]);
	slot.push([slotSide3, 2, null, -1]);
	slot.push([slotSide4, 2, null, -1]);
	slot.push([slotTop1, 3, null, -1]);
	slot.push([slotTop2, 3, null, -1]);
	slot.push([slotDrone, 4, null, -1]);
	slot.push([slotCharge, 5, null, -1]);
	slot.push([slotTele, 6, null, -1]);
	slot.push([slotHook, 7, null, -1]);
	slot.push([slotMod1, 8, null, -1]);
	slot.push([slotMod2, 8, null, -1]);
	slot.push([slotMod3, 8, null, -1]);
	slot.push([slotMod4, 8, null, -1]);
	slot.push([slotMod5, 8, null, -1]);
	slot.push([slotMod6, 8, null, -1]);
	slot.push([slotMod7, 8, null, -1]);
	slot.push([slotMod8, 8, null, -1]);
	
	trace("Workshop Initialized.");
}

slot[0][0] = slotTorso;
slot[1][0] = slotLegs;
slot[2][0] = slotSide1;
slot[3][0] = slotSide2;
slot[4][0] = slotSide3;
slot[5][0] = slotSide4;
slot[6][0] = slotTop1;
slot[7][0] = slotTop2;
slot[8][0] = slotDrone;
slot[9][0] = slotCharge;
slot[10][0] = slotTele;
slot[11][0] = slotHook;
slot[12][0] = slotMod1;
slot[13][0] = slotMod2;
slot[14][0] = slotMod3;
slot[15][0] = slotMod4;
slot[16][0] = slotMod5;
slot[17][0] = slotMod6;
slot[18][0] = slotMod7;
slot[19][0] = slotMod8;

itemSummary.visible = false;
versionTeller.text = "V" + ver;
changelogTab.txt.text = "Changelog V" + ver;

mcToBtn(dismountMechBtn);
dismountMechBtn.addEventListener(C, function (e:MouseEvent): void
{
	dismountMech();
});

mcToBtn(importExportBtn);
importExportBtn.addEventListener(C, function (e:MouseEvent): void
{
	stage.addChild(importExportTab);
	importExportTab.mechCode_txt.text = "@"+slot[0][3]+"&"+slot[1][3]+"&"+slot[2][3]+"&"+slot[3][3]+"&"+slot[4][3]+"&"+slot[5][3]+"&"+slot[6][3]+"&"+slot[7][3]+"&"+slot[8][3]+"&"+slot[9][3]+"&"+slot[10][3]+"&"+slot[11][3]+"&"+slot[12][3]+"&"+slot[13][3]+"&"+slot[14][3]+"&"+slot[15][3]+"&"+slot[16][3]+"&"+slot[17][3]+"&"+slot[18][3]+"&"+slot[19][3]+"="+customColor;
	
	importExportTab.applyBtn.addEventListener(C, closeTab);
	function closeTab (e:MouseEvent): void
	{
		stage.removeChild(importExportTab);
		importExportTab.applyBtn.removeEventListener(C, closeTab);
		
		trace(importExportTab.mechCode_txt.text);
	}
});

mcToBtn(changelogBtn);
changelogBtn.addEventListener(C, function (e:MouseEvent): void
{
	addChild(changelogTab);
	changelogTab.addEventListener(C, a);
	function a (e:MouseEvent): void
	{
		changelogTab.removeEventListener(C, a);
		removeChild(changelogTab);
	}
	updateWorkshopScreen();
});

mcToBtn(partsPacksBtn);
mcToBtn(partsPacksTab.applyBtn);
mcToBtn(partsPacksTab.officialItemsBtn);
mcToBtn(partsPacksTab.fanMadeItemsBtn);
mcToBtn(partsPacksTab.specialItemsBtn);
partsPacksBtn.addEventListener(C, function (e:MouseEvent): void
{
	addChild(partsPacksTab);
	
	partsPacksTab.applyBtn.addEventListener(C, a)
	function a (e:MouseEvent): void
	{
		partsPacksTab.applyBtn.removeEventListener(C, a);
		partsPacksTab.officialItemsBtn.removeEventListener(C, b);
		partsPacksTab.fanMadeItemsBtn.removeEventListener(C, d);
		partsPacksTab.specialItemsBtn.removeEventListener(C, c);
		removeChild(partsPacksTab);
		updateWorkshopScreen();
	}
	
	partsPacksTab.officialItemsBtn.addEventListener(C, b);
	function b (e:MouseEvent): void
	{
		if (getOfficialItems)
			getOfficialItems = false;
		else
			getOfficialItems = true;
		updateWorkshopScreen();
	}
	
	partsPacksTab.fanMadeItemsBtn.addEventListener(C, d);
	function d (e:MouseEvent): void
	{
		if (getFanMadeItems)
			getFanMadeItems = false;
		else
			getFanMadeItems = true;
		updateWorkshopScreen();
	}
	
	partsPacksTab.specialItemsBtn.addEventListener(C, c);
	function c (e:MouseEvent): void
	{
		if (getSpecialItems)
			getSpecialItems = false;
		else
			getSpecialItems = true;
		updateWorkshopScreen();
	}
});

mcToBtn(paintBtn);
paintBtn.addEventListener(C, function (e:MouseEvent): void
{
	addChild(paintTab);
	paintTab.addEventListener(Event.ENTER_FRAME, updateColor);
	
	paintTab.sprite.addEventListener(C, a);
	function a (e:MouseEvent): void
	{
		paintTab.redValuetxt.text = Math.ceil(Math.random() * 100) + "";
		paintTab.greenValuetxt.text = Math.ceil(Math.random() * 100) + "";
		paintTab.blueValuetxt.text = Math.ceil(Math.random() * 100) + "";
	}
	
	paintTab.applyPaintBtn.addEventListener(C, b);
	function b (e:MouseEvent): void
	{
		removeChild(paintTab);
		paintTab.sprite.removeEventListener(C, a);
		paintTab.applyPaintBtn.removeEventListener(C, b);
		paintTab.removeEventListener(Event.ENTER_FRAME, updateColor);
		displayFloatingText("New Color Applied!", customPaint);
		updateWorkshopScreen();
	}
});

getOpponentTab.bossesOpponentBtn.state.gotoAndStop("OFF");
getOpponentTab.metasOpponentBtn.state.gotoAndStop("OFF");
getOpponentTab.titansOpponentBtn.state.gotoAndStop("OFF");
getOpponentTab.counterOpponentBtn.state.gotoAndStop("OFF");
mcToBtn(battleBtn);
mcToBtn(getOpponentTab.previousOpponentBtn);
mcToBtn(getOpponentTab.dumbOpponentBtn);
mcToBtn(getOpponentTab.normalOpponentBtn);
mcToBtn(getOpponentTab.mirrorOpponentBtn);
mcToBtn(getOpponentTab.bossesOpponentBtn);
mcToBtn(getOpponentTab.metasOpponentBtn);
mcToBtn(getOpponentTab.titansOpponentBtn);
mcToBtn(getOpponentTab.counterOpponentBtn);
mcToBtn(getOpponentTab.dummyOpponentBtn);
battleBtn.addEventListener(C, function (e:MouseEvent): void
{
	if (slot[0][3] > -1 && slot[1][3] > -1)
	{
		updateWorkshopScreen();
		
		addChild(getOpponentTab);
		getOpponentTab.previousOpponentBtn.addEventListener(C, prevOp);
		function prevOp (e:MouseEvent): void
		{
			if (hasPreviousOpponent)
			{
				opponentClass = "Previous";
				closeGetOpponentTab();
			}
			else
				displayFloatingText("You haven't fought any mech.", blank);
		}
		
		getOpponentTab.dumbOpponentBtn.addEventListener(C, dumbOp);
		function dumbOp (e:MouseEvent): void
		{
			opponentClass =  "Noob";
			closeGetOpponentTab();
		}
		
		getOpponentTab.normalOpponentBtn.addEventListener(C, normOp);
		function normOp (e:MouseEvent): void
		{
			opponentClass = "Normal";
			closeGetOpponentTab();
		}
		
		getOpponentTab.mirrorOpponentBtn.addEventListener(C, mirrOp);
		function mirrOp (e:MouseEvent): void
		{
			opponentClass = "Mirror";
			closeGetOpponentTab();
		}
		
		getOpponentTab.bossesOpponentBtn.addEventListener(C, bossOp);
		function bossOp (e:MouseEvent): void
		{
			//closeGetOpponentTab();
			displayFloatingText("Comming soon.", blank);
		}
		
		getOpponentTab.metasOpponentBtn.addEventListener(C, metaOp);
		function metaOp (e:MouseEvent): void
		{
			//closeGetOpponentTab();
			displayFloatingText("Comming soon.", blank);
		}
		
		getOpponentTab.titansOpponentBtn.addEventListener(C, titaOp);
		function titaOp (e:MouseEvent): void
		{
			//closeGetOpponentTab();
			displayFloatingText("Comming soon.", blank);
		}
		
		getOpponentTab.counterOpponentBtn.addEventListener(C, counOp);
		function counOp (e:MouseEvent): void
		{
			//closeGetOpponentTab();
			displayFloatingText("Comming soon.", blank);
		}
		
		getOpponentTab.dummyOpponentBtn.addEventListener(C, dummOp);
		function dummOp (e:MouseEvent): void
		{
			opponentClass = "dummy";
			closeGetOpponentTab();
		}
		
		function closeGetOpponentTab (): void
		{
			hasPreviousOpponent = true;
			removeChild(getOpponentTab);
			getOpponentTab.previousOpponentBtn.removeEventListener(C, prevOp);
			getOpponentTab.dumbOpponentBtn.removeEventListener(C, dumbOp);
			getOpponentTab.normalOpponentBtn.removeEventListener(C, normOp);
			getOpponentTab.mirrorOpponentBtn.removeEventListener(C, mirrOp);
			getOpponentTab.bossesOpponentBtn.removeEventListener(C, bossOp);
			getOpponentTab.metasOpponentBtn.removeEventListener(C, metaOp);
			getOpponentTab.titansOpponentBtn.removeEventListener(C, titaOp);
			getOpponentTab.counterOpponentBtn.removeEventListener(C, counOp);
			getOpponentTab.dummyOpponentBtn.removeEventListener(C, dummOp);
			
			gotoAndStop("BATTLESCREEN");
		}
	}
	else
		displayFloatingText("Build a Mech first!", blank);
});

mcToBtn(arenaBuffBtn);
arenaBuffBtn.addEventListener(C, function (e:MouseEvent): void
{
	if (arenaBuffs)
	{
		arenaBuffs = false;
		
		healthBuff = 0;
		energyBuff = 1;
		regenBuff = 1;
		heatBuff = 1;
		coolingBuff = 1;
		phyResBuff = 1;
		expResBuff = 1;
		eleResBuff = 1;
		
		displayFloatingText("Arena Buffs Deactived", blank);
		updateWorkshopScreen();
	}
	else
	{
		arenaBuffs = true;
		
		healthBuff = 300;
		energyBuff = 1.20;
		regenBuff = 1.20;
		heatBuff = 1.20;
		coolingBuff = 1.20;
		phyResBuff = 1.40;
		expResBuff = 1.40;
		eleResBuff = 1.40;
		
		updateWorkshopScreen();
		displayFloatingText("Arena Buffs Actived", blank);
	}
	updateStats();
});

setSlotListeners();
updateWorkshopScreen();

/*
 * Initialization Above.
 *
 * Code Below.
 *
 */

function rngColor (): ColorTransform
{
	return new ColorTransform(Math.random(), Math.random(), Math.random());
}

function displayItemsList (slotID:int): void
{
	/*
	 * Shows Tab.
	 *
	 * List Items depending on which Slot was clicked.
	 *
	 */
	
	itemsTab.addEventListener(C, a);
	addChild(itemsTab);
	function a (e:MouseEvent):void
	{
		itemsTab.removeEventListener(C, a);
		removeChild(itemsTab);
		
		while (onTabItems.length > 0)
		{
			itemsTab.removeChild(onTabItems[0]);
			onTabItems.shift();
		}
	}
	
	// Build Item sprites
	for (i = 0; i < itemDB.length; i ++)
	{
		if (itemDB[i][1] == slot[slotID][1])
		{
			if (itemDB[i][31] == 0 && getOfficialItems)
				l(i);
			if (itemDB[i][31] == 1 && getFanMadeItems)
				l(i);
			if (itemDB[i][31] == 2 && getSpecialItems)
				l(i);
		}
	}
	function l(w:uint):void
	{
		var s:MovieClip = buildSprite(itemDB[w][0], 65, 65, true, true);
		mcToBtn(s);
		s.addEventListener(C, selectItemHandler(s, w));
		onTabItems.push(s);
	}
	
	// Set Item positions and add childs.
	for (i = 0; i < onTabItems.length; i ++)
	{
		onTabItems[i].x += 12;
		onTabItems[i].y += 120;
		
		p(i + 1);
	}
	function p (j:uint): void
	{
		if(j > 11)
		{
			j -= 11;
			onTabItems[i].y += 70;
			p(j);
		}
		else
		{
			onTabItems[i].x += j * 65;
			itemsTab.addChild(onTabItems[i]);
		}
	}
}

function buildSprite (inst:Object, w:int, h:int, hb:Boolean, ol:Boolean): MovieClip
{
	/*
	 * Returns a MovieClip out of the Object given.
	 *
	 * inst = Sprite instance
	 * d    = Sprite dimentions
	 * hb   = Add clicking hitBox
	 * ol   = Add outline
	 *
	 */
	
	var mc:MovieClip = new inst();
	
	// Aply clicking hitbox.
	if (hb)
	{
		var hitBox:MovieClip = new HitBox();
		
		if (mc.width > mc.height)
		{
			hitBox.width = mc.width;
			hitBox.height = hitBox.width;
		}
		else
		{
			hitBox.width = mc.height;
			hitBox.height = hitBox.width;
		}
		mc.addChild(hitBox);
	}
	
	// Dimentions.
	if (h > 0)
	{
		if(mc.height > h)
		{
			mc.width *= h / mc.height;
			mc.height = h;
		}
	}
	if (w > 0)
	{
		if(mc.width > w)
		{
			mc.height *= w / mc.width;
			mc.width = w;
		}
	}
	
	// Aply outline.
	if (ol)
	{
		var ds:DropShadowFilter = new DropShadowFilter();
		ds.distance = 0;
		ds.angle = 0;
		ds.alpha = 1;
		ds.blurX = 2;
		ds.blurY = 2;
		ds.strength = 4;
		
		mc.filters = new Array(ds);
	}
	
	// Sprite done
	return mc;
}

function selectItemHandler (s:*, itemID:int): *
{
	
	/*
	 * Called when some Item or no item is clicked on tab.
	 *
	 * Returns a function if the itemID is >= 0.
	 *
	 */
	
	return function(e:MouseEvent): void
	{
		if (itemID > -1)
		{
			slot[currentSlot][3] = itemID;
			getItemStats(itemID);
			if (itemDB[itemID][31] == 1)
				displayFloatingText(itemDB[itemID][32], blank);
		}
		updateWorkshopScreen();
	};
}

function updateWorkshopScreen (): void
{
	//Screen Updates
	for (i = 0; i < slot.length; i ++)
	{ // All slot have 2 childs as default.
		while (slot[i][0].numChildren > 2)
			slot[i][0].removeChildAt(2);
		if (slot[i][3] >= 0)
			h(i);
	}
	function h (j:uint): void
	{
		var sprite:MovieClip = buildSprite(itemDB[slot[j][3]][0], 70, 70, true, true);
		sprite.addEventListener(MouseEvent.MOUSE_OVER, function (e:MouseEvent): void
		{
			e.currentTarget.itemGfx.transform.colorTransform = white;
			getItemStats(slot[j][3]);
			itemSummary.visible = true;
		});
		sprite.addEventListener(MouseEvent.MOUSE_OUT, function (e:MouseEvent): void
		{
			e.currentTarget.itemGfx.transform.colorTransform = blank;
			itemSummary.visible = false;
		});
		slot[j][0].addChild(sprite);
	}
	
	//Parts Packs Tab
	if (getOfficialItems)
		partsPacksTab.officialItemsBtn.gotoAndStop("ON")
	else
		partsPacksTab.officialItemsBtn.gotoAndStop("OFF")
	if (getFanMadeItems)
		partsPacksTab.fanMadeItemsBtn.gotoAndStop("ON");
	else
		partsPacksTab.fanMadeItemsBtn.gotoAndStop("OFF");
	if (getSpecialItems)
		partsPacksTab.specialItemsBtn.gotoAndStop("ON");
	else
		partsPacksTab.specialItemsBtn.gotoAndStop("OFF");
	
	// Arena buff
	if(arenaBuffs)
		arenaBuffBtn.gotoAndStop("ON");
	else
		arenaBuffBtn.gotoAndStop("OFF");
	
	// Battle Tab
	if (hasPreviousOpponent)
		getOpponentTab.previousOpponentBtn.state.gotoAndStop("ON");
	else
		getOpponentTab.previousOpponentBtn.state.gotoAndStop("OFF");
	
	// Workshop mech preview
	setMechStructure(mechStand, 0, slot[0][3], slot[1][3], slot[2][3], slot[3][3], slot[4][3], slot[5][3], slot[6][3], slot[7][3], slot[8][3], customPaint);
	
	updateStats();
}

//Update Stats
function updateStats (): void
{
	weight = 0;
	health = 0;
	energy = 0;
	regen = 0;
	heat = 0;
	cooling = 0;
	phyRes = 0;
	expRes = 0;
	eleRes = 0;
	
	for (i = 0; i < slot.length; i++)
	{
		if (slot[i][3] > -1){
			weight += itemDB[slot[i][3]][4];
			health += itemDB[slot[i][3]][5];
			energy += itemDB[slot[i][3]][13];
			regen += itemDB[slot[i][3]][14];
			heat += itemDB[slot[i][3]][11];
			cooling += itemDB[slot[i][3]][12];
			phyRes += itemDB[slot[i][3]][15];
			expRes += itemDB[slot[i][3]][16];
			eleRes += itemDB[slot[i][3]][17];
		}
	}
	
	if (health + healthBuff == healthBuff)
		mechSummary.health.txt.text = 0 + "";
	else
		mechSummary.health.txt.text = health + healthBuff + "";
	
	mechSummary.weight.txt.text = weight + "";
	mechSummary.energy.txt.text = Math.ceil(energy * energyBuff) + "";
	mechSummary.regen.txt.text = Math.ceil(regen * regenBuff) + "";
	mechSummary.heat.txt.text = Math.ceil(heat * heatBuff) + "";
	mechSummary.cooling.txt.text = Math.ceil(cooling * coolingBuff) + "";
	mechSummary.phyRes.txt.text = Math.ceil(phyRes * phyResBuff) + "";
	mechSummary.expRes.txt.text = Math.ceil(expRes * expResBuff) + "";
	mechSummary.eleRes.txt.text = Math.ceil(eleRes * eleResBuff) + "";
	
	if (weight > 989)
	{
		if (weight > 1000)
			mechSummary.weight.transform.colorTransform = red;
		else
			mechSummary.weight.transform.colorTransform = green;
	}
	else
		mechSummary.weight.transform.colorTransform = blank;
}
updateStats();

//Display floating text
function displayFloatingText (t:String, c:ColorTransform): void
{
	if (!stage.contains(floatingText))
	{
		addChild(floatingText);
		floatingText.addEventListener(Event.ENTER_FRAME, countAndFade);
		floatingText.startDrag(true);
	}
	
	floatingText.transform.colorTransform = c;
	floatingTextCount = t.length * 8;
	floatingText.txt.text = t;
	floatingText.alpha = 1;
	floatingTextMp3.play(0,0,generalVol);
		
	function countAndFade (e:Event): void
	{
		floatingTextCount --;
		floatingText.alpha = floatingTextCount * .025;
		
		if (floatingTextCount < 0)
		{
			floatingText.removeEventListener(Event.ENTER_FRAME, countAndFade);
			removeChild(floatingText);
		}
	}
}

//Stats listing
function getItemStats (ID:int): void
{
	currentItemStats.splice(0, currentItemStats.length);
	
	if(ID < 0 || ID > itemDB.length - 1)
	{
		displayFloatingText("ERROR 1: Can not get stats for item ID " + ID + "\nPlease contact KilliN.", red);
		ID = 0;
	}
	
	itemSummary.txt.text = itemDB[ID][2];
	
	for (i = 0; i <  stats.length; i ++)
	{
		if (stats[i] != null)
		{
			if (itemDB[ID][i] > 0)
			{
				currentItemStats.push(stats[i]);
				
				stats[i].txt.text = itemDB[ID][i];
				
				if (stats[i + 1] == null && itemDB[ID][i + 1] > 0)
					stats[i].txt.text = stats[i].txt.text + "-" + itemDB[ID][i + 1];
				
				if (stats[i] == itemSummary.isDmg || stats[i] == itemSummary.isResDmg)
					stats[i].itemElement.gotoAndStop(itemDB[ID][3]);
				
				stats[i].visible = true;
			}
			else
				stats[i].visible = false;
		}
	}
	
	for (i = 0; i < currentItemStats.length; i ++)
	{
		currentItemStats[i].x = -235;
		currentItemStats[i].y = 0;
		p(i + 1);
	}
	
	function p (j:uint)
	{
		if(j > 2)
		{
			j -= 2;
			currentItemStats[i].y += 28.5;
			p(j);
		}
		else
			currentItemStats[i].x += (j * 130);
	}
	
	// Item Summary has 27 childs by default.
	while (itemSummary.numChildren > 27)
		itemSummary.removeChildAt(27);
	
	if (itemDB[ID][1] == "Legs")
	{
		var s:MovieClip = buildSprite(itemDB[ID][0], 180, 100, false, true);
		s.y = -60;
		itemSummary.addChild(s);
		var k:MovieClip = buildSprite(itemDB[ID][0], 180, 100, false, true);
		k.y = -60;
		itemSummary.addChild(k);
		
		if (s.width > s.height)
		{
			s.x = s.width * .15;
			k.x = k.width * - .15;
		}
		else
		{
			s.x = s.width * .20;
			k.x = k.width * - .20;
		}
	}
	else
	{
		var c:MovieClip = buildSprite(itemDB[ID][0], 220, 100, false, true);
		c.y = -60;
		itemSummary.addChild(c);
	}
}

function updateColor(e:Event): void
{
	var r:int = int(paintTab.redValuetxt.text);
	var g:int = int(paintTab.greenValuetxt.text);
	var b:int = int(paintTab.blueValuetxt.text);
	
	if (r > 100) r = 100;
	if (g > 100) g = 100;
	if (b > 100) b = 100;
	if (r < 0) r = 0;
	if (g < 0) g = 0;
	if (b < 0) b = 0;
	
	paintTab.redValuetxt.text = r + "";
	paintTab.greenValuetxt.text = g + "";
	paintTab.blueValuetxt.text = b + "";
	
	customPaint = new ColorTransform(r*.01,g*.01,b*.01);
	
	paintTab.sprite.mcColor.visible = true;
	paintTab.sprite.mcColor.alpha = 1;
	paintTab.sprite.mcColor.blendMode = BlendMode.OVERLAY;
	paintTab.colorBar.transform.colorTransform = customPaint;
	paintTab.sprite.mcColor.transform.colorTransform = customPaint;
}

function dismountMech ()
{
	for (i = 0; i < slot.length; i ++)
	{// Default childs in each slot is 2
		while (slot[i][0].numChildren > 2) slot[i][0].removeChildAt(2);
		slot[i][3] = -1;
	}
	while (mechStand.numChildren > 1) mechStand.removeChildAt(1);
	updateWorkshopScreen();
}

import flash.display.MovieClip;
import flash.display.Sprite;
import fl.transitions.TweenEvent;
import fl.transitions.Tween;

var pMechBase:MovieClip = new MovieClip();
var oMechBase:MovieClip = new MovieClip();

var playerWeaponsList:Array = new Array();
var areasArray:Array = new Array();
var controlsArray:Array = new Array();
var animations:Array = new Array();
var playerSetup:Array = new Array();
var opponentSetup:Array = new Array();
var xPos:Array = new Array(0, 58, 134, 210, 286, 362, 438, 514, 590, 666, 742);
var healthBarWidth:uint = 245;
var heatBarWidth:uint = 95;
var energyBarWidth:uint = 95;
var runningAnim:Boolean = false;
var isPlayerTurn:Boolean = true;
var totalTurns:int = -1;
var pTurns:int = 2;
var oTurns:int = 0;

var pPosition:int = 0;
var pHealthMax:int = 0;
var pHealth:int = 0;
var pEnergyMax:int = 0;
var pEnergy:int = 0;
var pRegen:int = 0;
var pHeatMax:int = 0;
var pHeat:int = 0;
var pCooling:int = 0;
var pPhyRes:int = 0;
var pExpRes:int = 0;
var pEleRes:int = 0;
var pWalkDist:int = 0;
var pJumpDist:int = 0;
var pDroneActive:Boolean = false;

var oPosition:int = 0;
var oHealthMax:int = 0;
var oHealth:int = 0;
var oEnergyMax:int = 0;
var oEnergy:int = 0;
var oRegen:int = 0;
var oHeatMax:int = 0;
var oHeat:int = 0;
var oCooling:int = 0;
var oPhyRes:int = 0;
var oExpRes:int = 0;
var oEleRes:int = 0;
var oWalkDist:int = 0;
var oJumpDist:int = 0;
var oDroneActive:Boolean = false;

playerHeatBar.width = 0;
opponentHeatBar.width = 0;
land.visible = false;
pMechBase.scaleX = 0.22;
pMechBase.scaleY = 0.22;
pMechBase.name = "player";
stage.addChild(pMechBase);
oMechBase.scaleX = 0.22;
oMechBase.scaleY = 0.22;
oMechBase.name = "opponent";
stage.addChild(oMechBase);

mcToBtn(workshopBtn);
workshopBtn.addEventListener(C, function (e:MouseEvent): void
{
	stage.removeChild(pMechBase);
	stage.removeChild(oMechBase);
	gotoAndStop("WORKSHOP");
	updateWorkshopScreen();
});
mcToBtn(battleInfoBtn);
battleInfoBtn.addEventListener(C, function (e:MouseEvent): void
{
	var pData = battleInfoTab.playerData_txt;
	var oData = battleInfoTab.opponentData_txt;
		
	pData.text = "Health: " + pHealth + "/" + pHealthMax + "\n";
	pData.text = pData.text + "Heat: " + pHeat + "/" + pHeatMax + "\n";
	pData.text = pData.text + "Cooling: " + pCooling + "\n";
	pData.text = pData.text + "Energy: " + pEnergy + "/" + pEnergyMax + "\n";
	pData.text = pData.text + "Regen: " + pRegen + "\n";
	pData.text = pData.text + "Phy Resist: " + pPhyRes + "\n";
	pData.text = pData.text + "Exp Resist: " + pExpRes + "\n";
	pData.text = pData.text + "Ele Resist: " + pEleRes + "\n";
	pData.text = pData.text + "Turns: " + pTurns + "\n";
	pData.text = pData.text + "Position: " + pPosition;
	//pData.text = pData.text + "MC: "+slot[0][3]+"&"+slot[1][3]+"&"+slot[2][3]+"&"+slot[3][3]+"&"+slot[4][3]+"&"+slot[5][3]+"&"+slot[6][3]+"&"+slot[7][3]+"&"+slot[8][3]+"&"+slot[9][3]+"&"+slot[10][3]+"&"+slot[11][3]+"&"+slot[12][3]+"&"+slot[13][3]+"&"+slot[14][3]+"&"+slot[15][3]+"&"+slot[16][3]+"&"+slot[17][3]+"&"+slot[18][3]+"&"+slot[19][3];
	
	oData.text = "Health: " + oHealth + "/" + oHealthMax + "\n";
	oData.text = oData.text + "Heat: " + oHeat + "/" + oHeatMax + "\n";
	oData.text = oData.text + "Cooling: " + oCooling + "\n";
	oData.text = oData.text + "Energy: " + oEnergy + "/" + oEnergyMax + "\n";
	oData.text = oData.text + "Regen: " + oRegen + "\n";
	oData.text = oData.text + "Phy Resist: " + oPhyRes + "\n";
	oData.text = oData.text + "Exp Resist: " + oExpRes + "\n";
	oData.text = oData.text + "Ele Resist: " + oEleRes + "\n";
	oData.text = oData.text + "Turns: " + oTurns + "\n";
	oData.text = oData.text + "Position: " + oPosition;
	//oData.text = oData.text + "MC: "+prevOpTorso+"&"+prevOpLegs+"&"+prevOpSide1+"&"+prevOpSide2+"&"+prevOpSide3+"&"+prevOpSide4+"&"+prevOpTop1+"&"+prevOpTop2+"&"+prevOpDrone+"&"+prevOpCharge+"&"+prevOpTele+"&"+prevOpHook+"&"+prevOpMod1+"&"+prevOpMod2+"&"+prevOpMod3+"&"+prevOpMod4+"&"+prevOpMod5+"&"+prevOpMod6+"&"+prevOpMod7+"&"+prevOpMod8;
	
	stage.addChild(battleInfoTab);
	battleInfoTab.addEventListener(C, clickTab);
	function clickTab (e:MouseEvent): void
	{
		battleInfoTab.removeEventListener(C, clickTab);
		stage.removeChild(battleInfoTab);
	}
});

function useItem (ID:uint): void
{
	var dmg:int = Math.random() * (itemDB[ID][7] - itemDB[ID][6]) + itemDB[ID][6];
	var initialPosition:int = 0;
		
	if (itemDB[ID][1] == 1)
		stompMp3.play(0, 0);
	
	if (isPlayerTurn)
	{
		initialPosition = oPosition;
		
		//Give Knockback
		if (oPosition > pPosition) {
			if (oPosition < 10)
			oPosition += itemDB[ID][22];
			if (oPosition > 1)
			oPosition -= itemDB[ID][23];
		}
		if (oPosition < pPosition) {
			if (oPosition > 1)
			oPosition -= itemDB[ID][22];
			if (oPosition < 10)
			oPosition += itemDB[ID][23];
		}
		
		//Give element-based damages
		switch (itemDB[ID][3])
		{
			case 1:
				dmg -= oPhyRes;
				oPhyRes -= itemDB[ID][10];
				break;
			
			case 2:
				dmg -= oExpRes;
				oExpRes -= itemDB[ID][10];
				break;
			
			case 3:
				dmg -= oEleRes;
				oEleRes -= itemDB[ID][10];
				break;
		}
		
		//Give regular damages.
		if (dmg < 1)
			dmg = 1;
		
		oHealth -= dmg;
		oHeatMax -= itemDB[ID][18];
		oHeat += itemDB[ID][8];
		oCooling -= itemDB[ID][19];
		oEnergyMax -= itemDB[ID][20];
		oEnergy -= itemDB[ID][9];
		oRegen -= itemDB[ID][21];
		pHeat += itemDB[ID][30];
		pEnergy -= itemDB[ID][29];
		
		if (oPosition != initialPosition)
			knockBackAnim("opponent", oPosition);
		
	} else {
		//Give Knockback
		if (pPosition > oPosition)
		{
			if (pPosition < 11)
			pPosition += itemDB[ID][22];
			if (pPosition > 0)
			pPosition -= itemDB[ID][23];
		}
		if (pPosition < oPosition)
		{
			if (pPosition > 0)
			pPosition -= itemDB[ID][22];
			if (pPosition < 11)
			pPosition += itemDB[ID][23];
		}
		
		//Give element-based damages
		switch (itemDB[ID][3])
		{
			case 1:
				dmg -= pPhyRes;
				pPhyRes -= itemDB[ID][10];
				break;
			
			case 2:
				dmg -= pExpRes;
				pExpRes -= itemDB[ID][10];
				break;
			
			case 3:
				dmg -= pEleRes;
				pEleRes -= itemDB[ID][10];
				break;
		}
		
		//Give regular damages.
		if (dmg < 1)
			dmg = 1;
		
		pHealth -= dmg;
		pHeatMax -= itemDB[ID][18];
		pHeat += itemDB[ID][8];
		pCooling -= itemDB[ID][19];
		pEnergyMax -= itemDB[ID][20];
		pEnergy -= itemDB[ID][9];
		pRegen -= itemDB[ID][21];
		oHeat += itemDB[ID][30];
		oEnergy -= itemDB[ID][29];
				
		if (pPosition != initialPosition)
			knockBackAnim("player", pPosition);
	}
	displayDamage(dmg);
	runTurn();
}

function updateBattle (): void
{
	if (oPosition > pPosition)
	{
		oMechBase.scaleX = -.22;
		pMechBase.scaleX = .22;
	}
	else
	{
		oMechBase.scaleX = .22;
		pMechBase.scaleX = -.22;
	}
	
	// Stats caping
	if (pHeatMax < 1)
		pHeatMax = 1;
	
	if (oHeatMax < 1)
		oHeatMax = 1;
	
	if (pEnergyMax < 1)
		pEnergyMax = 1;
	
	if (oEnergyMax < 1)
		oEnergyMax = 1;
	
	if (pHeat < 0)
		pHeat = 0;
	
	if (oHeat < 0)
		oHeat = 0;
	
	if (pEnergy < 0)
		pEnergy = 0;
	
	if (oEnergy < 0)
		oEnergy = 0;
	
	if (pEnergy > pEnergyMax)
		pEnergy = pEnergyMax;
	
	if (oEnergy > oEnergyMax)
		oEnergy = oEnergyMax;
	
	if (pPosition > xPos.length)
		pPosition = xPos.length;
	
	if (oPosition > xPos.length)
		oPosition = xPos.length;
	
	if (pPosition < 1)
		pPosition = 1;
	
	if (oPosition < 1)
		oPosition = 1;
	
	//Stats Display
	playerHealthTxt.text = pHealth + "/" + pHealthMax;
	playerHeatTxt.text = pHeat + "/" + pHeatMax;
	playerEnergyTxt.text = pEnergy + "/" + pEnergyMax;
	if (opponentClass != "dummy") {
		opponentHealthTxt.text = oHealth + "/" + oHealthMax;
		opponentHeatTxt.text = oHeat + "/" + oHeatMax;
		opponentEnergyTxt.text = oEnergy + "/" + oEnergyMax;
	} else {
		opponentHealthTxt.text = "infinite";
		opponentHeatTxt.text = "infinite";
		opponentEnergyTxt.text = "infinite";
	}
	playerPhyResTxt.text = pPhyRes.toString();
	opponentPhyResTxt.text = oPhyRes.toString();
	playerExpResTxt.text = pExpRes.toString();
	opponentExpResTxt.text = oExpRes.toString();
	playerEleResTxt.text = pEleRes.toString();
	opponentEleResTxt.text = oEleRes.toString();
	
	if (pHealth < 0)
		playerHealthTxt.transform.colorTransform = red;
	else
		playerHealthTxt.transform.colorTransform = blank;
	
	if (oHealth < 0)
		opponentHealthTxt.transform.colorTransform = red;
	else
		opponentHealthTxt.transform.colorTransform = blank;
	
	//Bar width animation
	if (pHealth / pHealthMax * healthBarWidth > 0 || playerHealthBar.width > 0)
		new Tween(playerHealthBar, "width", Strong.easeOut, playerHealthBar.width, pHealth / pHealthMax * healthBarWidth, .5, true);
	if (oHealth / oHealthMax * healthBarWidth > 0 || opponentHealthBar.width > 0)
		new Tween(opponentHealthBar, "width", Strong.easeOut, opponentHealthBar.width, oHealth / oHealthMax * healthBarWidth, .5, true);
	if (pHeat / pHeatMax * heatBarWidth > heatBarWidth)
		new Tween(playerHeatBar, "width", Strong.easeOut, playerHeatBar.width, heatBarWidth, .5, true);
	else
		new Tween(playerHeatBar, "width", Strong.easeOut, playerHeatBar.width, pHeat / pHeatMax * heatBarWidth, .5, true);
	if (oHeat / oHeatMax * heatBarWidth > heatBarWidth)
		new Tween(opponentHeatBar, "width", Strong.easeOut, opponentHeatBar.width, heatBarWidth, .5, true);
	else
		new Tween(opponentHeatBar, "width", Strong.easeOut, opponentHeatBar.width, oHeat / oHeatMax * heatBarWidth, .5, true);
	if (pEnergy / pEnergyMax * energyBarWidth > 0 || playerEnergyBar.width > 0)
		new Tween(playerEnergyBar, "width", Strong.easeOut, playerEnergyBar.width, pEnergy / pEnergyMax * energyBarWidth, .5, true);
	if (oEnergy / oEnergyMax * energyBarWidth > 0 || opponentEnergyBar.width > 0)
		new Tween(opponentEnergyBar, "width", Strong.easeOut, opponentEnergyBar.width, oEnergy / oEnergyMax * energyBarWidth, .5, true);
	
	//Actual Bar width
	playerHealthBar.width = pHealth / pHealthMax * healthBarWidth;
	opponentHealthBar.width = oHealth / oHealthMax * healthBarWidth;
	playerHeatBar.width = pHeat / pHeatMax * heatBarWidth;
	opponentHeatBar.width = oHeat / oHeatMax * heatBarWidth;
	playerEnergyBar.width = pEnergy / pEnergyMax * energyBarWidth;
	opponentEnergyBar.width = oEnergy / oEnergyMax * energyBarWidth;
}

function setPlayerConfig(torso, legs, side1, side2, side3, side4, top1, top2, drone, charge, tele, hook, mod1, mod2, mod3, mod4, mod5, mod6, mod7, mod8, paint): void
{
	playerSetup.push(torso, legs, side1, side2, side3, side4, top1, top2, drone, charge, tele, hook, mod1, mod2, mod3, mod4, mod5, mod6, mod7, mod8);
	
	pHealthMax = 0;
	pHealth = 0;
	pHeatMax = 0;
	pHeat = 0;
	pCooling = 0;
	pEnergyMax = 0;
	pEnergy = 0;
	pRegen = 0;
	pPhyRes = 0;
	pExpRes = 0;
	pEleRes = 0;
		
	for(i = 0; i < playerSetup.length; i++){
		if(playerSetup[i] > -1){
			pHealthMax += itemDB[playerSetup[i]][5];
			pHeatMax += itemDB[playerSetup[i]][11];
			pCooling += itemDB[playerSetup[i]][12];
			pEnergyMax += itemDB[playerSetup[i]][13];
			pRegen += itemDB[playerSetup[i]][14];
			pPhyRes += itemDB[playerSetup[i]][15];
			pExpRes += itemDB[playerSetup[i]][16];
			pEleRes += itemDB[playerSetup[i]][17];
			pWalkDist += itemDB[playerSetup[i]][26];
			pJumpDist += itemDB[playerSetup[i]][27];
		}
	}
	
	pHealthMax += healthBuff;
	pHealth = pHealthMax;
	pHeatMax *= heatBuff;
	pHeat = 0;
	pCooling *= coolingBuff;
	pEnergyMax *= energyBuff;
	pEnergy = pEnergyMax;
	pRegen *= regenBuff;
	pPhyRes *= phyResBuff;
	pExpRes *= expResBuff;
	pEleRes *= eleResBuff;
		
	setMechStructure(pMechBase, 1, torso, legs, side1, side2, side3, side4, top1, top2, drone, paint);
	
	updateBattle();
}
setPlayerConfig(slot[0][3], slot[1][3], slot[2][3], slot[3][3], slot[4][3], slot[5][3], slot[6][3], slot[7][3], slot[8][3], slot[9][3], slot[10][3], slot[11][3], slot[12][3], slot[13][3], slot[14][3], slot[15][3], slot[16][3], slot[17][3], slot[18][3], slot[19][3], customPaint);

function setOpponentConfig(torso, legs, side1, side2, side3, side4, top1, top2, drone, charge, tele, hook, mod1, mod2, mod3, mod4, mod5, mod6, mod7, mod8, paint): void
{
	opponentSetup.push(torso, legs, side1, side2, side3, side4, top1, top2, drone, charge, tele, hook, mod1, mod2, mod3, mod4, mod5, mod6, mod7, mod8);
	
	oHealthMax = 0;
	oHealth = 0;
	oHeatMax = 0;
	oHeat = 0;
	oCooling = 0;
	oEnergyMax = 0;
	oEnergy = 0;
	oRegen = 0;
	oPhyRes = 0;
	oExpRes = 0;
	oEleRes = 0;
	prevOpTorso = torso;
	prevOpLegs = legs;
	prevOpSide1 = side1;
	prevOpSide2 = side2;
	prevOpSide3 = side3;
	prevOpSide4 = side4;
	prevOpTop1 = top1;
	prevOpTop2 = top2;
	prevOpDrone = drone;
	prevOpCharge = charge;
	prevOpTele = tele;
	prevOpHook = hook;
	prevOpMod1 = mod1;
	prevOpMod2 = mod2;
	prevOpMod3 = mod3;
	prevOpMod4 = mod4;
	prevOpMod5 = mod5;
	prevOpMod6 = mod6;
	prevOpMod7 = mod7;
	prevOpMod8 = mod8;
	prevOpPaint = paint;
		
	if (opponentClass != "dummy")
	{
		for(i = 0; i < opponentSetup.length; i++)
		{
			if(opponentSetup[i] > -1)
			{
				oHealthMax += itemDB[opponentSetup[i]][5];
				oHeatMax += itemDB[opponentSetup[i]][11];
				oCooling += itemDB[opponentSetup[i]][12];
				oEnergyMax += itemDB[opponentSetup[i]][13];
				oRegen += itemDB[opponentSetup[i]][14];
				oPhyRes += itemDB[opponentSetup[i]][15];
				oExpRes += itemDB[opponentSetup[i]][16];
				oEleRes += itemDB[opponentSetup[i]][17];
				oWalkDist += itemDB[opponentSetup[i]][26];
				oJumpDist += itemDB[opponentSetup[i]][27];
			}
		}
		oHealthMax += healthBuff;
		oHealth = oHealthMax;
		oHeatMax *= heatBuff;
		oHeat = 0;
		oCooling *= coolingBuff;
		oEnergyMax *= energyBuff;
		oEnergy = oEnergyMax;
		oRegen *= regenBuff;
		oPhyRes *= phyResBuff;
		oExpRes *= expResBuff;
		oEleRes *= eleResBuff;
	}
	else
	{
		oHealthMax = 10000000;
		oHealth = oHealthMax;
		oHeatMax = 10000000;
		oHeat = 0;
		oCooling = 10000000;
		oEnergyMax = 10000000;
		oEnergy = oEnergyMax;
		oRegen = 10000000;
		oPhyRes = 0;
		oExpRes = 0;
		oEleRes = 0;
		oWalkDist = 0;
		oJumpDist = 0;
	}
	setMechStructure(oMechBase, 2, torso, legs, side1, side2, side3, side4, top1, top2, drone, paint);
	updateBattle();
}

function getOpponent(): void
{
	var mod1:int = -1;
	var mod2:int = -1;
	var mod3:int = -1;
	var mod4:int = -1;
	var mod5:int = -1;
	var mod6:int = -1;
	var mod7:int = -1;
	var mod8:int = -1;
	
	badWeaponsList.splice(badWeaponsList.length);
	
	switch (opponentClass)
	{
		case "Previous":
			setOpponentConfig(prevOpTorso, prevOpLegs, prevOpSide1, prevOpSide2, prevOpSide3, prevOpSide4, prevOpTop1, prevOpTop2, prevOpDrone, prevOpCharge, prevOpTele, prevOpHook, prevOpMod1, prevOpMod2, prevOpMod3, prevOpMod4, prevOpMod5, prevOpMod6, prevOpMod7, prevOpMod8, prevOpPaint);
			break;
			
		case "Noob":
			badWeaponsList.push(getID("Mighty Protector"), getID("UltraHot Protector"), getID("SuperCharge Protector"), getID("Maximum Protector"));
			opponentNameTxt.text = "Possibly Not You";
			setOpponentConfig(rngItem(0, 0), rngItem(1, 0), rngItem(2, 0), rngItem(2, 0), rngItem(2, 0), rngItem(2, 0), rngItem(3, 0), rngItem(3, 0), rngItem(4, 0), rngItem(5, 0), rngItem(6, 0), rngItem(7, 0), rngItem(8, 0), rngItem(8, 0), rngItem(8, 0), rngItem(8, 0), rngItem(8, 0), rngItem(8, 0), rngItem(8, 0), rngItem(8, 0), new ColorTransform(Math.random() * .2 + .4, Math.random() * .2 + .4, Math.random() * .2 + .4));
			break;
			
		case "Normal":
			opponentNameTxt.text = "KilliN"
			badWeaponsList.push(getID("Avenger"), getID("Defense Matrix Torso"), getID("Defense Matrix Legs"), getID("Armor Annihilation"), getID("Armor Dissolver"), getID("BloodWeep"), getID("Terror Cry"), getID("Defense Matrix Weapon"), getID("UltraBright"), getID("Hot Flash"), getID("Reckless Beam"), getID("Desert Fury"), getID("Iron Frenzy"), getID("Desert Snake"), getID("Savagery"), getID("Grim Cobra"), getID("Delerium"), getID("HurlBat"), getID("Greedy"), getID("DustMaker"), getID("Snack"), getID("Torment"), getID("Anguish"), getID("Shockwave"), getID("Double Teleporter"));
			var r:uint = Math.ceil(Math.random() * 3);
			
			if (r == 1)
			{
				mod1 = getID("Platinum Plating");
				mod2 = getID("Platinum Plating");
				mod3 = getID("Platinum Plating");
				mod4 = getID("Platinum Plating");
				mod5 = getID("Maximum Protector");
				mod6 = getID("Heat Engine");
				mod7 = getID("Heat Mass Booster");
				mod8 = getID("Heat Mass Booster");
			}
			if (r == 2)
			{
				mod1 = getID("Platinum Plating");
				mod2 = getID("Platinum Plating");
				mod3 = getID("Platinum Plating");
				mod5 = getID("Maximum Protector");
				mod5 = getID("Heat Engine");
				mod6 = getID("Heat Engine");
				mod7 = getID("Heat Mass Booster");
				mod8 = getID("Heat Mass Booster");
			}
			if (r == 3)
			{
				mod1 = getID("Platinum Plating");
				mod2 = getID("Platinum Plating");
				mod5 = getID("Maximum Protector");
				mod3 = getID("Heat Engine");
				mod5 = getID("Energy Engine");
				mod6 = getID("Energy Engine");
				mod7 = getID("Energy Engine");
				mod8 = getID("Energy Engine");
			}
			setOpponentConfig(rngItem(0, r), rngItem(1, r), rngItem(2, r), rngItem(2, r), rngItem(2, r), rngItem(2, r), rngItem(3, r), rngItem(3, r), rngItem(4, r), rngItem(5, 0), rngItem(6, 0), rngItem(7, 0), mod1, mod2, mod3, mod4, mod5, mod6, mod7, mod8, new ColorTransform(Math.random(), Math.random(), Math.random()));
			break;
			
		case "Mirror":
			opponentNameTxt.text = "Mirror";
			setOpponentConfig(slot[0][3], slot[1][3], slot[2][3], slot[3][3], slot[4][3], slot[5][3], slot[6][3], slot[7][3], slot[8][3], slot[9][3], slot[10][3], slot[11][3], slot[12][3], slot[13][3], slot[14][3], slot[15][3], slot[16][3], slot[17][3], slot[18][3], slot[19][3], customPaint);
			break;
			
	/*	case "":
			
			break;
			
		case "":
			
			break;
			
		case "":
			
			break;
			
		case "":
			
			break;
	*/
		default:
			opponentNameTxt.text = "Defense Matrix";
			setOpponentConfig(getID("Defense Matrix Torso"), getID("Defense Matrix Legs"), getID("Defense Matrix Weapon"), getID("Defense Matrix Weapon"), -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, new ColorTransform(Math.random() * .3, .2 + Math.random() * .3, .8 + Math.random() * .2));
	}
}
getOpponent();

function setStartingPosition (): void
{
	var p:Number = Math.random();
	
	if (p > .66)
	{
		pPosition = 5;
		oPosition = 6;
	}
	else if (p > .33)
	{
		pPosition = 4;
		oPosition = 7;
	}
	else
	{
		pPosition = 3;
		oPosition = 8;
	}
	pMechBase.x = xPos[pPosition];
	pMechBase.y = land.y;
	oMechBase.x = xPos[oPosition];
	oMechBase.y = land.y;
	updateBattle();
}
setStartingPosition();

function runTurn (): void
{
	totalTurns++;
	
	if (pTurns > 0) {
		stage.setChildIndex(stage.getChildByName("player"), stage.numChildren - 1);
		isPlayerTurn = true;
		playerControls.visible = true;
		trace(totalTurns + " -> Player Move");
		if (opponentClass != "dummy") pTurns--;
		if (pTurns == 0)
		{
			if (pDroneActive)
				useItem(slot[8][3]);
			
			pEnergy += pRegen;
			
			isPlayerTurn = false;
			oTurns = 2;
			var tween1:Tween = new Tween(playerControls, "y", Strong.easeOut, playerControls.y, playerControls.y + 90, .3, true);
			tween1.addEventListener(TweenEvent.MOTION_FINISH, hideControls);
			function hideControls (e:TweenEvent): void {
				tween1.removeEventListener(TweenEvent.MOTION_FINISH, hideControls);
				playerControls.visible = false;
			}
			displayFloatingText("Opponent's Turn", blank);
		}
	}
	else if (oTurns > 0)
	{
		stage.setChildIndex(stage.getChildByName("opponent"), stage.numChildren - 1);
		oTurns--;
		trace(totalTurns + " -> Opponent Move");
		if (oTurns == 0)
		{
			if (oDroneActive)
				useItem(prevOpDrone);
			
			oEnergy += oRegen;
			
			getControls("main");
			isPlayerTurn = true;
			playerControls.visible = true;
			pTurns = 2;
			new Tween(playerControls, "y", Strong.easeOut, playerControls.y, playerControls.y - 90, .3, true);
			displayFloatingText("Your Turn", blank);
		}
	}
	updateBattle();
}
runTurn();

function getControls (section:String): void
{
	while (controlsArray.length > 0)
	{
		playerControls.removeChild(controlsArray[0]);
		controlsArray[0] = null;
		controlsArray.shift();
	}
	
	switch (section)
	{
		case "main":
			if (slot[1][3] > -1)
			{
				if (itemDB[slot[1][3]][26] > 0 || itemDB[slot[1][3]][27] > 0)
				{
					var motionBtn:MovieClip = new BattleControlBtn();
					motionBtn.addChild(new MotionBtnIcon());
					motionBtn.addEventListener(C, function (e:MouseEvent): void
					{
						if (isPlayerTurn)
							getControls("motion");
					});
					mcToBtn(motionBtn);
					controlsArray.push(motionBtn);
				}
			}
			if (slot[2][3] > -1 || slot[3][3] > -1 || slot[4][3] > -1 || slot[5][3] > -1 || slot[6][3] > -1 || slot[7][3] > -1)
			{
				var weaponsBtn:MovieClip = new BattleControlBtn();
				weaponsBtn.addChild(new WeaponsBtnIcon());
				weaponsBtn.addEventListener(C, function (e:MouseEvent): void
				{
					if (isPlayerTurn)
						getControls("weapons");
				});
				mcToBtn(weaponsBtn);
				controlsArray.push(weaponsBtn);
			}
			if (slot[8][3] > -1 || slot[9][3] > -1 || slot[10][3] > -1 || slot[11][3] > -1)
			{
				var specialsBtn:MovieClip = new BattleControlBtn();
				specialsBtn.addChild(new SpecialsBtnIcon());
				mcToBtn(specialsBtn);
				controlsArray.push(specialsBtn);
			}
			if (itemDB[slot[1][3]][6] > 0)
			{
				var stompBtn:MovieClip = new BattleControlBtn();
				stompBtn.addChild(new StompBtnIcon());
				stompBtn.addEventListener(C, function (e:MouseEvent): void
				{
					if (canMove())
						useStomp("player");
				});
				mcToBtn(stompBtn);
				controlsArray.push(stompBtn);
			}
			if (pCooling > 0)
			{
				var shutdownBtn:MovieClip = new BattleControlBtn();
				shutdownBtn.addChild(new ShutdownBtnIcon());
				shutdownBtn.addEventListener(C, function (e:MouseEvent): void
				{
					if (canMove()) {
						pHeat -= pCooling;
						runTurn();
						shutdownAnim("player");
					}
				});
				mcToBtn(shutdownBtn);
				controlsArray.push(shutdownBtn);
			}
			break;
		
		case "motion":
			backControlsBtn();
			if (pWalkDist)
			{
				var dist:int = 0;
				
				if (pWalkDist > pJumpDist)
					dist = pWalkDist * -1;
				else
					dist = pJumpDist * -1;
				
				while (dist <= pWalkDist || dist <= pJumpDist)
				{
					makeArea(pPosition + dist);
					dist++;
				}
			}
			break;
			
		case "weapons":
			backControlsBtn();
			for (i = 2; i <= 7; i++)
			{
				if (slot[i][3] > -1)
				{
					var weapon:MovieClip = new BattleControlBtn();
					var weaponIcon:Sprite = buildSprite(itemDB[slot[i][3]][0], 60, 60, false, true);
					weapon.addChild(weaponIcon);
					function f (n:uint): void
					{
						weapon.addEventListener(C, function (e:MouseEvent): void
						{
							if (canMove())
								useItem(slot[n][3]);
						});
					}
					f(i);
					mcToBtn(weapon);
					controlsArray.push(weapon);
				}
			}
			break;
	}
	
	function makeArea (position): void
	{
		if (position != pPosition && position != oPosition && position > 0 && position < 11)
		{
			if (pPosition < oPosition)
			{
				if (position < pPosition)
					f();
				else if (position < oPosition)
					f();
			}
			else
			{
				if (position > pPosition)
					f();
				else if (position > oPosition)
					f();
			}
		}
		
		function f (): void
		{
			var area2:MovieClip = new ATGAIdentifier();
			area2.addEventListener(C, mechMotionAnim());
			area2.name = (position).toString();
			area2.x = xPos[position];
			area2.y = land.y;
			areasArray.push(area2);
			stage.addChild(area2);
		}
	}
	
	function mechMotionAnim (): *
	{
		return function (e:MouseEvent): void
		{
			if (isPlayerTurn)
			{
				if (canMove()) {
					pPosition = int(e.target.name);
					getControls("main");
					if (itemDB[slot[1][3]][33] == "roll")
						rollAnim("player", xPos[pPosition]);
					else
						jumpAnim("player", xPos[pPosition]);
				}
			}
			else
			{
				oPosition = int(e.target.name);
				if (itemDB[prevOpLegs][33] == "roll")
					rollAnim("opponent", xPos[oPosition]);
				else
					jumpAnim("opponent", xPos[oPosition]);
			}
			removeATGA();
			runTurn();
		}
	}
	
	if (controlsArray.length)
	{
		for (i = 0; i < controlsArray.length; i++)
		{
			controlsArray[i].x = i * 76 - 360;
			playerControls.addChild(controlsArray[i]);
		}
	}
}
getControls("main");

function backControlsBtn (): void
{
	var backControlsBtn:MovieClip = new BattleControlBtn();
	backControlsBtn.addChild(new BackControlsBtnIcon);
	backControlsBtn.addEventListener(C, function (e:MouseEvent): void
	{
		removeATGA();
		getControls("main");
	});
	mcToBtn(backControlsBtn);
	controlsArray.push(backControlsBtn);
}

function removeATGA (): void
{
	while (areasArray.length > 0)
	{
		stage.removeChild(areasArray[0]);
		areasArray[0] = null;
		areasArray.shift();
	}
}

function jumpAnim (target:String, finalPos:uint): void
{
	runningAnim = true;
	
	var duration:uint = 1;
	var mechBase = stage.getChildByName(target);
	var motion1:Tween = new Tween(mechBase, "y", Regular.easeOut, mechBase.y, land.y - 80, duration / 2, true);
	
	new Tween(mechBase, "x", None.easeNone, mechBase.x, finalPos, duration, true);
	
	motion1.addEventListener(TweenEvent.MOTION_FINISH, reachMaxHeigth);
	function reachMaxHeigth (e:TweenEvent): void {
		motion1.removeEventListener(TweenEvent.MOTION_FINISH, reachMaxHeigth);
		var motion2:Tween = new Tween(mechBase, "y", Regular.easeIn, mechBase.y, land.y, duration / 2, true);
		motion2.addEventListener(TweenEvent.MOTION_FINISH, hitGround);
		function hitGround (e:TweenEvent): void {
			runningAnim = false;
			heavyImpactMp3.play();
			motion2.removeEventListener(TweenEvent.MOTION_FINISH, hitGround);
		}
	}
}

function rollAnim (target:String, finalPos:uint): void
{
	runningAnim = true;
	
	var duration:uint = 2;
	var mechBase = stage.getChildByName(target);
	var motion1:Tween = new Tween(mechBase, "x", Regular.easeInOut, mechBase.x, finalPos, duration, true);
		
	motion1.addEventListener(TweenEvent.MOTION_FINISH, reachFinalPos);
	function reachFinalPos (e:TweenEvent): void
	{
		runningAnim = false;
		motion1.removeEventListener(TweenEvent.MOTION_FINISH, reachFinalPos);
	}
}

function shutdownAnim (target:String): void
{
	var duration:Number = 2
	var mechBase = stage.getChildByName(target);
	var mechTorso = mechBase.getChildByName("torso");
	var indicator:MovieClip = new ShutdownIndicator();
	var transition1:Tween = new Tween(indicator, "name", Regular.easeOut, 0, 100, duration * .8, true);
	
	runningAnim = true;
	stage.addChild(indicator);
	shutdownMp3.play();
	indicator.x = mechBase.x;
	indicator.y = mechBase.y;
	indicator.play();
	
	mechBase.addEventListener(Event.ENTER_FRAME, updateAlpha);
	function updateAlpha (e:Event): void
	{
		mechTorso.mcShutdown.alpha = int(indicator.name) / 100;
	}
	
	transition1.addEventListener(TweenEvent.MOTION_FINISH, reachMaxAlpha);
	function reachMaxAlpha (e:TweenEvent): void
	{
		var transition2:Tween = new Tween(indicator, "name", Regular.easeOut, 100, 0, duration * .2, true);
		
		transition2.addEventListener(TweenEvent.MOTION_FINISH, reachMinAlpha);
		function reachMinAlpha (e:TweenEvent): void
		{
			mechBase.removeEventListener(Event.ENTER_FRAME, updateAlpha);
			transition1.removeEventListener(TweenEvent.MOTION_FINISH, reachMaxAlpha);
			transition2.removeEventListener(TweenEvent.MOTION_FINISH, reachMinAlpha);
			stage.removeChild(indicator);
			indicator = null;
			runningAnim = false;
		}
	}
}

function useStomp (target:String): void
{
	var duration:Number = 1;
	var mechBase = stage.getChildByName(target);
	var mechLeg = mechBase.getChildByName("leftLeg");
	var initialY:Number = mechLeg.height * -0.5;
	var finalY:Number = mechLeg.height * -0.5 - 25;
	var transition1:Tween = new Tween(mechLeg, "y", None.easeNone, initialY, finalY, duration * .6, true);
	
	runningAnim = true;
	transition1.addEventListener(TweenEvent.MOTION_FINISH, reachMaxHeight);
	function reachMaxHeight (e:TweenEvent): void
	{
		var transition2:Tween = new Tween(mechLeg, "y", Strong.easeIn, finalY, initialY, duration * .4, true);
		transition2.addEventListener(TweenEvent.MOTION_FINISH, hitGround);
		function hitGround (e:TweenEvent): void
		{
			transition1.removeEventListener(TweenEvent.MOTION_FINISH, reachMaxHeight);
			transition2.removeEventListener(TweenEvent.MOTION_FINISH, hitGround);
			useItem(slot[1][3]);
			runningAnim = false;
		}
	}
}

function knockBackAnim (target:String, X:uint): void
{
	var duration:Number = 1;
	var mechBase = stage.getChildByName(target);
	var finalPos:uint = xPos[X];
	var transition1:Tween = new Tween(mechBase, "x", Strong.easeOut, mechBase.x, finalPos, duration, true);
	
	runningAnim = true;
	
	transition1.addEventListener(TweenEvent.MOTION_FINISH, reachFinalPos);
	function reachFinalPos (e:TweenEvent): void
	{
		runningAnim = false;
		transition1.removeEventListener(TweenEvent.MOTION_FINISH, reachFinalPos);
	}
}

var dmgTxtContainer:MovieClip = new MovieClip();
stage.addChild(dmgTxtContainer);
function displayDamage(dmg:uint): void
{
	var duration:Number = 1.5;
	var a:Tween = null;
	var t:TextField = new TextField();
	var f:TextFormat = new TextFormat();
	var d:DropShadowFilter = new DropShadowFilter();
	
	t.text = "-" + dmg;
	t.width = 100;
	t.height = 50;
	t.selectable = false;
	t.transform.colorTransform = new ColorTransform(1, 1 - dmg * .002, 1 - dmg * .002);
	
	if (isPlayerTurn)
	{
		t.x = oMechBase.x - (t.width * .5);
		t.y = oMechBase.y + 100;
	}
	else
	{
		t.x = pMechBase.x - (t.width * .5);
		t.y = pMechBase.y + 100
	}
	
	f.align = "center";
	f.font = "Humnst777 Blk BT";
	f.color = 0xEEEEEE;
	f.size = 30;
	t.setTextFormat(f);
	
	d.distance = 0;
	d.angle = 0;
	d.alpha = 1;
	d.blurX = 5;
	d.blurY = 5;
	d.strength = 2;
	t.filters = new Array(d);
	
	dmgTxtContainer.addChild(t);
	
	new Tween(t, "y", Strong.easeOut, t.y, t.y - 100 + Math.random() * 50, duration * .3, true);
	new Tween(t, "x", Regular.easeOut, t.x, t.x - 15 + Math.random() * 30, duration * .3, true);
	a = new Tween(t, "alpha", Regular.easeOut, 3, 0, duration * .4, true);
	
	a.addEventListener(TweenEvent.MOTION_FINISH, v(t));
	function v (o:DisplayObject): Function
	{
		return function (e:TweenEvent): void
		{
			while (dmgTxtContainer.numChildren > 0)
			{
				var child = dmgTxtContainer.getChildAt(0);
				dmgTxtContainer.removeChild(child);
				child.removeEventListener(TweenEvent.MOTION_FINISH, v);
				child = null;
			}
		}
	}
}

function canMove (): Boolean
{
	if (!isPlayerTurn)
	{
		displayFloatingText("It's not your turn.", blank);
		return false;
	}
	else if (runningAnim)
	{
		displayFloatingText("Please Wait...", blank);
		return false;
	}
	else
		return true
}

//Dev usage
oMechBase.addEventListener(MouseEvent.CLICK, function(e:MouseEvent): void
{
	if (!runningAnim)
	{
		if (!isPlayerTurn)
		{
			oHeat -= oCooling;
			runTurn();
			shutdownAnim("opponent");
		}
		else
			trace("Not opponent Turn");
	}
});

pMechBase.addEventListener(MouseEvent.CLICK, function(e:MouseEvent): void
{
	clearStage();
});

function clearStage (): void
{
	for (i = 0; i < dmgTxtContainer.numChildren; i++)
		trace("kill " + dmgTxtContainer.getChildAt(i));
}
