summary(ABIA)

ABIA<-subset(ABIA,ArrDelay!="NA")
ABIA<-subset(ABIA,DepDelay!="NA")

ABIA_summ=ABIA%>%
  group_by(Month,DayofMonth,DayOfWeek)%>%
  summarise(mean.ArrDelay=mean.default(ArrDelay),mean.DepDelay=mean.default(DepDelay))

ggplot(ABIA_summ) + 
  geom_point(mapping = aes(x = DayOfWeek, y = mean.DepDelay))
ggplot(ABIA_summ) + 
  geom_point(mapping = aes(x = DayOfWeek, y = mean.ArrDelay))

ggplot(ABIA_summ) + 
  geom_point(mapping = aes(x = DayofMonth, y =mean.DepDelay))+
  facet_wrap(~ Month, nrow = 2)
ggplot(ABIA_summ) + 
  geom_point(mapping = aes(x = DayofMonth, y =mean.ArrDelay))+
  facet_wrap(~ Month, nrow = 2)

ABIA_summ=ABIA%>%
  group_by(ArrTime,DepTime,Month,DayofMonth,DayOfWeek)%>%
  summarise(mean.DepDelay=mean.default(DepDelay),mean.ArrDelay=mean(ArrDelay))
ggplot(ABIA_summ) + 
  geom_point(mapping = aes(x = DepTime, y = mean.DepDelay))
ggplot(ABIA_summ) + 
  geom_point(mapping = aes(x = ArrTime, y = mean.ArrDelay))
