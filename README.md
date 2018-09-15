# RandomSubsetElasticNet


The RandomSubsetElasticNet model will split training data into randomly generated subsets and train an Elastic Net
model for each subset. Subsets are determined by splitting on the training data's binary categorical features. These
feature indices must be provided to the model at instantiation. Subsets are created with replacement, so one sample
can be part of the training data for multiple ElasticNet models. These subsets are created until a percentage of the
training data greater than or equal to the coverage_threshold fits at least one generated models to create is
provided, it will make boolean subsets until that number is hit (determined by ). subset. If an explicit number of
models to create is provided, it will make boolean subsets until that number is hit (determined by
explicit_model_count). It can exit early if no more samples are covered after a certain number of attempts are made
(determined by max_boolean_generation_attempts). Each boolean statement must cover between lower_bound and upper_bound
percent of the complete training data. There will also be a fallback ElasticNet model which is trained on the
entirety of the training data. For each model created, the R^2 score will be recorded fitted against the subset of
samples which match the corresponding boolean phrase.

For prediction and scoring, the testing sample will be tested against all models whose corresponding boolean phrase
matches. The predictive score is determined by either the best performing matching model, a weighted subset determined
by the individual R^2 values, or a mix between the two. This weight is determined by the p value.

RandomSubsetElasticNet uses sklearn.metrics.r2_score and sklearn.linear_model.ElasticNet.