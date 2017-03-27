# CDF Tweet UI Module (@cdf/cdf-ng-tweet)
[![version][npm-image]][npm-url]
[![downloads][downloads-image]][downloads-url]

> CDF-NG-TWEET is an Angular module containing UI components for displaying Twitter tweeets.  CDF-NG-TWEET is a UI module existing in [Content Delivery Framework's][cdf-url] eco-system.

> Happy Coding!

![](logo-535x141.png)

# Requirements
CDF-NG-TWEET requires the latest version of Angular (at the time of this writing: 2.4.7).
```sh
  //package.json
  
  "dependencies": {
    "@angular/common": "2.4.7",
    "@angular/compiler": "2.4.7",
    "@angular/core": "2.4.7",
    "@angular/forms": "2.4.7",
    "@angular/http": "2.4.7",
    "@angular/platform-browser": "2.4.7",
    "@angular/platform-browser-dynamic": "2.4.7",
    "@angular/router": "3.4.7"
	...
  }
```


# Installation


## Installing CDF-NG-TWEET in your Angular application:
```sh
    //INSTALL CDF-NG-TWEET

    npm install @cdf/cdf-ng-tweet --save
    
```

# How to use CDF-NG-TWEET


```sh

//STEP 1: QUERY TWITTER FOR TWEETS
     
    getTweets() : Observable<any> 
    {
         let url = 'https://api.twitter.com/1.1/statuses/user_timeline.json?count=20&screen_name=XXXXX';
         
         return this.http.get(url)
                         .map((res:Response) => res.json())
                         .catch((error:any) => Observable.throw(error.json().error));
    }

//STEP 2 CONVERT RAW JSON FROM TWITTER INTO CdfTweetModel
	
	import { CdfTweetModel } from '@cdf/cdf-ng-tweet/lib';

	...

	tweetList : CdfTweetModel[] = [];
	
	getTweets().subscribe
	(
		(rawJson) =>
		{
			//TWITTER DATA
			for (let entry of rawJson) 
			{
				this.tweetList.push(new CdfTweetModel(entry));
			}			
		}
	);

//STEP 3 Display Tweets

	<section *ngFor="let item of tweetList">
		<cdf-tweet [tweetModel]="item"></cdf-tweet>
	</section>

```



# CDF-NG-TWEET Models
CDF-NG-TWEET containes the following models:
* CdfTweetModel
* CdfTweetUserModel

## *CdfTweetModel*
CdfTweetModel is the model containing data about a Tweet from Twitter.  CdfTweetModel contains the following data points:

```sh
	Id: string;
	Text: string;
	User: CdfTweetUserModel;
	MediaUrl: string;
	HashTags: string[] = [];
	CreatedAt: string;
	TimeStamp: Date; 
```
  
## *CdfTweetUserModel*
CdfTweetUserModel is the model containing data about the Tweet author.  CdfTweetUserModel contains the following data points:

```sh
	Id: string;
	Name: string;
	ScreenName: string;
	Description: string;
	Location: string;
	ProfileImageUrl: string;
	ProfileImageUrlHttps: string;	
	CreatedAt : string;
```


# CDF-NG-TWEET Components
CDF-NG-TWEET containes the following components:
* CdfTweetComponent


## **CdfTweetComponent**
**CdfTweetComponent** is the component used to display a Twitter tweet.  CDF-NG-TWEET contains a service, CdfTweetService, responsible for loading Twitter JavaScript widget (https://platform.twitter.com/widgets.js).  See [Twitter Embeded Timelines][twitter-embedded-timeline-url] for more details.  

The Twitter widget is responsible for rendering a tweet.  This component relies upon a connection to Twitter to render the tweet.  If the connection is lost, or is not available, then the component simply renders the Tweet's text and timestamp.  Otherwise, if a connection exists, the component uses Twitter's JavaScript widget to render the tweet.


Tweet rendered by Twitter:

![][cdf-ng-tweet-url]

Tweet rendered when Twitter not loaded/available:

![][cdf-ng-tweet-no-connection-url]





# Helpful Links
* [Angular](https://angular.io/)
* [Twitter Embeded Timelines][twitter-embedded-timeline-url]
* [Solutia Consulting](http://solutiaconsulting.com)


## Release History

* 1.0.0
  * initial development

# Meta

Tom Schreck – [@tschreck](https://twitter.com/tschreck) – tom_schreck@solutiaconsulting.com

[https://github.com/tomschreck](https://github.com/tomschreck)

# License

[MIT](https://opensource.org/licenses/MIT)

[npm-image]: https://img.shields.io/npm/v/@cdf/cdf-ng-tweet.svg?style=flat-square
[npm-url]: https://www.npmjs.com/package/@cdf/cdf-ng-tweet
[downloads-image]: https://img.shields.io/npm/dm/@cdf/cdf-ng-tweet.svg?style=flat-square
[downloads-url]: https://npm-stat.com/charts.html?package=%40cdf%2Fcdf-ng-tweet&from=2017-03-01
[license-image]: https://img.shields.io/npm/l/@cdf/cdf-ng-tweet.svg?style=flat-square
[license-url]: http://opensource.org/licenses/MIT
[twitter-embedded-timeline-url]:https://dev.twitter.com/web/embedded-timelines
[cdf-url]:http://cdf.cloud/

[cdf-ng-tweet-url]:http://admin.cdf.cloud/domain-images/cdf-ng-tweet.png
[cdf-ng-tweet-no-connection-url]:http://admin.cdf.cloud/domain-images/cdf-ng-tweet-no-connection.png