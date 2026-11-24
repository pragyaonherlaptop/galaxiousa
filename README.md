── ⋆⋅𖤓⋅⋆ ──
# galaxiousa
 
a random html-css practice project 

:every picture on every slide (the galaxy, the moon, the mountains, the spiral) is drawn with CSS shapes and gradients.




---


## Features

- 5 slides, all drawn with pure CSS
- Slow 1 second fade between slides
- Left and right arrow buttons on every slide
- Clickable dots at the bottom showing which slide you are on
- Twinkling stars on every slide
- Animated shooting stars
- A slowly spinning spiral galaxy (one full turn every 2 minutes)
- A "You are here" marker showing where our Sun is
- Works on phones (layout changes under 600px wide)
- Zero dependencies, nothing to install, nothing to build

---

## The slides

| # | Title | What you see |
|---|-------|--------------|
| 1 | **The Milky Way** | A glowing galaxy band tilted across a dark blue sky, a dark dust lane through the middle, a brighter core patch, two dark hills and a small glowing orange tent |
| 2 | **The Galactic Core** | A big blurred glow going from white-yellow in the middle through orange and purple to dark blue, with three dark dust lanes across it |
| 3 | **The Moon** | A false-colour Moon with blue, red, orange and yellow patches, small craters, a big bright crater with white rays, and two small bright spots |
| 4 | **Shooting Stars** | Two shooting stars that streak across a night sky above a mountain range |
| 5 | **The Spiral** | The Milky Way seen from above: two spiral arms going from yellow to blue, a bright centre with a bar, and a yellow dot marking our Sun |

The Moon on slide 3 is shown in false colour. The colours are not what your eyes would see. In real false-colour Moon photos, the colours show different minerals on the surface (blue areas have more titanium, orange and red areas have less).

---

## How to run it

**Option 1 - open the file**

1. Download or clone this repo
2. Double-click `index.html`

It opens in your browser. That's it.

**Option 2 - clone with git**

```bash
git clone https://github.com/<pragyaonherlaptop>/galaxiousa.git
cd galaxiousa
```

Then open `index.html` in your browser.

`index.html` and `style.css` must stay in the same folder, because the page loads the CSS with a relative link.

---

## Controls

| Action | What it does |
|--------|--------------|
| Click the **right arrow** | Go to the next slide |
| Click the **left arrow** | Go to the previous slide |
| Click a **dot** at the bottom | Jump straight to that slide |

Slides loop. The right arrow on slide 5 goes back to slide 1, and the left arrow on slide 1 goes to slide 5.

There is no autoplay and no keyboard shortcut, because both would need JavaScript.

---

## Project files

```
galaxiousa/
├── index.html          # the 5 slides (HTML structure)
├── style.css           # all the drawing, colours and animations
├── screenshots/        # pictures used in this README
│   ├── 01-milky-way.png
│   ├── 02-galactic-core.png
│   ├── 03-moon.png
│   ├── 04-shooting-stars.png
│   ├── 05-spiral.png
│   └── 06-phone-view.png
├── README.md           # this file
├── LICENSE             # MIT license
└── .gitignore          # files git should ignore
```

---

## How it works

### The slideshow trick (no JavaScript)

The slideshow uses hidden **radio buttons** and the CSS `:checked` selector.

1. At the top of the page there are 5 radio buttons (`#s1` to `#s5`). They are hidden with `display: none`.
2. Every arrow and every dot is a `<label for="s3">` style element. Clicking a label ticks the radio button it points to.
3. Every slide starts invisible (`opacity: 0; visibility: hidden`).
4. This rule shows the slide that matches the ticked radio button:

```css
#s1:checked ~ .slideshow .slide1,
#s2:checked ~ .slideshow .slide2 {
  opacity: 1;
  visibility: visible;
}
```

5. `transition: opacity 1s, visibility 1s` makes the change a smooth fade.
6. The dots work the same way. The dot for the open slide is filled in white.

### Stars on every slide

`.slide::before` draws 6 layers of tiny `radial-gradient` dots. Each layer repeats at a different size (`background-size`), so the dots don't line up in a visible grid. The `twinkle` animation fades them between 100% and 55% opacity every 4 seconds.

### The text

Each slide has a `.caption` with a title (`h2`) and one line of text (`p`). A double `text-shadow` keeps the text readable on top of bright parts like the galaxy band.

---

## How each picture is drawn

### Slide 1 - The Milky Way
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/1476e4c0-1f36-4c36-ab94-d332fd331fba" />

- `.slide1` has a vertical `linear-gradient` from near-black to dark blue to a purple-blue at the bottom
- `.band` is a wide, short `<div>` rotated -18 degrees. Its background is a `radial-gradient` ellipse that goes cream, then lilac, then blue, then transparent. `filter: blur(14px)` softens it
- `.dust` is a dark, blurred, rotated ellipse on top of the band. It makes the dark dust lane
- `.core1` is a small bright yellow blurred ellipse for the brighter galactic core
- `.hill1` and `.hill2` are `<div>`s with `border-radius: 50% 50% 0 0`, which turns a rectangle into a hill shape
- `.tent` is the classic CSS triangle trick (zero width and height, with thick transparent side borders and a coloured bottom border), plus `drop-shadow` for the glow

### Slide 2 - The Galactic Core
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/f18ee160-cf21-46ec-b504-c9bb02493c9c" />



- `.glow` is one big circle (`85vmin` wide) with a 6-stop `radial-gradient` and a blur
- `.lane1`, `.lane2`, `.lane3` are dark blurred ellipses, each rotated differently, to look like dust clouds blocking the light
- Sizes use `vmin` so the glow stays round and fits on any screen shape

### Slide 3 - The Moon
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/1d64f59e-3b20-45dc-9972-dfcf856a98ef" />


- `.moon` is a 590px circle (`border-radius: 50%`) with a grey-lavender background and an inner `box-shadow` that darkens the edge so it looks like a ball
- `overflow: hidden` keeps all the colour patches inside the circle
- 13 `.blob` elements are blurred ovals in blue, purple, red, pink, orange and yellow. The `blur(22px)` makes them mix into each other like a real false-colour photo
- 10 `.crater` elements are small circles with a faint white fill and an inner shadow
- `.bigcrater` is a white circle with a large white glow (like the crater Tycho)
- 12 `.ray` elements are thin white lines that fade out. Each one starts at the big crater and is rotated to a different angle with `transform-origin: left center`
- `.spot1` and `.spot2` are two smaller bright spots
- `.moonwrap` scales the whole 590px Moon down to 62% so it fits in the slide (50% on phones)

### Slide 4 - Shooting Stars
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/56f11eed-acf9-4c0c-97f5-ab3ea6f8546c" />


- `.shoot` is a thin 160 x 2px line with a gradient from transparent to white
- The `shoot` animation rotates it 25 degrees and slides it 650px across. It fades in at 4%, then fades out by 25%, then waits for the rest of the 5 second loop
- `.shoot2` uses `animation-delay: 2.5s`, so the two stars take turns
- `.mountains` is a full-width `<div>` cut into a mountain outline with `clip-path: polygon(...)`

### Slide 5 - The Spiral
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/15832ba1-f39a-4979-ae5d-9ead87e82765" />


- `.galaxy` is a square box in the middle of the slide (`62vmin`)
- Each spiral arm is a row of 60 small glowing dots (`.star`). The number `--i` (0 to 59) is set in the HTML with `style="--i:12"`
- CSS uses `--i` to work out each dot's size, colour, angle and distance from the centre. A bigger `--i` means the dot is turned a bit more (4.8 degrees per step) and sits further out (0.46vmin per step), so the dots curve outwards in a spiral
- The dots get slightly bigger and more transparent further out, and the colour goes from yellow to blue using `color-mix()`
- `.armB` is a copy of `.armA` turned 180 degrees, which gives the two arms
- `.arms` spins with the `spin` animation: one full turn every 120 seconds
- `.bar` is a rotated blurred yellow ellipse for the bar in the middle of the galaxy
- `.centre` is the bright core
- `.you` is the yellow dot for our Sun. It sits outside `.arms`, so it does not spin and the label stays readable


---

## Browser support

Works in current versions of Chrome, Edge, Safari and Firefox.

The spiral colours use `color-mix()`, which needs:

- Chrome / Edge 111 or newer
- Safari 16.2 or newer
- Firefox 113 or newer

On an older browser the spiral dots would have no colour. Everything else uses older CSS features.

---


---

## License

MIT. See the [LICENSE](LICENSE) file.
