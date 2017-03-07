# Xamarin with Bot Framework hands-on-lab

## Mission Brief
Your crew on Mars has lost contact with Earth and as a result is lacking some essential functions for the mission. Your team has some satellite phones running Android, but the communcation tablets are running Windows.

Your crew has just found an alien bot on Mars that understands English, but we need to deploy it in order for us to connect. We also need to use an interface to interact with the bot. As we need a tool that works across all the team's devices, we will be deploying a bot and building an application in Xamarin.

## Mission Setup

There are a few pre-requisites in order to develop with Xamarin: (On Windows)

1. Visual Studio 2015 has to be installed
2. Xamarin components are installed and up-to-date
3. Windows 10 if you want to run/test Universal Windows Platform (UWP) applications

### If you don't have Visual Studio installed:

1. Download Visual Studio 2015 from [here](https://www.visualstudio.com/downloads/)
2. Run the installer
3. Select a custom install  
![custominstall](https://i-msdn.sec.s-msft.com/dynimg/IC845234.jpeg)
4. Check these boxes:
  * Cross-Platform Mobile Development > C#/.NET (Xamarin)
  * Cross-Platform Mobile Development > Microsoft Visual Studio Emulator for Android
  * Windows and Web Development > Universal Windows App Development Tools
![components](https://i-msdn.sec.s-msft.com/dynimg/IC841374.jpeg)
5. Click install and let the installer run. (This can take up to a few hours)
6. Done

### If you have Visual Studio installed:

#### Check if you have the Xamarin components
1. On the top bar of Visual Studio, navigate to Tools > Options.
2. If Xamarin is installed correctly, there should be a Xamarin option there.

#### If you have the Xamarin components
1. Go to Tools > Options > Xamarin > Other.
2. You will find a `Check Now` link which will allow you to update Xamarin. 
![updatexamarin](https://i-msdn.sec.s-msft.com/dynimg/IC841120.jpeg)
3. Update Xamarin to the latest version and you're good to go!

#### If you don't have the Xamarin components
1. Go to Control Panel > Programs and Features.
2. Go to Visual Studio 2015 and click `Change`
3. Check these boxes:
  * Cross-Platform Mobile Development > C#/.NET (Xamarin)
  * Cross-Platform Mobile Development > Microsoft Visual Studio Emulator for Android
  * Windows and Web Development > Universal Windows App Development Tools
![components](https://i-msdn.sec.s-msft.com/dynimg/IC841374.jpeg)
4. Click install and let the installer run. (This can take up to a few hours)
5. Done


### Starting Project
In this repository there is a blank Xamarin.Forms shared project that has been pre-configured with the right nugets for you. You can find it above under `MarsBuddyBlank`.

The main nugets installed in this project are:
- [Bot Connector DirectLine](https://www.nuget.org/packages/Microsoft.Bot.Connector.DirectLine/3.0.0)
- [Rest Client Runtime](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime/)

These nugets allow us to communicate with the bot using pre-defined methods and classes, without the need for manually writing HTTP calls.

Click on the `MarsBuddyBlank` submodule in this repository to download the starting project. 

## Mission Walkthrough
Xamarin allows you to write your code base once in C#/.NET and have it deployed across the 3 popular mobile platforms, iOS, Android and Windows Phone.

This HOL will bring you through deploying a simple bot using the Microsoft Bot Framework, setting up a DirectLine (REST API) connection and building a Xamarin app to work with it:

1. [Publishing a bot and getting DirectLine](https://github.com/ujjwalmsft/XamarinBotHOL/blob/master/MISSION1.md)
2. [Connecting to a bot](https://github.com/ujjwalmsft/XamarinBotHOL/blob/master/MISSION2.md)
3. [Making an interface to interact with the bot](https://github.com/ujjwalmsft/XamarinBotHOL/blob/master/MISSION3.md)

## Mission Check
You can see the final completions for both the missions and challenges in the `CompletedScreenshots` folder.

You can also find the completed project in the submodule above under `MarsBuddyComplete`.

# Mission 1: Publishing a NodeJS bot to Azure

## Introuction

In this mission, we will deploy a bot that uses NodeJS and the Microsoft Bot Framework to Azure. 
This simple bot has already been built for you and you can find the project files above under "marsbot".

There are 3 steps to this tutorial:

1. Publishing the bot to Github
2. Deploying to Azure using CI from Github
3. Registering the bot on the Bot Framework portal 

## Prerequisites

- Install git - https://git-scm.com/downloads
- Make a Microsoft account if you don't have one
- Make a Github account if you don't have one

## Downloading the project

First, go to this [repository](https://github.com/ujjwalmsft/MarsBot) and download the ZIP file. 
Make sure to unarchive it and store it somewhere like your Desktop.

## Initialise a Github repository

A Github repository is a great way to store your code online and collaborate with others on a codebase. You can plug your repository in to a hosted web app and each time you make changes to the repository, the changes automatically deploy onto your web app (this is called Continuous Integration). Log in to [Github](http://github.com). Click on the + sign at the top right hand corner, and then click on New Repository. Name and create your repository. Once that's created, click on the Code tab of your repository. Click on the green "Clone or download" button, then copy the url (it should end with .git). 

Next, open your command prompt.

Navigate to the folder with the project. If your project is on the desktop, the command would be like this:

```shell
cd Desktop/marsbot
```

Now, we need to make the current folder containing your bot a Git repository. Use this command:

```shell
git init
```

We now need to link our local Git folder to the remote Github repository. Type in the following command:

```shell
git remote add origin https://github.com/yourusername/yourrepositoryname.git
```

Make sure you use the url you copied earlier in the above command. Your local Git repository is now remotely tracking your Github repository online. Type `git remote -v` to check that it points to the correct url.

Once that's done, let's commit and push our code to the Github repo. Run the following commands (separately):

```shell
git add .
git commit -m "Initial commit"
git push origin master
```

If you refresh your Github repository online, you should see that your code has been pushed to it. Now let's use continuous integration to deploy the code in our Github repo into a web app hosted online. 

## Set the start command

In your package.json file (if you're using nodejs), we need to update the start script. Update your package.json file to the following:

```js
{
    ...
    "main": "app.js",
    "scripts": {
        "start": "node app.js" // tells the web service where the start script is
    }
    ...
}
```

This step is very important - your bot service may not work if you do not do this.

## Publish the bot online

We have to publish the bot online as the Bot Framework won't be able to talk to a local url. 

Go to the [Azure Portal](https://portal.azure.com). Click on 'New' (it's at the sidebar), go into the web + mobile tab, and click on Web App. Name your web app whatever you'd like, name your resource group something sensible. Your Subscription should be free, and the location your app is hosted on can be anywhere, but it might be good to set it to a region close to you. Go ahead and create your web app.

It might take a while, but you will get notified when your web app has been successfully created. Once it has been created go into All Resources (it's on the sidebar) and look for the web app you just created. Click into it and it should display a dashboard with info about your web app. Click into the Github blade under Choose Source. Then, click into Authorization and log in with your Github credentials. Then, select the project and branch (should be master) that your bot is in. Leave the Performance Test as not configured and hit ok. 

![CI](https://raw.githubusercontent.com/ujjwalmsft/XamarinBotHOL/master/Images/cintegration.PNG)

It may take a while for the latest commit to sync and be deployed to your web app. If the latest commit doesn't seem to be syncing, just hit sync. You'll see a green tick with your latest commit once it's done. 

![CISuccess](https://raw.githubusercontent.com/ujjwalmsft/XamarinBotHOL/master/Images/cintsuccess.PNG)

## Registering your bot on the portal
In order for your bot to talk to the Bot Connector and reach your users on the different channels, the bot has to be first registered on the Bot Framework portal. 

First, go to this link on your browser: https://dev.botframework.com/bots/new

You will be prompted to sign in with your Microsoft account. Take note to use a personal Microsoft account (usually Hotmail, Outlook, MSN, Live email addresses) and not your school or organization's Office365 account.

After signing in, you will be greeted with a simple form that allows you to register your bot. 

#### Make sure your bot's name is "MarsBot".

Most of the fields are self-explanatory. 
- The "Messaging Endpoint" field should be filled with the domain given to you on your Azure Web App, but subdomain to /api/messages.
- The "Create Microsoft App ID and Password" will give you a new ID and password. Save this as we need it later.
- You can also input your Azure Application Insights key if you enabled it when creating the Web App on Azure, but it's optional.

![Registration](https://raw.githubusercontent.com/ujjwalmsft/XamarinBotHOL/master/Images/marsbotregistration.PNG)

## Authorizing your bot
Now that you have the bot deployed on Azure and registered on the Bot Framework, we need to add the App ID and Password on Azure.

Go back to your deployment on Azure and click on App Settings, configuring the App ID and Password we got just now.

![AppSettings](https://raw.githubusercontent.com/ujjwalmsft/XamarinBotHOL/master/Images/marsbotsettings.PNG)

## Managing your new bot
After registering, you'll be sent to the page where you can manage all your bots. Click on the bot you just created. The page should look like this:

![Management](https://raw.githubusercontent.com/ujjwalmsft/XamarinBotHOL/master/Images/marsbotportal.PNG)

The top portion has several useful functions.
- A testing function which will send a simple HTTP request to your messaging endpoint and give you back an appropriate success or error message.
- The Web Chat (iframe) channel that has been pre-embedded for you on the page, allowing you to talk to your bot from the portal

Try writing "Hi" to the bot in the web chat and see if it responds. If it does then we have successfully deployed the bot.

## Setting up Direct Line

![DirectLine](https://raw.githubusercontent.com/ujjwalmsft/XamarinBotHOL/master/Images/marsbotdl.PNG)



Go down to the Direct Line row and click "Add" on the right. Click "Add new site" on the left and add a new site.
You will be given 2 keys, copy the first key and save it somewhere, we will need this key later.

## Finish Line
Now we will have a bot deployed on Azure and a DirectLine key which will allow us to proceed with Mission 2.

# Mission 2: Connecting to a bot
We just deployed the alien bot we found on Mars. There's a problem though. The bot has it's own special set of parameters and communication methods.
As a result, we need to craft a class which will help us in connecting to the bot. We need to establish the right functions in our new class for use in our application later.

## Introduction
In this mission, we will be connecting to the bot. Bots built using the Microsoft Bot Framework have a Direct Line channel.
This channel is essentially a REST API that allows us to interact with the bot using HTTP requests and responses.

Although it is possible to setup your own classes and models for accessing the REST API, it can be troublesome. Luckily, there is a Nuget package published by Microsoft
for use with .NET projects which helps us abstract the REST API calls. The Nuget has already been installed for you in this project.

## Connecting the bot
Our application needs to communicate with the bot in 2 ways: Sending and receiving messages. As a result, we will need to use methods to send messages to the bot as well as constantly receive messages from the bot.

The DirectLine nuget we installed will allow us to more easily implement this within our application without having to write any HTTP calls manually. Let's make a new class where we will contain and abstract all the connection-related code.

Right click on the main project and go to Add > New Item > Class and name it `BotConnection.cs`.

### Imports
We need to import the relevant namespace from the DirectLine nuget package in order to use its classes and methods.
```cs
using Microsoft.Bot.Connector.DirectLine;
```

### Fields
Let's define a few new variables in our new blank class.

```cs
class BotConnection
{
    public DirectLineClient Client = new DirectLineClient("Place key here");
    public Conversation MainConversation;
    public ChannelAccount Account;
}
```

First, we create a new `DirectLineClient` object using a DirectLine key (taken from the bot's portal in Mission 1).

Then, there are another 2 variables for storing the current conversation as well as the user's account, which we will define later.

### Constructor
We will be using the constructor of this class to initialize the `MainConversation` and `Account` fields. These fields will store the information about the current conversation and user.

```cs
class BotConnection
{
    public BotConnection(string accountName)
    {
        MainConversation = Client.Conversations.StartConversation();
        Account = new ChannelAccount { Id = accountName, Name = accountName };
    }
}
```
In this constructor, we can take in a parameter with the user's name to create an account object. We will also start a new conversation using the client.

### Message sending method
Next, we need to craft a method that allows us to send messages to the bot.

```cs
public void SendMessage(string message)
{
    Activity activity = new Activity
    {
        From = Account,
        Text = message,
        Type = ActivityTypes.Message
    };
    Client.Conversations.PostActivity(MainConversation.ConversationId, activity);
}
```
This method will take in a parameter with a simple text message
and use that to create an `Activity` that will be sent to the conversation we initialized.

### Message receiving method
#### MessageListItem Class
We will need to create a class that will be used to store the messages in an `ObservableCollection`.

This class will later be used for data binding in the UI.

Right click on the main project and go to Add > New Item > Class and name it MessageListItem.cs.

Change the class to look like this:

```cs
class MessageListItem
{
    public string Text { get; set; }
    public string Sender { get; set; }

    public MessageListItem(string text, string sender)
    {
        Text = text;
        Sender = sender;
    }
}
```

#### Method implementation
Lastly, we need to have a method that continuously checks the conversation on the server for new messages from the bot.

```cs
public async Task GetMessagesAsync(ObservableCollection<MessageListItem> collection)
{
    string watermark = null;

    //Loop retrieval
    while(true)
    {
        Debug.WriteLine("Reading message every 3 seconds");
        
        //Get activities (messages) after the watermark
        var activitySet = await Client.Conversations.GetActivitiesAsync(MainConversation.ConversationId, watermark);

        //Set new watermark
        watermark = activitySet?.Watermark;

        //Loop through the activities and add them to the list
        foreach(Activity activity in activitySet.Activities)
        {
            if (activity.From.Name == "MarsBot")
            {
                collection.Add(new MessageListItem(activity.Text, activity.From.Name));
            }             
        }

        //Wait 3 seconds
        await Task.Delay(3000);
    }
}
```

This method takes in an `ObservableCollection` typed parameter. 
This collection will later be binded to the UI in Xamarin, so we will need to push any new messages into this collection.

In this method, it checks for new messages every 3 seconds, establishing a watermark every iteration to ensure that we do not retrieve old messages.
Whenever we retrieve a new message, we create a new `MessageListItem` from it and push it into the collection.

In the next mission, we will look into utilizing the class we crafted here. 


# Mission 3: Making an interface to interact with the bot
Now that we've established how to connect to the alien MarsBot, we need to let our team members utilize this connection easily.
By building a quick Xamarin application with a simple UI, our team members will be able to use all their different devices to talk to and get answers from the bot.

## Introduction
In this mission, we will create a simple application page with these components:

1. Create a simple Xamarin UI using XAML
2. Make a `ListView` for displaying the messages between the user and the bot
3. Make a `Entry` for sending messages to the bot
4. Making the BotConnection work with the UI through data binding

## Breaking it down
In the project, there should be a `MainPage.xaml`. This `.xaml` file represents the first page your application will default to when you start it.

Every `.xaml` file also has a "code-behind" file which can be used to contain the code and logic for that page. You can see this file by clicking the small arrow next to the `MainPage.xaml` file and clicking on `MainPage.xaml.cs`.

In this tutorial, we will be using both the `.xaml` and `.xaml.cs` files to design the UI and make it work.

## Laying out the UI
XAML is used to define the visual contents of an application's page. 
It allows you to define the page's elements, including its position, color, text and many other properties.

For example, let's open and look at the default `MainPage.xaml` that we have:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:MarsBuddy"
             x:Class="MarsBuddy.MainPage">

	<Label Text="Welcome to Xamarin Forms!" 
           VerticalOptions="Center" 
           HorizontalOptions="Center" />

</ContentPage>
```

This is a simple layout with 1 `Label` saying "Welcome to Xamarin Forms!" that is horizontally and vertically centered in the application.

Of course, we can also change many other properties of the `Label` in XAML, some examples being size and color. That would look something like this:

```xml
<Label Text="Welcome to Xamarin Forms!" 
        TextColor="#77d065" 
        FontSize = "20"
        VerticalOptions="Center" 
        HorizontalOptions="Center" />
```

For our simple chat application, we want to have 2 things:

1. A `ListView` to show the messages in the conversation
2. A `Entry` (text box) which will use to enter text we want to send to the bot

In this scenario, a `StackLayout` works perfect. A `StackLayout` allows us to easily position elements in our XAML, setting horizontal and vertical properties.

Replace the `Label` with this `StackLayout` element: 

```xml
<StackLayout Spacing="10" Padding="10" HorizontalOptions="Fill" VerticalOptions="Fill" Orientation="Vertical">
</StackLayout>
```

This `StackLayout` fills the whole page, with some padding on the edges. It also defines a spacing of 10 between the elements in a vertical order.

A `StackLayout` is useless without elements in it. Let's add in `ListView` and `Entry` elements into the `StackLayout`.

```xml
<StackLayout Spacing="10" Padding="10" HorizontalOptions="Fill" VerticalOptions="Fill" Orientation="Vertical">
        <ListView x:Name="MessageListView"
                        VerticalOptions="StartAndExpand"
                        HorizontalOptions="Fill"
                        >
        </ListView>
    
        <Entry Placeholder="Message"
                VerticalOptions="End"
                HorizontalOptions="Fill"
                HorizontalTextAlignment="End"
                />
</StackLayout>
```

In this `StackLayout`, we've added a `ListView` and `Entry`. It's important for us to also define the `VerticalOptions` and `HorizontalOptions` properties of the elements
so that the elements know how to be positioned within the `StackLayout`.

The `ListView` in it's current state won't be able to work properly though. Remember that we define the visual properties of elements within our XAML, but
a `ListView` is special in the sense that it has its own elements as well. When the list is populated, it will have its own rows/cells.

Currently, our `ListView` doesn't know how it should display these cells. Luckily, it's fairly simple to define how these cells should be displayed.

In this snippet, we use a simple `TextCell`, which is a pre-defined cell type provided by Xamarin. It's a simple cell that has Text and Detail properties.

```xml
<ListView x:Name="MessageListView"
                VerticalOptions="StartAndExpand"
                HorizontalOptions="Fill"
                >
        <ListView.ItemTemplate>
                <DataTemplate>
                <TextCell Text="{Binding Text}" Detail="{Binding Sender}" />
                </DataTemplate>
        </ListView.ItemTemplate>
</ListView>
```

## Connecting the bot to this page
Since we've already abstracted all the connection logic into a different class in Mission 1,
we can simply make a new object to connect to the bot in code.

Open the code-behind file `MainPage.xaml.cs` and simply make a new object with your name in the constructor parameter:

```cs
//Initialize a connection with ID and Name
BotConnection connection = new BotConnection("James");
```

Done! Now this page in your application will be able to access the bot through code.

## Data binding
### Introduction
Often times, UI isn't static. It is dynamic and needs to display data accordingly.

For example, if we wanted to populate a `ListView`, we can't just hardcode data in. That makes the list pretty useless.
What you would do instead, is to retrieve data from a database or service and display it on the list.

But then comes another problem. Data changes all the time and updates can be made to the data. If the data is updated,
we will need to manually update the displayed list as well, which means you have to write more code.

As developers, we want a easier way to do this and that's where data binding comes in.
Data binding allows you to establish a contract bewteen the data and the display.

### ListView Binding
In our case, the `ListView` will be used to display messages to and from the bot. We will use an `ObservableCollection`, which is a special collection type that can be binded to a `ListView`.

Previously in Mission 1, we created a `MessageListItem` class that we will be able to use here. 

Let's open `MainPage.xaml.cs` and make a new `ObservableCollection` that takes in the type `MessageListItem`.

```cs
ObservableCollection<MessageListItem> messageList = new ObservableCollection<MessageListItem>();
```

The reason we created and used a custom `MessageListItem` class with the properties `Text` and `Sender`, is to bind the properties to the cells in the list.

You can see that binding in the XAML of the `ListView`.
```xml
<TextCell Text="{Binding Text}" Detail="{Binding Sender}" />
```

Previously, in our XAML, we gave the `ListView` a name of "MessageListView". Assigning a name to the element in XAML allows us to access it as a variable
in the code-behind file of the XAML. 

Let's use that to bind our newly created `ObservableCollection` to the `ListView` in the constructor of the MainPage.

```cs
//Initialize a connection with ID and Name
BotConnection connection = new BotConnection("James");

//ObservableCollection to store the messages to be displayed
ObservableCollection<MessageListItem> messageList = new ObservableCollection<MessageListItem>();

public MainPage()
{
    InitializeComponent();

    //Bind the ListView to the ObservableCollection
    MessageListView.ItemsSource = messageList;
}
```
Now that's done! Any new additions to the `messageList` collection will magically reflect on the UI in the `MessageListView`.

### Connecting messages to the collection
Let's revise what we currently have. At the moment, we have a `ListView` UI element that has been binded to an `ObservableCollection`.
This means any changes to the collection will reflect in the `ListView`. 

Every `MessageListItem` object added to the collection will also get it's own cell with the message data in the `ListView`.

Now that the binding has been setup, we just have to let any new messages that come in be added to the `ObservableCollection`.
This is where our Mission 1 method comes in handy. We can simply do this:

```cs
//Initialize a connection with ID and Name
BotConnection connection = new BotConnection("James");

//ObservableCollection to store the messages to be displayed
ObservableCollection<MessageListItem> messageList = new ObservableCollection<MessageListItem>();

public MainPage()
{
    InitializeComponent();

    //Bind the ListView to the ObservableCollection
    MessageListView.ItemsSource = messageList;

    //Start listening to messages and add any new ones to the collection
    var messageTask = connection.GetMessagesAsync(messageList);
}
```

## Input events
We also have a `Entry` box that allows the user to enter messages. We need to make it so that when the user presses enter, it sends a message to the bot.

In order to do that, we have to link the UI up to the code. We want a method to execute when the user presses return.

We can do that by setting an event in the XAML of the `Entry` element.

```xml
<Entry Placeholder="Message"
        VerticalOptions="End"
        HorizontalOptions="Fill"
        HorizontalTextAlignment="End"
        Completed="Send"
        />
```

What this change does is that it tells the program: "Hey, when the user presses return, run the Send() method".

Now that we've declared this in the XAML, we also need to define the method in the code-behind file.

Open `MainPage.xaml.cs` and define a new method named Send():

```cs
public void Send(object sender, EventArgs args)
{
        //Get text in entry
        var message = ((Entry)sender).Text;

        if(message.Length > 0)
        {
            //Clear entry
            ((Entry)sender).Text = "";

            //Make object to be placed in ListView
            var messageListItem = new MessageListItem(message, connection.Account.Name);
            messageList.Add(messageListItem);

            //Send the message to the bot
            connection.SendMessage(message);
        }
}
```

Now this method will be executed whenever someone presses return on the `Entry` box:

1. Get the user's message
2. Clear the entry box
3. Add the message into the collection for display
4. Send the message to the bot

## Finish Line
At the end, you should have an application that can talk to the bot.

Try asking it a few questions to test it!

1. How big is mars?
2. How far away is mars?
3. Is there life on mars?

You should get a reply from the bot.

You'll notice there's a an issue with the UI when you run it on Android however. The message cuts off if it's too long and the cells aren't suitable for messages.
We'll look into this in Challenge 1 later.

# Challenge 1: Quality Control
If you finished Mission 2, you would realize there's a problem with the `ListView` on Android: the messages cut off if they are too long.

The issue here is that the default `TextCell` in the ListView will cut off text that is too long by default.

```xml
<ListView x:Name="MessageListView"
                VerticalOptions="StartAndExpand"
                HorizontalOptions="Fill"
                >
        <ListView.ItemTemplate>
                <DataTemplate>
                <TextCell Text="{Binding Text}" Detail="{Binding Sender}" />
                </DataTemplate>
        </ListView.ItemTemplate>
</ListView>
```

As a result, we will need to use a custom cell instead for the template.

You can look at how to define a custom cell in XML here:
https://developer.xamarin.com/guides/xamarin-forms/user-interface/listview/customizing-cell-appearance/

You'll also need to configure the `ListView` to allow uneven rows.

## Finishing Requirements
At the end of this challenge, the cells in the `ListView` should be flexible and adapt its size according to the contents,
therefore allowing for longer messages to be displayed.

# Challenge 2 Solution

## Introduction
In this mission, we will implement a camera control in our application and send the taken photo to the [Microsoft Computer Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api).
The CV API is part of the Microsoft Cognitive Services, a set of easy-to-use APIs which expose artificial intelligence and machine learning. The CV API allows us to detect what's in an image.

Although the CV API is a web service which requires HTTP requests and responses to work, it has a .NET library which will allow us photo
simply call methods within our application. This means that we won't need to manually structure our HTTP requests and handle JSON files.

There are 2 steps to this mission:

1. Implement a camera function
2. Send the captured image to the Computer Vision API and get a result


## Setup

### Nugets needed
There are 2 Nugets which we want to install in our project:

1. Xamarin Media Plugin
  * For camera controls
2. Computer Vision Client library
  * To work with the Computer Vision API

### Installation steps

![step1](https://github.com/ujjwalmsft/XamarinBotHOL/blob/master/Images/solutionnugets.png) 

1. Right-click on the solution and click "Manage NuGet packages for solution".
2. Click on the "Browse" tab
3. Search for `Xam.Plugin.Media`
4. Tick all the boxes on the right for the 3 platforms
5. Click install

Repeat the above steps and install `Microsoft.ProjectOxford.Vision` as well.

## Implementing the camera
Xamarin.Forms doesn't natively provide the ability to access camera APIs, 
but the `Xam.Plugin.Media` plugin helps us to access the camera APIs on each native platform in shared code.

### Setting up the plugin

In this lab, we will be testing the application in UWP, since only the UWP application runs on your computer natively and will be able to access your webcam.

We need to enable the webcam permission on the UWP project for testing.

1. Open `Package.appxmanifest` in your UWP project.
2. Click the Capabilities tab
3. Tick the Webcam checkbox
4. Done!

Next, we need to initialize the plugin in code. Open `MainPage.xaml.cs` and add the plugin namespace, initializing it in the constructor:

```cs
using Plugin.Media;

public MainPage()
{
    InitializeComponent();

    //Bind the ListView to the ObservableCollection
    MessageListView.ItemsSource = messageList;

    //Start listening to messages
    Task.Run(() => connection.GetMessagesAsync(messageList));

    //Initialize camera plugin
    CrossMedia.Current.Initialize();
}
```

Done! Now we can call the plugin in other parts of the code and it will be able to access the camera in UWP.

### Triggering the camera

We want to make it so that the camera opens on a button click. Let's first define a button in our `MainPage.xaml`
below the `Entry` box.

```xml
<StackLayout Spacing="10" Padding="10" HorizontalOptions="Fill" VerticalOptions="Fill" Orientation="Vertical">
        <ListView x:Name="MessageListView"
                        VerticalOptions="StartAndExpand"
                        HorizontalOptions="Fill"
                        >
            <ListView.ItemTemplate>
              <DataTemplate>
                <TextCell Text="{Binding Text}" Detail="{Binding Sender}" />
              </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    
        <Entry Placeholder="Message"
                VerticalOptions="End"
                HorizontalOptions="Fill"
                HorizontalTextAlignment="End"
                />

        <Button Text="Take Picture"
          VerticalOptions="End"
          HorizontalOptions="Fill"
          Clicked="TakePic"
          />
</StackLayout>
```

In the XAML, we defined that when we click the button, we should execute the `TakePic()` method.

Let's define our method in `MainPage.xaml.cs` to open the camera.

```cs
public async void TakePic(object sender, EventArgs args)
{
    //Check if camera is available
    if (CrossMedia.Current.IsCameraAvailable && CrossMedia.Current.IsTakePhotoSupported)
    {
        //Supply media options for saving our photo after it's taken.
        var mediaOptions = new Plugin.Media.Abstractions.StoreCameraMediaOptions
        {
            Directory = "Receipts",
            Name = $"{DateTime.UtcNow}.jpg"
        };

        //Get taken picture
        var file = await CrossMedia.Current.TakePhotoAsync(mediaOptions);
    }
}
```

Using the Xamarin Media Plugin makes it simple to call the camera on any platform. After checking for camera availability
and specifying the format which we want to save the picture, we can get the picture taken in a variable.

## Implementing Computer Vision
Now that we have the camera setup and can get the captured picture from it, we need to pass it into the Computer Vision API.

Since we installed a Nuget that helps us interact with the API, let's make a simple method that uses the client library.

First, we need to initialize the client library with our CV API key. (I've provided an API key here for convenience)

```cs
using Microsoft.ProjectOxford.Vision;
using Microsoft.ProjectOxford.Vision.Contract;

//Computer Vision client
VisionServiceClient visionClient = new VisionServiceClient("775c63123c104445bbc227eb90496098");
```

Then, we can define the method:

```cs
public async Task<AnalysisResult> GetImageDescriptionAsync(Stream imageStream)
{
    VisualFeature[] features = { VisualFeature.Tags, VisualFeature.Categories, VisualFeature.Description };
    var result = await visionClient.AnalyzeImageAsync(imageStream, features.ToList(), null);
    return result;
}
```

This simple method takes in a stream, passes it into the API and returns the result. 

We can now call this method in our `TakePic()` function.

```cs
public async void TakePic(object sender, EventArgs args)
{
    if (CrossMedia.Current.IsCameraAvailable && CrossMedia.Current.IsTakePhotoSupported)
    {
        //Supply media options for saving our photo after it's taken.
        var mediaOptions = new Plugin.Media.Abstractions.StoreCameraMediaOptions
        {
            Directory = "Receipts",
            Name = $"{DateTime.UtcNow}.jpg"
        };

        //Get taken picture
        var file = await CrossMedia.Current.TakePhotoAsync(mediaOptions);
        var fileStream = file.GetStream();

        //Display loading
        await DisplayAlert("Loading Result", "Please wait", "OK");
        
        //Send file to ComputerVision
        var result = await GetImageDescriptionAsync(fileStream);
        await DisplayAlert("Detection Result", "I think it's " + result.Description.Captions[0].Text, "OK");
    }
}
```

After getting the file from the camera, we convert that into a stream and pass it into the CV API and display the result in an alert window.

Done! Your users should now be able to click the button, take a picture and get an analysis result.