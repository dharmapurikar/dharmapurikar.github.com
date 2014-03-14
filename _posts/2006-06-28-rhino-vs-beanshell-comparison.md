--- 
layout: post
title: Rhino, BeanShell comparison
categories: 
- Articles
- Java
- Programming
tags:
- performance
- rhino
- javascript
- beanshell
status: publish
type: post
published: true
meta: 
  dsq_thread_id: "420851723"
  _edit_last: "1"
---
<blockquote>Update (22/May/2007): I have also included Groovy performance as per Tom's comment. The post is <a href="http://thoughtworker.in/2007/05/22/update-on-performance-of-scripting-languages/">here</a>.</blockquote>
Recently I got a requirement to provide scripting capabilities in our product. A while ago, I was reading about <a title="JSR 223" href="http://www.jcp.org/en/jsr/detail?id=223">JSR 223</a> and thought to have hands on the scripting capabilities of Java. While searching Internet I came across a <a href="http://www.robert-tolksdorf.de/vmlanguages.html">page </a>which states number of programming languages for Java VM. The most appealing options for me were <a href="http://www.mozilla.org/rhino/">Rhino</a>, <a href="http://www.beanshell.org/">BeanShell </a>and <a href="http://www.judoscript.com/judo.html">JudoScript</a>. Ofcourse <a href="http://groovy.codehaus.org/">Groovy</a>, <a href="http://www.ruby-lang.org/en/">Ruby </a>and others are good too, but I wanted a simple and close to Java scripting for my product.

To get a quick start, I chose Rhino and BeanShell. JudoScript sounded like lots of in-built capabilities and since I didn’t want a Swiss-knife kind of thing with me so I chose to go with generic approach of Rhino and BeanShell.

In our case, developers will write some small routines to process sql resultsets. Typically the operations will be getting values in different columns or creation of sets etc. So my job is to provide a framework which takes sql queries dynamically and pass on the resultset to script. Script will process resultset and return the Lists or HashMap to framework again so that further processing can be done. So from my perspective resultset processing abilities was a winning point. For those who are more interested in computational performance analysis, I hope they will love to see this <a href="http://www.pankaj-k.net/spubs/articles/beanshell_rhino_and_java_perf_comparison/index.html">page</a>.

Coming back to data processing capabilities, I set a simple test case with following steps:

* Get Resultset
* Note start time
* Process Resultset using Java / Rhino / Beanshell code.
* Note end time

I kept number of records as a variable in all of the executions. Thus I wanted to see the effect of increasing recordset size on performance. I started with 50 records and final reading was taken at 50000 records. Result of tests is as follows -

<a class="imagelink" title="Script Performance Analysis" href="http://dharmapurikar.files.wordpress.com/2006/06/comparison.PNG"><img src="http://i71.photobucket.com/albums/i157/dharmapurikar/ThoughtWorker/comparison.png" alt="Script Performance Analysis" width="416" height="286" /></a>

To help you understand clear the tabular representation of above data is -

| Num of Records | Java | Rhino | BeanShell |
|----------------|------|-------|-----------|
| 50             | 31   | 375   | 250       |
| 500            | 110  | 391   | 453       |
| 5000           | 359  | 844   | 1391      |
| 50000          | 2375 | 5515  | 11406     |


On your machine the figures may vary a little bit but the ratio should be roughly same. BeanShell's performance is dropped suddenly with the larger size of record set. On the other hand Rhino performs consistently and balances better with the size record set. For Java the ratio for 50:50000 records is 1:37 but for Rhino its 1:15. For Beanshell same ratio stands as 1:45! This clearly shows that there is consistency in performance of Rhino compared to BeanShell.

Although Rhino is winner from the performance perspective, I need to admit Beanshell is homely for Java developers. The communication between beanshell and java is almost seamless. For Rhino you need to understand Scope, context and little more Rhino specific things but for BeanShell there is no complexity. So from simplicity perspective I vote for BeanShell.

My advice to others will be, there is not much difference in both of the scripting engines. Normally neither we process (or at least not supposed to process) 100000 element sized lists nor so big datasets. So its mere matter of choice for majority of users. Go with BeanShell if your end-user is a Java Developer as its very easy to understand the operation and there is very little learning curve.

If you like JavaScript or needs millisecond accurate performance guarantee then choose Rhino as it proves to be consistent. I didn't get chance to test E4x and other features but overall Ecmascript 4 is good. I will love to hear any other experiences regarding above two or any new engines.
