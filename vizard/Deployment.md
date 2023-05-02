## Process Management

>[!INFO] Related Issues
>[Concurrency · Issue #3 · Nikronic/table-ocr (github.com)](https://github.com/Nikronic/table-ocr/issues/3). Note that although this issue is defined in `table-ocr` project, the idea of **process managamet** for shipping any API is required, hence the dicussion here with regard to **Docker** can be utilized globally across all projects, including [[vizard/Intro|Vizard (Intro)]] and [[table-ocr/Intro|Table OCR (intro)]].

>... you would probably want to build a **Docker image from scratch**, installing your dependencies, and running **a single Uvicorn process** instead of this image. (ref: [tiangolo/uvicorn-gunicorn-docker: Docker image with Uvicorn managed by Gunicorn for high-performance web applications in Python with performance auto-tuning. Optionally with Alpine Linux. (github.com)](https://github.com/tiangolo/uvicorn-gunicorn-docker#-warning-you-probably-dont-need-this-docker-image))

So, the actual "correct" way of doing this is to use `docker` and it's `swarm` feature, but it would be overkill when only we have internal users (at max 2). But in case that in future we want to expose these APIs to public, then it would be necessary.

Given this, for local development so far,  multiple (4) workers via `guvicorn` have been used. For the `docker` image, we will use *a single process* of `guvicorn` has the process management will be done via on the container level.
