THE MOST COMMON MISTAKES DONE WHEN MAKING AN ANIMATION

1. PNG FILES :
- forgetting the first frame should be named frame_0.png
- missing a number while saving frames as : frame_0.png, frame_1.png, frame_2.png frame_3.png, [missing frame], frame_5.png...
- wrong naming first frames by adding a "0" like frame_01.png 
- having your OS not showing file extensions so you end up with files like frame_1.png.png or meta.txt.txt
- having PNG with a non-valid pixel size
- having frames saved under another file format than PNG (ie JPG, etc...)

2. META.TXT :
- Set incorrect pixel frame size (Width & Height values different from your png ones)
- bad counting frames by forgetting the "0" one
- forgetting to put a positive number in active cycles when you have active frames (or putting a positive number there when you have NO active frames)
- Bad frames counting : Remember that the total inputs of frame order should equal active + passive frames numbers
- Forgetting to set the correct number of Bubble slots
- Forgetting to set first bubble slot as 0 (1 would be the second one... cf frames counting)
- Bad counting of bubble slots :<BR>
  » Random bubbles set on same bubble slot count for 1 in Bubble slots<BR>
  » Having 2 bubbles on slot 0 and 3 on slot 1 would only count for 2 in "bubble slots"

3. MANIFEST.TXT :
- forgetting to add an entry for your animation...
- typo in your animation name
- setting out-of-range levels or butthurt
- setting weight = 0

4. COPYING ON FLIPPER :
- copying on SD/dolphin/ the folder containing PNG files instead of BM files's one...
- forgetting to update your SD/dolphin/manifest.txt
