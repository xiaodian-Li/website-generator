---
title: echarts快速上手
date: 2018-05-09 17:01:06
tags: [echarts表格]
---
ECharts，一个使用 JavaScript 实现的开源可视化库，可以流畅的运行在 PC 和移动设备上，兼容当前绝大部分浏览器（IE8/9/10/11，Chrome，Firefox，Safari等），底层依赖轻量级的矢量图形库 ZRender，提供直观，交互丰富，可高度个性化定制的数据可视化图表。
### 【方法一：模块化单文件引入(推荐)】
<!--more-->
1.新建一个echarts.html文件，为ECharts准备一个具备大小(宽高)的Dom：
```
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>ECharts - 孤影'Blog</title>
</head>

<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="height:400px"></div>
</body>
```
2.新建'script'标签引入模块化单文件echarts.js：

```
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>ECharts - 孤影'Blog</title>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="height:400px"></div>
    <!-- ECharts单文件引入 -->
    <script src="http://echarts.baidu.com/build/dist/echarts.js"></script>
</body>
```
3.新建'script'标签中为模块加载器配置echarts和所需图表的路径(相对路径为从当前页面链接到echarts.js):

```
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>ECharts - 孤影'Blog</title>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="height:400px"></div>
    <!-- ECharts单文件引入 -->
    <script src="http://echarts.baidu.com/build/dist/echarts.js"></script>
    <script type="text/javascript">
        // 路径配置
        require.config({
            paths: {
                echarts: 'http://echarts.baidu.com/build/dist'
            }
        });
    </script>
</body>
```
4.'script'标签内动态加载echarts和所需图表，回调函数中可以初始化图表并驱动图表的生成：
 ```
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>ECharts - 孤影'Blog</title>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="height:400px"></div>
    <!-- ECharts单文件引入 -->
    <script src="http://echarts.baidu.com/build/dist/echarts.js"></script>
    <script type="text/javascript">
        // 路径配置
        require.config({
            paths: {
                echarts: 'http://echarts.baidu.com/build/dist'
            }
        });

        // 使用
        require(
            [
                'echarts',
                'echarts/chart/bar' // 使用柱状图就加载bar模块，按需加载
            ],
            function (ec) {
                // 基于准备好的dom，初始化echarts图表
                var myChart = ec.init(document.getElementById('main')); 

                var option = {
                    tooltip: {
                        show: true
                    },
                    legend: {
                        data:['销量']
                    },
                    xAxis : [
                        {
                            type : 'category',
                            data : ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
                        }
                    ],
                    yAxis : [
                        {
                            type : 'value'
                        }
                    ],
                    series : [
                        {
                            "name":"销量",
                            "type":"bar",
                            "data":[5, 20, 40, 10, 10, 20]
                        }
                    ]
                };

                // 为echarts对象加载数据 
                myChart.setOption(option); 
            }
        );
    </script>
</body>
```
5.浏览器中打开ecarts.html，就可以看到以下效果：

![image](http://images.daojia.com/assets/other/images/1.jpeg)

### 【方法二：标签式单文件引入】
1.新建一个echarts.html文件，为ECharts准备一个具备大小(宽高)的Dom。

```
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>ECharts - 孤影Blog</title>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="height:400px"></div>
</body>
```
2.新建'script'标签引入echart-all.js。

 ```
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>ECharts - 孤影'Blog</title>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="height:400px"></div>
    <!-- ECharts单文件引入 -->
    <script src="http://echarts.baidu.com/build/dist/echarts-all.js"></script>
</body>
```
3.新建'script'，使用全局变量echarts初始化图表并驱动图表的生成。

```
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>ECharts - 孤影'Blog</title>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="height:400px"></div>
    <!-- ECharts单文件引入 -->
    <script src="http://echarts.baidu.com/build/dist/echarts-all.js"></script>
    <script type="text/javascript">
        // 基于准备好的dom，初始化echarts图表
        var myChart = echarts.init(document.getElementById('main')); 

        var option = {
            tooltip: {
                show: true
            },
            legend: {
                data:['销量']
            },
            xAxis : [
                {
                    type : 'category',
                    data : ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
                }
            ],
            yAxis : [
                {
                    type : 'value'
                }
            ],
            series : [
                {
                    "name":"销量",
                    "type":"bar",
                    "data":[5, 20, 40, 10, 10, 20]
                }
            ]
        };

        // 为echarts对象加载数据 
        myChart.setOption(option); 
    </script>
</body>
```
4.浏览器中打开echarts.html，可以看到如下效果：

![image](http://images.daojia.com/assets/other/images/2.jpeg)


> 参考文章：http://echarts.baidu.com/feature.html


