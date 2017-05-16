## Introduction

As most OSNs do not permit the third-party release of content posted on them,
we have only included the IDs of the users and posts in our dataset. These
can be used to retrieve the actual post content from each OSN's API - this
document provides a brief overview of how this might be done.

### IDs
A user ID corresponds to a single user profile on an OSN, while an activity
ID corresponds to a single activity (post, image, etc.) on an OSN. These
concepts remain the same across OSNs, though each OSN uses a different
term to refer to them - the corresponding column in each OSN's table is
also different:

<table>
<thead>
<tr>
<th>Social Network</th>
<th>Database Table</th>
<th>User ID Column</th>
<th>Activity ID Column</th>
</tr>
</thead>
<tbody>
<tr>
<td>Flickr</td>
<td><code>flickr_photo_id</code></td>
<td><code>user_id</code></td>
<td><code>photo_id</code></td>
</tr>
<tr>
<td>Google+</td>
<td><code>googleplus_photo_id</code></td>
<td><code>user_id</code></td>
<td><code>post_id</code></td>
</tr>
<tr>
<td>Instagram</td>
<td><code>instagram_photo_id</code></td>
<td><code>user_id</code></td>
<td><code>photoId</code></td>
</tr>
<tr>
<td>Tumblr</td>
<td><code>tumblr_post_id</code></td>
<td><code>user_name</code></td>
<td><code>post_id</code></td>
</tr>
<tr>
<td>Twitter</td>
<td><code>twitter_tweet_id</code></td>
<td><code>screen_name</code></td>
<td><code>tweet_id</code></td>
</tr>
<tr>
<td>YouTube</td>
<td><code>youtube_feed_id</code></td>
<td><code>channel_id</code></td>
<td><code>id</code></td>
</tr>
</tbody>
</table>

### Finding User Activity Across Networks
The various <code>iden</code> columns in the <code>about_me</code> table correspond to the User ID
columns in each OSN's table. For example, given the following (ficticious, truncated) record in <code>about_me</code>:
table>
<thead>
<tr>
<th>aboutme_user_name</th>
<th>flickr_iden</th>
<th>googleplus_iden</th>
<th>...</th>
</tr>
</thead>
<tbody>
<tr>
<td>JaneDough</td>
<td>12345@N12</td>
<td>1234567</td>
<td>...</td>
</tr>
</tbody>
</table>

This user's Flickr posts can be found by retrieving all records in
<code>flickr_photo_id</code> with <code>user_id</code> <em>12345@N12</em>:
<code>SELECT * FROM dataset.flickr_photo_id WHERE user_id = '12345@N12';</code>
Their Google+ posts can be found in a similar manner:
<code>SELECT * FROM dataset.googleplus_photo_id WHERE user_id = '1234567';</code>

### Retrieving Post Content
This process differs between OSNs, and is best accomplished by using
an appropriate client library for your programming language of choice.
This section provides basic instructions using Python 3, which are accurate
as of December 2015; they are provided as a rough guideline, and should not
be construed as an endorsement of any library, method, or programming
language.

There are three general steps which apply to all OSNs, with the exact details varying between OSNs:
* Register an application on the OSN's developer portal. This represents the
script/program that will be used to retrieve posts from the OSN.
* (If applicable) Authenticate a user account through your script/program.
OSNs typically use OAuth for this process, which is made simpler by most
client libraries.
* Using the credentials obtained (an application key and secret, and a user
access token), retrieve posts by their IDs from the OSN.

Note that each OSN usually limits the number of accesses to their API over a
period of time. <strong>This is outside the scope of these examples, and should be
taken into account in your own scripts</strong>, particularly if you are retrieving
large amounts of posts at a time. We also retrieve posts one-by-one in these
examples, though certain networks may have API calls that allow batches of
posts to be retrieved at a time - this too is outside the scope of this
guide.

## 1. Flickr
* Client Library Setup

  This guide uses the <a href="https://stuvel.eu/flickrapi">Python Flickr API kit</a>.
  Its documentation can be found <a href="https://stuvel.eu/media/flickrapi-docs/documentation/index.html">here.</a>
  To install, run <code>pip install flickrapi</code>, preferably in a virtualenv.

* Register an Application (Step 1)

  Apply for an application key at <a href="https://www.flickr.com/services/apps/create/apply/">Flickr's App Garden</a> website.This process will provide you with an API key and secret.

  <blockquote>
  <p><strong>Ensure that both your key and secret are kept a secret, and are not
  revealed to the public.</strong> If you are going to make your scripts open-source,
  ensure that the key/secret are not included within.</p>
  </blockquote>

* Authenticate a User Account (Step 2, skipped)

  As Flickr does not require authentication with a user account in order to retrieve posts, Step 2 does not apply here.


* Retrieve Posts by ID (Step 3)

  This code instantiates the client library with the client key and secret, and uses it to retrieve posts whose IDs are specified in a list.
  It has been adapted from the <a href="https://stuvel.eu/media/flickrapi-docs/documentation/3-auth.html">authentication documentation</a>
  for the Python Flickr API kit.
  
  <pre><code>import flickrapi

  # ENSURE THAT THIS IS NOT REVEALED TO THE PUBLIC!
  API_KEY = 'YOUR_KEY_HERE'
  API_SECRET = 'YOUR_SECRET_HERE'

  # Instantiates the client library, and specifies that we want results
  # returned as a dict.
  flickr = flickrapi.FlickrAPI(API_KEY, API_SECRET, format='parsed-json')

  # Post IDs to be retrieved.
  post_ids = []

  for post_id in post_ids:
      # Retrieve the post from the service.
      post_details = flickr.photos.getInfo(photo_id=post_id)

      # Process the post dictionary.
      print(post_details)

  </code></pre>
  
## 2. Google+
* Client Library Setup

  This guide uses the <a href="https://developers.google.com/api-client-library/python/">Google APIs Client Library for Python</a>.
  To install, run <code>pip install google-api-python-client</code>, preferably in a virtualenv.

* Register a Project (Step 1)
  Create a new project at the <a href="https://console.developers.google.com/project">Google Developers Console</a>,
  and enable access to the Google+ API: from the Dashboard,
  click <code>Enable and manage APIs</code>, then <code>Google+ API</code>, and finally <code>Enable API</code>.
  
  Without leaving the same screen (which should now be the API Manager), click
  <code>Credentials</code> on the left sidebar. Select <code>New credentials</code>, then click
  <code>API key</code>, followed by <code>Server key</code>, and <code>Create</code>. This will provide you with an API key.

  <blockquote>
  <strong>Ensure that your key is kept a secret, and is not revealed to the
  public.</strong> If you are going to make your scripts open-source,
  ensure that the key is not included within.
  </blockquote>
  
* Authenticate a User Account (Step 2, skipped)
 
  As Google+ does not require authentication with a user account to retrieve posts, Step 2 does not apply here.

* Retrieve Posts by ID (Step 3)

  This code instantiates the client library with the API key, and uses it to
  retrieve posts whose IDs are specified in a list.
  
  <pre><code>from apiclient.discovery import build

    # ENSURE THAT THIS IS NOT REVEALED TO THE PUBLIC!
    API_KEY = 'YOUR_KEY_HERE'

    # Instantiate the client library with the API key.
    service = build('plus', 'v1', developerKey=API_KEY)
    resource = service.activities()

    # Post IDs to be retrieved.
    post_ids = []

    for post_id in post_ids:
        # Retrieve the post from the service.
        post_details = resource.get(activityId=post_id).execute()

        # Process the post dictionary.
        print(post_details)
    </code></pre>

## 3. Instagram
<blockquote>
<strong>Note that Instagram now requires developers to submit their application
for review before allowing full access to their API.</strong> In the case of
retrieving posts from the API, developers must request the <code>public_content</code>
permission. More details about this process can be found <a href="https://www.instagram.com/developer/review/">here.</a>
</blockquote>

<blockquote>
This review process was not in place at the time the dataset was collated, and
we are unable to comment on whether or not a research application will be approved.
</blockquote>

* Client Library Setup
  This guide uses Instagram's <a href="https://github.com/Instagram/python-instagram">python-instagram</a> library. 
  To install, run <code>pip install python-instagram</code>, preferably in a virtualenv.
  
* Register an Application (Step 1)

  Register as a developer on Instagram's <a href="https://www.instagram.com/developer/register/">developer website</a>,
  then <a href="https://www.instagram.com/developer/clients/register/">create a new Client</a>.
  When prompted for a redirect URL, use http://127.0.0.1.
  Once complete, this will provide you with an API key and secret.
  
  <blockquote> <strong>Ensure that your keys are kept a secret, and are not revealed to the
  public.</strong> If you are going to make your scripts open-source,
  ensure that the keys are not included within.</blockquote>
  
* Authenticate a User Account (Step 2)
 
  Instagram <a href="https://github.com/Instagram/python-instagram/blob/master/get_access_token.py">provides a Python script</a>
  to ease the process of obtaining a user access token for testing
  purposes - this is suitable for our needs, though inappropriate
  for an actual application. Run the script, providing the
  client ID, secret, and redirect URLs from the previous step.
  When prompted for requested scopes, enter &quot;basic public_content&quot;.

  After visiting the URL given and providing authorization, copy
  the string of characters after &quot;code=&quot; in the URL. If successful,
  the script will output a tuple:
  <code>('abcdefg12345', {'bio': '', ...})</code><
  
  The string in the 0th-position of this tuple is the access token needed for the next step.
  
* Retrieve Posts by ID (Step 3)

  This code instantiates the client library with the API secret and access token
  obtained previously, and uses it to retrieve posts whose IDs are specified in
  a list.
  <pre><code>from instagram.client import InstagramAPI

  # ENSURE THESE ARE NOT REVEALED TO THE PUBLIC!
  ACCESS_TOKEN = &quot;YOUR_TOKEN_HERE&quot;
  CLIENT_SECRET = &quot;CLIENT_SECRET_HERE&quot;

  # Instantiate the client library with the access token and client secret.
  instagram_api = InstagramAPI(access_token=ACCESS_TOKEN, client_secret=CLIENT_SECRET)

  # Post IDs to be retrieved.
  post_ids = []

  for post_id in post_ids:
      # Retrieve the post from the service.
      post = instagram_api.media(post_id)

      # Process the post dictionary.
      print(post)
  </code></pre>
  
## 4. Tumblr
* Client Library Setup
 
  This guide uses Tumblr's <a href="https://github.com/tumblr/pytumblr">pytumblr</a> library. 
  To install, run <code>pip install pytumblr</code>, preferably in a virtualenv.
  
* Register an Application (Step 1)
  
  Create a new application on Tumblr's <a href="https://www.tumblr.com/oauth/register">developer website</a>.
  This will provide you with the Consumer Key and Secret Key needed.
  
  <blockquote>
  <strong>Ensure that your keys are kept a secret, and are not revealed to the
  public.</strong> If you are going to make your scripts open-source,
  ensure that the keys are not included within.</p>
  </blockquote>
  
* Authenticate a User Account (Step 2, skipped)

  As Tumblr doesn't require authentication with a user account to retrieve posts,
  Step 2 does not apply here.
  
* Retrieve Posts by Username and ID (Step 3)
  
  Unlike the other networks here, Tumblr requires two pieces of information to
  retrieve a post: the name of the blog that post was on, and the post ID itself.
  The blog's name has been included in the dataset in the <code>user_name</code> column.
  
  In the following code, each entry in the list of IDs is assumed to be a dictionary
  with the following format:
  <pre><code>{
      'blog_name': &lt;blog name, from user_name column&gt;,
      'post_id': &lt;corresponding post ID, from post_id column&gt;
  }
  </code></pre>

  <pre><code>import pytumblr

  # ENSURE THIS IS NOT REVEALED TO THE PUBLIC!
  CONSUMER_KEY = 'YOUR_KEY_HERE'

  # Instantiate the client library with the consumer key.
  tumblr_client = pytumblr.TumblrRestClient(CONSUMER_KEY)

  post_records = []

  for record in post_records:
      # Format the blog name into the URL which Tumblr requires.
      blog_url = '%s.tumblr.com' % record['blog_name']
      post_id = record['post_id']

      # Retrieve the post from the service.
      post = client.posts(blog_url, id=post_id)

      # Process the post dictionary.
      print(post)
  </code></pre>
  
## 5. Twitter
* Client Library Setup

  This guide uses the <a href="https://github.com/tweepy/tweepy">tweepy</a> library. Its
  documentation can be found <a href="https://tweepy.readthedocs.org/en/v3.5.0/">here.</a>
  To install, run <code>pip install tweepy</code>, preferably in a virtualenv.
  
* Register an Application (Step 1)

  Create a new application on <a href="https://apps.twitter.com/app/new">Twitter's developer site.</a>.
  When complete, this will bring you to the application's configuration page - click
  <code>Keys and Access Tokens</code> to obtain the Consumer Key and Consumer Secret needed.
  
  <blockquote>
  <strong>Ensure that your keys are kept a secret, and are not revealed to the
  public.</strong> If you are going to make your scripts open-source,
  ensure that the keys are not included within.
  </blockquote>

* Authenticate a User Account (Step 2, skipped)

  As Twitter doesn't require authentication with a user account to retrieve posts,
  Step 2 does not apply here.

* Retrieve Posts by ID (Step 3)

  This code instantiates the client library with the consumer key and secret from
  before, and uses it to retrieve posts whose IDs have been specified in a list.
  
  <pre><code>from tweepy import API, AppAuthHandler

    # ENSURE THESE ARE NOT REVEALED TO THE PUBLIC!
    CONSUMER_KEY = &quot;YOUR_KEY_HERE&quot;
    CONSUMER_SECRET = &quot;YOUR_SECRET_HERE&quot;

    # Instantiate the client library.
    authenticator = AppAuthHandler(CONSUMER_KEY, CONSUMER_SECRET)
    twitter_api = API(auth_handler=authenticator)

    # Post IDs to be retrieved.
    post_ids = []

    for post_id in post_ids:
        # Retrieve the post from the service.
        post = twitter_api.get_status(id=post_id)

        # Tweepy returns an object for each post.
        # Process it here.
        print(post)
    </code></pre>
    
    


  
  
 
 
