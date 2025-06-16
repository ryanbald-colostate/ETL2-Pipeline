# ETL2-Pipeline
End goal is to populate the pr_issue table.\
Reads the file with issues and PRs linked and populates the pr_issue table (skills database).\

Takes in CSV files for issues, pull requests, and commits from a given repo on github.\
The programs will combine these CSV's and clean them, creating the output that is fed into [IssueMapper](https://github.com/fabiojavamarcos/mapIssues2).\
Examples ran through in the programs are from [Jabref](https://github.com/JabRef/jabref). It is useful to compare with the source repo if you need a better understanding of the data.

## MergeDF
Issues definition: We will treat issue numbers as containing all issues and pull requests.\
Input: CSVs for Issues, Pull Requests, and Commits.\
Output: dataMerged_Final_only_closed.csv

Steps:

- Clean the data
  - Remove multiple commits for a single issue number (commits are only on prs). Ideally would be done by closed date, but that would be difficult so they are just done by last and assume they are already in order by closed date.
  - If issues data does not contain pull requests, create a copy of prs to later combine with issues.
  - Rename and remove certain columns from the corresponding dataframes.
- Merge Dataframes
  - Merge pull requests + issues = pull_commit.csv.
  - If issues contains prs already -> issues.csv. Otherwise concat prs onto issues and sort by issue number -> issues.csv.
  - Merge pull_commit with issues (with indicator on) to create the result dataframe.
- Clean results
  - Use the indicator (_merge) to assign values for isPR.
  - Remove any pr closed dates which are NaN.
- Create dataMerged_Final_only_closed.csv

## updated_procIssues
arguments:

postgres - username
admin - password
all_projects_without_filter_new - database name
/Users/fd252/OneDrive/Production/ETL2-Pipeline-main/data/output/rxjava/rxjava_df_merge.csv - input file
rxjava - project
"AS IS" - opation s: // "LOWER" - every text is lower case (good for TF-IDF). "AS IS" cases as is. Templates are not removed. Any other value: removes templates comparing the characters without transform in lower cases.
