## 1. 页面基本结构
        loading   
            text  
            progress  
            footer  
        cover  
        home  
        result  
## 2. loading导出图片
        导出图片 右键图目录git bash here，执行命令 ls > aaa.txt，打开aaa.txt  ctrl+h 将换行符选择放到第1个input，第2个input替换框放","css/，把首位没用的部分去掉，还有.css和.less文件删除
## 3. js逻辑
        1. loading  
            先声明count,每次for循环count++,当count等于i时,图片加载完成(onload为异步,i瞬间执行结束,所以加个count)  
        2. 选择性别页  
            点击后将页面向下翻一屏,记录性别,根据性别在下一页显示不同人物  
        3. 点击按钮  
            1. 将result(答对的题数),answerCount(答题数),isfinished(答题是否完成)置为初始状态  
            2. 当按钮被锁定时点击无效  
            3. 获取此按钮的data(忠,智,文,性,锐)  
            4. 对答题页面作初始化并向下滚动一屏到答题页面  
        4. 初始化答题页  
            1. 将answerIndex(答题页页数)置为0,获取相应的data数据,获取数据长度,使answerIndex等于answerCount  
            2. 将答题页数填充数据,判断答题页数加1等于数据长度时,isfinished = true,将答题页数据填充进去  
            3. 给问题页加上data为该按钮的data  $('.answer').data('daoju', daoju);  
        5 . 答题页,点击选项  
            1. 避免重复点击,先设置lock = false,点击时lock置为true,如果点击时lock = true,则返回  
            2. answerCount++,将正确答案赋给本次答题页面,获取点击的选项,判断是否等于正确答案,并获取answer的data数据(忠,智,文,性,锐),如果答对,则答题正确,result++,否则错误  
            3. 将lock置为false
        6. 答题正确  
            1. 判断isfinished是否为true,接下来判断daoju是否为renwu  
            2. 如果不为renwu,则当result>=2时,调用答题成功,否则调用答题失败;如果为renwu,则调用renwuresult  
            3. 如果isfinished为false,则显示对号,再隐藏,并重新渲染下一道答题数据  
        7. 错误答题  
            同正确答题  
        8. 答题成功  
            1. 给对应的(忠,智,文,性,锐)添加样式  
            2. 最后一道题的正确或错误显示,将lock=false,再将结果隐藏,渲染结果页数据,将结果页展示,再隐藏结果页,显示人物页,并添加相应道具  
        9. 答题失败  
            1. 同答题成功,但是不用给对应的data添加样式,结果页不用变,且不用在人物页添加道具  
        10 .人物升级  
            1. 获取答对的题数,将其除以2并向上取整,如果答对0题,默认为1

```
            num = result;
            result = Math.ceil(num/2);
            if (result == 0) {
                result = 1;
            }
```

            2. 同答题成功,将相应数据渲染到人物升级的结果页,并根据答对题数改变人物
