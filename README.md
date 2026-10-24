<!--    
    ================================================================================================
    README.md
    ================================================================================================
-->

# Libertinus Conda Recipes

*Conda recipes for the Libertinus font family, plus the pixi configurations to build and install them straight from git.*

<!--    
    ================================================================================================
-->

## Project Structure

```
conda-recipe-libertinus/
├── otf/                    # Conda recipe for the static OpenType fonts of the
│   │                       # Libertinus family. Installs the `.otf` files into
│   │                       # `share/fonts/otf/` of the target environment.
│   │
│   ├── pixi.toml           # Pixi package manifest declaring the
│   │                       # `pixi-build-rattler-build` backend, so pixi can
│   │                       # build this recipe from a git dependency.
│   │
│   └── recipe.yaml         # Recipe in the v1 format: upstream release
│                           # source with checksum, install script, and
│                           # package metadata.
│
├── ttf/                    # Conda recipe for the static TrueType fonts.
│   │                       # Mirrors `otf/` and installs the `.ttf` files into
│   │                       # `share/fonts/ttf/`.
│   │
│   ├── pixi.toml
│   └── recipe.yaml
│
└── woff2/                  # Conda recipe for the static WOFF2 web fonts.
    │                       # Mirrors `otf/` and installs the `.woff2` files into
    │                       # `share/fonts/woff2/`.
    │
    ├── pixi.toml
    └── recipe.yaml
```

## Installation

### I. Prerequisites

| Component            | Requirement                                                                     |
| :------------------- | :------------------------------------------------------------------------------ |
| **Package Manager**  | [`Pixi`](https://pixi.prefix.dev/latest/) with `pixi-build` support             |
| **Operating System** | Unix-like system [^1]                                                           |
| **Architecture**     | Any                                                                             |
| **Network**          | Internet access to fetch the font archive from the official upstream repository |

[^1]: The build scripts use POSIX shell, so Windows is not supported.

<!--    
    ================================================================================================
-->

### II. Enable `pixi-build`

Add the `pixi-build` preview feature to the `[workspace]` section of your `pixi.toml`:

```toml
[workspace]
preview = ["pixi-build"]
```

> **Note:**  
> As of Pixi 0.81.0, `pixi-build` is still a preview feature, so it has to be enabled explicitly. Once it is stabilized, this step may become unnecessary and the syntax may change.

<!--    
    ================================================================================================
-->

### III. Installation

Add the font format you need. Pixi will fetch the recipe from this repository, build the package, and install it into your environment:

```bash
# OpenType
pixi add \
    --git https://github.com/snegoviol/libertinus-conda-recipes \
    --rev 0f3101bdf9b3eb4dfc6c2418990922d6488bef51 \
    --subdirectory otf \
    libertinus-otf

# TrueType
pixi add \
    --git https://github.com/snegoviol/libertinus-conda-recipes \
    --rev 0f3101bdf9b3eb4dfc6c2418990922d6488bef51 \
    --subdirectory ttf \
    libertinus-ttf

# WOFF2
pixi add \
    --git https://github.com/snegoviol/libertinus-conda-recipes \
    --rev 0f3101bdf9b3eb4dfc6c2418990922d6488bef51 \
    --subdirectory woff2 \
    libertinus-woff2
```

The fonts are installed into `$CONDA_PREFIX/share/fonts/<format>/` of the environment.

<!--    
    ================================================================================================
-->

## License

Each file in this repository is licensed under the [MIT No Attribution License](LICENSE.txt).

<!--    
    ================================================================================================
-->
