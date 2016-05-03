---
layout: post
title: The function import cannot be executed because it is not mapped to a store function
---

I am currently working with Entity Framework hardcore model-first type database and recently I was in need of updating database entities. I had never had any experience with model-first databses, and as it does not have any type of migration scripts - it is easy to fuck things up. Today I got an error trying to call stored function: 

**The function import cannot be executed because it is not mapped to a store function**

First few links on google didn't help so here I repost what I found on http://sanganakauthority.blogspot.com/ and what helped me.

### The function import cannot be executed because it is not mapped to a store function


This is very typical error you receive when your underlying database store is changed and there is no update made to EDMX file.
For example, I imported a stored procedure in edmx and saved it. After that I change the stored procedure and do not update edmx. I run the application and at runtime the error is encountered as - “the function import cannot be executed because it is not mapped to a store function”.
This error can be resolved easily by updating the edmx. Following is procedure to resolve the error –
Open the edmx and open Model Browser. Model browser can be opened as shown below.
![](http://2.bp.blogspot.com/-nc3H2bB66bY/UdaQgKbB5LI/AAAAAAAAAZY/kRKevijp8XI/s1280/1.png)

Find the required stored procedure in model browser. The right click and select option – “Delete from Model” as shown below –
![](http://3.bp.blogspot.com/-gCIrqOojXtU/UdaQnOKk95I/AAAAAAAAAZg/0F3wKHnyLyA/s1280/2.png)

 
Now right click on any area on edmx file and select the option “Update Model from Database” option. The popup containing the list of Tables, View and stored procedure will appear. Select the earlier deleted stored procedure and click “Finish” on the pop up.
Now again open the model browser and find the added stored procedure. Right click on it and select the “Edit” option as shown below - 
![](http://4.bp.blogspot.com/-NmvCcKukQek/UdaQykG6eUI/AAAAAAAAAZo/cZNkGVzxD0I/s1280/3.png)
 
“Edit function Import” pop up will appear. For the selected stored procedure you will find that, return collection is having the two options which end with “Results1” and “Results”. Out of these two options select Results option and click OK.
![](http://4.bp.blogspot.com/-hbBQTNPzAgc/UdaQ4qee1SI/AAAAAAAAAZw/scXvN3oB4fU/s1280/4.png)

This will resolve the error. Hope it helps.
Cheers…
Happy Importing!!!

---

*Thanks Sanganak :)*
