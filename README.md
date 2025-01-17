# 项目说明
本项目fork自[site-map](https://github.com/c4software/python-sitemap)，新增了页面缓存功能，防止运行被中断后，重新启动需要从头开始抓取。
缓存路经为：`cache`，如果需要重新抓取最新网页，请先清空这个目录下的文件。
2023.04.02

# Python-Sitemap

Simple script to crawl websites and create a sitemap.xml of all public link in it.

Warning : This script only works with ***Python3***

## Simple usage

	>>> python main.py --domain http://blog.lesite.us --output sitemap.xml

## Advanced usage

Read a config file to set parameters:
***You can overide (or add for list) any parameters define in the config.json***

	>>> python main.py --config config/config.json

#### Enable debug:

  ```
	$ python3 main.py --domain https://blog.lesite.us --output sitemap.xml --debug
  ```

#### Enable verbose output:

  ```
  $ python main.py --domain https://blog.lesite.us --output sitemap.xml --verbose
  ```

#### Enable Image Sitemap

More informations here https://support.google.com/webmasters/answer/178636?hl=en

  ```
  $ python main.py --domain https://blog.lesite.us --output sitemap.xml --images
  ```

#### Enable report for print summary of the crawl:

  ```
  $ python main.py --domain https://blog.lesite.us --output sitemap.xml --report
  ```

#### Skip url (by extension) (skip pdf AND xml url):

  ```
  $ python main.py --domain https://blog.lesite.us --output sitemap.xml --skipext pdf --skipext xml
  ```

#### Drop a part of an url via regexp :

  ```
  $ python main.py --domain https://blog.lesite.us --output sitemap.xml --drop "id=[0-9]{5}"
  ```

#### Exclude url by filter a part of it :

  ```
  $ python main.py --domain https://blog.lesite.us --output sitemap.xml --exclude "action=edit"
  ```

#### Read the robots.txt to ignore some url:

  ```
  $ python main.py --domain https://blog.lesite.us --output sitemap.xml --parserobots
  ```

#### Human readable XML

```
$ python3 main.py --domain https://blog.lesite.us --images --parserobots | xmllint --format -
```

#### Multithreaded

```
$ python3 main.py --domain https://blog.lesite.us --num-workers 4
```

#### with basic auth
***You need to configure `username` and `password` in your `config.py` before***
```
$ python3 main.py --domain https://blog.lesite.us --auth
```

#### Output sitemap index file
***Sitemaps with over 50,000 URLs should be split into an index file that points to sitemap files that each contain 50,000 URLs or fewer.  Outputting as an index requires specifying an output file.  An index will only be output if a crawl has more than 50,000 URLs:***
```
$ python3 main.py --domain https://blog.lesite.us --as-index --output sitemap.xml
```

## Docker usage

#### Build the Docker image:

  ```
  $ docker build -t python-sitemap:latest .
  ```

#### Run with default domain :

  ```
  $ docker run -it python-sitemap
  ```

#### Run with custom domain :

  ```
  $ docker run -it python-sitemap --domain https://www.graylog.fr
  ```

#### Run with config file and output :
***You need to configure config.json file before***

  ```
  $ docker run -it -v `pwd`/config/:/config/ -v `pwd`:/home/python-sitemap/ python-sitemap --config config/config.json
  ```
