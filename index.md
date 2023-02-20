---
title: Project Proposal - Clinical Trials
feature_text: |
  ## Projects in CS
  A website to document my progress on my project!
feature_image: "https://picsum.photos/1300/500?image=430"
---

{% include button.html text="Github" icon="github" link="https://github.com/jz3453" color="#00916e" %}

## Introduction / Background

**Clinical trials** are a type of research that studies new tests and treatments and evaluates their effects on human health outcomes. Enrolling in a clinical trial can be extremely beneficial for both patients with chronic conditions and healthy volunteers.

> “For those suffering from a chronic condition, enrolling in a clinical trial may offer options that might be unavailable otherwise and it also presents an opportunity to have access to top notch medical care as well as being a unique way of contributing to the advancement of medical knowledge. For healthy volunteers, knowing that others may benefit from their efforts can be very rewarding, and participating in clinical research can sometimes uncover health problems that people are not aware of.” 
> ~ Tesheia Johnson, executive director of the Yale Center for Clinical Investigation

Unfortunately, the challenges in clinical trials usually aren’t discussed as much as the results themselves. One of the biggest challenges is faced just before starting clinical trials: patient recruitment. [Around 80% of these studies are either halted or even closed due to low patient recruitment](https://www.clinicaltrialsarena.com/features/featureclinical-trial-patient-recruitment/). One reason for this is the specific requirements of the trial. Each disease area has a unique patient base for clinical trials, and finding the right patients is often a huge challenge.

Moreover, NIH focus groups in 2011 found that many members of the general public lacked familiarity with clinical trials and were unaware of opportunities for participation by healthy volunteers. This lack of awareness has certainly been a contributing factor to the fact that only 4% of Americans have ever been involved in a clinical trial.

## Goals and Objectives

**Motivation**: Improve patient recruitment for clinical trials & provide medical information in a more colloquial way.

- Build a website for users to find interested clinical trials easily.
- Recommend clinical trials updates and news to users.

**How will our product be different from existing products?**

- Aggregate trial information in one central site and provide live updates to make trial progresses easier to follow
  - Keep track of new papers with references to trials/studies on our site
- Provide more digestible information for people unfamiliar with medical jargon. A major cause of low enrollment is the lack of understanding about what’s involved in clinical research and why it’s important to participate
- Personalization features
  - Allow users to set up a profile and follow medical topics/trials of interest so that they are notified if any updates occur
  - Also give recommendations based on user profile

## Data / Resources

- Clinical Trials
  - [https://clinicaltrials.gov/](https://clinicaltrials.gov/)
  - [https://clinicaltrials.gov/ct2/resources/download](https://clinicaltrials.gov/)
- News/Articles
  - PubMed
  - MedRxiv
  - Healthcare news sites
- Taxonomy
  - SNOMED
  - MeSH (https://meshb.nlm.nih.gov/treeView)
- Connection in the medical field: Dr. Song


## Tech for frontend

- React for user interface
- API Gateway to handle requests and responses
- AWS Lambda for the backend logic to fetch data from DynamoDB

## Background Research
### Front-End Framework: Why React?
Other front-end frameworks: Vue.js, Ember.js, or Angular.js
- Responsive user interface for website, web and mobile app
- Flexible - can easily create web apps and transform them into mobile apps
- Easier to learn
- Fast - you can start development instantly, and provides resources for developing reusable and easily integrable UI components that reduce development time
- Great documentation - broad community support

### Why use RESTful API over GraphQL?

- A fixed set of resources and endpoints (Web URL Structure: domain/condition/trial name/number): RESTful APIs have a clear structure, with resources being identified by URIs and accessed using standard HTTP methods. This makes it easy to understand how the API works and how to interact with it, which is particularly useful when the resources and endpoints are well-defined and unlikely to change.
- Support caching: RESTful APIs rely on standard HTTP caching mechanisms, which makes it easy to cache responses and improve performance. Caching is not built-in to GraphQL, but can be implemented with additional libraries.

### Why use REST API over HTTP API (both offered by AWS API Gateway)?
*Development:*

<img width="518" alt="Screen Shot 2023-02-05 at 2 57 18 PM" src="https://user-images.githubusercontent.com/97906628/216841765-dad605b7-f1d5-40b2-b3a5-612a871ca0fc.png">

*Integrations:*

<img width="646" alt="Screen Shot 2023-02-05 at 2 58 20 PM" src="https://user-images.githubusercontent.com/97906628/216841817-f9f97219-21cc-4ecf-b823-2323a2bc6b72.png">

### Why AWS?

- Wide range of services: AWS offers a wide range of services, including storage, databases, analytics, machine learning, and more. This means that you can find the services you need to build and run your application in one place, and that you can easily integrate them together.
- Scalability: AWS allows you to easily scale up or down your resources as needed, which means that you can handle sudden spikes in traffic or usage without having to make significant investments in infrastructure.
- Cost-effectiveness: AWS provides a pay-as-you-go pricing model, which means that you only pay for what you use.
- Most familiar to us :)

## Timeline for Front-End

- By early February: have Home Page ready (using dummy data).
- By mid-February: have an MVP ready.
  - Web Pages (Web URL Structure: domain/condition/trial name/number)
  - Home Page: List of conditions and number of trials per condition (set limit at first - later add pagination)
  - Condition Pages: list of trials
  - Trial Pages: details of each trials
- By end of February: allow pagination
- By early March: add basic filters.
  - Country (Home page and Condition Page)
  - Only Recruiting and not yet recruiting studies
- By end of March: add search bar to allow for user queries, and map to database.
- By end of April: add personalization features & more filters.
  - Subscription form
  - User profile page
  - Notification features
- By end of April: add caching?? Elasticache?


# Brainstorm Session: How will our Data be stored in DynamoDB?
![Scratch Paper-1](https://user-images.githubusercontent.com/97906628/218331572-1c9c5b9f-5827-4e1f-bf76-b043ee6add00.jpg)

![Scratch Paper-3](https://user-images.githubusercontent.com/97906628/218331590-20497865-71ab-4890-af4e-a4a719f35957.jpg)


## Background: How to Integrate REST API on API Gateway with Lambda
There are two methods to create an API with Lambda integration, via Lambda proxy integration or Lambda non-proxy integration.

### Lambda Proxy Integration
The Lambda proxy integration allows the client to call a single Lambda function in the backend. 

In Lambda proxy integration, when the client makes a request, the API Gateway forwards the request to Lambda without transforming/modifying it. When a client submits an API request, API Gateway passes to the integrated Lambda function the raw request as-is. This request data includes the request headers, query string parameters, URL path variables, payload, and API configuration data. 

> Notes: This is helpful in my project in that I can easily access the URL path variables by parsing event.path to retrieve information on what page the user wants to pull up. (Web URL Structure: domain/condition/trial name/number)
> ![Screen Shot 2023-02-12 at 2 00 35 PM](https://user-images.githubusercontent.com/97906628/218331323-d992f10d-796c-4c1d-bf8a-1667145d13f7.png)


For API Gateway to pass the Lambda output as the API response to the client, the Lambda function must return the result in this format.
![Screen Shot 2023-02-12 at 1 54 47 PM](https://user-images.githubusercontent.com/97906628/218331021-896f2818-8414-48f1-905c-b661066ef0e3.png)

> Notes: The response body must be a string, whereas I want to return data from the DynamoDB table as a JSON response.
> Update: Was informed that you can convert JSON to string using stringify() then back with JSON.parse(). However, I'm a little concerned about any data getting "mistranslated".

### Lambda Non-Proxy Integration
In Lambda non-proxy integration, when the client makes a request, the API Gateway is able to transform it and then forwards it to the lambda. Similarly, when the response data comes from the lambda function to the API Gateway, it sets the header, status code etc.

Lambda function for the Lambda custom integration only takes input from the API Gateway API integration request body, provided that API Gateway maps the required API request parameters to the integration request body before forwarding the client request to the backend. For this to happen, the API developer must create a mapping template and configure it on the API method when creating the API.

![Screen Shot 2023-02-12 at 1 58 36 PM](https://user-images.githubusercontent.com/97906628/218331219-60c62782-ef47-4e97-bde8-c3832eefd321.png)

The function can return an output of any JSON object, a string, a number, a Boolean, or even a binary blob. 

> Notes: According to [StackOverflow](https://stackoverflow.com/questions/42474264/lambda-integration-vs-lambda-proxy-pros-and-cons), Lambda Non-Proxy Integration involves a lot more of work to set it up, but it allows the developer to decouple what the lambda receives and returns, and how it gets mapped to different HTTP status codes, headers, and payloads.
> According to Rick Haffey, "Using Proxy Integration forces (at least a subset of) that responsibility onto the Lambda function. (i.e. knowing how to interpret and decide on HTTP headers, query parameters, status codes, etc.). In doing that, I feel that it muddies the responsibility of the backing Lambda function -- Lambda now needs to both handle whatever "business" logic it's being called to do, and also handle interpreting the incoming HTTP values and decide on the outgoing HTTP response values."
> Also what my supervisor said :).
> In the long run, most developers seem to prefer non-proxy integration over proxy integration, so I would rather set it up now rather than use proxy integration and have to rebuild the API later.

## Update to Timeline:
Dedicate entire month of February to building out home page, condition pages, and trial pages.

## Progress Update (2/16 1:14AM):
Something that took me a *looooooong* time to figure out on the backend: *THE CORS ERROR*.
Solution: Simply clicking Enable CORS under Resource Options on API Gateway does not always work. You may need to go in and manually add in the headers under Method Response and the Header Mappings under Integration Response.
![Screen Shot 2023-02-16 at 10 22 31 PM](https://user-images.githubusercontent.com/97906628/219541744-190e76e1-78b4-4514-a916-db8b649fad1c.png)
![Screen Shot 2023-02-16 at 10 23 00 PM](https://user-images.githubusercontent.com/97906628/219541754-2d097f61-f047-4b5d-ab5e-a09befa73f74.png)

Scrapped and rewrote code to "component-ize" my code better. Also learned how to use the React Router ([tutorial](https://upmostly.com/tutorials/how-to-pass-param-to-a-component-in-react-router#:~:text=React%20Router%20v6%20has%20made,pass%20props%20to%20the%20component.
)).

React Router enables "client side routing". Client side routing allows your app to update the URL from a link click without making another request for another document from the server. Instead, your app can immediately render some new UI and make data requests with fetch to update the page with new information. [article](https://reactrouter.com/en/main/start/overview)

I used the Router to allow for switching between the ConditionPage and TrialPages.
<img width="838" alt="Screen Shot 2023-02-16 at 1 24 40 AM" src="https://user-images.githubusercontent.com/97906628/219285415-58f98cbb-2e25-49a3-97f2-c85211fc423d.png">

It reroutes correctly when I click on a condition to bring up all the trials related to that condition, but the trial page is not being generated.
> This was because I was using async so that I could await fetch() data from my API. When I deleted the asynchronous components and instead just hardcoded in the list, the page generated.

Task: Figure out how to use Async/Await in the functional component React.js

### New Feature Alert:
Add tree structure to show related mesh term taxonomy.
Something like this:
<img width="568" alt="Screen Shot 2023-02-16 at 1 16 02 AM" src="https://user-images.githubusercontent.com/97906628/219283862-f0b7053e-21d8-4236-85c5-27c3fdadc5a7.png">

[link](https://mui.com/material-ui/react-tree-view/)

Task: Think about how to dynamically build such tree given a trial. Also keep in mind that a trial could fit along multiple paths in the tree.


## Progress Update (2/16 10:11PM):
Task Completed: Figured out how to "make" (more like fake) an asynchronous call in a functional component: using useEffect() and fetch().
![Screen Shot 2023-02-16 at 10 14 25 PM](https://user-images.githubusercontent.com/97906628/219540507-0c75bba3-6d94-4997-be04-e6b8e3b41d05.png)

[tutorial](https://www.freecodecamp.org/news/fetch-data-react/)

## Update on Using React (2/19 5:40PM):
In the process of exploring some of the Components offered by MUI.

Import these packages:
@mui/material, @mui/icons-material, @emotion/styled, @emotion/react

### Using these MUI Components:
* [AppBar](https://mui.com/material-ui/react-app-bar/)
* [Drawer](https://mui.com/material-ui/react-drawer/)
* [Menu](https://mui.com/material-ui/react-menu/)

### Progress Check:
**Timestamp 8:22PM**
Finished building out the Primary App Bar with a Search Bar & Icons.
![Screen Shot 2023-02-19 at 8 24 02 PM](https://user-images.githubusercontent.com/97906628/219988783-d25185e9-c656-4bdb-9841-c6bd1da320ac.png)

Accounted for Mobile Rendering to make App Bar flexible for Desktop and Mobile viewing.
![Screen Shot 2023-02-19 at 8 25 52 PM](https://user-images.githubusercontent.com/97906628/219988933-e29df8ed-71ef-4bbd-b016-e5028cae76f8.png)

Included Menu dropdown when Profile Icon is clicked.
![Screen Shot 2023-02-19 at 8 27 25 PM](https://user-images.githubusercontent.com/97906628/219989116-d69d66b8-e1d8-4fd7-b4cb-bc39e9a444eb.png)


