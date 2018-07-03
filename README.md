# Office Building Web Architecture (OWBA)
**This article is still in draft, so not all ideas, concepts, naming conventions and etc. have been fully fleshed out and will be changing/evolving/improving.**

This document aims to describe a (hopefully) new architecture, along with a set of rules for implementation, that will provide more separations of concerns (layers) that will be well defined. This architecture and rule set will try to make implementations stay more true to the classical definition of Object Oriented (OO) programming and should help steer towards “best practices”, like SOLID.

Diagram:

(Todo)

Definitions and Comparison to MVC:
* Front Door: This is the entry point into your application. In PHP this would be the index.php that located in a publicly accessible folder and it would load in the non-publicly accessible code (Lobby).
* Lobby: This is where things get initialized for use by the application. HTTP request, cookies, configuration, dependency injection, routing and such. 
* Office Directory: This object would be the request router.
* Public / Front Office (Ex: IndexPublicOffice / IndexFrontOffice): This would be that class that would be analog for “Controller”.
* Front Desk: This is a virtual name for methods, which would be the analog for “Action” in a “Controller”. 
* Private / Back Office / Department (Ex: ?): Not “accessible” by the public. Typically does auxiliary work.
* Utility Closet: This would be for utility classes, like a class that works with strings.
* Data  /  Records Office (Ex: ?): A virtual grouping of the data departments, which are departments that deal with data, such as database related requests.
* Data Inquiry / Query Department (Ex: PostsDataInquery, PostsDataQuery): This class will have methods which only a single query will be performed. No logic should be performed on the data received. Logic performed on the data provided to the query should be limited, such as casting values to proper types, but avoid things like ‘strrev’ (PHP function to reverse a string). Logic that is performed by receiving entity (like MySQL) via the query request (query string) is OK. 
* Data Reports Department (Ex: PostsDataReport): This class will be used to perform logic on the data sent to or received from the Data Inquiry Department. Also you can perform multiple Data Inquiry Department calls here in a single method, but it recommend not getting to carried away with that freedom.
* Presentation Department / Office: (Virtual grouping?) This would the analog to “View”. 
* Type Set Desk / Printing Press: (Can we split this into two things?) Takes data in, fills in the templates, returns filled template.

Implementation Rules, Guidelines and Considerations:
* Must adhere to the SOLID Principles. https://en.wikipedia.org/wiki/SOLID
* Must adhere to the “Seven Virtues of a Good Object”. https://www.yegor256.com/2014/11/20/seven-virtues-of-good-object.html
* Must not use the term or name “Back Door”.
* Should avoid things that are controversial in nature, like ORMs, template engines that include logic, etc.
