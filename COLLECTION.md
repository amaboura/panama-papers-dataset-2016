### Collecting the data

Some of you have been asking about the process that went into collecting these data, it's not an inside leak or anything, this is a couple of tricks here and there that you can use to reproduce the dataset, or you can keep them for your future data gathering.

#### Getting the CSV files
I have to say that collecting the main stories from ICIJ website was pretty straightforward, i was able to catch CSV files through Network Monitoring feature that is available in Chrome, that is generally used to monitor the outgoing requests.

###### Reproducing the step
* Load [the ICIJ stories link] (https://panamapapers.icij.org/the_power_players/)
* Open the Chrome inspector ( *Right Click* -> *Inspect Element* )
* Under **Network** tab, navigate to **XHR** subtab
* Refresh the page, and you will be able to see the list of outgoing requests
* You will notice an **en.csv** file, *Right Click -> Copy Link address*, and there you have it.
* You can also catch the CSV file just by typing *csv* into the **Filter** text field
* Because stories are available in different languages, so you can guess the name of other files (fr, de, pt ..etc)

#### Getting the JSON files

Each released story has a graph visualization, which is built with a tool called [Linkurious](http://linkurio.us/),i tried the data source with *Network Monitor* (mentioned above), but couldn't get any useful results.
Digging back into the CSV file, i noticed that there was a visualization ID that came with each story, this is a string that surely has to do with Linkurious, the tool they used.
After looking into Linkurious, i found that they have a feature that allows you to embed widgets into your website, and each widget comes with a unique link, that, you can guess, is the visualization ID found with each story. A Widget link can be like this (*https://linkurious.icij.org/widget/45747ce9*), This link can be found when you load each story, navigate to the HTML source and look for the word **widget**.

Now that Widget link will give you a full preview of the graph representation, in which you can zoom, click for details ..etc, Luckily, when you load the full preview, it brings up *Search* within the graph, which helps you find edges and nodes.

If you inspect the search button, using the Chrome Developer tools, you will notice that is invoking ``` LK.search() ``` method. Now ``` LK ``` sounds familiar, it's the main Linkurious javascript object used to do all the rendering, if you try to output the ``` LK ``` object, by going just to **Console** tab, type ``` LK ``` and hit *Enter*. You will see the list of properties and methods that goes into that object, and if you look closely, there is a property called ``` content ``` that has ``` graph ``` property, that contains the nodes and edges data used to feed the graph.

Now you found your way into the data, next, you want to be able to download them, use this small script in your **Console** tab to help you do so
``` javascript
var pp = document.createElement('a');
pp.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(JSON.stringify(LK.content.graph)));
pp.setAttribute('download', window.location.pathname.split('/')[2]);
pp.click();
```

This will download the file for you, and name it after the widget ID.

Now you have a lot of data to download, you can choose to do that manually, or if you've got sometime, [build a chrome extension](https://developer.chrome.com/extensions/getstarted) that goes through the list of visualization IDs, and downloads them for you, i went with the manual option because i'm a lazy human being.

That's it

If you want to add more details, or maybe other tricks or tools you want to share, please feel free to send a PR.

Enjoy!
