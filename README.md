## 说明
jupyterlab + js 环境

```shell
FROM ubuntu:22.10

USER root

RUN cat /etc/apt/sources.list

RUN mkdir /opt/notebooks \
&& sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list \
&& apt update -y \
&& apt install -y nodejs npm vim curl wget python3 python3-pip -y \
&& alias python=python3

RUN pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ "jupyterlab==3.5.2" \
&& pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ pandas \
&& pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ numpy \
&& pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ matplotlib \
&& pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ tqdm \
&& pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ scikit-learn \
&& jupyter lab --generate-config \
&& chmod -R 777 /root/.jupyter/jupyter_lab_config.py \
&& chmod -R 777 /opt/notebooks

# RUN pip install "jupyterlab-kite>=2.0.2" \
RUN pip install jupyterlab_code_formatter \
&& pip install ipympl

RUN npm i ijavascript -g

RUN node /usr/local/lib/node_modules/ijavascript/bin/ijavascript.js

# RUN pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ jupyterlab-language-pack-zh-CN

VOLUME /opt/notebooks

EXPOSE 8888


CMD jupyter lab --notebook-dir=/opt/notebooks --ip='*' --port=8888 --allow-root --no-browser

```