# Installation

## Pre-requisites
There are a few pre-requisites in order to develop with Xamarin: (On Windows)

1. Visual Studio 2015 has to be installed
2. Xamarin components are installed and up-to-date
3. Windows 10 if you want to run/test Universal Windows Platform (UWP) applications

## If you don't have Visual Studio installed:

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

## If you have Visual Studio installed:

### Check if you have the Xamarin components
1. On the top bar of Visual Studio, navigate to Tools > Options.
2. If Xamarin is installed correctly, there should be a Xamarin option there.

### If you have the Xamarin components
1. Go to Tools > Options > Xamarin > Other.
2. You will find a `Check Now` link which will allow you to update Xamarin. 
![updatexamarin](https://i-msdn.sec.s-msft.com/dynimg/IC841120.jpeg)
3. Update Xamarin to the latest version and you're good to go!

### If you don't have the Xamarin components
1. Go to Control Panel > Programs and Features.
2. Go to Visual Studio 2015 and click `Change`
3. Check these boxes:
  * Cross-Platform Mobile Development > C#/.NET (Xamarin)
  * Cross-Platform Mobile Development > Microsoft Visual Studio Emulator for Android
  * Windows and Web Development > Universal Windows App Development Tools
![components](https://i-msdn.sec.s-msft.com/dynimg/IC841374.jpeg)
4. Click install and let the installer run. (This can take up to a few hours)
5. Done
