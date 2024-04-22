# Meeting SDK for Windows - Local Recording
A Windows C++ Application demonstrate Zoom Meeting SDK receiving Local Recording from a Zoom Meeting, containerized

# Install vcpkg for adding dependency libs.
You might need to use Powershell (as administrator) or Windows Terminal to execute the sh script files
```
cd ~
cd source
git clone https://github.com/Microsoft/vcpkg.git
cd vcpkg
./bootstrap-vcpkg.sh
./vcpkg integrate install --vcpkg-root c:\vcpkg
```

# Add dependency libs


```
./vcpkg install jsoncpp
./vcpkg install curl
```



## Add a configuration file named `config.json`
## Disclaimer
Please be aware that all hard-coded variables and constants shown in the documentation and in the demo, such as Zoom Token, Zoom Access, Token, etc., are ONLY FOR DEMO AND TESTING PURPOSES. We STRONGLY DISCOURAGE the way of HARDCODING any Zoom Credentials (username, password, API Keys & secrets, SDK keys & secrets, etc.) or any Personal Identifiable Information (PII) inside your application. WE DON’T MAKE ANY COMMITMENTS ABOUT ANY LOSS CAUSED BY HARD-CODING CREDENTIALS OR SENSITIVE INFORMATION INSIDE YOUR APP WHEN DEVELOPING WITH OUR SDK.




```
{
  "sdk_jwt": "<your_sdk_jwt>",
  "meeting_number": <meeting_number_to_join>,
  "passcode": "<passcode>",
  "video_source": "test",
  "zak":""
}
```

The app will try to join the meeting follow the Meeting Number you specified in the config.json. 

## Add the sdk files into a folder name `SDK`

You will need to download the Windows Meeting SDK C++ SDK from marketplace.zoom.us and place the SDK files into the SDK folder in this project.
The directory should look something like this
- x64 (folder)
  - bin
  - h
  - lib
- x86 (folder)
  - bin
  - h
  - lib
- CHANGELOG.md
- OSS-LICENSE.html
- README.md
- version.txt

## Open and Run Project

Open "MSDK_LocalRecording.vcxproj" file from Visual Studio 2022.

Hit F5 or click from menu "Debug" -> "Start Debugging" in x86 or x64 to launch the application.


## Error

if you are getting an error about not being able to open source json/json.h , include this in your

Visual Studio Project -> Properties. Under C/C++ ->General ->Additional Include Directories,

 ### x64
 C:\yourpath\whereyouinstalled\vcpkg\packages\jsoncpp_x64-windows\include
 
 or

 ### x86
 C:\yourpath\whereyouinstalled\vcpkg\packages\jsoncpp_x86-windows\include

   # Error

  what if i would like to use x64 environment?

  add this to your environment variable before installing openCV from vcpkg

  VCPKG_DEFAULT_TRIPLET = x64-windows

  you can use `setx VCPKG_DEFAULT_TRIPLET "x64-windows"` to set it via command line

  and reinstall by using the command below

  ```
  ./vcpkg install jsoncpp
  ```

## Getting Started

The main method, or main entry point of this application is at `MSDK_LocalRecording.cpp`

From a high level point of view it will do the below

- Join a meeting
- Wait for callback or status update. There are some prerequistes before you can get video raw data. The `CanIStartRecording()` method helps to check if you have fulfilled these requirements
  - You need to have host, co-host or recording permissions
  - You need to be in-meeting. This is the status when you have fully joined a meeting.
- Get the Meeting Recording Controller
  - Use the Meeting Recording Controller to call `StartRecording()`. Do note that you can only either run `StartRecording()` or `StartRawRecording()`. You cannot run them both at once.
- The files are stored in your user direct /Documents/Zoom
	-	When the meeting ends or when the SDK exits the meeting, it is automatically converted

# Upgrading Guide

You will need to download the latest Meeting SDK Windows for c++ from marketplace.zoom.us

Replace the files in the folder `SDK` with those found in the downloaded files from marketplace.zoom.us

You will need to ensure any missing abstract classes are implemented etc... before you can compile and upgrade to a newer SDK version.

