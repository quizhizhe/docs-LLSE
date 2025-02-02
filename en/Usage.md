# Installation and Usage

## 💻 Install LiteLoaderBDS

### Install on Windows (Recommended)

We recommend installing LiteLoaderBDS on these platforms:

* Windows 10 21H2 or later
* Windows 11
* Windows Server 2019 or later

Follow these steps to install:

1. Download and unzip Bedrock Dedicated Server for Minecraft (BDS) supported by the latest version of LiteLoaderBDS from [Minecraft Wiki](https://minecraft.fandom.com/wiki/Bedrock_Dedicated_Server#Download). Visit [our home page](https://www.litebds.com) to see the supported version.
2. Download the latest version of LiteLoaderBDS from [GitHub releases](https://github.com/LiteLDev/LiteLoader/releases/latest).
3. Unzip the achieve file you downloaded in step 2, putting all files in the directory of BDS. If conflicts occurs, overwrite the files.
4. Check if the `bedrock_server.pdb` file exists. If not, download [here](https://github.com/LiteLDev/LiteLoader/releases/latest) and put them in the directory of BDS.
5. In the directory of BDS, run `LLPeEditor.exe` and wait until the program hints to close it.
6. In the directory of BDS, run `bedrock_server_mod.exe` to launch the server. Note that you should always run `bedrock_server_mod.exe` to launch ther server. Otherwise, not only features provided by LiteLoaderBDS are unavailable but also some bugs will occur, causing various unexpected crashes.

### Install on Linux Distributions

### Via Scripts (Available on Ubuntu)

In the directory to put the server, run:

```sh
wget https://raw.githubusercontent.com/LiteLDev/LiteLoaderBDS/main/Scripts/install.sh
chmod +x install.sh
./install.sh
```

### Via Docker

You should have the latest version of Docker installed. Then run:

```sh
docker pull shrbox/liteloaderbds
docker create --name <container name> -v <installation directory>:/root/bedrock-server -p <port>:19132/udp -it shrbox/liteloaderbds
```

You ought to adapt the `<installation directory>` and the `<port>` to your environment.

* `<container name>` is the name of the container. You can choose any name you like meeting the requirements of Docker. If you have no idea, how about `llbds`?
* `<installation directory>` is directory to put the BDS server and the data. It's a good idea to put it in a directory that everyone can read and write.
* `<port>` is the port that players fill in when connecting to the server.

It takes more time to start up for the first time downloading BDS and LiteLoaderBDS. Please wait patiently.

Some common commands are shown below:

* Start the server: `docker start <container name>`
* Stop the server: `docker stop <container name>`
* Attach to the console: `docker attach <container name>`
* Detach from the console: Press `Ctrl` + `P` + `Q`. You should not press `Ctrl` + `C` or the server will terminate immediately.

Now that you have LiteLoaderBDS installed, how about adding some plugins?

## 🎯 Add Some Plugins

There are two types of plugins: LL plugins and LLSE plugins.

LL plugins are compiled native plugins, written in C++, Go, C# or Rust, which have better performance but cannot be loaded, unloaded or reloaded after the server starts.

LLSE plugins are script plugins, written in JavaScript, Python or Lua, which can be flexibly managed and have better security but perform worse.

### Find Your Favorite Plugins

You can look for plugins in these websites:

* [LiteLoader Forum](https://forum.litebds.com/)
* [MineBBS (LL plugins)](https://www.minebbs.net/resources/?prefix_id=59)
* [MineBBS (LLSE plugins)](https://www.minebbs.net/resources/?prefix_id=67)

### Install Plugins

1. Unzip if you have got an archieve file.
2. Check the content of the plugin. The file names of LiteLoaderBDS plugins end with `.dll`, `.js` or `.lua`.
3. Place the files in the `plugins` directory. Some plugins may be distributed with other files, you should put them in the `plugins` directory at the same time.

## 🔌 Manage Plugins

You can manage the plugins with the commands listed below:

* `ll list`: list all plugins
* `ll load plugins/xxxx.js`: load an LLSE plugin
* `ll unload plugin/xxxx.js`: unload an LLSE plugin
* `ll reload plugin/xxxx.js`: reload an LLSE plugin
* `ll reload`: reload all LLSE plugins
* `ll version`: print the LiteLoaderBDS version
* `ll upgrade`: Check for LiteLoaderBDS updates

### Notice

* After unloading a plugin, the commands registered by it will NOT be totally removed, which may resulting in hinting the command not existent when players attempts to use the commands.
* If the plugin unloaded exports interfaces used by other plugins, the other plugins will be unavailable.
* DO NOT unload or reload plugins when the server has not been started or there are players in the server, or the server will face the risk to crash.
* On loading a plugin, the `onServerStarted` event and the the `onPlayerJoin` events of all players will be triggered in the plugin.

> [!WARNING]
> DO NOT load, unload or reload any plugin under production environment.

## 🎨 Manage Addons

Copy the addon whose file name ends with `.mcpack`, `.mcaddon` or `.zip` to `plugins/AddonsHelper/` and restart the server. The addons will then be automatically added to the world.

You can manage them with command `addons` in the console.

## 📡 Debug Plugins

You can type these commands to enter the corresponding debug mode:

* `jsdebug`: JavaScript debug mode
* `luadebug`: Lua debug mode

In debug mode, all texts you type will be parsed as scripts and be executed in real time, as the console of developer tools of browsers do. If any error occurs, you will see an error report.

You can type `jsdebug` / `luadebug` and enter to exit the debug mode.