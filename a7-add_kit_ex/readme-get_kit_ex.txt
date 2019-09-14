#########################
## Function GET_KIT_EX ##
#########################

Author: Argent77
Licence: Public Domain
Date: 2019-08-26


Description
~~~~~~~~~~~

GET_KIT_EX allows you to retrieve information about any existing kit. The function provides full support for both
classic and EE games.

The following games are currently supported:
BG2 (with or without ToB), Tutu, BGT, BG:EE (with or without SoD), BG2:EE, EET, IWD:EE and PST:EE*.

(*) PST:EE does theoretically support kits, but lacks the necessary files.

Parameters:
STR_VAR kit_name    (required) The internal name of the kit as specified in kitlist.2da.
INT_VAR use_parent  (optional) Set to 1 to derive missing information from the kit's parent class if available.
                    Set to 0 to leave missing fields empty. Default: 0

Return values:
RET kit_id          The numeric value of the specified kit. For "modern" kits this value is exactly 0x4000 less than
                    the number defined in kit.ids. For "classic" kits (such as specialist mages or the barbarian kit)
                    this value is identical to the number defined in kit.ids. Returns -1 if the kit is not available.
                    Note: Because of WeiDU restrictions the value of the Wild Mage kit is returned as -2147483648.
RET kit_class       Numeric value of the parent class associated with the kit. -1 if this information is not available.
RET mixed           Mixed name strref of the kit. -1 if this information is not available.
RET lower           Lower name strref of the kit. -1 if this information is not available.
RET help            Description string of the kit. -1 if this information is not available.
RET biography       (EE-only) Biography strref of the kit. -1 if this information is not available.
RET briefdesc       (EE-only) Short class or kit description strref. -1 if this information is not available.
RET fallen          (EE-only) Whether the kit is a "fallen" variant. -1 if this information is not available.
RET fallen_notice   (EE-only) Fallen notice strref. Notice is shown in combat log when the fallen status is applied to
                    the character. -1 if this information is not available.
RET unusable        Unusability code associated with the kit in hexadecimal notation. Empty string if this information
                    is not available. Note: Defined as string parameter to work around WeiDU restrictions.
RET clasweap        2DA string from clasweap.2da. Empty string if this information is not available.
RET weapprof        2DA string from weapprof.2da. Empty string if this information is not available.
RET abclasrq        2DA string from abclasrq.2da. Empty string if this information is not available.
RET abclsmod        2DA string from abclsmod.2da. Empty string if this information is not available.
RET abdcdsrq        2DA string from abdcdsrq.2da. Empty string if this information is not available.
RET abdcscrq        2DA string from abdcscrq.2da. Empty string if this information is not available.
RET alignmnt        2DA string from alignmnt.2da. Empty string if this information is not available.
RET dualclas        2DA string from dualclas.2da. Empty string if this information is not available.
RET luabbr          2DA string from luabbr.2da. Empty string if this information is not available.
RET stweap          2DA string from 25stweap.2da. Empty string if this information is not available.
RET clab_res        The CLAB-style 2DA resref associated with the kit. Empty string if this information is not
                    available.
RET kittable        List of which class and race combinations the kit is available for, as per kittable.2da.
                    Empty string if this information is not available.
RET clsrcreq        (EE-only) 2DA string from clsrcreq.2da.
RET clswpbon        (EE-only) 2DA string from clswpbon.2da.
RET hpclass         (EE-only) HPCLASS table resref associated with the kit. Empty string if this information is not
                    available.
RET numwslot        (EE-only) Number of slots available for the kit, as defined in numwslot.2da. Empty string if this
                    information is not available.
RET clascolr        (EE-only) 2DA string from clascolr.2da. Empty string if this information is not available.
RET clasiskl        (EE-only) 2DA string from clasiskl.2da. Empty string if this information is not available.
RET clasthac        (EE-only) Class/kit THAC0 bonus or penalty as defined in clasthac.2da. Empty string if this
                    information is not available.
RET thiefscl        (EE-only) 2DA string from thiefscl.2da.
RET backstab        (EE-only) 2DA string from backstab.2da. Empty string if this information is not available.
RET sneakatt        (EE-only) 2DA string from sneakatt.2da. Empty string if this information is not available.
RET crippstr        (EE-only) 2DA string from crippstr.2da. Empty string if this information is not available.
RET thiefskl        (EE-only) 2DA string from thiefskl.2da. Empty string if this information is not available.
RET traplimt        (EE-only) Trap cap number, as defined in traplimt.2da. Empty string if this information is
                    not available.
RET bdstweap        (EE-only) 2DA string from bdstweap.2da.


Changelog
~~~~~~~~~

v0.1.0:
- First beta
