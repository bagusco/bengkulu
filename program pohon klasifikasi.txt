#membaca data
data <- read.csv("D:/lowbwt.csv")

#melihat data
View(data)

#menampilkan beberapa baris data paling atas
head(data, n=4)

#membuat pohon klasifikasi
#perlu package bernama: rpart
#1. menginstall package rpart
# install.packages("rpart")
#2. memanggil/nge-load package
library(rpart)
#membuat model pohon klasifikasi
pohon <- rpart(low ~ age + lwt + race + smoke, data=data,
      method='class')

#menampilkan gambar pohon klasifikasi
#memerlukan package bernama: rpart.plot
#install.packages("rpart.plot")
library(rpart.plot)
rpart.plot(pohon, extra=4)

#memprediksi resiko lahir dengan berat kurang
#untuk ibu yang:
#lwt = 110
#age = 26
#race = Black
#smoke = No

karakteristik <- data.frame(lwt=110, age=26,
                            race="Black", smoke="No" )
predict(pohon, karakteristik)

#untuk ibu yang:
#lwt = 110
#age = 26
#race = Black
#smoke = Yes

karakteristik <- data.frame(lwt=110, age=26,
                            race="Black", smoke="Yes" )
predict(pohon, karakteristik)
