```
Design a simplified version of Twitter where users can post tweets, follow/unfollow another user and is able to see the 10 most recent tweets in the user's news feed. Your design should support the following methods:

postTweet(userId, tweetId): Compose a new tweet.
getNewsFeed(userId): Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent.
follow(followerId, followeeId): Follower follows a followee.
unfollow(followerId, followeeId): Follower unfollows a followee.
Example:

Twitter twitter = new Twitter();

// User 1 posts a new tweet (id = 5).
twitter.postTweet(1, 5);

// User 1's news feed should return a list with 1 tweet id -> [5].
twitter.getNewsFeed(1);

// User 1 follows user 2.
twitter.follow(1, 2);

// User 2 posts a new tweet (id = 6).
twitter.postTweet(2, 6);

// User 1's news feed should return a list with 2 tweet ids -> [6, 5].
// Tweet id 6 should precede tweet id 5 because it is posted after tweet id 5.
twitter.getNewsFeed(1);

// User 1 unfollows user 2.
twitter.unfollow(1, 2);

// User 1's news feed should return a list with 1 tweet id -> [5],
// since user 1 is no longer following user 2.
twitter.getNewsFeed(1);
```

```java
public class Twitter {
    private static int timeStamp = 0;
    
    class Tweet{
        int id;
        Tweet next;
        int time;
        
        public Tweet(int id){
            this.id = id;
            this.time = timeStamp++;
            next = null;
        }
    }
    
    class User{
        int id;
        Set<Integer> followers;
        Tweet tweet_head;
        
        public User(int id){
            this.id = id;
            tweet_head = null;
            followers = new HashSet<Integer>();
        }
        
        public void follow(int userId){
            followers.add(userId);
        }
        
        public void unfollow(int userId){
            followers.remove(userId);
        }
        
        public void postTweet(int tweetId){
            Tweet tweet = new Tweet(tweetId);
            tweet.next = tweet_head;
            tweet_head = tweet;
        }
    }
    
    Map<Integer, User> userMap;
    
    public Twitter() {
        userMap = new HashMap<Integer, User>();
    }
    
    /** Compose a new tweet. */
    public void postTweet(int userId, int tweetId) {
        if(!userMap.containsKey(userId)){
            User user = new User(userId);
            userMap.put(userId, user);
        }
        
        userMap.get(userId).postTweet(tweetId);
    }
    
    /** Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent. */
    public List<Integer> getNewsFeed(int userId) {
        
        //we need a DS which gives you the tweet with maximum timestamp in it. We can use a maxHeap which provides the maximum in O(1) time
        List<Integer> res = new ArrayList<Integer>();
        
        //if the user we are asking for is not in map return empty
        if(!userMap.containsKey(userId)) return res;
        
        Set<Integer> followers = userMap.get(userId).followers;
        PriorityQueue<Tweet> pq = new PriorityQueue<Tweet>(followers.size() + 1, new Comparator<Tweet>(){
            @Override
            public int compare(Tweet a, Tweet b){
                return b.time - a.time;  //max heap
            }
        });
        
        //add current user's tweet head
        Tweet currentUserTweet = userMap.get(userId).tweet_head;
        if(currentUserTweet!= null ) pq.add(currentUserTweet);
        
        //do the same for all followers
        for(int follower : followers){
            Tweet head = userMap.get(follower).tweet_head;
            
            //add only if not null
            if(head != null) pq.add(head);
        }
        
        int i = 0;
        while(!pq.isEmpty() && i < 10){
            i++;
            Tweet tweet = pq.poll();
            res.add(tweet.id);
            
            //add the next tweet by that user in the max heap so that its also picked up
            if(tweet.next != null) pq.add(tweet.next);
        }
        
        return res;
    }
    
    /** Follower follows a followee. If the operation is invalid, it should be a no-op. */
    public void follow(int followerId, int followeeId) {
        //if he is following himself return
        if(followerId == followeeId) return;
        
        if(!userMap.containsKey(followerId)){
            User user = new User(followerId);
            userMap.put(followerId, user);
        }
        
        if(!userMap.containsKey(followeeId)){
            User user = new User(followeeId);
            userMap.put(followeeId, user);
        }
        
        userMap.get(followerId).follow(followeeId);
    }
    
    /** Follower unfollows a followee. If the operation is invalid, it should be a no-op. */
    public void unfollow(int followerId, int followeeId) {
        if(!userMap.containsKey(followerId) || followerId == followeeId) return;
        
        userMap.get(followerId).unfollow(followeeId);
    }
}

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter obj = new Twitter();
 * obj.postTweet(userId,tweetId);
 * List<Integer> param_2 = obj.getNewsFeed(userId);
 * obj.follow(followerId,followeeId);
 * obj.unfollow(followerId,followeeId);
 */
```
