[Click for Xamarin.iOS Version](https://github.com/CloudRail/cloudrail-si-xamarin-ios-sdk)

[Click for Xamarin.Android Version](https://github.com/CloudRail/cloudrail-si-xamarin-android-sdk)

<p align="center">
  <img width="200px" src="http://cloudrail.github.io/img/cloudrail_logo_github.png"/>
</p>

# CloudRail SI for .NET
Integrate Multiple Services With Just One API

<p align="center">
  <img width="300px" src="http://cloudrail.github.io/img/cloudrail_si_github.png"/>
</p>

CloudRail is an API integration solution which abstracts multiple APIs from different providers into a single and universal interface.

**Current Interfaces:**
<p align="center">
  <img width="800px" src="http://cloudrail.github.io/img/available_interfaces_v3.png"/>
</p>

---
---

Full documentation can be found at our [website](https://cloudrail.com/integrations).

Learn more about CloudRail on https://cloudrail.com

---
---
With CloudRail, you can easily integrate external APIs into your application.
CloudRail is an abstracted interface that takes several services and then gives a developer-friendly API that uses common functions between all providers.
This means that, for example, Upload() works in exactly the same way for Dropbox as it does for Google Drive, OneDrive, and other Cloud Storage Services, and GetEmail() works similarly the same way across all social networks.

## Download Nuget Package or DLL and Basic setup
You can download CloudRail SDK Nuget Package from:
https://www.nuget.org/packages/CloudRail.SDK
Or just download and add the DLL `CloudRailSI.dll` file to your project reference
and starting using it. 
**Note**: If you are using the DLL you must download the Dependecies. 

```groovy
using Com.Cloudrail.SI;

CloudRail.AppKey = "{Your_License_Key}";
```
[Get a free license key here](https://cloudrail.com/signup)

## Dependencies Required for DLL
Use the specific version number for Newtonsoft.Json which is 10.0.3
[Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/10.0.3)

[OpenSSL.X509Certificate2.Provider](https://www.nuget.org/packages/OpenSSL.X509Certificate2.Provider/1.2.0)

## Platforms Support
Cloudrail SDK is built with Microsoft .NET Standard 2.0 which supports the following platforms: 
[Platform Support](https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md#platform-support)

## Current Interfaces
Interface | Included Services
--- | ---
Cloud Storage | Dropbox, Google Drive, OneDrive, Box, pCloud, Egnyte, OneDrive Business
Business Cloud Storage | AmazonS3, Microsoft Azure, Rackspace, Backblaze, Google Cloud Platform
Social Profiles | Facebook, GitHub, Google+, LinkedIn, Slack, Twitter, Windows Live, Yahoo, Instagram, Heroku
Social Interaction | Facebook, FacebookPage, Twitter
Payment | PayPal, Stripe
Email | Maljet, Sendgrid, Gmail
SMS | Twilio, Nexmo
Point of Interest | Google Places, Foursquare, Yelp
Video | YouTube, Twitch, Vimeo
Messaging | Facebook Messenger, Telegram, Line, Viber, SlackBot
---
### Cloud Storage Interface:

* Dropbox
* Box
* Google Drive
* Microsoft OneDrive
* pCloud
* Egnyte
* OneDrive Business

#### Features:

* Download files from Cloud Storage.
* Upload files to Cloud Storage.
* Upload files with modified date to Cloud Storage.
* Get Meta Data of files, folders and perform all standard operations (copy, move, etc) with them.
* Retrieve user and quota information.
* Generate share links for files and folders.

[Full Documentation](https://cloudrail.com/integrations/interfaces/CloudStorage;platformId=DotNet)
#### Code Example:

```` csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.CloudRail.SI.ServiceCode.Commands.CodeRedirect;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";

// ICloudStorage cs = new Box(RedirectReceiver, "[clientIdentifier]", "[clientSecret]","[redirectUri]", "[state]");
// ICloudStorage cs = new OneDrive(RedirectReceiver, "[clientIdentifier]", "[clientSecret]","[redirectUri]", "[state]");
// ICloudStorage cs = new PCloud(RedirectReceiver, "[clientIdentifier]", "[clientSecret]","[redirectUri]", "[state]");
// ICloudStorage cs = new GoogleDrive(RedirectReceiver, "[clientIdentifier]", "", "[redirectUri]", "[state]");

ICloudStorage cs = new Dropbox(RedirectReceiver, "[clientIdentifier]", "", "[redirectUri]", "[state]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
        IList<CloudMetaData> filesFolders = cs.GetChildren("/");
        //IList<CloudMetaData> filesFolders = cs.GetChildrenPage("/", 1, 4);  // Path, Offet, Limit
        //cs.Upload(/image_2.jpg,Stream,1024,true);   // Path and Filename, Stream (data), Size, overwrite (true/false)
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }
})).Start();
````
---

### Business Cloud Storage Interface:

* Amazon S3
* Microsoft Azure
* Rackspace
* Backblaze
* Google Cloud Platform

#### Features:

* Create, delete and list buckets
* Upload files
* Download files
* List files in a bucket and delete files
* List files in a with prefix
* Get file metadata (last modified, size, etc.)

[Full Documentation](https://cloudrail.com/integrations/interfaces/BusinessCloudStorage;platformId=DotNet)
#### Code Sample
```` csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";


// IBusinessCloudStorage cs = new MicrosoftAzure(null, "[accountName]", "[accessKey]");
// IBusinessCloudStorage cs = new Rackspace(null, "[username]", "[apiKey]", "[region]");
// IBusinessCloudStorage cs = new Backblaze(null, "[accountId]", "[appKey]");
// IBusinessCloudStorage cs = new GoogleCloudPlatform(null, "[clientEmail]", "[privateKey]", "[projectId]");
IBusinessCloudStorage cs = new AmazonS3(null, "[accessKeyId]", "[secretAccessKey]", "[region]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
        Bucket bucket = cs.CreateBucket("");
        cs.UploadFile(bucket,"Data.csv",stream,stream.Length);
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

})).Start();
````

---

### Social Media Profiles Interface:

* Facebook
* Github
* Google Plus
* LinkedIn
* Slack
* Twitter
* Windows Live
* Yahoo
* Instagram
* Heroku

#### Features

* Get profile information, including full names, emails, genders, date of birth, and locales.
* Retrieve profile pictures.
* Login using the Social Network.

[Full Documentation](https://cloudrail.com/integrations/interfaces/Profile;platformId=DotNet)
#### Code Example:

```` csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.CloudRail.SI.ServiceCode.Commands.CodeRedirect;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";


// IProfile profile = = new Twitter(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
// IProfile profile = new GooglePlus(RedirectReceiver, "[clientIdentifier]", "", "[redirectUri]", "[state]");
// IProfile profile = new GitHub(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
// IProfile profile = new Slack(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
// IProfile profile = new Instagram(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
// IProfile profile = new MicrosoftLive(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
// ...
IProfile profile = new Facebook(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
       Console.WriteLine("Email: {0}", profile.GetEmail());
       Console.WriteLine("Name: {0}", profile.GetFullName());
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

})).Start();
````
---

### Social Media Interaction Interface:

* Facebook
* FacebookPage
* Twitter

#### Features

* Get a list of connections.
* Make a post for the user.
* Post images and videos.

[Full Documentation](https://cloudrail.com/integrations/interfaces/Social;platformId=DotNet)
#### Code Example:

```` csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.CloudRail.SI.ServiceCode.Commands.CodeRedirect;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";


// ISocial social = new Twitter(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
// ISocial social = new FacebookPage(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
ISocial social = new Facebook(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
       social.PostUpdate("Hey there! I'm using CloudRail.");
       IList<String> connections = social.GetConnections();
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

})).Start();
````
---

### Payment Interface:

* PayPal
* Stripe

#### Features

* Perform charges
* Refund previously made charges
* Manage subscriptions

[Full Documentation](https://cloudrail.com/integrations/interfaces/Payment;platformId=DotNet)
#### Code Example

```` csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";


// IPayment payment = new Stripe(null, "[secretKey]");
IPayment payment = new PayPal(null, true, "[clientIdentifier]", "[clientSecret]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
       CreditCard source = new CreditCard(null, 6, 2021, "xxxxxxxxxxxxxxxx", "visa", "<FirstName>", "<LastName>", null);
       Charge charge = payment.CreateCharge(500, "USD", source);
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

})).Start();
````
---
### Email Interface:

* Mailjet
* Sendgrid
* Gmail

#### Features

* Send Email (with Attachments)

[Full Documentation](https://cloudrail.com/integrations/interfaces/Email;platformId=DotNet)

#### Code Example

```` csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.CloudRail.SI.ServiceCode.Commands.CodeRedirect;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";


// IEmail email = new MailJet(null, "[clientIdentifier]", "[clientSecret]");
// IEmail email = new GMail(RedirectReceiver, "[clientIdentifier]", "", "[redirectUri]", "[state]");
IEmail email = new SendGrid(null, "API Key");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
       IList<string> toAddresses = new List<string>();
       toAddresses.Add("foo@bar.com");
       toAddresses.Add("bar@foo.com");
       
       Attachment imageFile = new Attachment(Stream, "image/jpg", "File.jpg"); //Stream, MimeType, File Name
       IList<Attachment> attachments = new List<Attachment>();
       attachments.Add(imageFile);
       
       email.SendEmail("info@cloudrail.com", "CloudRail", toAddresses, "Welcome", "Hello from CloudRail", null, null, null, attachments);
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

})).Start();
````
---
### SMS Interface:

* Twilio
* Nexmo
* Twizo

#### Features

* Send SMS

[Full Documentation](https://cloudrail.com/integrations/interfaces/SMS;platformId=DotNet)

#### Code Example

````csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";


// ISMS sms = new Nexmo(null, "[clientIdentifier]", "[clientSecret]");
// ISMS sms = new Twizo(null, "[clientIdentifier]");
ISMS sms = new Twilio(null, "[clientIdentifier]", "[clientSecret]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
       sms.SendSMS("CloudRail", "+4912345678", "Hello from CloudRail");
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

})).Start();
````
---
### Points of Interest Interface:

* Google Places
* Foursquare
* Yelp

#### Features

* Get a list of POIs nearby
* Filter by categories or search term

[Full Documentation](https://cloudrail.com/integrations/interfaces/PointsOfInterest;platformId=DotNet)
#### Code Example

```` csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";


// IPointsOfInterest poi = new Foursquare(null, "[clientID]", "[clientSecret]");
// IPointsOfInterest poi = new Yelp(null, "[consumerKey]", "[consumerSecret]", "[token]", "[tokenSecret]");
IPointsOfInterest poi = new GooglePlaces(null, "[apiKey]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
       List<string> categories = new List<String>
       {
            "restaurant"
       };

       IList<POI> res = poi.GetNearbyPOIs(9.4557091, 8.5279138, 1000, "pizza", categories);
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

})).Start();
````
---
### Video Interface:

* YouTube
* Twitch
* Vimeo

#### Features

* Search for videos
* Upload videos
* Get a list of videos for a channel
* Get channel details
* Get your own channel details
* Get video details 

[Full Documentation](https://cloudrail.com/integrations/interfaces/Video;platformId=DotNet)
#### Code Example

```` csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.CloudRail.SI.ServiceCode.Commands.CodeRedirect;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";


// IVideo video = new Twitch(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
// IVideo video = new Vimeo(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");
IVideo video = new YouTube(RedirectReceiver, "[clientIdentifier]", "[clientSecret]", "[redirectUri]", "[state]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
    try
    {
       IList<VideoMetaData> searchVideos = video.SearchVideos("Game of Thrones", 0, 1);  // Query, Offet, Limit
        //VideoMetaData videoData = video.UploadVideo("Best Video","One of my best videos",stream,1024, "channelID", "video/mp4");   // Title, Description, Stream (data), Size, ChannelID (optional for Youtube) and Video Mime type
        
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

})).Start();
````
---
### Messaging Interface:

* FacebookMessenger
* Telegram
* Line
* Viber
* SlackBot

#### Features

* Send text messages
* Send files, images, videos and audios
* Parse a message received on your webhook
* Download the content of an attachment sent to your webhook

#### Code Example - Objective-C
[Full Documentation](https://cloudrail.com/integrations/interfaces/Messaging;platformId=DotNet)

```csharp
using Com.Cloudrail.SI;
using Com.Cloudrail.SI.Interfaces;
using Com.Cloudrail.SI.Exceptions;
using Com.Cloudrail.SI.Services;
using Com.Cloudrail.SI.Types;

CloudRail.AppKey = "{Your_License_Key}";

IMessaging service;

// service = new Viber(null, "[Bot Token]", "[Webhook URL]", "[Bot Name]");
// service = new Telegram(null, "[Bot Token]", "[Webhook URL]");
// service = new Line(null, "[Bot Token]");
// service = new SlackBot(null, "[Bot Token]");

service = new FacebookMessenger(null, "[Bot Token]");

new System.Threading.Thread(new System.Threading.ThreadStart(() =>
{
	try
	{
	    Message result = service.SendMessage("12123242","It's so easy to send message via CloudRail");
	    Console.WriteLine(result);
	}
	catch (Exception e)
	{
	   Console.WriteLine(e.Message);
	}

})).Start();

```
---

More interfaces are coming soon.

## Advantages of Using CloudRail

* Consistent Interfaces: As functions work the same across all services, you can perform tasks between services simply.

* Easy Authentication: CloudRail includes easy ways to authenticate, to remove one of the biggest hassles of coding for external APIs.

* Switch services instantly: One line of code is needed to set up the service you are using. Changing which service is as simple as changing the name to the one you wish to use.

* Simple Documentation: There is no searching around Stack Overflow for the answer. The CloudRail documentation at https://cloudrail.com/integrations is regularly updated, clean, and simple to use.

* No Maintenance Times: The CloudRail Libraries are updated when a provider changes their API.

* Direct Data: Everything happens directly in the Library. No data ever passes a CloudRail server.

## Sample Applications

If you don't know how to start or just want to have a look at how to use our SDK in a real use case, we created a few sample application which you can try out:

* Sample using the CloudStorage interface: [UnifiedCloudStorage](https://github.com/CloudRail/cloudrail-si-dotnet-sdk/tree/master/Examples/UnifiedCloudStorage)
* Sample using the Social Profile interface: [UnifiedSocialProfile](https://github.com/CloudRail/cloudrail-si-dotnet-sdk/tree/master/Examples/UnifiedSocialProfile)
* Sample using the Bucket Storage interface: [UnifiedBucketCloudStorage](https://github.com/CloudRail/cloudrail-si-dotnet-sdk/tree/master/Examples/UnifiedBucketCloudStorage)

## License Key

CloudRail provides a developer portal which offers usage insights for the SDKs and allows you to generate license keys.

It's free to sign up and generate a key.

Head over to https://cloudrail.com/signup

## Pricing

Learn more about our pricing on https://cloudrail.com/pricing

## Other Platforms

CloudRail is also available for other platforms like Xamarin(iOS/Android), iOS, Java and NodeJS. You can find all libraries on https://cloudrail.com

## Questions?

Get in touch at any time by emailing us: support@cloudrail.com

or

Tag a question with cloudrail on [StackOverflow](http://stackoverflow.com/questions/tagged/cloudrail)
