---
layout: post
title: "Google Local Business Center, bulk feed uploads, and OpenOffice"
excerpt: "Google Local Business Center is a great tool but t"
tags: 
- google
published: true
---

Google Local Business Center is a great tool but their instructions on using uploading Bulk Business Feeds is a little lacking for people who don't have Microsoft Excel. If you're using the OpenOffice.org[1] suite you can still upload feeds though the procedure is a little different.

Create your spreadsheet as per Google's instructions, then when you're ready choose `Save As`, change the type to `Text CSV` and hit `Save`. 

You'll be presented with an Export window where you need to:

1. change the `Character set` to `Unicode (UTF-8)`
2. change the `Field delimiter` to `{Tab}`
3. clear the `Text delimieter` field of any values -- this is very important!

Click `OK`, then find the file in your filesystem and change the extension from `.csv` to `.txt`. 

You should now be able to upload your file successfully!


  [1]:http://www.openoffice.org
