# Find seminal papers on google scholar

It's quite frustrating to search a key word on Google Scholar and not know which papers are the seminal papers in the particular field. Also, Google scholar search is limited to the specific key words you put in. In my manual literature review process, I find myself clicking through the "cited by" articles, and finding out who has cited these. This code aims to automate the search for good papers and finding top 1-5 papers per year of a specific topic. 

The goal of this is to not just aggregate results of the given search keyword but to also extend it to potentially related keyword searches to find seminal papers. For example, "object tracking" does not give me results for a seminal paper that is titled "Simple Online Realtime tracking". However if I simply search "tracking", the first result on google scholar returns "tracking hurricanes". 

This code has been adapted from the [repository](https://github.com/WittmannF/sort-google-scholar) by WITTMANN, Fernando Marcos.  

**Limitations:**
- This code can't handle robot captchas so try not to overuse the search function.
- Selenium is used to handle robot checking; you might be asked to manually solve the first captcha when retrieving the content of the pages

**TODO**
- Right now the program only does search by keyword; extend the application to search by cited articles to get more relevant papers that don't have those specific search keywords. 


### Usage of `sortgs.py`
```
usage: sortgs.py [-h] [--kw KEYWORD] [--sortby SORTBY] [--nresults NRESULTS]
                 [--csvpath CSVPATH] [--notsavecsv] [--plotresults]
                 [--startyear STARTYEAR] [--endyear ENDYEAR]

Example: $python sortgs.py --kw 'deep learning'

optional arguments:
  -h, --help            show this help message and exit
  --kw KEYWORD          Keyword to be searched. Default is 'machine learning'
                        Use double quote followed by simple quote to search 
			for an exact keyword. Example: "'exact keyword'"
  --sortby SORTBY       Column to be sorted by. Default is by the columns
                        "Citations", i.e., it will be sorted by the number of
                        citations. If you want to sort by citations per year,
                        use --sortby "cit/year"
  --nresults NRESULTS   Number of articles to search on Google Scholar.
                        Default is 100. (carefull with robot checking if value
                        is too high)
  --csvpath CSVPATH     Path to save the exported csv file. By default it is
                        the current folder
  --notsavecsv          By default results are going to be exported to a csv
                        file. Select this option to just print results but not
                        store them
  --plotresults         Use this flag in order to plot the results with the
                        original rank in the x-axis and the number of citaions
                        in the y-axis. Default is False
  --startyear STARTYEAR
                        Start year when searching. Default is None
  --endyear ENDYEAR     End year when searching. Default is current year
```

### Example
The following code will search for the top 100 results, rank by number of citations and save as a .csv file (same name of the keyword):
```
$python sortgs.py --kw "machine learning"
```

Sorted by number of citations per year (**HIGHLY RECOMMENDED**):
```
$python sortgs.py --kw "machine learning" --sortby "cit/year"
```

From 2005 to 2015:
```
$python sortgs.py --kw "machine learning" --startyear 2005 --endyear 2015
```

Save results under a subfolder called 'examples'
```
$ python sortgs.py --kw 'neural networks' --csvpath './examples/'
```

Example of output while running:
```
Loading next 10 results
Robot checking detected, handling with selenium (if installed)
Loading...
Solve captcha manually and press enter here to continue...
year not found, appending 0
Loading next 20 results
Robot checking detected, handling with selenium (if installed)
Loading next 30 results
Robot checking detected, handling with selenium (if installed)
Loading next 40 results
```

### Installation
1. Install Python 3 and its dependencies from **Requirements** (suggestion: use Ananconda https://www.anaconda.com/distribution/)
2. Download the repository. Two ways to do this:
    - Use the command `git clone https://github.com/darrenjkt/find-papers-google-scholar.git` in your terminal (if linux/MAC) or CMD (if windows)
3. Open the folder of sortgs on your terminal (if linux/MAC) or CMD (if windows)
4. Use the provided jupyter notebook or simply`python sortgs.py --kw "your keyword"` (replace "your keyword" to any keyword that you'd like to search)
6. A CSV file with the name `your_keyword.csv` should be created. 

### Requirements
If you install anaconda, all of those requirements (except selenium) are going to be met:
- Python 2.7 or Python 3
- Install from the requirements file: `pip install -r requirements.txt`

Highly suggested, if having problems with robot checking:
- ChromeDriver: http://chromedriver.chromium.org/
    - After downloading chromedriver, rename it to `chromedriver` and add it in a folder accessible by the PATH (Example: your python directory. Mine is at `/Users/.../anaconda/bin/`)
