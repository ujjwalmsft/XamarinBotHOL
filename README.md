# Mars Mission - Xamarin with Bot Framework hands-on-lab

## Mission Brief
Your crew on Mars has lost contact with Earth and as a result is lacking some essential functions for the mission. Your team has some satellite phones running Android, but the communcation tablets are running Windows.

Your crew has just found an alien bot on Mars that understands English, but we need to deploy it in order for us to connect. We also need to use an interface to interact with the bot. As we need a tool that works across all the team's devices, we will be deploying a bot and building an application in Xamarin.

## Mission Setup
### Installation
Go through this [document](https://github.com/jamesleeht/XamarinMarsHOL/blob/master/INSTALL.md) to ensure that your Xamarin has been installed and setup correctly.

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

1. [Publishing a bot and getting DirectLine](https://github.com/jamesleeht/XamarinMarsHOL/blob/master/MISSION1.md)
2. [Connecting to a bot](https://github.com/jamesleeht/XamarinMarsHOL/blob/master/MISSION2.md)
3. [Making an interface to interact with the bot](https://github.com/jamesleeht/XamarinMarsHOL/blob/master/MISSION3.md)

If you've finished the missions, there are some challenges for you to complete to and win some prizes.

1. [Challenge 1: Custom ListView Cells](https://github.com/jamesleeht/XamarinMarsHOL/blob/master/CHALLENGE1.md)
2. [Challenge 2: Computer Vision with Camera](https://github.com/jamesleeht/XamarinMarsHOL/blob/master/CHALLENGE2.md)

## Mission Check
You can see the final completions for both the missions and challenges in the `CompletedScreenshots` folder.

You can also find the completed project in the submodule above under `MarsBuddyComplete`.

## Contributions
Feel free to fork this repository for your own use, or make a pull request and contribute to this repository if you have any suggestions.