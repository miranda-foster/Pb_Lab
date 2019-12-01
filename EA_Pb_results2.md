## Converting the Values on a per gram of soil basis

Currently, we have a concentration based on 10 grams of soil that was digested and diluted upto 100 mL. So, we next need to change our concentration in the digestion relative to the soils (ug/g -> mg/kg)
```{r convertunits}
parkdata$SoilPb = parkdata$Pb208/10 
```

```{r boxplot}
boxplot(SoilPb ~ PARK, data=parkdata)
```

Let's fix the names of the parks and then adjust the size to fit on the boxplot.

```{r fixnames}
#droplevels(parkdata$PARK)
levels(parkdata$PARK) <- c("Blaisdell", "Chapparal", "Jaeger", "La Puerta", "Larkin", "Marston", "Memorial", "R. Torrez", "Walker", "Wheeler")
unique(levels(parkdata$PARK))
aggregate(parkdata$SoilPb, list(parkdata$PARK), length)
```

```{r boxplot2}
par(las=1)
boxplot(SoilPb ~ PARK, data=parkdata, xlab="", xaxt="n")
axis(1, 1:10, parkdata$PARK, labels=F)
text(x = 1:10+.25,
     y = par("usr")[3] - 20,
     labels = unique(levels(parkdata$PARK)),
     xpd = NA,
     ## Rotate the labels by 35 degrees.
     srt = 35, pos=2,
     cex = 1.2)
```
