# CassetteBeasts-BootlegPaletteSwapping
A Guide to making palette swap mods 

# Introduction
This guide aims to explain both how the color palettes for bootlegs/coatings are set and how to mod them. It's worth noting that editing a monster palettes will also affect their fusion color palette. This guide will not cover the details for fusion color palette, but it's similar to bootlegs and can be experimented with.

# Prerequisites 
- Decompiled Cassette Beasts Project as explained in this [guide](https://wiki.cassettebeasts.com/wiki/Modding:Mod_Developer_Guide)

# Monster Form File
You will find the monster form files in the ```res://data/monster_forms/``` folder of the decompiled project. Choose a monster you want to edit and double click the file to see it in the Godot Inspector window. 

For this example we will use ```gearyu.tres```. You'll notice there is a section named ```Swap Colors```, this is what determines which colors from the monster's color palette will be used/swapped out in case of fusions/bootlegs. This is what we will be editing for our palette swap.

![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/5a20220e-1bb3-4540-a958-3ef2a21528c5)
![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/99519d18-eeb0-4994-9414-ac1e50752de5)

# Elemental Type Palettes
Bootleg colors are determined by the palette found in each elemental type. These files are found in the ```res://data/elemental_types/``` folder of the project. For this example we'll focus on ```lightning.tres```, but the same applies to any of the other palettes. 

Notice we have the same kind of palette list found on gearyu's monster profile. These are the colors that will replace part of our monster's swap palette in the case of coatings/bootlegs. 

![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/8202aa62-f7da-4387-bc0d-2a0a7927b810)

# Color Mapping
How the colors map is pretty simple, each color on the elemental type's palette will replace a color on the monster's swap palette until there are no more colors left on the elemental type palette. Since the elemental types only have 5 colors listed this means they will only replace the first 5 colors on the monster's palette. Without adding more colors to the elemental palette, this means that to change our bootleg/coating color mapping we have to move the colors we want changed up on the monster's swap palette list to fall into the first 5.

This is how a lightning Gearyu maps:

![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/cde9f3ef-e495-4a28-b299-7d747dc7b847)

You may have noticed the darker colors aren't really that visible anywhere on the bootleg form. This is because the colors those replaced are usually the outlines/edges that tend to use darker tones. Keep that in mind when deciding what you will change the targets to.

Let's try changing the order of the colors found on the monster form to target gearyu's main body. The color palettes are organized in descending order from darkest tone to lightest for any particular color. So to get a simple swap we can just take the gray colors from Gearyu's gear's and move them up to the first 5 slots on the list, pushing down the blue hues that were originally there (remember to keep them in descending order of darkness to keep the same style of the original). 

The modified color palette will look like this along with the resulting lightning bootleg example.

![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/57096a1f-3a69-4135-b9d8-f5af504b3ac2)
![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/dfc4d457-3231-4dc2-9803-7f93bfbdba2e)


That's already pretty good! Let's see what it looks like with the red accents changed instead. Here's the palette and the result.

![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/46638905-beb8-479f-8b7b-f35823592d89)
![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/cdc3ad96-6d6c-407b-b046-e2f169883228)

Again, the colors swapped pretty clean. Notice that for the clean looking swap, we had to use all 5 colors from a particular section (The greys for the body and the reds for the accents). With only 5 colors on an elemental type palette, we have little room to mix and match parts if there's too many colors on a specific section. Let's try using only parts of the grey and parts of the red to try and get both sections changed. 

Here's the palette and result:

![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/b040c0ec-988b-4d33-8c09-d5b75af2c86f)
![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/d9a77bed-c474-4651-8e4c-ca0a042fea1d)


Not very good, we're missing important parts of both sections that would otherwise make this work. Some monster forms will target several parts with similar colors, which makes it easier to target other areas. However often times we have situations like this, where there's no good middle ground and we're forced to pick a side (unless the result was your thing, in which case go for it!).

# Previewing Changes
There is a helpful tool included in the project that can be used to preview monster changes. Just open the scene located here ```res://tools/monster_preview/MonsterPreview.tscn``` and run it. Then you can select any monster and preview their fusions/coatings/animations. 

# Packing The Mod
So assuming we found a result that we're happy with, now we're ready to pack this into a neat little mod file. We'll start by making sure we have the right folders set up in our project.

In your FileSystem, make sure you have a mods folder created (this is where you will store any future mod files/folders). Then inside that mods folder we're going to make one for our current mod, I'll call this one ```gearyu_swap```. It should look like this:

![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/f086fbfa-ba75-4dd7-9a02-13a8e5d91656)
![image](https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/602ee11d-6c97-496a-aa46-87e0f7571c43)

Follow these steps to create the mod's metadata file:
- Right click the gearyu_swap folder
- Select New Resource
- Search for ContentInfo and click Create
- Name the file ```metadata.tres```
 
https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/60a32b65-3372-4c90-8621-9fa93e2239f7

Now we populate the metadata fields with the mod information and export that file using the export mod tool.

https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/52d2b97c-1d5f-4584-9cc5-b646efb4fe9f

https://github.com/ninaforce13/CassetteBeasts-BootlegPaletteSwapping/assets/68625676/531a65f0-24be-4f7a-a1fd-0471c736068e


And that's it! We have a mod file ready to be used in our game!


# Notes
As we saw in the example above, we're pretty limited by the number of colors available on the elemental type. You could just add more colors to the elemental type palette or even duplicate the ones already there. Keep in mind though that adding more colors to the palette will affect everyone that uses it and doing so may have unintended issues elsewhere in the game.

This guide is just one way to handle this kind of mod. There is potentially more ways to expand these palettes and customize the forms further with some code edits to the ```ElementalType.gd``` script's method for generating the color palette. 

If you want to exactly identify which colors on a monster's palette belong to which parts of their sprite. I recommend taking the monster's sprite png file from the project and loading it into either aseprite or any other image editing software with a color picker available. That way you can get the exact Hex value of a part color and can check it against the monster form file. 
