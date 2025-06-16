# ETL2-Pipeline
End goal is to populate the pr_issue table.\
Reads the file with issues and PRs linked and populates the pr_issue table (skills database).\

Takes in CSV files for issues, pull requests, and commits from a given repo on github.\
The programs will combine these CSV's and clean them, creating the output that is fed into [IssueMapper](https://github.com/fabiojavamarcos/mapIssues2).\
Examples ran through in the programs are from [Jabref](https://github.com/JabRef/jabref). It is useful to compare with the source repo if you need a better understanding of the data.

## MergeDF

## updated_procIssues
arguments:

postgres - username
admin - password
all_projects_without_filter_new - database name
/Users/fd252/OneDrive/Production/ETL2-Pipeline-main/data/output/rxjava/rxjava_df_merge.csv - input file
rxjava - project
"AS IS" - opation s: // "LOWER" - every text is lower case (good for TF-IDF). "AS IS" cases as is. Templates are not removed. Any other value: removes templates comparing the characters without transform in lower cases.
