---
title: Project Proposal - Clinical Trials
feature_text: |
  ## Projects in CS
  A website to document my progress on my project!
feature_image: "https://picsum.photos/1300/400?image=430"
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

### Why React?

- Responsive user interface for website, web and mobile app
- Flexible - can easily create web apps and transform them into mobile apps
- Easy to learn
- Fast - you can start development instantly, and provides resources for developing reusable and easily integrable UI components that reduce development time
- Great documentation - broad community support

### Why use RESTful API over GraphQL?

- A fixed set of resources and endpoints (Web URL Structure: domain/condition/trial name/number): RESTful APIs have a clear structure, with resources being identified by URIs and accessed using standard HTTP methods. This makes it easy to understand how the API works and how to interact with it, which is particularly useful when the resources and endpoints are well-defined and unlikely to change.
- Support caching: RESTful APIs rely on standard HTTP caching mechanisms, which makes it easy to cache responses and improve performance. Caching is not built-in to GraphQL, but can be implemented with additional libraries.

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
