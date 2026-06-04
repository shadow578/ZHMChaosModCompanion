this directory contains patches to duplicate existing outfits to the globaldata brick, so they are available from chunk0.
this is kind of a hack, but i don't want to mess with a) loading the outfit bricks at runtime or b) spawning the globaloutfitkits manually.
so, instead i simply copy the global outfit kits i want to the globaldata brick, and then setup SMF to port the charset and outfit templates to chunk0.

to add another outfit for this, you'll need to:
1) copy the globaloutfitkit entity to `OutfitDuplicates.entity.patch.json` patch, parented to `_ChaosMod_Outfits` entity.
2) cleanup entities below the globaloutfitkit entity, you'll only need the charset and maybe animset (tho the last one is optional).
3) find the repository entry via the `m_sId` property of the outfitkit, then modify `OutfitDuplicates.repository.json`. Simply copy & paste the entry with the matching repository id into a new repo entry, then update the commonname. Outfits added by ChaosMod use the `CM_` prefix!
4) update the `m_sId` and `m_sCommonName` properties of the outfitkit entity to match the new repository entry.
5) you may also have to update the `m_pParentOutfit` property. Outfits from other bricks may pull in a external reference to globaldata here - but since we're in globaldata already, you can simply do a direct reference. Generally, you'll want to point this to the `Base_CivMale` base outfit (EID `6736fcbbd3e73209`). `postInit` should be set to true as well. Note that you may have to remove the external scene reference that glacierkit automatically adds when copy/pasting.
6) add the charset template factory path to the dependencies in `manifest.json`, if it's not in chunk0 already.
7) open the charset template, and find any references to outfit templates in it. note the ioi paths for them, then add them to the dependencies in `manifest.json` as well, assuming they're not in chunk0 already.
8) done. you should now be able to select your `CM_**` outfit and change actors to the outfit in SMFs actor mod.

refer to the commit introducing this README.md for a full example.


Note:
- `OutfitDuplicates.entity.patch.json` patches `[assembly:/_pro/scenes/bricks/globaldata.brick].pc_entitytype`
- `OutfitDuplicates.repository.json` patches `[assembly:/repository/pro.repo].pc_repo`
