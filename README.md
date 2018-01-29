# Conda S2I Images

This is a series of Linux Container Images that revolve around [Anaconda](https://www.anaconda.com/what-is-anaconda/) to provide Jupyter notebook functionality, although the approach is probably more generally applicable. Anaconda is composed of the package manager [conda](https://conda.io/docs/) which primarily pulls from the [anaconda distribution](https://www.anaconda.com/distribution/). Anaconda is unique in that the distribution spans more than one language, which is important in the poly-glot nature of data science (i.e. various parts of the same organizations may work in R/Python/Scala/Julia). 

The approach uses [OpenShift's S2I](https://docs.openshift.com/container-platform/3.7/architecture/core_concepts/builds_and_image_streams.html#source-build) to build a base image with [Miniconda](https://conda.io/miniconda.html), as well as S2I assemble scripts that will allow extending images to install arbitrary conda packages. As examples, there is a minimal Juptyer notebook and a kitchen sink Jupyter notebook, both created using the S2I base image.

It borrows heavily from [jupyter-on-openshift](https://github.com/jupyter-on-openshift) and [radanalytics](https://github.com/radanalyticsio/base-notebook).

## Usage

The env var `JUPYTER_NOTEBOOK_PASSWORD` is functional like on the other images if you want it.

1. `$ oc new-app https://github.com/sherl0cks/anaconda-s2i --context-dir conda-jupyter-base --name conda-jupyter-base`
2. `$ oc expose conda-jupyter-base`
3. `$ oc new-app conda-jupyter-base~https://github.com/sherl0cks/anaconda-s2i --context-dir jupyter-kitchen-sink --name jupyter-kitchen-sink`