# PP_Power-BI_California-Schools-Data

The data for this project is courtesy of [CTU Relational Dataset Repository](https://relational.fel.cvut.cz/dataset/CDESchools) which sourced it from [2016.padjo.org](http://2016.padjo.org/tutorials/sqlite-data-starterpacks/#toc-california-school-sat-performance-and-poverty-data). 

The data was collated from 3 datasets provided by the California Department of Education ([link](https://www.cde.ca.gov/)) :
- School Directory
- Free-or-Reduced-Price-Meal Eligibility Data
- Postecondary Preparation (SAT) Test Results

I chose this dataset because I wanted to practice on real data, and also to have a go at testing something I once heard from one of my Econometrics professors. He was warning us about confounding variables and the example he gave was a study that linked "IQ" with future income, but whose effect vanished once the parent income was controlled for. He didn't cite the specific study - which in hindsight, I should have asked for. From what I've learned since, there is no shortage of evidence for the effect of generational wealth on success, may it be financial or academic.

Even with this prior knowledge, I was still a bit shocked to observe the strong linear relationship in this particular dataset. Along the way, I also had fun using Power BI Parameter feature to make this exploration more interactive.

![Video](https://github.com/plklinh/PP_Power-BI_California-Schools-Data/blob/main/images/FRMP-SAT-Scores.mov)

## Data 
The original data consists of 3 tables:
- schools: School Directory
- frmp: Free-or-Reduced-Price-Meal Eligibility Data
- satscores: SAT Test Results

To avoid affecting CTU's database, I chose **Import** mode instead of Direct Query. There wasn't much remodelling required, because the original data collector already linked the tables with a GUID.

The brief cleaning I had to do in PBI M Query consisted of the following:
- **Remove columns to reduce redundancy**: Some data i.e. School Name, School District... was duplicated across the tables, so I deleted them and left only the data in the main schools table.
- **Filter out schools closed before school year 2014-205**: The FRMP data only has data for academic year 2014-2015. Since I wanted to focus on this, I filtered out shools closed prior to reduce model size.
- **Derive addtional metrics**: I calculated the percentage of test takers versus the number of 12th graders enrolled, thinking that maybe poverty would also affect SAT participation. I ended up with some values over 100% suggesting either data entry errors, or that some non-12th graders also took the SAT.
- **Rename columns and tables for consistency and readability**

## Getting Started

You can download the PBIX file and explore the model and dashboard.

To connect to the data source, please follow below steps:

1. **Download MariaDB Connector for Power BI**: PBI doesn't include any MariaDB connector out of the box. It took some fiddling for me, but I eventually got it to work on my Windows VM instance.
2. **Connect to CTU MariaDB database from Power BI**: Follow the instructions here [link](https://relational.fel.cvut.cz/dataset/CDESchools). I suggest using Import mode to not affect their DB.
