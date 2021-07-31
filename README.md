# Mental Health in Tech Industry 2019 

DEFINE A GOAL

The point of this Power BI report is to visualize the mental health in tech industry in 2019.

SEARCH & DOWNLOAD DATA

For the row dataset was retrieved from Kaggle and downloaded into a csv format.

![Kaggle dataset](https://user-images.githubusercontent.com/71211875/126689688-c6be5b38-e0db-4b0b-ad21-94fb02d9504f.GIF)

DATA LOADING & EXPLORING

Loading the row dataset into Power Query and start exploring the dataset to define how to use, clean and transform this dataset to meet the project goal.

![DATA SET IN PQ](https://user-images.githubusercontent.com/71211875/126689729-6ca7a067-77cf-461d-a9f7-29f302613eeb.GIF)

DATA CLEANSING & TRANSFORMATION

After exploring the dataset, I already had an idea about the data quality and how the dataset needs to be cleaned, which columns and rows to remove, which to reformat, which to rename and reorder….etc.

Removing unnecessary columns
Remove empty, error/unrelated, unnecessary rows
Re-write values
Reformat/ recreate columns
Below you can find data cleansing steps in M Language

![CLEANED DATA](https://user-images.githubusercontent.com/71211875/126689808-3d7ae0d8-30e2-405b-b98a-2a6ac2000e3b.GIF)

```
= Table.SelectRows(#"Removed Unnecessary Columns", each ([#"How many employees does your company or organization have?"] <> ""))

= Table.RenameColumns(#"Removed Empty Rows",{{"*Are you self-employed?*", "Self-Employed"}, {"How many employees does your company or organization have?", "Company Size (Employees Number)"}, {"Is your employer primarily a tech company/organization?", "Tech Company"}, {"Is your primary role within your company related to tech/IT?", "Tech/IT Role"}, {"Does your employer provide mental health benefits as part of healthcare coverage?", "Mental Health Benefit as Part of Healthcare Coverage Provided By Employer"}, {"Has your employer ever formally discussed mental health (for example, as part of a wellness campaign or other official communication)?", "Mental Health Been Formally  Discussed By Employer"}, {"Does your employer offer resources to learn more about mental health disorders and options for seeking help?", "Offering Resources to Learn More about Mental Health for Seeking Help"}, {"Is your anonymity protected if you choose to take advantage of mental health or substance abuse treatment resources provided by your employer?", "Anonymity Protection When Choosing to Take Advantage of Mental Health or Substance Abuse Treatment Resources Provided by Employer"}, {"Overall, how much importance does your employer place on mental health?", "How Much Importance Dose Employer Place on Mental Health?"}, {"Do you *currently* have a mental health disorder?", "Having Mental Disorder"}, {"*If possibly, what disorder(s) do you believe you have?*", "Disorder(s) Believe You May Have (If Possibly)"}, {"*If so, what disorder(s) were you diagnosed with?*", "Disorder(s) Diagnosed With"}, {"Have you had a mental health disorder in the past?", "Had Mental Disorder"}, {"Have you ever sought treatment for a mental health disorder from a mental health professional?", "Sought Treatment for a Mental Health Disorder from a Mental Health Professional"}, {"Do you have a family history of mental illness?", "Have a Family History of Mental Illness"}, {"If you have a mental health disorder, how often do you feel that it interferes with your work *when being treated effectively?*", "Interfere of Mental Health Disorder With Work *when being treated effectively*"}, {"If you have a mental health disorder, how often do you feel that it interferes with your work *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*", "Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"}, {"Overall, how well do you think the tech industry supports employees with mental health issues?", "How Well Tech Indusrty Supports Mental Health Issues"}, {"What is your age?", "Age"}, {"What is your gender?", "G"}, {"What country do you *work* in?", "Country (Working In)"}})

= Table.SelectRows(#"Renamed Columns", each ([Age] <> 0))

= Table.ReorderColumns(#"Removed Outliers",{"Self-Employed", "Tech/IT Role", "Age", "G", "Country (Working In)", "Company Size (Employees Number)", "Tech Company", "Mental Health Benefit as Part of Healthcare Coverage Provided By Employer", "Mental Health Been Formally  Discussed By Employer", "Offering Resources to Learn More about Mental Health for Seeking Help", "Anonymity Protection When Choosing to Take Advantage of Mental Health or Substance Abuse Treatment Resources Provided by Employer", "How Much Importance Dose Employer Place on Mental Health?", "How Well Tech Indusrty Supports Mental Health Issues", "Having Mental Disorder", "Disorder(s) Believe You May Have (If Possibly)", "Disorder(s) Diagnosed With", "Had Mental Disorder", "Sought Treatment for a Mental Health Disorder from a Mental Health Professional", "Have a Family History of Mental Illness", "Interfere of Mental Health Disorder With Work *when being treated effectively*", "Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"})

= Table.AddIndexColumn(#"Reordered Columns", "Index", 1, 1, Int64.Type)

= Table.ReorderColumns(#"Added Index Column",{"Index", "Self-Employed", "Tech/IT Role", "Age", "G", "Country (Working In)", "Company Size (Employees Number)", "Tech Company", "Mental Health Benefit as Part of Healthcare Coverage Provided By Employer", "Mental Health Been Formally  Discussed By Employer", "Offering Resources to Learn More about Mental Health for Seeking Help", "Anonymity Protection When Choosing to Take Advantage of Mental Health or Substance Abuse Treatment Resources Provided by Employer", "How Much Importance Dose Employer Place on Mental Health?", "How Well Tech Indusrty Supports Mental Health Issues", "Having Mental Disorder", "Disorder(s) Believe You May Have (If Possibly)", "Disorder(s) Diagnosed With", "Had Mental Disorder", "Sought Treatment for a Mental Health Disorder from a Mental Health Professional", "Have a Family History of Mental Illness", "Interfere of Mental Health Disorder With Work *when being treated effectively*", "Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"})

= Table.SelectRows(#"Moved Index to The Begining", each ([Index] <> 106 and [Index] <> 110 and [Index] <> 127 and [Index] <> 139 and [Index] <> 194 and [Index] <> 195 and [Index] <> 202 and [Index] <> 212 and [Index] <> 242))

= Table.RenameColumns(#"Removed Errors/ Unrelated Rows",{{"Index", "Participant Number"}})

= Table.AddColumn(#"Renamed Index to Participant Number", "Gender", each if [#"G"] = "female" then "Female " else if [#"G"] = "Female" then "Female " else if [#"G"] = "Woman" then "Female " else if [#"G"] = "Non binary" then "Non-binary" else if [#"G"] = "F" then "Female " else if [#"G"] = "Non-binary" then "Non-binary" else "Male", type text)

= Table.ReorderColumns(#"Replaced Gender Value",{"Participant Number", "Self-Employed", "Tech/IT Role", "Age", "G", "Gender", "Country (Working In)", "Company Size (Employees Number)", "Tech Company", "Mental Health Benefit as Part of Healthcare Coverage Provided By Employer", "Mental Health Been Formally  Discussed By Employer", "Offering Resources to Learn More about Mental Health for Seeking Help", "Anonymity Protection When Choosing to Take Advantage of Mental Health or Substance Abuse Treatment Resources Provided by Employer", "How Much Importance Dose Employer Place on Mental Health?", "How Well Tech Indusrty Supports Mental Health Issues", "Having Mental Disorder", "Disorder(s) Believe You May Have (If Possibly)", "Disorder(s) Diagnosed With", "Had Mental Disorder", "Sought Treatment for a Mental Health Disorder from a Mental Health Professional", "Have a Family History of Mental Illness", "Interfere of Mental Health Disorder With Work *when being treated effectively*", "Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"})

= Table.TransformColumnTypes(#"Reordered Gender Column",{{"Self-Employed", type text}})

= Table.ReplaceValue(#"Changed Self-Employed Column Type to Text","false","Not Self-Employed ",Replacer.ReplaceText,{"Self-Employed"})

= Table.TransformColumnTypes(#"Replaced Self-Employed Values",{{"Tech/IT Role", type text}})

= Table.ReplaceValue(#"Changed Tech/IT Role Column Type to Text","true","Tech/ IT Role ",Replacer.ReplaceText,{"Tech/IT Role"})

= Table.ReplaceValue(#"Replaced Tech/IT Role Column Values (true)","false","Non Tech/ IT Role ",Replacer.ReplaceText,{"Tech/IT Role"})

= Table.TransformColumnTypes(#"Replaced Tech/IT Role Column Values (false)",{{"Tech Company", type text}})

= Table.ReplaceValue(#"Changed Tech Company Column Type to Text","true","Tech Company",Replacer.ReplaceText,{"Tech Company"})

= Table.ReplaceValue(#"Changed Tech Company Column Type to Text","true","Tech Company",Replacer.ReplaceText,{"Tech Company"})

= Table.ReplaceValue(#"Replaced Tech Company Values (true)","false","Non-Tech Company",Replacer.ReplaceText,{"Tech Company"})

= Table.RemoveColumns(#"Replaced Tech Company Values (false)",{"G"})

= Table.AddColumn(#"Removed G Column", "Custom", each if [#"Disorder(s) Believe You May Have (If Possibly)"] = "" then "N/A" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Mood Disorder*" then "Mode Disorder " else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Mood Disorder (Depression, Bipolar Disorder, etc), Anxiety Disorder (Generalized, Social, Phobia, etc)" then "Mode Disorder" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Anxiety Disorder (Generalized, Social, Phobia, etc), Mood Disorder (Depression, Bipolar Disorder, etc), Attention Deficit Hyperactivity Disorder" then "Anxiety Disorder" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Anxiety Disorder (Generalized, Social, Phobia, etc), Mood Disorder (Depression, Bipolar Disorder, etc)" then "Anxitey Disorder" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Mood Disorder (Depression, Bipolar Disorder, etc), Stress Response Syndromes, Eating Disorder (Anorexia, Bulimia, etc)" then "Mode Disorder" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Mood Disorder (Depression, Bipolar Disorder, etc), Post-traumatic Stress Disorder, Anxiety Disorder (Generalized, Social, Phobia, etc)" then "Mode Disorder" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Anxiety Disorder (Generalized, Social, Phobia, etc)" then "Anxiety Disorder" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Anxiety Disorder (Generalized, Social, Phobia, etc), Personality Disorder (Borderline, Antisocial, Paranoid, etc), Obsessive-Compulsive Disorder" then "Anxiety Disorder" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Stress Response Syndromes, Mood Disorder (Depression, Bipolar Disorder, etc)" then "Stress Response Syndromes" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Attention Deficit Hyperactivity Disorder, Anxiety Disorder (Generalized, Social, Phobia, etc)" then "Attention Deficit Hyperactivity" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Anxiety Disorder (Generalized, Social, Phobia, etc), Substance Use Disorder, Mood Disorder (Depression, Bipolar Disorder, etc), Post-traumatic Stress Disorder" then "Anxiety Disorder" else if [#"Disorder(s) Believe You May Have (If Possibly)"] = "Personality Disorder (Borderline, Antisocial, Paranoid, etc)" then "Personality Disorder" else [#"Disorder(s) Believe You May Have (If Possibly)"], type text)

= Table.TransformColumnTypes(#"Added Conditional Column",{{"Sought Treatment for a Mental Health Disorder from a Mental Health Professional", type text}})

= Table.ReplaceValue(#"Changed Sought Treatment for a Mental Health Disorder from a Mental Health Professional Column Type to Text","true","Yes",Replacer.ReplaceText,{"Sought Treatment for a Mental Health Disorder from a Mental Health Professional"})

= Table.SplitColumn(#"Replaced Sought Treatment for a Mental Health Disorder from a Mental Health Professional Value(true)", "Disorder(s) Believe You May Have (If Possibly)", Splitter.SplitTextByEachDelimiter({"("}, QuoteStyle.Csv, false), {"Disorder(s) Believe You May Have (If Possibly).1", "Disorder(s) Believe You May Have (If Possibly).2"})

= Table.SplitColumn(#"Split Disorder(s) Believe You May Have Column 1", "Disorder(s) Believe You May Have (If Possibly).1", Splitter.SplitTextByEachDelimiter({","}, QuoteStyle.Csv, false), {"Disorder(s) Believe You May Have (If Possibly).1.1", "Disorder(s) Believe You May Have (If Possibly).1.2"})

= Table.RemoveColumns(#"Split Disorder(s) Believe You May Have Column 2",{"Disorder(s) Believe You May Have (If Possibly).1.2", "Disorder(s) Believe You May Have (If Possibly).2"})

= Table.SplitColumn(#"Removed Uncleand Disorder Believe You May Have Column", "Disorder(s) Diagnosed With", Splitter.SplitTextByEachDelimiter({"("}, QuoteStyle.Csv, false), {"Disorder(s) Diagnosed With.1", "Disorder(s) Diagnosed With.2"})

= Table.SplitColumn(#"Split Disorder(s) Diagnosed With 1", "Disorder(s) Diagnosed With.1", Splitter.SplitTextByEachDelimiter({","}, QuoteStyle.Csv, false), {"Disorder(s) Diagnosed With.1.1", "Disorder(s) Diagnosed With.1.2"})

= Table.RemoveColumns(#"Split Disorder(s) Diagnosed With 2",{"Disorder(s) Diagnosed With.1.2", "Disorder(s) Diagnosed With.2"})

= Table.RenameColumns(#"Removed Uncleaned Split Disorder(s) Diagnosed With",{{"Disorder(s) Believe You May Have (If Possibly).1.1", "Disorder(s) Believe You May Have (If Possibly)"}, {"Disorder(s) Diagnosed With.1.1", "Disorder(s) Diagnosed With"}})

= Table.ReplaceValue(#"Renamed Disorder(s) Believe You May Have (If Possibly).1.1","false","No",Replacer.ReplaceText,{"Sought Treatment for a Mental Health Disorder from a Mental Health Professional"})

= Table.AddColumn(#"Replaced Sought Treatment for a Mental Health Disorder from a Mental Health Professional Value(false)", "Sorting Interfere of Mental Health Disorder with Work *when being treated effectively*", each if [#"Interfere of Mental Health Disorder With Work *when being treated effectively*"] = "Often" then 1 else if [#"Interfere of Mental Health Disorder With Work *when being treated effectively*"] = "Sometimes" then 2 else if [#"Interfere of Mental Health Disorder With Work *when being treated effectively*"] = "Rarely" then 3 else if [#"Interfere of Mental Health Disorder With Work *when being treated effectively*"] = "Never" then 4 else if [#"Interfere of Mental Health Disorder With Work *when being treated effectively*"] = "Not applicable to me" then 5 else null)

= Table.AddColumn(#"Added Sorting Interfere of Mental Health Disorder with Work *when being treated effectively* Column", "Sorting Interfere of Mental Health Disorder with Work *when not being treated effectively*", each if [#"Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"] = "Often" then 1 else if [#"Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"] = "Sometimes" then 2 else if [#"Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"] = "Rarely" then 3 else if [#"Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"] = "Never" then 4 else if [#"Interfere of Mental Health Disorder With Work  *when* _*NOT*_* being treated effectively (i.e., when you are experiencing symptoms)?*"] = "Not applicable to me" then 5 else null)
```

 After finishing cleaning, the data, it was loaded to Power Desktop to start creating the report.

REPORT DESIGNING

After being the data ready to visualize and before start creating the report, first I plan on how to design the report since it is multi-page and includes a lot of information to visualize. I start answering:

- How to present the data? 
- How many pages?
- What dose each page present/ what is each page goal?
- How each page will achieve its goal?


REPORT CREATING

After deciding how to visualize the data, I started creating the repot. First, I set up the background layout page (color, title, font.etc) then I started creating the dashboard.

Below you will find the final report.

![FEATURE IMAGE](https://user-images.githubusercontent.com/71211875/126689901-a6371188-4ae4-47c3-ad8b-07c60fe351ab.GIF)

For the final report: https://app.powerbi.com/reportEmbed?reportId=07a4d42c-071a-4729-aaf8-e498a7e9e858&autoAuth=true&ctid=766ae0a8-2dd1-4de3-9241-97090c9c8d3d&config=eyJjbHVzdGVyVXJsIjoiaHR0cHM6Ly93YWJpLXVhZS1ub3J0aC1hLXByaW1hcnktcmVkaXJlY3QuYW5hbHlzaXMud2luZG93cy5uZXQvIn0%3D

For the project description: https://reemalraeai.wordpress.com/portfolio/mental-health-in-tech-industry-2019/
