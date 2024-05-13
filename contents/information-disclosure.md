---
title: Information Disclosure - Portswigger Labs
description: Information Disclosure - Portswigger Labs
excerpt:
  Information disclosure, also known as information leakage, is when a website unintentionally reveals sensitive information to its users. 
datetime: 2024-05-10T12:33:07.000+00:00
tags:
  - Information Disclosure
  - Portswigger
  - Labs
featured: true
category: Tutorial
author: nGbonzini
type: article
coverImage:  https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/Designer.png
coverImageAlt: Microsoft AD
coverImageWidth: "2725"
coverImageHeight: "1400"
ogImage: "/assets/blog/hello-world/cover.jpg"
ogImageAlt: something
language: "English"
---
----

As preparation for the eWPTX im going to work through the Portswigger labs. In this post im going to steal... take notes about Information Disclosure and resolve the labs. Let's get started!!!

## Whats is Information Disclosure?

Information disclosure, also known as information leakage, is when a website unintentionally reveals sensitive information to its users. Depending on the context, websites may leak all kinds of information to a potential attacker:
- Data about other users, such as usernames or financial information
- Sensitive commercial or business data
- Technical details about the website and its infrastructure

## Basic examples of information disclosure


- Revealing the names of hidden directories, their structure, and their contents via a robots.txt file or directory listing
- Providing access to source code files via temporary backups
- Explicitly mentioning database table or column names in error messages
- Unnecessarily exposing highly sensitive information, such as credit card details
- Hard-coding API keys, IP addresses, database credentials, and so on in the source code
- Hinting at the existence or absence of resources, usernames, and so on via subtle differences in application behavior

## How to find and exploit information disclosure vulnerabilities ?

- Fuzzing
- Using Burp Scanner
- Using Burp's engagement tools
- Engineering informative responses

## Error messages

The content of error messages can reveal information about what input or data type is expected from a given parameter. This can help you to narrow down your attack by identifying exploitable parameters.

## Lab 1 - Information Disclosure in error messages

>This lab's verbose error messages reveal that it is using a vulnerable version of a third-party framework. To solve the lab, obtain and submit the version number of this framework. 

When start the lab, we see a typically web shop page. Go to View Details.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l1/2024-05-09_23-19.png)

Prove if we do a error if change the product id.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l1/2.png)

And yes!
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l1/3.png)

## Debugging Data

For debugging purposes, many websites generate custom error messages and logs that contain large amounts of information about the application's behavior. 

- Values for key session variables that can be manipulated via user input
- Hostnames and credentials for back-end components
- File and directory names on the server
- Keys used to encrypt data transmitted via the client

## Lab 2 - Information Disclosure on debug page

> This lab contains a debug page that discloses sensitive information about the application. To solve the lab, obtain and submit the SECRET_KEY environment variable.

Every time when we do a penetration test in a web application is indispensable read the code of the application for comments.

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l2/1.png)
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l2/2.png)

## User account pages

By their very nature, a user's profile or account page usually contains sensitive information.
Some websites contain logic flaws that potentially allow an attacker to leverage these pages in order to view other users' data. 

For example:
```
GET /user/personal-info?user=carlos
```

## Source code disclosure via backup files

Obtaining source code access makes it much easier for an attacker to understand the application's behavior and construct high-severity attacks. Sensitive data is sometimes even hard-coded within the source code.

## Lab 3 - Source code disclosure via backup files

>This lab leaks its source code via backup files in a hidden directory. To solve the lab, identify and submit the database password, which is hard-coded in the leaked source code. 

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l3/1.png)
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l3/2.png)

## Information disclosure due to insecure configuration

Websites are sometimes vulnerable as a result of improper configuration. This is especially common due to the widespread use of third-party technologies, whose vast array of configuration options are not necessarily well-understood by those implementing them. 

## Lab 4 - Authentication bypass via information disclosure

> This lab's administration interface has an authentication bypass vulnerability, but it is impractical to exploit without knowledge of a custom HTTP header used by the front-end.To solve the lab, obtain the header name then use it to bypass the lab's authentication. Access the admin interface and delete the user carlos.You can log in to your own account using the following credentials: wiener:peter 

Enter with the credentials 
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l4/1.png)

Before send the request,change the method for Trace.
>The HTTP TRACE method is designed for diagnostic purposes. If enabled, the web server will respond to requests that use the TRACE method by echoing in the response the exact request that was received. This behavior is often harmless, but occasionally leads to information disclosure, such as the name of internal authentication headers that may be appended to requests by reverse proxies. 

And we see when the Request reaches the server,does with a header with our ip address.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l4/2.png)

Change the url to see if got access to the admin dashboard. But a message appears. "...local users..." 🤔 
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l4/3.png)

Put the header and a local ip. And we see the admin dashboard. Delete a Carlitos.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l4/4.png)
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l4/5.png)

## Lab 5 - Information disclosure in version control history

>This lab discloses sensitive information via its version control history. To solve the lab, obtain the password for the administrator user then log in and delete the user carlos.

In the end of the URL put ```/.git```.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l5/1.png)

In ```COMMIT_EDITMSG``` we see this message.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l5/2.png)

I open my Kali and download.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l5/4.png)

With the command ```git diff``` i see the difference between two commits.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l5/5.png)

If i see the history of commits and the comments, i find which commit have the credentials that search.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l5/6.png)


With ```git checkout``` i change to the branch that have the credentials hardcoded.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l5/7.png)

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l5/8.png)

To finally, delete Carlos.
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/id/l5/2024-05-10_13-46.png)

I hope you find it useful.👨‍💻
If you have another type of solution or if i am mistaken about something, please let me know.