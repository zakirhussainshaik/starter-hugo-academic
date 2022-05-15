---
title: Integrating GraphComment to Wowchemy Static Website
date: 2022-05-15T07:15:32.303Z
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
This article summarizes the steps I have followed to add comments to my static website using [GraphComment](https://graphcomment.com/en/). My choice to go with GraphComment primarily is due to two following reasons:

1. It has a free basic plan, which is immensely useful for a technical website such as this which hardly expects heavy traffic.
2. This being a European based company, they will comply with GDPR regulations.

Now I will list down the steps I have followed for integrating this service with the wowchemy theme built using Hugo.

1. First, go to the [GraphComment](https://graphcomment.com/en/) website and create your account.
2. Next select *add a new website* option.  Enter the *Site Name* (it is just a label/tag to choose the specific website from the list if in case you have many websites), *Unique ID* (this is the ID you will be using later in wowchemy theme files to link the website), *Website URL* (this is the website to which you want to add comment system, e.g. www.example.com), *Website Preferred Language* (enter your prefered language, I have used English). I have skipped *Whitelist domains.* Then save the data.
3. Next click on your site name under *My Sites.* Then select *SETUP* and then *Universal Code.* Scroll below the page and copy the HTML code.
4. Next head into directories of your wowchemy source files. Create the following folders/subfolders if there not there already: **\starter-hugo-academic\layouts\partials\comments**
5. Create **graphcomment.html** file and past the code copied in step 3.
6. Then head to the **params.yaml** file in **\starter-hugo-academic\config_default\**
7. Scroll to the **comments** section then enter graphcomment in provider i.e., **provider: 'graphcomment'**
8. You can customize to which pages the comments should appear.

That's it you are good to go.