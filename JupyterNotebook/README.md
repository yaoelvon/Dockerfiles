> * Jupyter Notebook 5.0.x
> * 支持python3.x和python2.7


## 一键启动尝鲜
```
docker run -it --rm -p 8888:8888 fengyao/jupyter-notebook
```

## 好的启动方式
```
docker run -d -p 8980:8888 \
    --name='jupyter-notebook' \
    -v /root/jupyter-notebook/ssl:/etc/ssl/notebook \
    fengyao/jupyter-notebook:v17.05.15 start-notebook.sh \
    --NotebookApp.password='sha1:149e2303fd48:3591ba2fd67734e116caa2991abb688fc61c008d' \
    --NotebookApp.base_url=/jn
```