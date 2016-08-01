##plotly简介:
交互式可视化探索——plotly,Plotly 是个交互式可视化的第三方库，官网提供了Python，R，Matlab,JavaScript，Excel的接口，因此我们可以很方便地在这些软件中调用Plotly，从而实现交互式的可视化绘图。
这篇文章主要从 R 的角度来介绍Plotly的使用。R中的Plotly是一个基于浏览器的图形包，即使在本地使用，它也可以实现交互式的可视化。推荐使用RStudio中的knitr包来展示交互式可视化。
##使用简介
如果你很熟悉ggplot2，那么你可以利用ggplot2绘制一个可视化图形，然后利用ggplotly函数就可以实现可视化的交互式展现。

```

p <- ggplot(data = d, aes(x = carat, y = price)) +
  geom_point(aes(text = paste("Clarity:", clarity)), size = 4) +
  geom_smooth(aes(colour = cut, fill = cut)) + facet_wrap(~ cut)

gg <- ggplotly(p)

```

如果用plotly绘制可视化,其主要函数有三个:plot_ly,add_trace,layout.
plotly生成一个基础图形,其语法格式为:

```
plot_ly(data = data.frame(), …, type = “scatter”, group, color, colors, symbol, symbols, size)
```

data是要绘图的数据集,x是横坐标轴变量,y是纵坐标轴变量,type是指定绘图类型,类型有’scatter’,’bar’,’box’,’heatmap’,’histogram’,’histogram 2d’,’area’,’pie’,’contour’,’histogram 2d’, ‘contour’,’scatter3d’,’surface’,’mesh3d’,scattergeo’,’choropleth’.

group是指定分组变量,color是指定颜色变量,colors是指定具体颜色变量,colors可以是RColorBrewer包中的调色板颜色，也可以是十六进制的 “#RRGGBB” 格式；symbol指定符号变量；symbols指定具体的符号类型，比如 ‘dot’, ‘cross’, ‘diamond’, ‘square’, ‘triangle-down’, ‘triangle-left’, ‘triangle-right’, ‘triangle-up’；size指定尺寸变量
实例:

```
p <- plot_ly(economics, x = date, y = uempmed, type = "scatter", showlegend = FALSE)
```

add_trace函数是在已有图形上添加新的图形,其基本语法如下:

add_trace(p = last_plot(), …, group, color, colors, symbol, symbols, size, data = NULL, evaluate = FALSE)
p指定要添加到哪个图形上，默认是上一个，其他参数变量意义同plot_ly中相同，data指定添加的数据集，默认是plot_ly中的数据.

实例:

```
p2 <- add_trace(p, y = fitted(loess(uempmed ~ as.numeric(date))))
```

layout 函数用来设置图形外观，比如标题属性，横纵坐标轴属性，图例属性，图形外边距属性，这些属性包括字体，颜色，尺寸等，
实例:

```
maxdf <- dplyr::filter(uempmed == max(uempmed))

p <- layout(p,              
    title = "unemployment", 
    xaxis = list(            #设置X轴标题和刻度线
        title = "time",     
        showgrid = F         
    ),
    yaxis = list(             
    title = "uidx"      
    ),
    annotations = list(          #添加注释
        list(
            x = maxdf$date,     
            y = maxdf$uempmed,   
            text = "Peak",       
            showarrow = T  
        )
    )
)
```

##保存到个人空间
我们可以把我们的可视化结果保存到我们的个人空间，并且可以利用官网提供的网页代码，将我们的可视化结果嵌入到我们的网页文件中，这样我们的网页中就出现了一个带链接的图片，点击图片会跳到带有交互式的可视化结果网页中。

首先到官网注册创建个人账号
在R中输入下面代码，设置自己的账号，plotly_api_key在个人设置页面的左下角的api keys中。
```
 Sys.setenv("plotly_username"="your_plotly_username")
 Sys.setenv("plotly_api_key"="your_api_key")
```
将结果上传到个人空间，并设置其他人是否可见。
```
 plotly_POST(p, filename = "r-docs/midwest-boxplots", world_readable=TRUE)
```