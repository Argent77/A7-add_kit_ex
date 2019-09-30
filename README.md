# WeiDU functions: ADD_KIT_EX and GET_KIT_EX

This project aims at unifying WeiDU's built-in functions ADD_KIT and COPY_KIT as well as the complementary function [fl#add_kit_ee](https://github.com/WeiDUorg/fl-add_kit_ee).

## ADD_KIT_EX

### Overview

ADD_KIT_EX allows you to add new kits to the game or create copies of existing kits. In both cases it is possible to alter selected attributes of the kit and let the function derive the remaining information either from a specified source kit or the kit's parent class. The function provides full support for both classic and EE games.

The following games are currently supported: BG2 (with or without ToB), Tutu, BGT, BG:EE (with or without SoD), BG2:EE, EET, IWD:EE and PST:EE*. TobEx and GemRB are considered when detected.

*(\*) PST:EE does theoretically support kits, but lacks the necessary files.*

**Notes:**<br/>
Adding the kit name to any of the specified 2DA strings is optional. It will be included automatically if needed.

Unless stated otherwise, if no value is provided for one or more of the optional parameters, the corresponding value of a given source kit or the parent class (in that order) will be copied and used for this kit if needed.

Missing entries in specified 2da strings will be filled with sane default values if needed.

Parameter | Description
---|---
STR_VAR&nbsp;kit_name  | (required) The internal name of your kit. This name is used throughout all relevant IDS and 2DA files to reference your kit.
INT_VAR visible        | (optional) Indicates whether the kit will be selectable during character creation. Set to 0 to make it unselectable for player characters. Default: 1
INT_VAR kit_class      | (required, unless "source_kit" is specified) Parent class ID added to kitlist.2da.
INT_VAR mixed          | (required, unless "source_kit" is specified) Mixed name strref of your kit, added to kitlist.2da.
INT_VAR lower          | (optional) Lower name strref of your kit, added to kitlist.2da. A lower-cased version of "mixed" is generated if this parameter is not available.
INT_VAR help           | (optional) Description string of your kit, added to kitlist.2da.
INT_VAR biography      | (optional, EE-only) The biography strref of your kit, added to clastext.2da.
INT_VAR briefdesc      | (optional, EE-only) Short class or kit description strref added to clastext.2da.
INT_VAR fallen         | (optional, EE-only) 0 or 1. Indicates whether the kit is a "fallen" variant. This parameter is only relevant for ranger and paladin kits. Added to clastext.2da.
INT_VAR fallen_notice  | (optional, EE-only) Fallen notice strref. Notice is shown in combat log when the fallen status is applied to the character. Added to clastext.2da.
STR_VAR source_kit     | (optional, unless "kit_class" is omitted)  Name of an existing kit to copy information from for all omitted parameters. Specify this parameter and set "visible" to 0 to imitate behavior of the original WeiDU function "COPY_KIT".
STR_VAR unusable       | (optional) Unusability code added to kitlist.2da. Must be a positive number in decimal or (preferrably) hexadecimal notation. Omit to inherit usability of source kit or parent class.<br/>***Note:** Defined as string parameter to work around WeiDU restrictions.*
STR_VAR clasweap       | (optional) 2DA string added to clasweap.2da.
STR_VAR weapprof       | (optional) 2DA string added to weapprof.2da.
STR_VAR abclasrq       | (optional) 2DA string added to abclasrq.2da.
STR_VAR abclsmod       | (optional) 2DA string added to abclsmod.2da.
STR_VAR abdcdsrq       | (optional) 2DA string added to abdcdsrq.2da.
STR_VAR abdcscrq       | (optional) 2DA string added to abdcscrq.2da.
STR_VAR alignmnt       | (optional) 2DA string added to alignmnt.2da.
STR_VAR dualclas       | (optional) 2DA string added to dualclas.2da.
STR_VAR luabbr         | (optional) 2DA string added to luabbr.2da.
STR_VAR stweap         | (optional) 2DA string added to 25stweap.2da.
STR_VAR clab_path      | (optional) The path to the CLAB-style 2DA file of your kit. File is installed and reference is added to kitlist.2da. Omit to inherit the CLAB of specified source kit or parent class instead which may be created dynamically if needed (e.g. for multiclass kits).
STR_VAR kittable       | (optional) List of which class and race combinations the kit should be available for, as per kittable.2da. Omit to make kit available for all races. Use parameter "visible" instead if you want to make the kit unavailable for all races during character creation.
STR_VAR clsrcreq       | (optional, EE-only) 2DA string added to clsrcreq.2da.
STR_VAR clswpbon       | (optional, EE-only) 2DA string added to clswpbon.2da.
STR_VAR hpclass        | (optional, EE-only) 2DA string added to hpclass.2da. If this string references a custom 2DA file, it needs to be copied into the game separately.
STR_VAR numwslot       | (optional, EE-only) 2DA string added to numwslot.2da.
STR_VAR clascolr       | (optional, EE-only) 2DA string added to clascolr.2da.
STR_VAR clasiskl       | (optional, EE-only) 2DA string added to clasiskl.2da.
STR_VAR clasthac       | (optional, EE-only) 2DA string added to clasthac.2da.
STR_VAR thiefscl       | (optional, EE-only) 2DA string added to thiefscl.2da.
STR_VAR backstab       | (optional, EE-only) 2DA string added to backstab.2da. Missing columns are filled with copies of the last specified value. This argument should only be provided for thief kits and will be ignored for other classes.
STR_VAR sneakatt       | (optional, EE-only) 2DA string added to sneakatt.2da. Missing columns are filled with copies of the last specified value. This argument should only be provided for thief kits and will be ignored for other classes.
STR_VAR crippstr       | (optional, EE-only) 2DA string added to crippstr.2da. Missing columns are filled with copies of the last specified value. This argument should only be provided for thief kits and will be ignored for other classes.
STR_VAR thiefskl       | (optional, EE-only) 2DA string added to thiefskl.2da. This argument should only be provided for thief and monk kits and will be ignored for other classes.
STR_VAR traplimt       | (optional, EE-only) 2DA string added to traplimt.2da. This argument should only be provided for thief kits and will be ignored for other classes.
STR_VAR bdstweap       | (optional, EE-only) 2DA string added to bdstweap.2da.
RET kit_id             | The numeric value generated for the specified kit. This value is exactly 0x4000 less than the number your kit is assigned in kit.ids. Returns -1 if the kit couldn't be installed.

#### Experimental parameters for testing purposes only:
Parameter | Description
---|---
INT_VAR \_\_kits_limit_override  | Maximum number of supported kit entries. Default: 0 (autodetect)
INT_VAR \_\_kits_base_value      | The kit base value added to "kit_id" when added to kitlist.2da or kit.ids. *Default: 0x4000*

### Usage

Launch `ADD_KIT_EX` via `LAUNCH_ACTION_FUNCTION` and specify the parameter you want to have set or changed.

Example of a minimalistic kit definition:
```
LAUNCH_ACTION_FUNCTION ADD_KIT_EX
  INT_VAR
    kit_class = 4   // Parent class: Thief
    mixed     = RESOLVE_STR_REF(~Adventurer~)
    lower     = RESOLVE_STR_REF(~adventurer~)   // Not strictly necessary: will be auto-generated if omitted
    help      = RESOLVE_STR_REF(~ADVENTURER: A jack-of-all-trades...~)  // Not strictly necessary: Parent class
                                                                        // description will be used if omitted
  STR_VAR
    kit_name  = "ADVENTURER"
  RET
    kit_id
END
```
This function call will install a new Thief kit called "Adventurer". Omitted attributes will be derived from the kit's base class if needed. At successful execution the kit will be installed and can be identified by the numeric value returned by the "kit_id" parameter.

## GET_KIT_EX

See function description here: [readme-get_kit_ex.txt](https://raw.githubusercontent.com/Argent77/A7-add_kit_ex/master/a7-add_kit_ex/readme-get_kit_ex.txt)
