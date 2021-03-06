

## Prediction

At last we’re ready to predict who survives among passengers of the Titanic based on variables that we carefully curated and treated for missing values. For this, we will rely on the randomForest classification algorithm; we spent all that time on imputation, after all.

### Split into training & test sets

Our first step is to split the data back into the original test and training sets.


```r
# Split the data back into a train set and a test set
train <- full[1:891,]
test <- full[892:1309,]
```

###  Building the model

We then build our model using randomForest on the training set.


```r
# Set a random seed
set.seed(754)

# Build the model (note: not all possible variables are used)
rf_model <- randomForest(factor(Survived) ~ Pclass + Sex + Age + SibSp + Parch + 
                                            Fare + Embarked + Title + 
                                            FsizeD + Child + Mother,
                                            data = train)

# Show model error
plot(rf_model, ylim=c(0,0.36))
legend('topright', colnames(rf_model$err.rate), col=1:3, fill=1:3)
```

<img src="17-Prediction_files/figure-html/unnamed-chunk-3-1.png" width="672" />

The black line shows the overall error rate which falls below 20%. The red and green lines show the error rate for ‘died’ and ‘survived’ respectively. We can see that right now we’re much more successful predicting death than we are survival.


### Variable importance

Let’s look at relative variable importance by plotting the mean decrease in Gini calculated across all trees.


```r
# Get importance
importance    <- importance(rf_model)
varImportance <- data.frame(Variables = row.names(importance), 
                            Importance = round(importance[ ,'MeanDecreaseGini'],2))

# Create a rank variable based on importance
rankImportance <- varImportance %>%
  mutate(Rank = paste0('#',dense_rank(desc(Importance))))

# Use ggplot2 to visualize the relative importance of variables
ggplot(rankImportance, aes(x = reorder(Variables, Importance), 
    y = Importance, fill = Importance)) +
  geom_bar(stat='identity') + 
  geom_text(aes(x = Variables, y = 0.5, label = Rank),
    hjust=0, vjust=0.55, size = 4, colour = 'red') +
  labs(x = 'Variables') +
  coord_flip() + 
  theme_few()
```

<img src="17-Prediction_files/figure-html/unnamed-chunk-4-1.png" width="672" />


Whoa, glad we made our title variable! It has the highest relative importance out of all of our predictor variables. I think I’m most surprised to see that passenger class fell to #5, but maybe that’s just bias coming from watching the movie Titanic too many times as a kid.


### Prediction!

We’re ready for the final step — making our prediction! When we finish here, we could iterate through the preceding steps making tweaks as we go or fit the data using different models or use different combinations of variables to achieve better predictions. But this is a good starting (and stopping) point for me now.


```r
# Predict using the test set
prediction <- predict(rf_model, test)

# Save the solution to a dataframe with two columns: PassengerId and Survived (prediction)
solution <- data.frame(PassengerID = test$PassengerId, Survived = prediction)

# Write the solution to file
write.csv(solution, file = 'rf_mod_Solution.csv', row.names = F)
```




**Thats all folks !**

![](./images/thankyou.gif)
