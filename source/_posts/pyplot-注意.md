---
title: pyplot 注意
date: 2019-08-28 15:16:31
tags: [AI,Pyplot]
---
plt.imshow()不显示图像？

解决方法:在后面加一句：plt.show()

原理：plt.imshow()函数负责对图像进行处理，并显示其格式，而plt.show()则是将plt.imshow()处理后的函数显示出来。