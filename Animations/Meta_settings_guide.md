# Flipper Animation Guide : meta.txt settings
 **📑 <ins>SUMMARY</ins>**
- **[📄 meta.txt : content overview]()**<BR>
- **[🐬 Flipper Zero official documentation : meta.txt]()**<BR>
- **[🎬 ANIMATION : Meta Main settings]()**<BR>
    - **[Frame dimensions]()**<BR>
- **[💬 BUBBLES : in-depth guide]()**<BR>
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
Meta is pure text file (.txt) and can be opened/edited via any text editor (such as *Notepad*).<BR>
I colored in purple the part that is mandatory, in green what is optional (only applies if **bubbles** are used) and in white the data filled by the user.<BR>

![meta-overview](https://github.com/user-attachments/assets/177fe028-83d8-487c-831c-7e0a0c610166)

<BR>

## 🐬 Flipper Zero official documentation : meta.txt
*Flipper Devices* provides to users basic information about meta file.<BR> 
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
The first two settings listed in meta.txt are `Width: ` & `Height`.<BR>
Values ​​are in pixels and must strictly match the dimensions of the animation frames.<BR>
Since the Flipper screen can display 128x64 pixels, these would therefore be the max values.<BR>

![W H](https://github.com/user-attachments/assets/8cd700df-05fe-420b-813b-c89e7d1ff050)

While most animations (from official Flipper Devices or custom makers) are made, for convenience mainly, on this frame size, one can choose to make an animation with smaller frames.<BR>
For instance, official release contains a bunch of animations that aren't 128x64px with values such as 128x51px or 128x49px.<BR>
Most of official non-128x64px anims are stored in flash memory (***internal*** & ***blocked*** anims) which makes sense in saving as much octets as possible due to the very low internal storage capacity. But even within the official ***external*** animations (those saved on SD), we can notice 3 (as of Nov. 24) that also use a reduced frame format.<BR>

For instance, the first frame of ***L1_Laptop_128x51***, is (as its name specifies) only 51px high :

![128x51_Laptop](https://github.com/user-attachments/assets/c240459a-32de-4a6b-b13b-84eb4927c714)

Frames are aligned on the BOTTOM LEFT corner without option to change that.<BR>
While it is not an issue at all when it comes to height (as the upper part of screen is mostly displaying the status bar and icons), it should be kept in mind when setting a width inferior to 128 as animation will be left-aligned.

For example, 64x32px frame position on screen :

![64x32px_frame](https://github.com/user-attachments/assets/d4340de3-3e18-42d1-b74a-ed4141b44ac6)

> [!TIP]
> Animation frame must be set up to 128x64px<BR>
> Width & Height values must match the pixel dimensions of the frames.<BR>
> Those being defined in the meta, all frames of one animation must have the same dimensions.<BR>
> Frames are bottom-left aligned.<BR>
> Using frames of dimensions inferior to 128x64px makes only sense when editing an animation meant to be put in Flipper's internal memory. There would not be any significant impact for the ones stored on SD.<BR>
<BR>

## 💬 BUBBLES : in-depth guide<BR>
‎
### 🔸  Bubbles : Definition
Bubbles are text inputs that will display as an additional layer above an animation, enclosed in coded-drawn lines in the spirit of comic book speech bubble.<BR><BR>

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
> ⮚ Postion of the [bubble tail](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubble-tail-positioning)<BR>

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
Depending on text input, it's a matter of testing to check if it fits or not.<BR>

To have multiple lines within the same bubble, `\n` can be used to define **newline**.<BR>
Next line first word should be written directly after the function. (no space in between).

An input such as `Text: First line\nSecond line\nThird line\nForth line\nFifth line` would render as :

![5LINES_1](https://github.com/user-attachments/assets/2e3bb69d-17ab-4e1e-8aab-b4cbf76d8936)

We note that we can only have **up to 5 lines** that would properly show on screen.<BR>
Of course, this will be dependent of the bubble placement and some lines can be displayed out of screen depending on `Y` value.<BR>
(`Y` must be set between 0 and 5 to be able to have 5 lines of text as well as the bubble outline in its whole displayed)

![5LINES_2](https://github.com/user-attachments/assets/1a4afe5b-6f58-4a5d-a372-8388fbe7c799)

Same goes with too many lines. Only fully displayable lines shows.<BR>
If we set the `Y` at its minimum value (0) and set the text on 6 lines with `Text: First line\nSecond line\nThird line\nForth line\nFifth line\nSixth Line`, 
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

We note that having both `AlignH` & `AlignV` set to `Center` results in hiding the tail.

The coded outline of the bubble is not dependent of the animation background and will remain black even on top of a black background, and as consequence will not be visible :

![Bubble_Tails_NEG](https://github.com/user-attachments/assets/aa5799df-bc04-4f27-9bff-afa4d19f5e52)

It then renders slightly more squared as the rounded-angles of the outline are not visible.

> [!TIP]
> Use `AlignH: Center` **+** `AlignV: Center` to have no bubble tail.
<BR>

### 🔸  Bubble coordinates & Tail positioning issues
Here comes the tricky part :<BR>
If you set a tail to be visible, in order to be correctly displayed on screen, its design ***in its whole*** must be set to fit on the screen. Otherwise, you will face some strange behaviours.

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

Black background allows to enlight that the tails themselves are correctly drawn and that the issue is only on their outlines.

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
