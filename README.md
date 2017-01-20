docker-scrapyd
==============

Dockerfile for building an image that runs [scrapyd](http://scrapyd.readthedocs.org/).

Building
--------

```
$ docker build -t scrapyd .
```

Running
-------

```
$ docker run -p 6800 scrapyd
```

If you want to persist logs or scraped items export files, create a
data-only container and link to it when running scrapyd:

```
$ docker run -v /var/lib/scrapyd -v /var/log/scrapyd -name scraped-data busybox true
$ docker run -p 6800 -volumes-from scraped-data scrapyd
```

Now you can rebuild/update the `scrapyd` image and container without
destroying any scraped data.

docker-compose up -d # 后台运行
scrapyd-deploy -all  # 部署爬虫
curl http://127.0.0.1:6800/schedule.json -d project=VeNews -d spider=oschina # 运行爬虫
