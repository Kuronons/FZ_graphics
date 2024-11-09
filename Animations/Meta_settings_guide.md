# Flipper Animation Guide : meta.txt settings
 **📑 <ins>SUMMARY</ins>**
- **[📄 meta.txt : content overview](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#-metatxt--content-overview)**<BR>
- **[🐬 Flipper Zero official documentation : meta.txt](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#-flipper-zero-official-documentation--metatxt)**<BR>
- **[🎬 ANIMATION : Meta Main settings](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#-animation--meta-main-settings)**<BR>
    - **[Frame dimensions](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--frame-dimensions)**<BR>
    - **[Passive & Active Frames : definition](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--passive--active-frames--definition)**<BR>
    - **[Frames order](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--frames-order)**<BR>
    - **[Active cycles](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--active-cycle)**<BR>
    - **[Frame rate](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--frame-rate)**<BR>
    - **[Duration](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--duration)**<BR>
    - **[Active cooldown](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--active-cooldown)**<BR>
- **[💬 BUBBLES : in-depth guide](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#-bubbles--in-depth-guide)**<BR>
    - **[Bubbles : definition](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubbles--definition)**<BR>
    - **[Bubble placement](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubble-placement)**<BR>
    - **[Bubble text line](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubble-text-line)**<BR>
    - **[Bubble tail positioning](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubble-tail-positioning)**<BR>
    - **[Bubble coordinates & Tail positioning issues](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubble-coordinates--tail-positioning-issues)**<BR>
> [!NOTE]
> For better visualization and understanding, I am using a custom firmware that allows to hide the top status bar border as well as top status icons to provide suitable screenshots.
<BR>

## 📄 meta.txt : content overview
Below an example of a meta.txt file content. (from Flipper Zero [L1_Cry_128x64](https://github.com/flipperdevices/flipperzero-firmware/tree/dev/assets/dolphin/external/L1_Cry_128x64) animation)<BR>
Meta is pure text file (.txt) and can be opened/edited via any text editor (such as *Notepad*).<BR><BR>
I colored in purple the part that is mandatory, in green what is optional (only applies if **bubbles** are used) and in white the data filled by the user.<BR>

![meta-overview](https://github.com/user-attachments/assets/177fe028-83d8-487c-831c-7e0a0c610166)

<BR>

## 🐬 Flipper Zero official documentation : meta.txt
*Flipper Devices* provides basic information about meta file in their Github repo.<BR> 
The following (here collapsible) content can be found in [flipperzero-firmware/assets/dolphin/readme.md](https://github.com/Kuronons/flipperzero-firmware/edit/dev/assets/dolphin/ReadMe.md)<BR>
<details><summary>🔹 Definition & Header settings</summary>
  
- meta.txt : Flipper Format File with ordered keys.<BR>
- Header:

```
Filetype: Flipper Animation
Version: 1
```
</details><details><summary>🔹 Animation dimensions settings</summary>
  
- `Width` - animation width in px (<= 128)
- `Height` - animation height in px (<= 64)
</details><details><summary>🔹 Frames ordering</summary>

- `Passive frames` - number of bitmap frames for passive animation state
- `Active frames` - number of bitmap frames for active animation state (can be 0)
- `Frames order` - order of bitmap frames where first N frames are passive and following M are active. Each X number in order refers to bitmap frame, with name frame\_X.bm. This file must exist. Any X number can be repeated to refer same frame in animation.
</details><details><summary>🔹 Animation settings</summary>
  
- `Active cycles` - cycles to repeat of N active frames for full active period. E.g. if frames for active cycles are 6 and 7, and active cycles is 3, so full active period plays 6 7 6 7 6 7. Full period of passive + active period are called *total period*.
- `Frame rate` - number of frames to play for 1 second.
- `Duration` - total amount of seconds to play 1 animation.
- `Active cooldown` - amount of seconds (after passive mode) to pass before entering next active mode.
</details><details><summary>🔹 Bubbles settings</summary>
  
- `Bubble slots` - amount of bubble sequences.
- Any bubble sequence plays whole sequence during active mode. There can be many bubble sequences and bubbles inside it. Bubbles in 1 bubble sequence have to reside in 1 slot. Bubbles order in 1 bubble sequence is determined by occurrence in file. As soon as frame index goes out of EndFrame index of bubble - next animation bubble is chosen. There can also be free of bubbles frames between 2 bubbles.

- `Slot` - number to unite bubbles for same sequence.
- `X`, `Y` - are coordinates of left top corner of bubble.
- `Text` - text in bubble. New line is `\n`
- `AlignH` - horizontal place of bubble corner (Left, Center, Right)
- `AlignV` - vertical place of bubble corner (Top, Center, Bottom)
- `StartFrame`, `EndFrame` - frame index range inside whole period to show bubble.
</details><details><summary>🔹 Frame indexes vizualisation</summary>
  
- Understanding of frame indexes

For example we have

```
Passive frames: 6
Active frames: 2
Frames order: 0 1 2 3 4 5 6 7
Active cycles: 4
```

Then we have indexes

```
                        passive(6)            active (2 * 4)
Real frames order:   0  1  2  3  4  5     6  7  6  7  6  7  6  7
Frames indexes:      0  1  2  3  4  5     6  7  8  9  10 11 12 13
```
</details><BR>

## 🎬 ANIMATION : Meta Main settings<BR>
### 🔸  Frame dimensions
The first two settings listed in meta.txt are :<BR>
- `Width:` being the frame measurement on the ***X*** axis, horizontal.<BR>
- `Height:` being the frame measurement on the ***Y*** axis, vertical.<BR>

Values ​​are in pixels and must strictly match the dimensions of the animation frames.<BR>
Since the Flipper screen can display 128x64 pixels, these would therefore be the max values.<BR>

![W H](https://github.com/user-attachments/assets/8cd700df-05fe-420b-813b-c89e7d1ff050)

While most animations (from official Flipper Devices or custom makers) are made, for convenience mainly, on this frame size, one can choose to make an animation with smaller frames.<BR><BR>
Official ***Flipper Devices*** firmware contains a bunch of animations that aren't 128x64px with values such as 128x51px or 128x49px.
Most of those are stored in flash memory (***internal*** & ***blocked*** anims) which makes sense in saving as much octets as possible due to the very low internal storage capacity. But even within the official ***external*** animations (those saved on SD), we can notice 3 (as of Nov. 24) that also use a reduced frame format.<BR><BR>
For instance, the first frame of ***L1_Laptop_128x51***, is (as its name specifies) only 51px high and will leave a 13px high unanimated area on top of the screen (blue-colored here) :

![128x51_Laptop](https://github.com/user-attachments/assets/80fda538-0cd5-4d5f-af9d-612d24195a93)

Frames are aligned on the BOTTOM LEFT corner without option to change that.<BR>
While it is not an issue at all when it comes to height (as the upper part of screen is mostly displaying the status bar and icons), it should be kept in mind when setting a width inferior to 128 as animation will be left-aligned.<BR><BR>
For example, 64x32px frame position on screen :

![64x32px_frame](https://github.com/user-attachments/assets/d4340de3-3e18-42d1-b74a-ed4141b44ac6)

> [!WARNING]
> Setting dimensions different from the actual bitmap image, while not causing the animation to fail, will result in a distorted display.<BR>
> Note that this will occur when compiling an animation with faulty meta values, but also when later editing the meta of an animation previously compiled with correct values.<BR>
> For instance, the very same 64x32px bitmap frame wrongly set to `Width:54` & `Height 22` and then to `Width:74` & `Height 42` :

![64x32px_frame-wrong_meta_size](https://github.com/user-attachments/assets/5e64fd72-71d7-4597-b0a6-f5bcd443a3a8)

> [!TIP]
> Animation frame must be set up to 128x64px<BR>
> Width & Height values must match the pixel dimensions of the frames.<BR>
> Those being defined in the meta, all frames of one animation must have the same dimensions.<BR>
> Frames are bottom-left aligned.<BR>
> Using frames of dimensions inferior to 128x64px makes only sense when editing an animation meant to be put in Flipper's internal memory. There would not be any significant impact for the ones stored on SD.
<BR>

### 🔸  Passive & Active Frames : definition
Animation frames can be of 2 kinds : passive or active.<BR>

***Passive frames*** are the ones that are played in loop on Flipper idle screen.<BR>
An animation requires at least 1 passive frame to work.<BR>
Therefore, minimum value could never go under ***1***.<BR>
`Passive frames:` value defines the passive sequence by the number of frames that will be picked up from the ones listed in ***Frames order***.

***Active frames*** are the ones that are played once triggered/activated.<BR>
They have 2 possible triggers : Hitting the ***back*** button or coming back to animation screen from any other menu.<BR>
Once triggered the active sequence will start to play. (ie. It won't wait for the passive sequence to end)<BR>
An animation does **NOT** require active frame(s) to work.<BR>
If no active frame, value must be set to ***0***.<BR>
`Active frames:` value defines the activable sequence by the number of frames that will be picked up from the ones listed in ***Frames order***.

The sum of values of `Passive frames:` and `Active frames:` must equal to the number of frames listed in ***Frames Order***.

The use of active frames is of maker's choice. It provides to the user a basic level of interraction and can be designed in many artistic or playful ways.<BR><BR>

### 🔸  Frames Order
`Frames order:` is used to define the sequences of passive and active frames.<BR>
It lists the frames by calling the bitmap files via their designed number. (ie the number between ***frame_*** and ***.bm*** in the file name : *frame_12.bm* = *12*)<BR><BR>
Passive frames are always listed first. Active frames (if any) comes after.<BR>
As said, the total of inputs must be equal to the sum of `Passive frames:` & `Active frames:` values.<BR><BR>
On top of that, each bitmap file must be listed at least once by its number.<BR>
As well, every listed input must refer to an existing bitmap file.<BR><BR>
In the following example (simple passive/active animation with no frame repetition), we have 10 .bm frames numbered frame_0.bm to frame_9.bm.<BR>
6 first frames (0 to 5) are set are the *passive* ones while the 4 remaining ones (6 to 9) are set to *active*.<BR>

![Frames_order](https://github.com/user-attachments/assets/fcc304c5-dc7a-49d7-bd08-027e6dda2bfe)

A bitmap file can be listed multiple times, and be counted multiple times in passive and/or active frames.<BR>
The frames order being the sequence(s) of bitmap displayed following maker's choice, it does **NOT** require to be a logical numerary suite (such as 1 2 3 4...) as long as it follows the requirements mentioned above.<BR><BR>
Next example shows those. It uses frame repetitions in an animation built on only 5 .bm frames numbered frame_0.bm to frame_4.bm, without listing the frames in a "logical" numerical order.<BR>
We emphasize here that the number of active/passive frames is not related to the number of bitmap images, but rather to the number of calls of these in their respective sequences.

![Frames_order_2](https://github.com/user-attachments/assets/7346c449-e23b-4435-96d9-7dc7d81d7743)

Still, trying to stick as much as possible to numeral order when it comes to name the bitmap files, accordingly to the position they should play within the animation, will greatly help building the ***frames order*** or editing it later (especially on long *frames order* listing 100+ inputs).<BR><BR>
Labelling of bitmap files requiring the first frame to be named ***frame_0.bm***, the minimum input value in `Frames order:` is ***0*** in the case of a 1 only passive frame animation.<BR><BR>

### 🔸  Active Cycles
`Active cycles:` value determines the number of time the active frames sequence will play in a row once triggered.<BR><BR>
Once the the active period (ie the number of cycles of the active sequence) is over, animation will revert to passive one.<BR><BR>
***Active cycles*** is a choice of design to limit the number of inputs listed in ***Frame order***.<BR><BR>
If animation has no active frames (ie `Active frames: 0`), `Active cycles:` should be set to `0` too.<BR>
As well if animation contains active frames, `Active cycles:` should be set to at least `1`.<BR>
> [!WARNING]
> If those values are not set accordingly, compiling the animation via `./fbt` (to make .png frames into .bm ones) **will definitely fail**.

![FBT_error-Active_Cycles](https://github.com/user-attachments/assets/560583ae-333d-4cd1-886e-68958f1d67b5)

However, and against all odds (and logics), an already compiled animation ***should*** still be able to play on Flipper without failure.<BR>
For instance, `Active frames: 1` while there is **no** active frames : no noticeable consequences.<BR>
**But**, having `Active frames: 0` when there are active frames will make the animation unable to trigger the active sequence : only passive frames will play in loop even if the ***back*** button is pushed.<BR><BR>
The number of frames that make up the ***active cycles*** above the first one are not counted as it in ***Active frames*** but will however be counted when it comes to ***bubbles***.<BR><BR>

### 🔸  Frame rate
`Frame rate:` is the well known ***fps*** : Frames Per Second.<BR>
It defines how many frames will be played during 1 second.<BR>
> [!NOTE]
> Historically, theatre movie standard fps was set on 24.<BR>
> Drawn-animation however had usually a fps set to 12 and even lower (mainly due to production costs) such as 6 or 8 when it came to *Saturday Morning Cartoons* type animations.

Flipper will not be able to handle very high fps mainly due to hardware limitation (RAM size and display capability).<BR>
Flipper screen refresh rate being what it is, flickering or ghosting effect will occur if fps is set too high.<BR>
As well, Flipper firmware may crash on high ***frame rate*** if RAM is oversatured.<BR><BR>
The usual working range of fps is 1-12, but it's not really recommended to have a frame rate above 8.<BR>
All original Flipper animations (external, internal, blocked and event the level-up ones) have their ***frame rate*** set to 2.<BR><BR>
`Frame rate:` value must be an integer (number without decimal) and therefore cannot be less than 1.<BR>
As consequence, the slowest animation would be of 1 frame per second. Only way to have one frame to play longer on screen is to double its input in ***Frames order***.<BR>
The time each frame will play on screen is then calculated as follow : ***1 second divided by frame rate***.<BR>
For instance, a frame rate of 4 will make each frame play 0.25 second on screen.<BR>
Adjusting frame rate and playing with the inputs in Frames order makes visual acceleration or slow-down effects possible.<BR><BR>

### 🔸  Duration
`Duration:` is used to determine the period of time one animation will run until it switches to the next random one.<BR>
Duration values are seconds.<BR><BR>
By default, most animations have a duration value of 3600 with equals to 1 hour.<BR><BR>
Duration is an underestimated setting that can be used to polish transitions in a suite of animations.<BR>
For example, having a total of 60 inputs in ***frames order*** and 2 as ***frame rate*** would result in a 30 seconds animation.<BR>
In order to play this animation 5 times entirely before it switches to the next, `Duration:` would be set to `150`.<BR>
This way, the switching will occur at the very end of the passive sequence instead of cutting it somewhere in the middle.<BR><BR>
***Duration*** can also add some game aspect to a suite of animations.<BR>
It can be used with passive/active animations having identical passive frames but different active sequences.<BR>
Setting a duration of 10mn (600) for example will make the user curious about what will be revealed if he presses back as, whatever the animation of the set is playing, it would always be the same passive sequence looping on the screen.<BR><BR>

### 🔸  Active cooldown
`Active cooldown:` is a delay, set in seconds, that will apply once an active period ends and during which the active sequence is not triggerable.<BR>
It forces passive frames to play during the defined time, temporarely disabling the back-button *active* trigger.<BR><BR>
As well as for ***Active cycles***, if animation has no active frames (ie `Active frames: 0`), `Active cooldown:` should be set to `0` too.<BR>
As well if animation contains active frames, `Active cooldown:` should be set to at least `1`.<BR>
> [!WARNING]
> If those values are not set accordingly, compiling the animation via `./fbt` (to make .png frames into .bm ones) **will definitely fail**.

![FBT_error-Active_Cooldown](https://github.com/user-attachments/assets/ae49d362-b639-4310-8ebb-8cb90ba42c69)

However, same as for ***Active cycles***, an already compiled animation ***should*** still be able to play on Flipper without failure.<BR>
For instance, `Active cooldown: 1` while there is no active frames : no consequences.<BR>
And same goes with `Active cooldown: 0` while there are active frames.<BR><BR>

## 💬 BUBBLES : in-depth guide<BR>
‎
### 🔸  Bubbles : Definition
Bubbles are text inputs that will display as an additional layer above an animation, enclosed in coded-drawn lines in the spirit of comic book speech bubble.<BR>
<BR>

### 🔸  Bubble placement
Bubble placement on screen is defined by its upper-left corner coordinates.<BR>
Screen is  128x64px. First column (X - from left) as well as first line (Y - from top) are designed by **0**.
Coordinates will be set as :
- `X: ` = horizontal coordinate (values range = `0` to `127`)
- `Y: ` = vertical coordinate (values range = `0` to `63`)

![BP0](https://github.com/user-attachments/assets/431a041f-98df-4eb2-910c-9492709d24be)

We will note that the bubble layer is not dependent of the animation frames size.<BR>
Bubble sticks to its screen coordinates and won't be affected in any way when displayed out the animation frames area as the following test shows (64x32px frames anim) :<BR>

![bubble_out_of_frame](https://github.com/user-attachments/assets/63b95d1b-2396-4f55-9645-c650d1cb2940)

> [!TIP]
> The placement being only defined by the upper-left corner of the bubble, it must be thought in regards of those 3 factors :<BR>
> ⮚ Lenght of the longest text line for the X value<BR>
> ⮚ Number of text lines for the Y one<BR>
> ⮚ Postion of the [bubble tail](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubble-tail-positioning)

> [!WARNING]
> A **negative value in X or Y** will result of a ***furi_hal error*** and would most likely put your Flipper in an **endless restart-loop !!**<BR>
> If it happens, just get the SD out and fix the meta by entering a positive value.<BR>
> If you don't have an SD card reader, take the SD card out and re-insert it again without passing the SD welcome splash-screen.<BR>
> It will allow you to overwrite the non-functioning meta via qFlipper files management.
<BR>

### 🔸  Bubble text line
The displayed text of the bubble is defined by the eponymous function :
- `Text: ` followed by the text to display. Note that the part of the text lenght that would be out of the screen will not be visible anyhow.

![ABCD](https://github.com/user-attachments/assets/58059654-ad11-4f02-b3f1-2f7fcc678f5b)

We see that a bubble can barely fit the 26 lowercase letters of the alphabet.<BR>
Depending on text input, it's a matter of testing to check if it fits or not.<BR><BR>
To have multiple lines within the same bubble, `\n` can be used to define **newline**.<BR>
Next line first word should be written directly after the function. (no space in between).<BR><BR>
An input such as `Text: First line\nSecond line\nThird line\nForth line\nFifth line` would render as :

![5LINES_1](https://github.com/user-attachments/assets/2e3bb69d-17ab-4e1e-8aab-b4cbf76d8936)

We note that we can only have **up to 5 lines** that would properly show on screen.<BR>
Of course, this will be dependent of the bubble placement and some lines can be displayed out of screen depending on `Y` value.<BR>
(`Y` must be set between 0 and 5 to be able to have 5 lines of text as well as the bubble outline in its whole displayed)

![5LINES_2](https://github.com/user-attachments/assets/1a4afe5b-6f58-4a5d-a372-8388fbe7c799)

Same goes with too many lines. Only fully displayable lines shows.<BR>
If we set the `Y` at its minimum value (0) and set the text on 6 lines :<BR>
`Text: First line\nSecond line\nThird line\nForth line\nFifth line\nSixth Line`<BR>
we end up with this result :

![6LINES](https://github.com/user-attachments/assets/fe852559-0b54-46b8-85be-5ad8555a12dd)

> [!TIP]
> A maximum of 5 lines of text in a bubble using the `\n` function.<BR>
> A maximum of 20-30 characters (spaces included) on a line.
<BR>

### 🔸  Bubble tail positioning
The positioning of the tail (the bubble pointer) is set by those 2 functions and their applicable options :
- `AlignH: ` = **H**orizontal **Align**ment (Options = `Left`, `Center`, `Right`)
- `AlignV: ` = **V**ertical **Align**ment (Options = `Top`, `Center`, `Bottom`)

As a result we have 9 (3x3) possible placement of the tail : 

![Bubble_Tails_POS](https://github.com/user-attachments/assets/ceb72d3d-a527-4f8d-b5bb-bc33d217209f)

We note that having both `AlignH` & `AlignV` set to `Center` results in hiding the tail.<BR><BR>
The coded outline of the bubble is not dependent of the animation background and will remain black even on top of a black background, and as consequence will not be visible :

![Bubble_Tails_NEG](https://github.com/user-attachments/assets/aa5799df-bc04-4f27-9bff-afa4d19f5e52)

It then renders slightly more squared as the rounded-angles of the outline are not visible.

> [!TIP]
> Use `AlignH: Center` **+** `AlignV: Center` to have no bubble tail.
<BR>

### 🔸  Bubble coordinates & Tail positioning issues
Here comes the tricky part :<BR>
If you set a tail to be visible, in order to be correctly displayed on screen, its design ***in its whole*** must be set to fit on the screen. Otherwise, you will face some strange behaviours.<BR><BR>
Tails are adding a 4 pixels design on the edge of the bubble they're placed on.

![TAIL_SIZE](https://github.com/user-attachments/assets/11cd9ce3-a3be-48aa-8b05-54390accc0e0)

To allow a tailed-bubble to be displayed on screen without issue, bubble coordinates values must be set taking into account those additionnal 4 pixels.<BR>
> [!WARNING]
> Issue will occur if there are less than 4 pixels between the screen's **left** or **top** border and the tail.

As a pict is worth a thousand words, let's have an insight on how it behaves if we set a bubble in the upper-left corner with not enough space from the edges to have its tail properly displayed.<BR>
In the following tests, we will set different bubble coordinates so it lacks 1 single pixel from the screen border to allow tail to be fully displayed.<BR>
Again we will test with both white (orange) and black backgrounds as it helps to understand what is drawn on screen.

![Bubble Tails_POS](https://github.com/user-attachments/assets/a0aae534-a37c-4f70-a027-0ea9ab890fd9)

It enlights that issues occur when there is not enough space on TOP and/or LEFT screen sides to display the tail, creating some *backdraft* tail that displays over the text.<BR>
We note that, apart for just displaying what fits the screen, there is no particular issue with BOTTOM or RIGHT sides of the screen.<BR>
We will also note that, despite there is no tail to be meant to be shown on middle screenshot (`AlignH` & `AlignV` both set to `Center`), it still creates, for some reason, a single and unwanted pixel dot in the upper-left corner.

![Bubble Tails_NEG](https://github.com/user-attachments/assets/02469597-30d5-4695-9698-f94061657ffb)

Black background allows to enlight that the tails themselves are correctly drawn and that the issue is only on their outlines.<BR><BR>
Testing on a single-line bubble makes even more weird result 👀 :

![Bubble Tails_singleline](https://github.com/user-attachments/assets/e2b8226e-304e-45e4-bf3f-cf58a4810448)

> [!NOTE]
> It's important to mention that those strange artifacts are just visual bugs and won't make Flipper to crash.<BR>
> One could decide to use those strange tail behaviours in some artistic way... 

> [!TIP]
> When ***bubble*** is a layer above the ***animation*** one, main screen ***status bar*** and ***icons/battery*** are on layers above bubble one.<BR>
> ⮚ That must be taken into consideration to avoid having text partially covered by those.<BR><BR>
> Ensure safe bubble coordinates and tail position accordingly.<BR>
> ⮚ It's safer/easier to set your bubble `X: ` & `Y: ` to at least `4` to ensure avoiding issue with tail.<BR>
> ⮚ If possible, set your tail position to the sides (or center) of the bubble that are furthest from the edge of the screen.
