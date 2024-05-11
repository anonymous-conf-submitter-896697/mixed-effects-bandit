# Mixed-Effects Bandit Algorithm

The code in this repository can be used to reproduce the simulation results in the paper "A Robust Mixed-Effects Bandit Algorithm for Assessing Mobile Health Interventions."

# Docker Usage

The purpose of including a Docker image in this repo is to make the simulations fully reproducible across different computer architectures and operating systems.
To use the image, you will first need to download Docker Desktop from [here](https://docs.docker.com/desktop/).
Then you can build the image as follows:

`docker build -t me-bandit --no-cache -f docker/Dockerfile .`

Reproducing the results in the paper (with no modifications to the code) requires a server with about 200Gb RAM and 25+ CPU cores.
We produced them on a single compute node with two 3.0 GHz Intel Xeon Gold 6154 processors and 180 GB of RAM.
To reproduce the results shown in the paper, run the following command:

```
docker run \
      -v $(pwd):/home/jovyan \
      --platform linux/amd64 \
      me-bandit
```

The platform flag is recommended if you are running on an M1 Mac; otherwise omit it.
If you are running in a scientific computing environment that does not support Docker, then you could convert your Docker image to a .sif file and run it via Singularity.

If you would like to modify the simulation interactively, comment out the entry point in the Dockerfile.
Then rebuild the Docker container and run the following code:

```
docker run \
      -p 8888:8888 \
      -v $(pwd):/home/jovyan \
      --platform linux/amd64 \
      me-bandit
```

Then navigate to the localhost URL to develop in Jupyter Lab.
Because the repo is attached as a Docker volume, any changes you make will be synced between the host and container.

# License

Most of the code contained in this repository is licensed under the GPL-3 (see LICENSE.md for full text).
The reason for this is that we use the CHOLMOD module from SuiteSparse which has a copy-left GPL-3 license.
The only files with a different license are bagging_mod.py and ensemble_mod.py, which are modified from the RiverML library.
That file is licensed under the BSD 3-clause license, which is included in both files.