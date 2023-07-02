tags:: [[tagAsciiDoc]]

- 官网：[Kroki!](https://kroki.io/)
- GitHub：[yuzutech/kroki: Creates diagrams from textual descriptions! (github.com)](https://github.com/yuzutech/kroki)
- 环境搭建：
	- Docker：[yuzutech/kroki - Docker Image | Docker Hub](https://hub.docker.com/r/yuzutech/kroki)
- 实战
	- ```yaml
	  # 仿照官方 docker-compose.yml 中步骤，自定义一个 docker-compose.yml
	  version: "3"
	  services:
	    kroki:
	      image: yuzutech/kroki
	      depends_on:
	        - blockdiag
	        - mermaid
	        - bpmn
	        - excalidraw
	      environment:
	        - KROKI_BLOCKDIAG_HOST=blockdiag
	        - KROKI_MERMAID_HOST=mermaid
	        - KROKI_BPMN_HOST=bpmn
	        - KROKI_EXCALIDRAW_HOST=excalidraw
	      ports:
	        - "9500:8000"
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
	  ```
	- ```bash
	  [root@demo ~]# ls
	  docker-compose.yml
	  [root@demo ~]# docker-compose up -d
	  [root@demo ~]# docker ps | grep 'yuzutech'
	  b20e820ab5ed   yuzutech/kroki                                   "/bin/sh -c 'exec ja…"   25 hours ago   Up 25 hours   0.0.0.0:9500->8000/tcp, :::9500->8000/tcp   kroki_kroki_1
	  e5afad6ffac0   yuzutech/kroki-bpmn                              "/usr/bin/bpmn"          25 hours ago   Up 25 hours   8003/tcp                                    kroki_bpmn_1
	  ee86c12a3cad   yuzutech/kroki-blockdiag                         "gunicorn --preload …"   25 hours ago   Up 25 hours   8001/tcp                                    kroki_blockdiag_1
	  75b6abb88d0f   yuzutech/kroki-mermaid                           "node src/index.js"      25 hours ago   Up 25 hours   8002/tcp                                    kroki_mermaid_1
	  8a3909721dd2   yuzutech/kroki-excalidraw                        "/usr/bin/excalidraw"    25 hours ago   Up 25 hours   8004/tcp                                    kroki_excalidraw_1
	  ```