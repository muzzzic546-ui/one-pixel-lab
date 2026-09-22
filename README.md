# One Pixel Lab: Safe or Bold?

A tiny classifier that labels an outfit (a top worn with a bottom) as a "Safe pairing" or a "Bold pairing" using only the brightness of each piece (0 = black, 255 = white). If the gap between the two brightness values is greater than 100, it's Bold; otherwise it's Safe.

Open `Safe-or-Bold.html` in a web browser to try it.

## The first ask

I asked for a first version with two sliders (top brightness and bottom brightness) and a Safe/Bold label based on the gap between them. I also asked for the numerical gap and the 100-point threshold to be shown on the page as evidence, not just the final label.

