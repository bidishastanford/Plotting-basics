## GGplot
##ggplot2
require(ggplot2)
Qplot is really basic for GGplot
```
x+y
library(ggplot2)
head(mpg)
str(mpg)
qplot(displ,hwy, data=mpg,geom=c("point","smooth"))
```

qplot may be used to make histogram and density
```
qplot(hwy,data=mpg,fill=drv)
qplot(hwy,data=mpg,geom="density")
```
###Facets within ggplot
Seperate plots for seperate sets of data-Use Facets
```
qplot(displ,hwy,data=mpg,facets=.~drv)
qplot(hwy,data=mpg,facets=.~drv)
```
###Use different color and shape to see differences in groups
```
qplot(displ,hwy,data=mpg,col=drv)
qplot(displ,hwy,data=mpg,shape=drv)
```

###Use regression line to see the relationship of the data
```
qplot(displ,hwy,data=mpg,col=drv)+geom_smooth(method="lm")
```

In Lattice plotting system, plots are made in one function, ggplot is much more layered. Start with the plot, overlay over that and annonate

###Ggplot layered method
```
g<-ggplot(data=mpg,aes(displ,hwy))
summary(g)
g+geom_point()
```
Can add more layers like smoothening it out
```
g+geom_point()+geom_smooth()
g+geom_point()+geom_smooth(method="lm")
```
Can also made different plots for different groups
```
g+geom_point(aes(color=class))+facet_grid(.~drv)+geom_smooth(method="lm")
```
Use the labs function to annotate the graphs
```
g+geom_point()+geom_smooth(method="lm")+labs(title="Display vs Highway",x="Display",y="Highway")

```
You can also change the confidence intervals when you use smooth linear regression model. Just write SE=False.

```
g+geom_point()+geom_smooth(method="lm",se=FALSE)
```

##Outliers on GGplot

```
testdata<-data.frame(x=1:100,y=rnorm(100))
testdata[50,2]<-100
plot(testdata$x,testdata$y,type="l",ylim=c(-3,3))
g<-ggplot(testdata,aes(x,y))
g+geom_line()+coord_cartesian(ylim=c(-3,3))
```

##Using facets
```
g<-ggplot(data=mpg,aes(displ,hwy))
g+geom_point()+geom_smooth(method="lm")+facet_grid(.~drv)
```
##Chaning grey background

```
g<-ggplot(data=mpg,aes(displ,hwy))
g+geom_point()+geom_smooth(method="lm")+facet_grid(.~drv)+theme_bw(base_family="Times")

```
##Some more fancy things
```
cutpoints<-quantile(diamonds$carat,seq(0,1,length=4),na.rm=TRUE)
cutpoints
diamonds$cars2<-cut(diamonds$carat,cutpoints)
diamonds$car2 <- cut(diamonds$carat,cutpoints) 
g<-ggplot(diamonds,aes(depth,price))
g+geom_point(alpha=1/3)+facet_grid(cut~car2)
```
