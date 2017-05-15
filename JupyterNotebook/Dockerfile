FROM ubuntu:trusty-20170330

MAINTAINER fengyao <yaoelvon@gmail.com>

RUN apt-get install python-pip

RUN pip install -U ipywidgets "ipython[notebook]"
RUN jupyter nbextension enable --py widgetsnbextension

CMD ['jupyter', 'notebook', '--port 8980', '--no-browser', '--ip="*"']
