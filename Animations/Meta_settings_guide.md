# Flipper Animation Guide : meta.txt settings

> [!NOTE]
> For better visualization and understanding, I am using a custom firmware that allows to hide the top status bar border as well as top status icons.<BR>

## 🗨️ BUBBLES<BR>
‎ **📑 <ins>SUMMARY</ins>**
- **[Bubbles : definition](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubbles--definition)**<BR>
- **[Bubble placement](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubble-placement)**<BR>
- **[Bubble's text line](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubbles-text-line)**<BR>
- **[Bubble's tail positioning](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubbles-tail-positioning)**<BR>
- **[Bubble coordinates & Tail positioning issues](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubble-coordinates--tail-positioning-issues)**<BR>

### 🔸  Bubbles : Definition
Bubbles are text inputs that will display as an additional layer above an animation, enclosed in coded-drawn lines in the spirit of comic book speech bubble.<BR><BR>

### 🔸  Bubble placement
Bubble's placement on screen is defined by its upper-left corner's coordinates.<BR>
Screen is  128x64px. First column (X - from left) as well as first line (Y - from top) are designed by **0**.
Coordinates will be set as :
- `X: ` = horizontal coordinate (values range = `0` to `127`)
- `Y: ` = vertical coordinate (values range = `0` to `63`)

![BP0](https://github.com/user-attachments/assets/4d25a2ae-4f55-434f-a954-87842172030b)

> [!TIP]
> The placement being only defined by the upper-left corner of the bubble, it must be thought in regards of those 3 factors :<BR>
> ⮚ Lenght of the longest text line for the X value<BR>
> ⮚ Number of text lines for the Y one<BR>
> ⮚ Postion of the [bubble's tail](https://github.com/Kuronons/FZ_graphics/blob/main/Animations/Meta_settings_guide.md#--bubbles-tail-positioning)<BR>

> [!WARNING]
> A **negative value in X or Y** will result of a ***furi_hal error*** and would most likely put your Flipper in an **endless restart-loop !!**<BR>
> If it happens, just get the SD out and fix the meta by entering a positive value.<BR>
> If you don't have an SD card reader, take the SD card out and re-insert it again without passing the SD welcome splash-screen.<BR>
> It will allow you to overwrite the non-functioning meta via qFlipper files management.
<BR>

### 🔸  Bubble's text line
The displayed text of the bubble is defined by the eponymous function :
- `Text: ` followed by the text to display. Note that the part of the text lenght that would be out of the screen will not be visible anyhow.

![ABCD](https://github.com/user-attachments/assets/1f21a19d-4bf8-4941-ab67-c74ccfb4964e)

&emsp;&emsp;We can see that a bubble can barely handle the 26 lowercase letters of the alphabet.<BR>
&emsp;&emsp;Depending on text input, it's a matter of testing to check if it fits or not.

- To have multiple lines within the same bubble, `\n` can be used to define **newline**. Next line first word should be written directly after the function. (no space in between).

An input such as `Text: First line\nSecond line\nThird line\nForth line\nFifth line` would render as :

![N1](https://github.com/user-attachments/assets/d1c56649-e34f-449c-9812-c899d65a0ecf)

We note that we would be allowed to have a **maximum of 5 lines** to show properly on screen.<BR>
Of course, this will be dependent of the bubble placement and some lines can be displayed out of screen depending on `Y` value.
(`Y` must be set between 0 and 5 to be able to have 5 lines of text as well as the bubble's outline in its whole displayed)

![N2](https://github.com/user-attachments/assets/9062bbbb-5d65-41c9-910d-e25c00ac0d15)

Same goes with too many lines. Only fully displayable lines shows. If we set the `Y` at its minimum value (0) and set the text on 6 lines with `Text: First line\nSecond line\nThird line\nForth line\nFifth line\nSixth Line`, 
we end up with this result :

![N3](https://github.com/user-attachments/assets/e15854b3-aff0-4954-ad0f-2a3f74fa56c3)

> [!TIP]
> A maximum of 5 lines of text in a bubble using the `\n` function.<BR>
> A maximum of 20-30 characters (spaces included) on a line.
<BR>

### 🔸  Bubble's tail positioning
The positioning of the tail (the bubble's pointer) is set by those 2 functions and their applicable options :
- `AlignH: ` = **H**orizontal **Align**ment (Options = `Left`, `Center`, `Right`)
- `AlignV: ` = **V**ertical **Align**ment (Options = `Top`, `Center`, `Bottom`)

As a result we have 9 (3x3) possible placement of the tail : 

![Bubble_Tails_POS](https://github.com/user-attachments/assets/ceb72d3d-a527-4f8d-b5bb-bc33d217209f)

We note that having both `AlignH` & `AlignV` set to `Center` results in hiding the tail.

The coded outline of the bubble is not dependent of the animation background and will remain black even on top of a black background, and as consequence will not be visible :

![Bubble_Tails_BEG](https://github.com/user-attachments/assets/c047120c-c801-4eef-8da1-9a681ad7b364)

It then renders slightly more squared as the rounded-angles of the outline are not visible.

> [!TIP]
> Use `AlignH: Center` **+** `AlignV: Center` to have no bubble tail.
<BR>

### 🔸  Bubble coordinates & Tail positioning issues
Here comes the tricky part :<BR>
If you set a tail to be visible, in order to be correctly displayed on screen, its design ***in its whole*** must be set to fit on the screen. Otherwise, you will face some strange behaviours.

Tails are adding a 4 pixels design on the edge of the bubble they're placed on.

![TAIL_SIZE](https://github.com/user-attachments/assets/210df639-40f8-4a60-9d06-416a4bf31789)

To allow a tailed-bubble to be displayed on screen without issue, bubble's coordinates values must be set taking into account those additionnal 4 pixels.<BR>
> [!WARNING]
> Issue will occur if there are less than 4 pixels between the screen's border and the tail.

As a pict is worth a thousand words, let's have an insight on how it behaves if we set a bublle in the upper-left corner with not enough space from the edges to have its tail properly displayed.<BR>
In the following tests, we will set bubble's coordinates as `X: 3` & `Y: 3` so it lacks only 1 single pixel on top and left bubble's sides.
