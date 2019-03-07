Define the core message or hypothesis of your project.
    - Hypothesis: There is a positive correlation between inclimate weather and the popularity of taxis
Describe the questions you asked, and why you asked them
    - Are more taxi trips taken on a clear weather day as opposed to an inclimate weather day?
    - Do people take fewer or more taxi trips when it's really cold and really hot than when it's a comfortable temperature?
    - Do people take fewer or more taxi trips when it's raining or snowing than when it isn't?
Describe whether you were able to answer these questions to your satisfaction, and briefly summarize your findings
    - We were able to answer the questions with some degree of certainty. 
    - More trips are not necessarily taken on clear weather days alone, however more trips ARE taken on days without precipitation and days with a comfortable temperature


Questions & Data
    Elaborate on the questions you asked, describing what kinds of data you needed to answer them, and where you found it
            ##  Are more taxi trips taken on a clear weather day as opposed to an inclimate weather day?
                    - Needed historical weather data for the days and locations that we had taxi trip data for
                    - Found the weather data from the Dark Sky API
                    - Grouped the weather conditions into clear, cloudy, partly cloudy, rain, and snow
            ## Do people take fewer or more taxi trips when it's really cold and really hot than when it's a comfortable temperature?
                    - Used the temperature data from the Dark Sky API and binned the data in groupings of temperatures
            ## Do people take fewer or more taxi trips when it's raining or snowing than when it isn't?
                    - Similiar to the first question, grouped the weather types and viewed trips taken

Data Cleanup & Exploration
    Describe the exploration and cleanup process
        - One of the biggest hurdles was just getting the data from the Dark Sky API. Re-calling the API every time our keys refreshed and making sure not to call the API for data we already had
        - Extracted a random 50,000 entries from over 101M rows in the original csv file with the bash shuf -n command. Excel couldn't even open the original file and VSCode could only open it after re-allocating more memory to the program
        - Several columns we didn't need (like Taxi ID and drop off location -- we only cared about where people called the cab / got picked up)
        - Trip ID was a column that we used as a unique identifier to join the weather data to the trip data
            - Called the weather data for each Trip ID's location and time
        - Created a master dataframe and made some summary CSVs from it so we could call the data easily in other scripts
    Discuss insights you had while exploring the data that you didn't anticipate
        - At first we didn't want to believe that our hypothesis was dead wrong, but we kept adding more and more data after calling to the weather API and found the exact opposite of our hypothesis to be true. 
            - More trips were taken during nice weather with no precipitation than during bad weather.
    Discuss any problems that arose after exploring the data, and how you resolved them
            - We couldn't be sure of the distribution of the different types of weather for the time period we examined -- we only had weather data for our specific time periods of taxi rides
            - Essentially the problem was because our API calls were limited. If we could've gotten data from Dark Sky for every few hours for every day in a specific time period when taxi trips were taken, then we could normalize how many trips we expected to see against how many we actually saw
    Present and discuss interesting figures developed during exploration, ideally with the help of Jupyter Notebook
        - Show figures in the images folder

Discussion
    Discuss your findings. Did you find what you expected to find? If not, why not? What inferences or general conclusions can you draw from your analysis?
        - We didn't find what we expected at all -- just the opposite, in fact. We found more taxi trips were taken on clear days than on days with bad weather.
        - Possibly conclude that people take more taxi trips on clear days because they're going out and doing more things on days with good weather
        - Possibly don't want to take cabs in bad weather because many times public transit will be faster (The El has dedicated transit lines as opposed to sharing lanes of traffic like taxis)
        - Possibly people are in better moods and willing to spend more money for a cab on days with good weather?
        - Can't be very sure about the implications without more research, but it's definitely a starting point for more analysis

Post Mortem
    Discuss any difficulties that arose, and how you dealt with them
        - Data normalization problem mentioned earlier
        - Limited number of API calls
        - Had to change our scope from ride sharing apps to taxis
            - Possibly this could be totally different for Uber and Lyft given how disruptive they've been to the taxi industry
            - Also possible they could show exactly the same thing, which may reinforce some of the possible conclusions above about how weather influences how people use cab services
    Discuss any additional questions that came up, but which you didn't have time to answer: What would you research next, if you had two more weeks?
        - With more time, we'd dedicate a good chunk of it to getting more API keys and getting more weather data so we could make more accurate analyses
        - Examine data by year, month, day of the week, etc. at a more granular level. 
            - Did people take more cabs before Uber starting getting really popular in 2013-2014? Did they take fewer taxis after? Was weather a bigger or small factor when Uber / Lyft were available?
        - Did people take longer / shorter trips during more severe or more "ideal" weather?
        - What correlations, if any, exist in the data as far as tips go?
            - Not shocking to see that out of 50,000 rows of data we had only 4 entries had listed a non-zero amount when the payment type was cash as opposed to credit