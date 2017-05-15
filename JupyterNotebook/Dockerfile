FROM jupyter/base-notebook

MAINTAINER fengyao <yaoelvon@gmail.com>

USER root

# Python dependencies
RUN apt-get -y update && \
  apt-get install -y python-qt4 && \
  apt-get clean

# Python 2
USER jovyan

# Install Python 2 packages
RUN conda install --yes \
    'python=2.7*' \
    'ipython=4.0*' \
    'ipywidgets=4.0*' \
    'pandas=0.16*' \
    'matplotlib=1.4*' \
    'scipy=0.15*' \
    'seaborn=0.6*' \
    'scikit-learn=0.16*' \
    'scikit-image=0.11*' \
    'sympy=0.7*' \
    'cython=0.22*' \
    'patsy=0.3*' \
    'statsmodels=0.6*' \
    'cloudpickle=0.1*' \
    'dill=0.2*' \
    'numba=0.20*' \
    'bokeh=0.9*' \
    'gensim=0.12*' \
    pyzmq \
    && conda clean -yt

USER root
