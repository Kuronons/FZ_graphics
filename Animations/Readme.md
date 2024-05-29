Here are the animations I made for Flipper Zero. Those are folder-sorted by theme with preview videos* :

- [Custom firmwares](https://github.com/Kuronons/FZ_graphics/tree/main/Animations/Custom_Firmwares) - Dedicated to cfw and affiliated
- [Black Flags](https://github.com/Kuronons/FZ_graphics/tree/main/Animations/Black_Flags_Collection) - 30 animations collection
- [Sci-Fi corpo logos](https://github.com/Kuronons/FZ_graphics/tree/main/Animations/SF_Corporations_Logos) - 12 animations collection
- [DOS viruses](https://github.com/Kuronons/FZ_graphics/tree/main/Animations/Virus) - 12 animations collection
- [Ghost in the Shell](https://github.com/Kuronons/FZ_graphics/tree/main/Animations/GITS) - 5 animations collection
- [Cyberpunk 2077](https://github.com/Kuronons/FZ_graphics/tree/main/Animations/CP77) - 4 animations collection
- [Monopoly cards](https://github.com/Kuronons/FZ_graphics/tree/main/Animations/Monopoly_Cards) - WIP, 2 animations
- [Miscellaneous](https://github.com/Kuronons/FZ_graphics/tree/main/Animations/Miscellaneous) - Unsorted

*edit 2024/03/04 : Replaced .webm files by .mp4 to make them viewable under iOS.<BR>

<BR>**TO INSTALL ON YOUR FLIPPER ZERO :**

1. Download animation zip file on your PC.<BR>
   (Each .zip file contains a folder including the animation frames under .bm files and its corresponding meta.txt)

2. Unzip and drag&drop / copy&paste the folder<BR>
-> If your are under official, Unleashed or RogueMaster firmware : into your flipper's ***SD/dolphin/*** folder.<BR>
-> If you are under Momentum or Xtreme firmware : into your flipper's asset pack folder (***SD/asset_packs/yourcustompacknamehere/Anims/***).
    
3. Manifest<BR>
-> Edit your manifest ***SD/dolphin/manifest.txt*** (OFW, UL or RM)<BR>
-> or create one ***SD/asset_packs/yourcustompacknamehere/Anims/manifest.txt*** (MFW or XFW)<BR><BR>
and add (or replace) an entry as example below.

          Filetype: Flipper Animation Manifest
          Version: 1

          Name: Kuronons_SFlogo_Tyrell_128x64
          Min butthurt: 0
          Max butthurt: 14
          Min level: 1
          Max level: 3
          Weight: 9
   Note that animation name entry must be the animation folder exact name.<BR>
   Edit the butthurt/level/weight values according to your needs and firmware.<BR>
   (You can also replace your existing manifest file by one I provided in this github...)
   
5. Reboot your Flipper (OS). And you're **DONE !**<BR>
Don't forget to select your asset pack if under Momentum / Xtreme.

<BR>

For better understanding on how animations work or how to make / set them, have a look at the [TURORIALS & TOOLS](https://github.com/Kuronons/FZ_graphics#links-of-interest--flipper-graphics---tutorials--other-hints) links section.<BR>
You will most probably find all you need there.

And don't hesitate to check [THE MOST COMMON MISTAKES DONE WHEN MAKING AN ANIMATION](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Common_mistakes.md) I wrote if you're facing some issue making your animation. Feedback showed that there is 99% chance your issue's origin is listed there !<BR><BR>
Feel free to ping me on Flip-related Discord(s) if you're stuck !<BR>

O_oV
