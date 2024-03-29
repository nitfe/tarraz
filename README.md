# Tarraz | طرّاز
A cross-stitch image generator.
Generates a cross stitch pattern from an image of your choice. The generated pattern is DMC colored.

Takes an image file and generates a cross stitch pattern using a user specified color..

## Supported image extensions
1. JPEG (.jpg, .jpeg)
2. PNG (.png)
3. WebP (.webp)

## Current color providers
1. DMC

## Results

<img src="https://github.com/nitfe/tarraz/raw/v1.2.0/images/palestine.png" alt="Palestinian Flag" style="display: inline-block; margin: 0 auto; max-width: 600px"/>

<img src="https://github.com/nitfe/tarraz/raw/v1.2.0/images/results/colored_symbols.jpg" alt="Colored with Symbols" style="display: inline-block; margin: 0 auto; max-width: 300px"/>
<img src="https://github.com/nitfe/tarraz/raw/v1.2.0/images/results/black_white_symbols.jpg" alt="Black White with Symbols" style="display: inline-block; margin: 0 auto; max-width: 300px"/>
<img src="https://github.com/nitfe/tarraz/raw/v1.2.0/images/results/colored.jpg" alt="Colored" style="display: inline-block; margin: 0 auto; max-width: 300px"/>
<img src="https://github.com/nitfe/tarraz/raw/v1.2.0/images/results/key.jpg" alt="Keys" style="display: inline-block; margin: 0 auto; max-width: 300px; height: 256px"/>


## Usage
### Installation
```
pip install tarraz
```

### CLI Example
```shell
tarraz images/palestine.png --colors 4 --stitches-count 200
```

### Python Example

```python
from tarraz import constants
from tarraz.processor import Tarraz
from tarraz.providers import DMCProvider
from tarraz.stitcher import SVGStitcher
from tarraz.models import RGB


# Choose a color provider
image_path = "images/palestine.png"
provider = DMCProvider()

tarraz = Tarraz(
    image_path,
    provider=provider,  # Optional if not using a custom provider
    x_count=100,        # Default 50
    colors_num=6,       # default 3
    result_width=200,   # Default 1000
    cleanup=True,       # Default True
)

# Process the image
pattern, colors = tarraz.process()

# Stitch the result
SVGStitcher.stitch(
    pattern,
    colors,
    tarraz.size,
    transparent=[RGB(255,255,255)],
    configs=constants.SVG_VARIANTS,
    cell_size=10,
    save_to="/tmp/test/",
)

```

### Options
```shell
$ tarraz --help
```

```
usage: tarraz [-h] [--version] [-c COLORS] [-n STITCHES_COUNT] [-w WIDTH] [-m DMC] [-t TRANSPARENT [TRANSPARENT ...]] [-o DIST] [-z CELL_SIZE] [--no-cleanup] [--svg] [-v] image

Generate a DMC-colored cross-stitch pattern from a given image.

positional arguments:
  image                 Input image

optional arguments:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  -c COLORS, --colors COLORS
                        Number of colors to use in the pattern.
  -n STITCHES_COUNT, --stitches-count STITCHES_COUNT
                        Number of stitches to use in the x axis.
  -w WIDTH, --width WIDTH
                        Result pattern width.
  -m DMC, --dmc DMC     DMC json color path.
  -t TRANSPARENT [TRANSPARENT ...], --transparent TRANSPARENT [TRANSPARENT ...]
                        A Color to ignore from the end result.
  -o DIST, --dist DIST  Output destination directory.
  -z CELL_SIZE, --cell-size CELL_SIZE
                        The size of the generated Aida fabric cell.
  --no-cleanup          Don't run cleanup job on generated image.
  --svg                 Export result to svg files.
  -v, --verbose         Show debug messages.
```

## Development
## Pre-requisites
```shell
pip3 install -U pip setuptools
pip3 install poetry


# Optional Auto-completion
poetry completions zsh > ~/.zfunc/_poetry
```
### Install dependencies
```shell
poetry shell
poetry install
pre-commit install
```

### Usage
Continue usage as listed above
