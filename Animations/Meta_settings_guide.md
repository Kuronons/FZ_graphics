# meta.txt file's settings - The guide

## 🗨️ BUBBLES
Bubble is a text input that will display on top of an animation enclosed in coded-drawn lines in the spirit of comic's speech bubble.
<BR>

### 🔸  Bubble's placement
Bubble's placement on screen is defined by its upper-left corner's coordinates.<BR>
Screen is  128x64px. First column (X - from left) as well as first line (Y - from top) are designed by **0**.
Coordinates will be set as :
- `X: ` = horizontal coordinate (values range = 0-127)
- `Y: ` = vertical coordinate (values range = 0-63)

> [!CAUTION]
> A **negative value in X or Y** will result of a furi_hal error and could put your Flipper in an **endless reset-loop**.<BR>
> If it happens, just get the SD out and fix the meta by entering a positive value.<BR>
> If you don't have an SD card reader, take the SD card out and re-insert it again without passing the SD welcome splash-screen.<BR>
> It will allow you to overwrite the non-functioning meta via qFlipper files management.
<BR>

### 🔸  Bubble's text
The displayed text of the bubble is defined by the eponymous function :
- `Text: ` followed by the text to display. Note that the part of the text lenght that would be out of the screen will not be visible anyhow.
- To have multiple lines within the same bubble, `\n` can be used to define **newline**. Next line first word should be written directly after the function. (no space in between).

An input such as `Text: First line\nSecond line\nThird line\nForth line\nFifth line` would render as :

![N](https://github.com/user-attachments/assets/2e5a22ad-927c-43c5-a104-ccbf4c7b5f92)

We note that we would be allowed to have a **maximum of 5 lines** to show properly on screen.<BR>
Of course, this will be dependent of the bubble placement and some lines can be displayed out of screen depending on `Y` value.
(`Y` must be set between 0 and 5 to be able to have 5 lines of text as well as the bubble's outline in its whole displayed)

![N2](https://github.com/user-attachments/assets/7a8fce73-cf7d-43f8-bdb5-41319091052a)

Same goes with too many lines. Only fully displayable lines shows. If we set the `Y` at its minimum value (0) and set the text on 6 lines with `Text: First line\nSecond line\nThird line\nForth line\nFifth line\nSixth Line`, 
we end up with this result :

![N3](https://github.com/user-attachments/assets/9b664935-ab83-4036-a823-fa519cc881ca)

<BR>

### 🔸  Bubble's tail placement
The placement of the tail (the bubble's pointer) is set by those 2 functions and their applicable options :
- `AlignH: ` = **H**orizontal **Align**ment (Options = `Left`, `Center`, `Right`)
- `AlignV: ` = **V**ertical **Align**ment (Options = `Top`, `Center`, `Bottom`)

As a result we have 9 (3x3) possible placement of the tail : 

![Bubble_Tails_POS](https://github.com/user-attachments/assets/ceb72d3d-a527-4f8d-b5bb-bc33d217209f)

We note that having both `AlignH` & `AlignV` set to `Center` results in hiding the tail.

The coded outline of the bubble is not dependent of the animation background and will remain black even on top of a black background, and as consequence will not be visible :

![Bubble_Tails_BEG](https://github.com/user-attachments/assets/c047120c-c801-4eef-8da1-9a681ad7b364)

It then renders slightly more squared as the rounded-angles of the outline are not visible.
