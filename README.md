# lpyout

[![PyPI](https://img.shields.io/pypi/v/lpyout)](https://pypi.org/project/lpyout/)
[![Docs](https://img.shields.io/readthedocs/lpyout)](https://lpyout.readthedocs.io/en/latest/)
[![License](https://img.shields.io/github/license/Modular-Game-Components/lpyout)](LICENSE)

`lpyout` handles grid layout math for you — so you can define a menu, tilemap, or inventory screen in terms of **rows and columns**, and let `lpyout` work out the actual pixel coordinates.

## Why

Building a menu or HUD usually starts the same way: subdivide the screen into a grid, then hand-compute the `(x, y)` position of every button, panel, and icon relative to the screen size. It's tedious, and it gets worse the moment you want margins, padding, spacing, or a grid nested inside another grid.

`lpyout` lets you think in **indices** (`row 1, column 2`) instead of coordinates, and converts between the two for you — including for grids of variable-size cells and grids-within-grids.

## Install

```bash
pip install lpyout

# with Pygame (CE) rendering helpers
pip install "lpyout[pygame]"
```

Requires Python 3.11+.

## Quickstart (Pygame)

```python
import pygame
from lpyout import Grid
from lpyout.pygame import screen_wrapper
from lpyout.pygame.render import fast_render

pygame.init()
screen = pygame.display.set_mode((1280, 720))
clock = pygame.time.Clock()
running = True

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    screen.fill("black")

    screen_wrapper.update()
    grid = Grid.fill_screen(screen_wrapper, 5, 5, m=30, s=10)  # 5x5 grid, margin, spacing
    fast_render(grid, screen)

    pygame.display.flip()
    clock.tick(60)

pygame.quit()
```

That's a fully working 5×5 grid with margins and spacing, no manual coordinate math. `lpyout` isn't tied to Pygame — the core `Grid`/`Cell` model is renderer-agnostic; the `lpyout.pygame` module is just the built-in convenience layer.

## Core ideas

- **Indices, not coordinates.** Ask for "the cell at `(1, 1)`" and get back real screen coordinates — you don't track `x`/`y`/`w`/`h` by hand.
- **Grids are trees.** A `Grid`'s children can be `Cell` leaves or other `Grid` objects, so nested/composite layouts fall out naturally.
- **CSS-flavored controls.** `margin`, `padding`, and `spacing` behave like their CSS counterparts, and class-method constructors (`fill_screen`, and friends) cover common layouts without boilerplate.

See the [Guiding Principles](https://lpyout.readthedocs.io/en/latest/overview.html) page for the full model.

## Learn more

- 📖 [Full documentation](https://lpyout.readthedocs.io/en/latest/) — guides, API reference, and a [chessboard custom-drawing example](https://lpyout.readthedocs.io/en/latest/draw.html)
- 🐛 [Issues](https://github.com/Modular-Game-Components/lpyout/issues) — bug reports and feature requests welcome
- 🔧 [Pull requests](https://github.com/Modular-Game-Components/lpyout/pulls) — contributions welcome

## Status

`lpyout` is a work in progress. The core API (`Grid`, `Cell`, margins/padding/spacing) is usable today; expect the surface area to grow.

## Contributing

Feel free to [file an issue](https://github.com/Modular-Game-Components/lpyout/issues), [open a pull request](https://github.com/Modular-Game-Components/lpyout/pulls), or, if you find the project useful, [donate](https://www.paypal.com/donate/?business=9ZQ9S6RJBVATY&no_recurring=0&currency_code=USD) (no pressure).

## License

Apache-2.0 — see [LICENSE](LICENSE).
