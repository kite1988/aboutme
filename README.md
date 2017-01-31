# About.Me Dataset for User-centric OSN Analysis

A user-centric study of cross Online Social Network (OSN) behavior requires a collective study of many individual users, each of whom use multiple OSNs. We purposefully sidestep the issue of user linkage to focus our attention on user behavior.
     
We leverage an OSN aggregation service called <a href="https://about.me/">About.me </a>, which enables people to easily create a public online identity that unifies a self-described short biography with prominent links to the person’s other OSN accounts and personal websites.


Using the About.me API, we collected a set of registered 180,000 user profiles, 
     and further limit the users that link to at least 4 out of 6 OSNs 
     (i.e., <a href="https://www.flickr.com/">Flickr</a>, 
     <a href="https://plus.google.com/">Google+</a>, 
     <a href="https://instagram.com/">Instagram</a>, 
     <a href="https://www.tumblr.com/">Tumblr</a>, 
     <a href="https://twitter.com">Twitter</a> and 
     <a href="https://www.youtube.com/">Youtube</a>). 
     These six OSNs are chosen for the reason that they are represent 
     the breadth of media and functionality common in today’s Web 2.0 ecology, 
     and they expose most user information publicly through an API.
     This selection criteria resulted in 15, 595 users in our dataset.
     
     
With these 15, 595 users and their user identity in the six OSNs,
	we crawled each user’s publicly accessible activities in the six OSNs via
	the respective APIs on 15 August 2013. Since all of the data
	we have obtained is public, and since we believe that the
	compiled dataset is a valuable resource for studying multiple
	OSN behavior, we have released our dataset for others to
	conduct further study. As required by most OSNs, we are not able 
    to distribute the actual content of a post. Followed the
    other public social datasets, 
    we release the post ID and its user identity instead.   
    
**If you use our dataset, please cite our ASONAM 2015 paper.  Thanks!**


###Dataset
This is a mysql dump file that contains user's profile name in about.me and their user identities in the six OSNs. 
* <A HREF="dataset/about_me.sql">about_me.sql (1.5MB) </A>

The following six dump files contain the post IDs and their user identities in the corresponding OSN. You can use the user identities in aboutme.sql to link user's activities in multiple social networks. With the post IDs, you can further pull
the acutal posts via respective APIs. Read our <a href="instructions.html" target="_blank">tutorial</a> on using these APIs.
      
* <A HREF="dataset/flickr_photo_id.sql">flickr_photo_id.sql (331MB) </A>     
* <A HREF="dataset/googleplus_post_id.sql">googleplus_post_id.sql (177MB) </A>
* <A HREF="dataset/instagram_photo_id.sql">instagram_photo_id.sql (79MB) </A> 
* <A HREF="dataset/tumblr_post_id.sql">tumblr_post_id.sql (245MB) </A>
* <A HREF="dataset/twitter_tweet_id.sql">twitter_tweet_id.sql(1.8GB) </A>
* <A HREF="dataset/youtube_feed_id.sql">youtube_feed_id.sql (94MB) </A>

Alternatively, you can download a <A HREF="aboutme.tar.gz">compressed (643M)</A> version of these seven files.

###Publications
Bang Hui Lim, Dongyuan Lu, Tao Chen and Min-Yen Kan (2015).#mytweet via   Instagram: Exploring User Behaviour across Multiple Social Networks. In Proceedings of IEEE/ACM International Conference on Advances in Social Networks Analysis and Mining (ASONAM'15), Paris, France, Aug 25-28, 2015.
          [&nbsp;<A HREF="http://wing.comp.nus.edu.sg/portal/publications.html?view=publication&task=show&id=218">More</A>&nbsp;]
          [&nbsp;<A HREF="http://wing.comp.nus.edu.sg/publications/2015/lim-et-al-15.pdf">Digital Version</A>&nbsp;]

###Group Members
* Bang Hui Lim
* Dongyuan Lu
* <a href="http://www.cs.jhu.edu/~taochen/">Tao Chen</A>
* <a href="http://www.comp.nus.edu.sg/~kanmy/">Min-Yen Kan</A> - Group lead

