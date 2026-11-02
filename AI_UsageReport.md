# Report on AI Usage
## Introduction
I was mainly using ChatGPT to help me with this project. I used it to help me find a suitable dataset in both Kaggle and on the web. I also used it for writing Python code, web scraping, data merging code, visualisations and troubleshooting errors. I used AI search on Google for help on how to format a Jupyter notebook, especially for font sizes. ChatGPT was really useful to me for understanding errors and how to set up my Python environment as well.

There were some things AI was not helpful for. The biggest challenge was accessing the Smithsonian website for web scraping. It kept returning the HTTP 403 Forbidden error. I tried using ChatGPT to help me bypass it but even though it suggested multiple solutions, none of them worked. I tried changing th HTTP headers and using Selenium but I was unable to bypass Cloudflare. I eventually saved the webpage manually through Chrome and used BeautifulSoup to extract the data.

### Finding a Suitable Dataset
Prompts used:
- "I need to merge a dataset and some web scraped data together. An example is pokemon cards dataset and website about pokemon cards. The website can't be wikipedia. The dataset needs to be from Kaggle. Find a topic I can do it on."

- "Find something with genuine data."

- "Do the websites have the right columns of data and are they relevant for more than 10% of the rows in the Kaggle dataset?"

- "Search for suitable topics please. The Kaggle dataset needs to be at least arounf 1,000 rows too."

- "923 records are ok, expand on the volcano topic."


ChatGPT suggested several topics like LEGO sets, books, movies, university rankings and volcanoes. I decided to pick the volcano dataset from Kaggle and the Smithsonian Global Volcanism Program website since it seemed the most likely to have a unique identifier that can be used to merge both datasets.

### Web Scraping

Prompts used:
- "Tell me how to scrape."

- "I need to be able to inspect the page with Chrome Developer Tools so I know what I'm trying to extract. Fetch the page using urllib and extract the data using Beautifull Soup."

- "Read the screenshots" (Google Developer Tools screenshots to identifiy the HTML table inside a div with the class VolcanoListTable. The HTML contained table rows (tr), cells (td) and hyperlinks with unique volcano numbers.)

- "This is a piece of example my lecturer used:
http.client._MAXHEADERS = 1000
request=urllib.request.Request(url)

- "HTTPError                                 Traceback (most recent call last) 
/tmp/ipykernel_1808/697176521.py in <cell line: 0>()       7 request.add_header("User-Agent", "UniversityResearchProject/1.0")       8  ----> 9 response = urllib.request.urlopen(request, timeout=30)      10       11 raw_html = response.read()  
5 frames
/usr/lib/python3.13/urllib/request.py in http_error_default(self, req, fp, code, msg, hdrs)     611 class HTTPDefaultErrorHandler(BaseHandler):     612     def http_error_default(self, req, fp, code, msg, hdrs): --> 613         raise HTTPError(req.full_url, code, msg, hdrs, fp)     614      615 class HTTPRedirectHandler(BaseHandler):  
HTTPError: HTTP Error 403: Forbidden"

- "How do I use the google inspect developer tools to know how to bypass?"

- "response server is cloudflare"

- "Find a way to use urllib to fetch the website directly over HTTPS."

- volcanos.xlsx Kaggle file

- "HTTP error: 403
Page title: Smithsonian request verification
Smithsonian request verification Request verification Please continue when verification is complete. Enable JavaScript and cookies to continue Smithsonian Institution Privacy Terms of Use"

- "Use Selenium"

- "Running cells with '.venv (3.11.9) (Python 3.11.9)' requires the ipykernel package. Install 'ipykernel' into the Python environment."

- "--------------------------------------------------------------------------- InvalidSessionIdException                 Traceback (most recent call last) Cell In[4], line 3       1 url = "[https://volcano.si.edu/volcanolist_holocene.cfm](https://volcano.si.edu/volcanolist_holocene.cfm)"       2  ----> 3 driver.get(url)       4        5 print(driver.title)  File \~\OneDrive - Technological University Dublin\3rd Year\VS Code\Python\\.venv\Lib\site-packages\selenium\webdriver\remote\webdriver.py:586, in WebDriver.get(self, url)     573 def get(self, url: str) -> None:     574     *"""Navigate the browser to the specified URL.*     575      576 *    The method does not return until the page is fully loaded (i.e. the*    (...)    584 *        \`driver.get("[https://example.com](https://example.com)")\`*     585 *    """* --> [586](https://file+.vscode-resource.vscode-cdn.net/c%3A/Users/nimmy/OneDrive%20-%20Technological%20University%20Dublin/3rd%20Year/VS%20Code/Python/~/OneDrive%20-%20Technological%20University%20Dublin/3rd%20Year/VS%20Code/Python/.venv/Lib/site-packages/selenium/webdriver/remote/webdriver.py:586)     self.execute(Command.GET, {"url": url})  File \~\OneDrive - Technological University Dublin\3rd Year\VS Code\Python\\.venv\Lib\site-packages\selenium\webdriver\remote\webdriver.py:566, in WebDriver.execute(self, driver_command, params)     563 response = cast(RemoteConnection, self.command_executor).execute(driver_command, params)     565 if response: --> [566](https://file+.vscode-resource.vscode-cdn.net/c%3A/Users/nimmy/OneDrive%20-%20Technological%20University%20Dublin/3rd%20Year/VS%20Code/Python/~/OneDrive%20-%20Technological%20University%20Dublin/3rd%20Year/VS%20Code/Python/.venv/Lib/site-packages/selenium/webdriver/remote/webdriver.py:566)     self.error_handler.check_response(response)     567     response["value"] = self.\_unwrap_value(response.get("value", None))     568     return response 
...
	(No symbol) [0x7ff7506dd364] 	(No symbol) [0x7ff7506c644c] 	(No symbol) [0x7ffb2823dda7] 	(No symbol) [0x7ffb29c3ee4c]"

- "The webpage asks for human verification and then doesn't load even when I click 'Verify that you are human'."

- "the Smithsonian volcano table opens successfully when you visit the website in your normal Chrome browser, without Selenium"

- "Rows found: 1214"

- "79.51%. how do i import to github?"


I asked ChatGPT to help me with Python code for extracting the volcano data from the website. I asked it originally for code using urllib.request to retrieve the webpage and BeautifulSoup for extraction but ChatGPT suggested using Selenium when that didn't work due to Cloudflare security. When Selenium didn't work either, ChatGPT suggected saving the webpage and using that for the project.

ChatGPT guided me through using the Chrome Develper Tools to identify the HTML table inside a div with the class VolcanoListTable. The HTML contained table rows (tr), cells (td) and hyperlinks with unique volcano numbers.

After finding the HTML structure, I used the AI-generated code to extract the volcano number, name, country, volcanic region, landform and eruption evidence.

AI also helped me set up Jupyter Notebook in VS Code, select a Python environment and install the required libraries. I was getting errors with missing Python packages, pip installation and Powershell commands. ChatGPT explained the causes and provided the commands to resolve them.

### Writing Code for Data Visualisations
Prompts used:
- "These are the questions I want to answer: Which countries have the most volcanoes? Which types of volcanoes are most common? How do eruption-evidence classifications differ between the older Kaggle data and the current website? Have any volcanoes changed classification or recorded eruption status?"
- "What are other potential questions I can answer?"

