# Artificial Metabolic Networks: AMN-Reservoir Re-implementation

This repository provides a re-implementation of the AMN-Reservoir architecture described by [Faure et al. (2023)](https://www.nature.com/articles/s41467-023-40380-0).

This hybrid framework is designed to bridge the gap between experimental media compositions and metabolic flux predictions. This addresses the "unknown uptake flux" problem in Constraint-Based Modeling (CBM).

### The AMN-Reservoir

The AMN-Reservoir solves this by embedding a metabolic model within a machine learning architecture. It uses a two-step learning process to map realistic uptake fluxes to its experimental media.

There are 2 main components to this framework: 

1. **The Frozen Reservoir (Mechanistic Layer)**:
First, an Artificial Metabolic Network (AMN) is pre-trained on a large dataset of FBA/pFBA simulations. This model learns the stoichiometric constraints of the metabolic network. Once trained, its parameters are frozen. This frozen model acts as a differentiable "Reservoir" that mimics the behavior of an FBA solver but allows for gradient backpropagation.
2. **The Trainable Pre-processing Layer (Neural Layer)**:
A trainable neural network layer is attached prior to the Reservoir. This layer takes experimental media composition ($C_{med}$) as input and predicts uptake flux bounds ($V_{in}$). The architecture is trained on measured growth rates. The error between the predicted and measured growth is backpropagated through the frozen Reservoir, to update the pre-processing layer. This forces the neural layer to learn the complex, non-linear relationship between the presence of nutrients and their specific uptake rates.


## Environment set-up 

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