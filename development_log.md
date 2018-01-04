开发日志
=============================================

## 2018/1/3
### Issues
* 无法正常访问 www.tensorflow.org

    >**已解决:**   需要将科学上网模式调成全局模式

* MuGo 无法训练，目前已经确定错误发生在 tf.train.Saver().save()函数中

## 2018/1/4
### Issues
* MuGo 无法训练，目前已经确定错误发生在 tf.train.Saver().save()函数中

    >**已解决:**   实际问题出在tf.train.Saver().restore()中，github上的源代码有逻辑错误，如果传入--save-file参数，程序会认为这个路径下有上次训练后保存下来的模型，而实际上这里面没有相应的文件。
    
    >解决办法是在main.train中加入一个resume_train参数，该参数值默认为false。这样policy network在初始化是不会去resotre上次训练的不行，这样训练程序就能顺利运行了。
