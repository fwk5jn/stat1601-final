# stat1601-final
project that examines the analytics behind Netflix films
code for project

          '''
          library(ggplot2)
          final <- read.csv("final_projdata.csv", header=TRUE)

          # median rating of overall data set
          median(final$rating)

          # check if all the data are in our data set
          levels(final$title)

          meaneachmovies <- aggregate(final[,2], list(final$title),mean)
          meaneachmovies
          medianeachmovies <- aggregate(final[,2], list(final$title),median)
          medianeachmovies
          meaneachmovies[which.max(meaneachmovies$x),]
          meaneachmovies[which.min(meaneachmovies$x),]

          final$genre <- ifelse(final$title == "Jaws   " 
                                | final$title == "The Game   " 
                                | final$title == "Donnie Darko   "
                                | final$title == "The Machinist   "
                                ,yes = "drama_movie", 
                                ifelse(final$title == "Spider-Man 2   " 
                                       | final$title == "Batman Begins   " 
                                       | final$title == "X-Men: The Legend of Wolverine   "
                                       | final$title == "X2: X-Men United   "
                                       ,yes = "super_hero_movie", no = "horror_movie"))

          final$genre<-as.factor(final$genre)


          #mean and median for each category
          aggregate(final[,2], list(final$genre),mean)

          #density plot
          ggplot(data=final, aes(x=year, y=rating)) + 
            geom_boxplot(colour="red") + 
            geom_dotplot(binaxis="y", stackdir="center",dotsize = 0.5,colour="black",fill="white")

          ggplot(final, aes(x=rating,colour=title)) + geom_density(alpha=.3)

          #regression of year vs rating
          regressionfinal <- lm(year ~ rating,data=final)
          print(regressionfinal)
          summary(regressionfinal)

          #graph
          ggplot(final, aes(x=rating)) + geom_bar(aes(y=..prop..)) + facet_grid(.~title)

          mean_movie <- aggregate(final[,2], list(final$title),mean)
          colnames(mean_movie) <- c("Title","Avg.rating")

          ggplot(mean_movie, aes(x=Title, y=Avg.rating)) + geom_point()  +theme(axis.text.x = element_text(angle=90, vjust=.5)) 
          + labs(title="Avg ratings of each movie")

          ggplot(final, aes(x=genre, y=rating)) + geom_boxplot(outlier.colour="red") + stat_summary(fun.y="mean", geom="point", colour="blue") 
          ##### horror genre has lower ratings than the other two. 
          #box plot of each genre

          ggplot(final, aes(x=rating)) + geom_bar(aes(y=..prop..)) + facet_grid(.~title)
          ## proportion by individual movies

          ggplot(final, aes(x=rating)) + geom_bar(aes(y=..prop..)) + facet_grid(cols=vars(genre))
          ## proportion by genre
          '''
