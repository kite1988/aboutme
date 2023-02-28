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
    
**If you use our dataset, please cite our [ASONAM](http://www.comp.nus.edu.sg/~kanmy/papers/asonam15.pdf) 2015 paper.  Thanks!**


## Dataset
This is a mysql dump file that contains user's profile name in about.me and their user identities in the six OSNs. 
* <A HREF="https://drive.google.com/file/d/0Bxi6M1XYLbjUQTFkUWV6bUthcVk/view?usp=sharing&resourcekey=0-nSKcHtkLi2sVNETlBUA8Hw">about_me.sql (727K) </A>

The following six dump files contain the post IDs and their user identities in the corresponding OSN. You can use the user identities in aboutme.sql to link user's activities in multiple social networks. With the post IDs, you can further pull
the acutal posts via respective APIs. Read our <a href="instructions.md" target="_blank">tutorial</a> on using these APIs.
      
* <A HREF="https://drive.google.com/file/d/0Bxi6M1XYLbjUUjJLVERRT2Q3ZTg/view?usp=sharing&resourcekey=0-fbTu8Vn66vNhisa-mMO5vA">flickr.sql (53MB) </A>     
* <A HREF="https://drive.google.com/file/d/0Bxi6M1XYLbjUeXlXQ1ZyNU9zUVE/view?usp=sharing&resourcekey=0-W3LQnd2jHlRFepxdVYqR9A">googleplus.sql (34MB) </A>
* <A HREF="https://drive.google.com/file/d/0Bxi6M1XYLbjUWUltek5lOGlaUGs/view?usp=sharing&resourcekey=0-f0ORIK2NbzjExX5skFZgqw">instagram.sql (19MB) </A> 
* <A HREF="https://drive.google.com/file/d/0Bxi6M1XYLbjUMUZTSmFyNmFia1U/view?usp=sharing&resourcekey=0-jJqGEMd7O49eeG8cv2mBCQ">tumblr.sql (49MB) </A>
* <A HREF="https://drive.google.com/file/d/0Bxi6M1XYLbjUMU0tdEJKYng5WGc/view?usp=sharing&resourcekey=0-hcKjQM0KlMH3Ad5bDh6vlg">twitter.sql(479MB) </A>
* <A HREF="https://drive.google.com/file/d/0Bxi6M1XYLbjUYU9iT28wWV91NE0/view?usp=sharing&resourcekey=0-5Wow12Kd_gCAN4o1kENJUg">youtube.sql (19MB) </A>

Alternatively, you can download a <A HREF="https://drive.google.com/file/d/0Bxi6M1XYLbjUckZzd3N0d3habFk/view?usp=sharing&resourcekey=0-Pkd6Nfxq-3o8m0qa-fMSrw">compressed (652M)</A> version of these seven files.


**Note: these files are hosted by Google Drive.**

## Publications
Bang Hui Lim, Dongyuan Lu, Tao Chen and Min-Yen Kan (2015).[#mytweet via   Instagram: Exploring User Behaviour across Multiple Social Networks](http://www.comp.nus.edu.sg/~kanmy/papers/asonam15.pdf). In Proceedings of IEEE/ACM International Conference on Advances in Social Networks Analysis and Mining (ASONAM'15), Paris, France, Aug 25-28, 2015.

## Group Members
* Bang Hui Lim
* Dongyuan Lu
* <a href="http://www.cs.jhu.edu/~taochen/">Tao Chen</a>
* <a href="http://www.comp.nus.edu.sg/~kanmy/">Min-Yen Kan</a> - Group lead

