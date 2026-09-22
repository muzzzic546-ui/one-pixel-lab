# Safe-or-Bold

Safe-or-Bold classifies a top/bottom outfit pairing as "Safe" or "Bold" based on how far apart their brightness values are.

## How to open and use

1. Open `Safe-or-Bold.html` in any browser. No internet connection, API keys, or installation needed.
2. Move the two sliders: **top brightness** and **bottom brightness**, both from 0 (black) to 255 (white).
3. Watch the prediction update live as you drag.

You can also click the example buttons to load preset pairings, or scroll down to "What the model can't see" to compare real outfit colors with what the model sees.

## How it predicts

The page calculates the gap between the two brightness numbers. If the gap is greater than 100, it predicts "Bold." Otherwise, it predicts "Safe." A gap of exactly 100 counts as Safe.

The page shows the calculated gap and the threshold so the prediction isn't just a label with no evidence. For example, with a top of 200 and a bottom of 40 it shows `gap = |200 − 40| = 160 · 160 > 100`, plus a bar that fills up to the gap with a line marking the threshold.

| Top | Bottom | Gap | Prediction |
|----:|-------:|----:|------------|
| 200 | 40 | 160 | Bold |
| 180 | 160 | 20 | Safe |
| 90 | 95 | 5 | Safe |
| 250 | 10 | 240 | Bold |

## Limitation discovered

The model only measures brightness, not color. It sees every outfit in shades of gray, so it can't tell navy from maroon or red from green. Because of that, it gets real outfits wrong in both directions:

- **Clashing colors can come out "Safe."** A navy top (brightness 44) with maroon pants (55) has a gap of only 11, so the model calls it Safe, even though many people think those colors clash. Red with green (94 and 101) also comes out Safe.
- **Classic combinations can come out "Bold."** A white shirt (247) with black jeans (26) has a gap of 221, so the model calls it Bold, even though it's one of the most classic outfits there is. Cream with chocolate brown (231 and 51) is also called Bold.

The threshold of 100 is also a rule I picked by hand from a few examples. The model didn't learn it from data. To judge real clashes, the classifier would need more information than brightness, such as the hue of each color.

## Development log

- **Set up the project.** Started a Git repository with the starter files and made the first commit, "Add starter One Pixel lab." Pushed it to a private GitHub repository, then made the repository public.
- **First ask.** I asked Claude Code for a page with two sliders (top brightness and bottom brightness) and a Safe/Bold label based on the gap between them. I also asked for the numerical gap and the 100-point threshold to be shown as evidence, not just the final label.
- **What the first version included.** Besides the sliders and label, it had a gray outfit that changes as you drag, the gap math and a gap bar with the threshold marked, buttons for my four examples, two edge-case buttons (a gap of exactly 100 vs. 101), and a "What the model can't see" section comparing real colors with the gray view the model gets.
- **Reorganized files.** I moved the classifier into its own file, `Safe-or-Bold.html`. `one-pixel.html` now holds a separate One Pixel ML Lab page.
- **Organized this README** into sections: purpose, how to use it, how it predicts, the limitation, and this log.
