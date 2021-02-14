\#\#Loading the necessary libraries etc.

    #install.packages('data.table')
    library(wordcloud2)

    ## Warning: package 'wordcloud2' was built under R version 4.0.3

    library(wordcloud)

    ## Warning: package 'wordcloud' was built under R version 4.0.3

    ## Loading required package: RColorBrewer

    ## Warning: package 'RColorBrewer' was built under R version 4.0.3

    library(slam)

    ## Warning: package 'slam' was built under R version 4.0.3

    library(quanteda)

    ## Warning: package 'quanteda' was built under R version 4.0.3

    ## Package version: 2.1.2

    ## Parallel computing: 2 of 8 threads used.

    ## See https://quanteda.io for tutorials and examples.

    ## 
    ## Attaching package: 'quanteda'

    ## The following object is masked from 'package:utils':
    ## 
    ##     View

    library(SnowballC)

    ## Warning: package 'SnowballC' was built under R version 4.0.3

    library(arules)

    ## Warning: package 'arules' was built under R version 4.0.3

    ## Loading required package: Matrix

    ## 
    ## Attaching package: 'arules'

    ## The following objects are masked from 'package:base':
    ## 
    ##     abbreviate, write

    library(proxy)

    ## Warning: package 'proxy' was built under R version 4.0.3

    ## 
    ## Attaching package: 'proxy'

    ## The following object is masked from 'package:Matrix':
    ## 
    ##     as.matrix

    ## The following object is masked from 'package:quanteda':
    ## 
    ##     as.matrix

    ## The following objects are masked from 'package:stats':
    ## 
    ##     as.dist, dist

    ## The following object is masked from 'package:base':
    ## 
    ##     as.matrix

    library(cluster)

    ## Warning: package 'cluster' was built under R version 4.0.3

    library(stringi)
    library(Matrix)
    library(tidytext)

    ## Warning: package 'tidytext' was built under R version 4.0.3

    library(plyr)

    ## Warning: package 'plyr' was built under R version 4.0.3

    library(ggplot2)

    ## Warning: package 'ggplot2' was built under R version 4.0.3

    library(factoextra)

    ## Warning: package 'factoextra' was built under R version 4.0.3

    ## Welcome! Want to learn more? See two factoextra-related books at https://goo.gl/ve3WBa

    library(mclust)

    ## Warning: package 'mclust' was built under R version 4.0.3

    ## Package 'mclust' version 5.4.6
    ## Type 'citation("mclust")' for citing this R package in publications.

    library(dplyr)

    ## Warning: package 'dplyr' was built under R version 4.0.3

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:plyr':
    ## 
    ##     arrange, count, desc, failwith, id, mutate, rename, summarise,
    ##     summarize

    ## The following objects are masked from 'package:arules':
    ## 
    ##     intersect, recode, setdiff, setequal, union

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

    library(tm)

    ## Warning: package 'tm' was built under R version 4.0.3

    ## Loading required package: NLP

    ## Warning: package 'NLP' was built under R version 4.0.3

    ## 
    ## Attaching package: 'NLP'

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     annotate

    ## The following objects are masked from 'package:quanteda':
    ## 
    ##     meta, meta<-

    ## 
    ## Attaching package: 'tm'

    ## The following object is masked from 'package:arules':
    ## 
    ##     inspect

    ## The following objects are masked from 'package:quanteda':
    ## 
    ##     as.DocumentTermMatrix, stopwords

    library(ggplot2)
    library(dplyr)
    library(gridExtra)

    ## Warning: package 'gridExtra' was built under R version 4.0.3

    ## 
    ## Attaching package: 'gridExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

    library(ggforce)

    ## Warning: package 'ggforce' was built under R version 4.0.3

    library(grid)
    library(data.table)

    ## Warning: package 'data.table' was built under R version 4.0.3

    ## 
    ## Attaching package: 'data.table'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     between, first, last

    ## The following object is masked from 'package:slam':
    ## 
    ##     rollup

\#Load in the Data

    papers<-read.csv('C:/Users/noahm/OneDrive/Desktop/fedPapers85.csv')
    paperscopy<-papers

\#Format Data for use in kmeans clustering

    paperskmeans<-paperscopy[,2:72]
    rownames(paperskmeans)<-paperskmeans[,1]
    paperskmeans[,1]<-NULL

\#Conduct initial analysis of the data to determine ideal number of
clusters

    fviz_nbclust(papers, FUN=hcut, method = 'wss')

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

    ## Warning in stats::dist(x, method = method, ...): NAs introduced by coercion

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-4-1.png)

    fviz_nbclust(papers, FUN=hcut, method='silhouette')

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

    ## Warning in stats::dist(x): NAs introduced by coercion

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-4-2.png)
\#initial value fell short. Chose 7 clusters for future use based on
assessment of the data.

    clusters<-kmeans(paperskmeans, 7)
    paperskmeans$Clusters<-as.factor(clusters$cluster)

\#additional visual exploration of the Data

    papers3<-papers
    papers3$Clusters<-as.factor(clusters$cluster)
    clusplot(paperskmeans, paperskmeans$Clusters, color = T, shade = T, labels = 0, lines = 0)

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-6-1.png)

\#Additional visual exploration made clusters seem like the ideal
choice.

    library(ggplot2)
    ggplot(data=papers3, aes(x=author, fill=Clusters))+geom_bar(stat='count')+labs(title="Potential K Values")+theme(plot.title=element_text(hjust = 0.5), text=element_text(size=12))

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-7-1.png)
\#Conducted additional cleaning of the data for kmeans evaluation

    FedPapers_HAC <- papers[,c(2:72)]
    rownames(FedPapers_HAC) <- FedPapers_HAC[,1]
    FedPapers_HAC[,1] <- NULL

\#Developed various distance formulas between variables using several
different methods

    distance  <- dist(FedPapers_HAC, method = "euclidean")
    distance2 <- dist(FedPapers_HAC, method = "maximum")
    distance3 <- dist(FedPapers_HAC, method = "manhattan")
    distance4 <- dist(FedPapers_HAC, method = "canberra")
    distance5 <- dist(FedPapers_HAC, method = "binary")

\#Developed Hierarchical Dendograms for each distance method before
settling on manhattan measurement

    HAC <- hclust(distance5, method="complete")
    plot(HAC, cex=0.6, hang=-1)
    rect.hclust(HAC, k =7, border=2:5)

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-10-1.png)
\#Manhattan measurement with a k of 7 provided the most distinct order
to the various papers and a patern began to emerge. You’ll note that the
disputed papers largely fall in with Madison’s work within the
Hierarchy.

    HAC2 <- hclust(distance3, method="complete")
    plot(HAC2, cex=0.6, hang=-1)
    rect.hclust(HAC2, k =7, border=2:5)

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-11-1.png)

\#I conducted additional cleaning of the data and separated subsets of
the data for visual comparison of where they fell within the clusters.

    hc <- hclust(distance3)
    cluster <- cutree(hc, k=7)
    xy<-data.frame(cmdscale(distance3), factor(cluster))
    names(xy) <- c("x", "y", "cluster")
    xy$model <- rownames(xy)

    #note the split of the data for comparison purposes.
    m<-xy[xy$model %like% 'Madison',]
    peac<-xy[xy$model %like% 'dispt',]
    hamton<-xy[xy$model %like% 'Ham',]
    joint<-xy[xy$model %like% 'HM',]

    n<-as.data.frame(bind_rows(m,peac))
    n<-as.data.frame(bind_rows(n,hamton))

\#The following charts depict the location of each of the papers
produced by Madison, Hamilton, and our mystery writer with relation to
one another corresponding with Manhattan Distance with a K of 7.

The first is Madison’s known works.

    ggplot(xy, aes(x, y)) + geom_point(aes(colour=cluster), size=3)+geom_text(data=m ,aes(label=model), size=2)+ggtitle('Madison Papers')

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-13-1.png)

    ggplot(xy, aes(x, y)) + geom_mark_ellipse(expand=0,aes(fill=cluster))+geom_point(data=m)+theme_bw()+geom_text(data=m,aes(label=model), size=1)+ggtitle('Madison Papers')

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-13-2.png)

The second is our mystery writer

    ggplot(xy, aes(x, y)) + geom_point(aes(colour=cluster), size=3)+geom_text(data=peac ,aes(label=model), size=2)+ggtitle('Disputed Papers')

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-14-1.png)

    ggplot(xy, aes(x, y)) + geom_mark_ellipse(expand=0,aes(fill=cluster))+geom_point(data=peac)+theme_bw()+geom_text(data=peac,aes(label=model), size=1)+ggtitle('Disputed Papers')

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-14-2.png)

The third is Hamilton’s known works

    ggplot(xy, aes(x, y)) + geom_point(aes(colour=cluster), size=3)+geom_text(data=hamton ,aes(label=model), size=2)+ggtitle('Hamilton Papers')

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-15-1.png)

    ggplot(xy, aes(x, y)) + geom_mark_ellipse(expand=0,aes(fill=cluster))+geom_point(data=hamton)+theme_bw()+geom_text(data=hamton,aes(label=model), size=1)+ggtitle('Hamilton Papers')

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-15-2.png)

I also plotted the location of papers coauthored by both Hamilton and
Madison to demonstrate the demonstrable difference such a paper has with
relation to others.

    ggplot(xy, aes(x, y)) + geom_point(aes(colour=cluster), size=3)+geom_text(data=joint ,aes(label=model), size=2)+ggtitle('Cowritten Papers')

![](Mott_Homework4_files/figure-markdown_strict/unnamed-chunk-16-1.png)

\#\#What I was able to gleen from the various clustering that was
conducted on the Federalist Papers was that it is highly likely that the
mystery writer for the papers with the unknown author are attributable
to Madison. You will note in the plots that while the plots overlap, the
majority of Hamilton’s work resides in the upper left of the plot while
Madison’s and the mystery author’s works are closer together and occupy
more of the middle of the plot. This holds true, not only for the
cluster plot but also for the hierarchical dendogram demonstrating a
clustering of Madison and the mystery author’s works.
