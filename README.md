# ETL2-Pipeline
End goal is to populate the pr_issue table.

Takes in CSV files for issues, pull requests, and commits from a given repo on github.\
The programs will combine these CSV's and link PRs to issues, creating the output that is fed into [IssueMapper](https://github.com/fabiojavamarcos/mapIssues2).\
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
Input: final merged csv from MergeDF. Please rename to begin with 'project_' i.e. jabref_example.csv.\
Output: CSV file with PRs linked to issues they solve.

When running the cell that searches the PRs for issues, it may be best to comment out all print statements, or at least the issue body print statement. If running on jupyter, it may be necesary to increase the I/O rate. To do this, open Anaconda Powershell Promt and input 'jupyter notebook --NotebookApp.iopub_data_rate_limit=1.0e10'. This will open a new port for jupyter notebook and use the Anaconda Powershell Prompt as the kernel. Also make sure the cell outputs have a scroll bar by clicking Cell > Current Output/All Output > Toggle Scrolling, so that the print statements are contained.

Steps:
- Setup input and outputs
- Search the PRs for issues
  - Will search for an octothorpe ('#').
  - Send a chunk of text with the octothorpe to clean it and make sure it has numbers and is therefore an issue number.
  - Add the PR's number and the issue number found to their corresponding list.
- Link the PRs and their issues
  - Check to make sure the issue number exists in the datafile and that it is not a PR.
  - Create dataframes containing data for PRs and linked issues.
- Merge input with the linked data
  - Clean and remove some columns
- Output the merged dataframes as two files (one has NaN replaced as 'NA')
