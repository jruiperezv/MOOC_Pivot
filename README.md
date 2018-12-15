# The MOOC Pivot: Supplementary material

This repository includes supplementary material to facilitate the replication of the data analysis presented in the Science paper titled as "The MOOC Pivot: From Teaching the World to Online Professional Degrees" with ID "10.1126/science.aav7958" co-authored by Justin Reich and José A. Ruipérez Valiente.


## Data request

MITx and HarvardX learner data are treated as student data meriting FERPA protections. MITx data can be requested at [http://web.mit.edu/ir/mitx/](http://web.mit.edu/ir/mitx/) and HarvardX data at [https://vpal.harvard.edu/vpal-research-request](https://vpal.harvard.edu/vpal-research-request). You should request the *person_course* course dataset containinig the 565 courses included in this analysis from 2012 to May 2018. The specific *course_id's* that you need to request are in the [*course_metadata*](course_metadata.csv) file. You should request the following columns for the *person_course* dataset: 

```
['course_id', 'user_id', 'cc_by_ip', 'roles', 'mode', 'viewed',
'explored', 'completed', 'certified', 'prs_reason_lc', 'prs_intent_verified',
'prs_intent_lecture', 'prs_intent_assess', 'prs_intent']
```

## Description of variables

More information about the *person\_course* dataset is available in the [following paper](https://dl.acm.org/citation.cfm?id=3053980) that explains *edx2bigquery* framework. The definition of the columns required for this paper are the following (all items with *prs* prefix are survey questions):

* *course\_id*: Course ID in the standard format as org/number/semester.
* *user\_id*: Internal ID of the user.
* *cc\_by\_ip*: Two-letter country code corresponding to the modal IP address
* *roles*: Roles played by the user in the course, 'Student' or 'Staff'
* *mode*: Mode of registrant, e.g. honor, audit, verified.
* *viewed*: Boolean flag, indicating that the user visited the course at least once.
* *explored*: Boolean flag, indicating that the user viewed at least half ofthe chapters of the course.
* *completed*: Boolean flag, indicated that the user completed the course byachieving a final grade above the overall passing threshold for the course(*grade >= passing_grade*)
* *certified*: Boolean flag, indicating that the user earned a certificate in the course.
* *prs\_reason\_lc*: User-provided; People register for HarvardX courses for different reasons. Which of the following best describes you? Possible values:	- 0 = Have not decided whether I will complete any course activities.	- 1 = Here to browse the materials, but not planning on completing any course activities (watching videos, reading text, answering problems, etc.).	- 2 = Planning on completing some course activities, but not planning on earning a certificate.	- 3 = Planning on completing enough course activities to earn a certificate.
* *prs\_intent\_verified*: User-provided; Do you intend to earn a verified certificate?	- -999 = Viewed question but did not answer	- Null = Did not view this question (incomplete survey)	- -1 = Unsure	- 0 = No	- 1 = Yes
* *prs\_intent\_lecture*: User-provided; How many course lectures do you intend to complete?	- -999 = Viewed question but did not answer	- Null = Did not view this question (incomplete survey)	- 0 = No lectures	- 1 = A few lectures	- 2 = Most lectures
* *prs\_intent\_assess*: User-provided; How many course assessments (quizzes, tests, etc.) do you intend to complete?	- -999 = Viewed question but did not answer	- Null = Did not view this question (incomplete survey)	- 0 = No assessments	- 1 = A few assessments	- 2 = Most assessments
* *prs\_intent*: User-provided; Which statement best describes your plan for taking this course? 
	- -999 = Viewed question but did not answer	- Null = Did not view this question (incomplete survey)
	- 0 = I am not sure yet	- 1 = I plan to just browse this course	- 2 = I plan to take some parts of this course	- 3 = I plan to take this course from start to finish

## Other data

The repository contains two other data sources:

* *course_metadata*: Contains metadata from the courses
	* *course_id*: Course identifier.
	* *semester*: Semester (Fall, Spring, Summer) and year when the course took place.
	* *year*: Operating year for the analysis computed based on the following function:

```
def defineYearBasedSemester(semester):
    year = None
    if(semester in ['Fall 2012','Spring 2013']):
        year = 'Year 1'
    elif(semester in ['Summer 2013', 'Fall 2013', 'Spring 2014']):
        year = 'Year 2'
    elif(semester in ['Summer 2014', 'Fall 2014', 'Spring 2015']):
        year = 'Year 3'
    elif(semester in ['Summer 2015', 'Fall 2015', 'Spring 2016']):
        year = 'Year 4'
    elif(semester in ['Summer 2016', 'Fall 2016', 'Spring 2017']):
        year = 'Year 5'
    elif(semester in ['Summer 2017', 'Fall 2017', 'Spring 2018']):
        year = 'Year 6'
    return year
```

* *country_metadata*: Contains metadata from each country. These data contain the 2018 Human Development Indices and Indicators from the United Nations (UN). More info available in this [link](http://hdr.undp.org/sites/default/files/hdr2018_technical_notes.pdf).
	* *name*: Name of the country.
	* *alpha-2*: Two-letter ISO code of the country.
	* *region*: Region of the country.
	* *sub-region*: Sub-region of the country.
	* *human\_development\_index*: It is a country composite measure provided by the UN based on three dimensions: health, knowledge and general quality of living.
	* *human\_development\_category*: Human development category provided by the UN with a set of values of low, medium, high and very high human development.


## Reproducing the analysis

The repository includes an IPython notebook with the metada files *course\_metadata.csv* and *country\_metadata.csv*. Once you request from MITx and HarvardX the person_course dataset with the indicated columns, name that file in the same folder than others as *person\_course.csv* and you should be able to proceed and reproduce the analysis with the script *MOOC\_Pivot.ipynb*. The code has been released under MIT license.

## Contact

For general questions about this research or access to data reach out to the corresponding author Justin Reich (<jreich@mit.edu>). For questions about data analysis and its reproducibility reach out to José A. Ruipérez Valiente (<jruipere@mit.edu>).




