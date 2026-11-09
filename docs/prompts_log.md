# Prompts log

The project rules ask for **all prompts used**. Below is every prompt the team sent to an AI assistant, word for word, with the files attached and what we used the answer for.

**Tool:** Claude (Anthropic), in the Claude app.
**Dates:** prompts 1–10 on 9 October 2026; prompts 11–21 between October and November 2026; prompts 22 onward on 9 November 2026 (submission day).

Prompts are word for word. Only prompt 23 is shortened, because it was just a list of the team's names, IDs and GitHub usernames (the same as the team table in the README).

| # | Prompt (word for word) | Files attached | What we used the answer for |
|---|---|---|---|
| 1 | "Here is everything related to the Data Engineering Project , I want you to analyze the file carefully read everything twice and then after that I want you to tell me what do you need from as course material for example or anything else before you start working , make sure that I want a  full grade on this project as it represents a large sum from the grades of the subject , also we are 6 members in the team so divide the work as you are moving on through the project so that every member know what to memorize as there is evaluation I think which is graded." | Project Description.pdf, Data Catalog.pdf | Checklist of deliverables and grading criteria; first team-role split; timeline |
| 2 | "I will upload to you the course materials right now so that you can start working but as for milestone 2 we don't have yet it hasn't been posted till now , and also I will provide you with the names and id's and the GitHub usernames as you want and for the strengths we are all the same so divide it as you like. We didn't choose a dataset yet so you choose for us the easiest" | none | Dataset choice: Affordable Housing Production by Building (H2) + SIRTA (T4), after checking their real columns and sizes |
| 3 | "Here are the lectures wait for the labs . There are a lot of things so I will provide them lab by lab ok ." | Lecture_1.pdf to Lecture_4.pdf | Course terms used in the notebook (ETL, tidy data, data types, IQR rule, chart choice, no pie charts) |
| 4 | "Here is lab 1." | Lab 1 notebook, adult.csv, Report.html, Adult_Sweetviz_Report.html, Adult_Sweetviz_Compare.html | EDA order, hidden missing values check, ydata-profiling and Sweetviz reports |
| 5 | "Wait I forgot these too in Lab 1" | 5 figures from Lab 1 (scraping pipeline, DOM tree, DevTools, tags) | Extract pipeline table in Section 1 |
| 6 | "Here is Lab 2" | Lab 2 notebook and datasets (retail_transactions, placement, heart, stock, Uni_Ranking, Airbnb_Open_Data) | Missing-value and outlier methods, Hot Deck imputation, Plotly maps, Dash callbacks |
| 7 | "Here is Lab 3" | Lab 3 manual, notes, Power BI file, 4 theme files, Links.doc, Remote Work dataset | Dashboard design (KPI cards, filters, safe division), whole-word replacement |
| 8 | "And finally here is Lab 4" | Lab 4 handout and notes | Drill-through, tooltips, ranking measures, merging after aggregation |
| 9 | "This is everything as course materials , you are the mentor here Claude don't ask me what to change just choose the easiest for us and also make sure to choose what gets us the full grade with the bonus if found too that's all we want" | none | Final research questions, integration levels and website plan |
| 10 | "Here you baby girl" | hg8x-zxpr.csv, xeqp-qz8h.csv (downloaded from the API) | Raw data snapshot used by the notebook and website |
| 11 | "How can I run the site to test it right now ?" | none | Steps to run the website (first in Google Colab) |
| 12 | "Give me step 2" | none | Next step of the run guide |
| 13 | "I unzipped everything and ran every cell what is next" | screenshot of the notebook outputs in Colab | Next step after the notebook ran |
| 14 | "??" | screenshot of a `ModuleNotFoundError` in Colab | Fix: the project files were not in the Colab session, so we uploaded them first |
| 15 | "Tell me something to try" | screenshot of the website running in Colab | Ideas to test the filters, search and Generate Report |
| 16 | "It is working fine , but I want to run it locally instead of Google Collab what should I do" | none | Guide to running the website on a Windows laptop |
| 17 | "Python 3.11.9" | none | Checked that this Python version works with our packages |
| 18 | ""C:\Users\LOQ\OneDrive\Desktop\nyc-housing-street-safety\nyc-housing-street-safety\app.py"" | none | Commands for this folder |
| 19 | "Is there something else ?" | screenshot of `pip install` running | Remaining local setup steps |
| 20 | "Which is the easiest member" | none | Choosing a role for Mazen (M6) |
| 21 | "As a member 6 what do suggest for me to do so I that I guarantee the full mark in the evaluation" | none | M6 evaluation preparation plan |
| 22 | "What is the file that we'll submit ? Today is the submission right ?" | none | Submission checklist: one email with the IDs, GitHub link, website link and dataset links |
| 23 | *(shortened)* the six team members' names and IDs, and five GitHub usernames | none | Team tables in the README and the notebook |
| 24 | "Wait I will tell you which is which member" | none | none |
| 25 | "Said -> 3 / Eyad Nada -> 5 / Ziad Mohamed -> 2 / Mohamed Nasr -> 4 / Mohamed Reyad -> 1 / Mazen -> 6" | none | Role of each member (M1–M6) |
| 26 | "Give me the link to the repo" | none | Creating the GitHub repository |
| 27 | "I can't find it" | screenshot of the GitHub repositories page | Finding the New repository button |
| 28 | "I added them all what now" | none | Uploading the files to the repository |
| 29 | "Where is it" | a quoted line from the previous answer | Direct upload link |
| 30 | "??" | screenshot of the repository after the first upload | Uploading the folders that were missing |
| 31 | "I want Claude Code to review everything after we finish can you make this possible" | none | Plan for a final review |
| 32 | "I want you to review everything right now we finished and deployed it" | none | Final review of the repository, notebook and website |
| 33 | "https://nyc-housing-street-safety-dun.vercel.app/ Here is the link" | none | The review found that this Vercel link returns an error (500), so we deployed on Render instead |

## How the answers were checked

- Every number in the notebook text was compared with the output of the code above it. Where they differed, the text was corrected.
- Cleaning methods were tested before use (for example, the ZIP imputation was tested on hidden ZIP codes: 92% and 73% correct).
- The website was tested with automatic tests (`tests/`) and a headless browser.
