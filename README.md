# Aion Classic Topic Modeling

This project uses rvest to mine text data from the [Aion Classic General Discussion Forums](https://forums.aiononline.com/forum/28-general-discussion/) and quanteda to visualize results. 

See the [writeup on my website](https://vanilla-dev.online/general/project-update/) or the [Dataset I have provided on Kaggle](https://www.kaggle.com/vanilladev/aion-classic-general-discussion-forum-posts) if you just want to use existing data.

This project is written using R Markdown (.rmd) - you will need an environment which can recognize these files to work with it. I recommend RStudio.

## Usage

If you want to use the existing data and re-run the visualization, start at the code block 
```{r}
load("texts.Rda")
```
to obtain the R data frame and use it for your own purposes.

If you wish to completely re-run the scraping, run the code blocks from scratch. **Please pay special attention to the code block**
```{r}
mapDate <- function(string)
{
  if (startsWith(string, "Saturday")) return("July 10")
  if (startsWith(string, "Sunday")) return("July 11")
  if (startsWith(string, "Monday")) return("July 12")
  if (startsWith(string, "Tuesday")) return("July 13")
  if (startsWith(string, "yesterday")) return("July 14")
  if (!startsWith(string, "June") && !startsWith(string, "July")) return("July 15")
  return(string)
}
```
which you will have to adjust in order to map the dates of the previous week to their correct true value.  
**Keep in mind that the scraping automatically pauses every 150 threads for 10 minutes in order to avoid triggering 403 (Forbidden) responses from the server.**

`topic_dict.yml` contains the seed words for seeded LDA. You may change these if you wish.  
`AionTopicModel.html` is the rendered version of the .Rmd file. 
