---
layout: post
title: "python logging"
date: 2014-09-15 01:11
comments: true
categories: [code,Python_library]
---


##python module **logging**.


###起因
* 是想用logging.debug来打印出变量值作用debug的时候用（取代print）


###需求
* 要可以打印当前文件，行的信息。

  [stackoverflow.com](http://stackoverflow.com/questions/10973362/python-logging-function-name-file-name-line-number-using-a-single-file)

  {% codeblock lang:python%}
  import logging

  logger = logging.getLogger('root')

  FORMAT = "[%(filename)s:%(lineno)s - %(funcName)20s() ] %(message)s"

  logging.basicConfig(format=FORMAT)

  logger.setLevel(logging.DEBUG)
  {% endcodeblock %}

  [详细的format相关内容](https://docs.python.org/2/library/logging.html#logrecord-attributes)

  [详细的教程](http://docs.python.org/2/howto/logging.html#logging-basic-tutorial)

###简介

* 快速使用

  {% codeblock lang:python %}
  import logging

  logging.basicConfig(format='%(levelname)s:%(message)s', level=logging.DEBUG)

  logging.debug('This message should appear on the console')

  logging.info('So should this')

  logging.warning('And this, too')
  {% endcodeblock %}