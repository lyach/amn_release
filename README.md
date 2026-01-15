# Welcome to the Artificial Metabolic Networks repository

This repository is entirely written in **python**. We make use of **jupyter** notebooks,
calling custom functions libraries storing the main objects and functions used in the project. We detail here two ways of using the repo, either on **Colab** or **locally**.

One can clone the git directly in a Google Drive and open the notebooks in Google Colab. This is a good way to make first testings and have a glimpse of the project.

Also, one can clone the git locally and install a **conda** environment we provide, to be used for the project once it's linked to your jupyter environment. This will provide better reproducibility than the colab install. We recommend this option for computationally costly usage of the repository.

A **tutorial** is available as the notebook `Tutorial.ipynb`. This is a good place to start, going through all the detailed steps for building and training an AMN model. This step-by-step exploration of the project will take about 20 minutes to be runned.

Note: For local installs, only Linux (Ubuntu 22.04) and MacOS (Monterey) have been tested, but Windows should work.

## Installation 

### Using `uv`

The following steps will set up a reproducible Python environment using `uv`. This approach avoids dependency conflicts and works seamlessly on HPC clusters.

**1. Install uv**

This will install a single static binary in your `$HOME/bin`:
```
curl -LsSf https://astral.sh/uv/install.sh | sh
```
**2. Navigate to the repository**
```
cd ~/amn-release
```

**3. Create a virtual environment**

Creates an isolated environment inside the repository:
```
uv venv .venv --python 3.9
```

**4. Activate venv**
```
source .venv/bin/activate
```

**5. Install dependencies**
Synchronize and install all dependencies listed in `pyproject.toml`:
```
uv sync
```
   This automatically resolves and locks dependencies for reproducibility (`uv.lock` file).

**6. Updating the environment**

Whenever you modify dependencies (add or update a package), run:
```
uv sync --upgrade
```

To install a single new package:
```
uv add <package-name>
```

To remove a single new package:
```
uv remove <package-name>
``` 