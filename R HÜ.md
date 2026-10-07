```R
#https://www.gastonsanchez.com/packyourcode/intro.html
set.seed(1257)
num_of_toss <- 9
coin <- c(0,1)
flip <- sample(coin,size=num_of_toss,replace=TRUE)
freq <- table(flip)
freq 

# Brute force through the array
data <- expand.grid(rep(list(coin), num_of_toss), stringsAsFactors = FALSE)
count <- 0
rv <- 0
for (i in 1:512) 
{
  for(j in 1:8)
  {
    if(data[i,j] != data[i,j+1])
    {
      count <- count +1
    }
    if(count == 2)
    {
      rv <- rv +1
    }
  }
}
#rv is wrong? 
print(rv)
# correct result? wtf
print(rv/512)

```