# How To Edit Mods
You might have just downloaded a mod and realized its close but not _exactly_ how you would like it, that happens to all of us, let's go through and edit a mod.
## Editing the Mod
+ Find the mod, in this example we'll use the mod we created in the last step called `MyMod`.
+ It should still be in your Workspace, but if it is a mod you downloaded you will want to add the mod folder to your workspace, once you are done editing it and do not want it in your workspace you can just right click on the folder and hit `Remove from Workspace`.
+ Now in your workspace go to the 'MyMod' folder and click on the 'Config' folder if it is not already open, now click on the `blocks.xml`.
+ You should now see the modded xml file, we are going to edit it to make the fallen tree drop a Truck instead of a jar of honey, and what chance that we could get it, remember this is just an example and I would not actually have this in my game, I just want to show you what you can do.
+ Find the line that says:
```xml
<drop event="Destroy" name="foodHoney" count="1,5" prob="0.25"/>
```
Now change the `"foodHoney"` to `"vehicle4x4TruckPlaceable"`. I found that by looking in the `items.xml`.    
Now change the `"0.25"` to `"1"`, making it a 100% chance to get it.    
Now change the `"1,5"` to `"1,1"`, making it to where we could only get 1.    
   
   
   

It should now look like: 
```xml
<drop event="Destroy" name="vehicle4x4TruckPlaceable" count="1,1" prob="1"/>
```

## Done
You have now edited the mod to drop a placeable Truck when you cut down any tree everytime.    

Remember we don't need to save since we have Autosave on, you can now go enjoy your truck dropping trees! haha     
[Back to Main Menu](../../main/README.md)
