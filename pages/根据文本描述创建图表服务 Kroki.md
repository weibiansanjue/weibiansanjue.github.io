tags:: [[tagAsciiDoc]]

- 官网：[Kroki!](https://kroki.io/)
- GitHub：[yuzutech/kroki: Creates diagrams from textual descriptions! (github.com)](https://github.com/yuzutech/kroki)
- 环境搭建：
	- Docker：[yuzutech/kroki - Docker Image | Docker Hub](https://hub.docker.com/r/yuzutech/kroki)
	- docker-compose.yml
		- ```yaml
		  version: "3"
		  services:
		    core:
		      image: yuzutech/kroki
		      environment:
		        - KROKI_BLOCKDIAG_HOST=blockdiag
		        - KROKI_MERMAID_HOST=mermaid
		        - KROKI_BPMN_HOST=bpmn
		        - KROKI_EXCALIDRAW_HOST=excalidraw
		        - KROKI_WIREVIZ_HOST=wireviz
		      ports:
		        # 主服务端口号
		        - "8000:8000"
		    blockdiag:
		      image: yuzutech/kroki-blockdiag
		      expose:
		        - "8001"
		    mermaid:
		      image: yuzutech/kroki-mermaid
		      expose:
		        - "8002"
		    bpmn:
		      image: yuzutech/kroki-bpmn
		      expose:
		        - "8003"
		    excalidraw:
		      image: yuzutech/kroki-excalidraw
		      expose:
		        - "8004"
		    # experimental!
		    diagramsnet:
		      image: yuzutech/kroki-diagramsnet
		      expose:
		        - "8005"
		    wireviz:
		      image: yuzutech/kroki-wireviz
		      ports:
		        - "8006:8006"
		  6"
		  ```
	- 效果
		- ```bash
		  [root@demo ~]# docker ps | grep 'yuzutech'
		  b20e820ab5ed   yuzutech/kroki                                   "/bin/sh -c 'exec ja…"   25 hours ago   Up 25 hours   0.0.0.0:9500->8000/tcp, :::9500->8000/tcp   kroki_kroki_1
		  e5afad6ffac0   yuzutech/kroki-bpmn                              "/usr/bin/bpmn"          25 hours ago   Up 25 hours   8003/tcp                                    kroki_bpmn_1
		  ee86c12a3cad   yuzutech/kroki-blockdiag                         "gunicorn --preload …"   25 hours ago   Up 25 hours   8001/tcp                                    kroki_blockdiag_1
		  75b6abb88d0f   yuzutech/kroki-mermaid                           "node src/index.js"      25 hours ago   Up 25 hours   8002/tcp                                    kroki_mermaid_1
		  8a3909721dd2   yuzutech/kroki-excalidraw                        "/usr/bin/excalidraw"    25 hours ago   Up 25 hours   8004/tcp                                    kroki_excalidraw_1
		  ```