A pythonic library that provides a simple interface to the Twitter API.

  * Values are normalized into python types.
  * Pagination logic is abstracted. You can slice/get items from result set and forget about implementation. Just like: `results[:100]` or `results[200:500]`
  * Search API included
  * Lazy search.


Still in beta.

**Implemented so far**:

  * search
  * trends/current
  * trends/daily
  * trends/weekly
  * statuses/friends
  * statuses/followers
  * statuses/user\_timeline
  * statuses/destroy
  * statuses/update
  * users/show
  * friendships/create
  * account/verify\_credentials
  * account/rate\_limit\_status

**TODO**:

  * statuses/public\_timeline
  * statuses/friends\_timeline
  * statuses/mentions
  * statuses/show
  * direct\_messages
  * direct\_messages/sent
  * direct\_messages/new
  * direct\_messages/destroy
  * friendships/destroy
  * friendships/exists
  * friends/ids
  * followers/ids
  * account/end\_session
  * account/update\_delivery\_device
  * account/update\_profile\_colors
  * account/update\_profile\_image
  * account/update\_profile\_background\_image
  * account/update\_profile
  * favorites
  * favorites/create
  * favorites/destroy
  * notifications/follow
  * notifications/leave
  * blocks/create
  * blocks/destroy
  * blocks/exists
  * blocks/blocking
  * blocks/ids

I'll be adding new features. Keep in touch.

## Usage ##

```
    # Authentication
    >>> import pytweet
    >>> api = pytweet.Twitter(username='testpy', password='pytweet')


    # Check credentials
    >>> api.is_authenticated()
    True
    >>> api.verify_credentials() # Returns (authenticated) user object
    <pytweet.objects.TwitterUser object at 0x...>


    # Limits
    >>> api.rate_remaining
    20000


    # Search
    >>> search = api.search('from:reflejo OR python') # Request not done yet.
    >>> res = search[:10] # Data is fetched and cached.
    >>> print res[0]
    <pytweet.objects.TwitterSearchResult object at 0x...>
    >>> print len(res), res[0].text, res[0].from_user, res[0].created_at
    10 Compiling qpid in a mother fucking toaster. #deprecated reflejo 2009-09-23 17:18:47
    >>> res = search[:101] # Pagination is done automatically.
    >>> len(res)
    101

    # Trends
    >>> for date, trends in api.trends().iteritems():
    ...        trends[0]
   <pytweet.objects.TwitterTrend object at 0x...>


    # Update
    >>> status = api.update('Big success!')
    >>> status.created_at, status.text
    (datetime.datetime(2009, 9, 23, 17, 28, 1), u'Big success!')


    # User
    >>> user = api.user('reflejo')
    >>> user.name
    u'Reflejo'
    >>> user.description
    u'All your whuffies are belong to us.'


    # Followers
    >>> for user in api.followers('reflejo'):
    ...     user.name, user
    ... 
    (u'mattbacak', <pytweet.objects.TwitterUser object at 0x...>)
    (u'Soc. Media 4Business', <pytweet.objects.TwitterUser object at 0x...>)
    (u'SEOptimise', <pytweet.objects.TwitterUser object at 0x...>)
    (u'The Swop', <pytweet.objects.TwitterUser object at 0x...>)
    (u'atommica', <pytweet.objects.TwitterUser object at 0x...>)
    # [.....]


    # Friends
    >>> for user in api.friends('testpy'):
    ...     user.name, user.status. user
    (u'Reflejo', <pytweet.objects.TwitterStatus object at 0x...>, <pytweet.objects.TwitterUser object at 0x...>)

    
    # Delete
    >>> api.destroy(12345)
    <pytweet.objects.TwitterStatus object at 0x...>


    # Friends
    >>> statuses = api.user_timeline('Reflejo')
    >>> for status in api.user_timeline('testpy'):
    ...     status.text, status
    ... 
    (u'Big success!', <pytweet.objects.TwitterStatus object at 0x...>)

```