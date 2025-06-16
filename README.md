# ETL2-Pipeline

reads the file with issues and PRs linked and populates the pr_issue table (skills database)

## MergeDF

## updated_procIssues
arguments:

postgres - username
admin - password
all_projects_without_filter_new - database name
/Users/fd252/OneDrive/Production/ETL2-Pipeline-main/data/output/rxjava/rxjava_df_merge.csv - input file
rxjava - project
"AS IS" - opation s: // "LOWER" - every text is lower case (good for TF-IDF). "AS IS" cases as is. Templates are not removed. Any other value: removes templates comparing the characters without transform in lower cases.
