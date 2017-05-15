FROM ubuntu:trusty-20170330

MAINTAINER fengyao <yaoelvon@gmail.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends python-pip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install -U ipywidgets "ipython[notebook]"
RUN jupyter nbextension enable --py widgetsnbextension

CMD ['jupyter', 'notebook', '--port 8980', '--no-browser', '--ip="*"']
