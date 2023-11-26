# selenium自动化之问题记录

1. 报错提示：ResourceWarning: Enable tracemalloc to get the object allocation traceback
  原因：多打开了一个self.driver = webdriver.Chrome()，没有关闭，删掉就好了