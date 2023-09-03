
## 🪟 LINE Notify Windows Credential Provider

![platform](https://img.shields.io/badge/platform%20toolset-v143%20%28MSVC%20redist%202022%29-blue.svg)
![flavor](https://img.shields.io/badge/flavor-windows%20x64-brightgreen.svg)
![size](https://img.shields.io/badge/size-92%20KB-yellow.svg)
![license](https://img.shields.io/badge/license-MIT%20%28inherited%29-blueviolet.svg)

Demonstrate the usage of Windows credential provider, built on top of [official V2 Credential Provider Sample](https://github.com/microsoft/Windows-classic-samples/tree/main/Samples/CredentialProvider). The repo extends the functionality, allowing a user to unlock a PC with a code sent via LINE Notify.

![SampleUsage.png](https://github.com/der3318/line-win-credprov/blob/main/Images/SampleUsage.png)


### 💻 Deployment & Setup

First of all, create a LINE chatroom and [associate it with a valid notify bearer](https://notify-bot.line.me/my/). Then, [download the sample DLL](https://github.com/der3318/line-win-credprov/releases/download/2023.09.02/SampleV2CredentialProvider.dll) and put it under System32 directory.

![SampleDeploy.png](https://github.com/der3318/line-win-credprov/blob/main/Images/SampleDeploy.png)

Also [download the registry file](https://github.com/der3318/line-win-credprov/releases/download/2023.09.02/register.reg) and double click to import module settings. This will add entries under `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\Credential Providers` and `HKCR\CLSID\{5fd3d285-0dd9-4362-8855-e0abaacd4af6}` to hint Windows to load the sample provider.

Open Registry Editor and navigate to `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\Credential Providers\{5fd3d285-0dd9-4362-8855-e0abaacd4af6}`. Insert these REG_SZ key-value pairs based on your own information:

| Name | Data |
| :- | :- |
| UserName | Account name. Let provider know which user the tile belongs to. |
| Password | Password to use, in plain text. |
| LineBearer | The LINE Notify bearer acquired in the first step. |

![SampleRegister.png](https://github.com/der3318/line-win-credprov/blob/main/Images/SampleRegister.png)

Unlock the device. Now a new interactable credential tile should show up in logon screen. If not, make sure [Microsoft Visual C++ Redistributable 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist) is properly installed on the machine.


### 🧹 Cleanup & Uninstall

Get the [Unregister.reg](https://github.com/der3318/line-win-credprov/releases/download/2023.09.02/Unregister.reg). Double click to remove the registry records. Delete the deployed SampleV2CredentialProvider DLL from System32 folder.


### 🔨 Compilation & Build

Open the solution file with Visual Studio 2022. Press CTRL+B to build the vcxproj and find the compiled binary in x64 directory.
