# UnityYAMLMerge

Configured copy of UnityYAMLMerge that falls back to my preferred diff apps and avoids having to change paths on each new version of Unity. Basically just moving Apple File Merge to the bottom since it comes built-in. If you've installed a standalone/paid diff app you'd probably prefer using that...

Clone this repo and follow the configuration steps below to setup each git client.

*NOTE:* All of the configurations below assume that you've cloned this repo to `~/UnityYAMLMerge/`. Adjust paths where appropriate if you've selected a different location.

 - [UnityYAMLMerge Docs](https://docs.unity3d.com/Manual/SmartMerge.html)


# Repository Configuration

If you're joining an existing project and have been sent here to setup UnityYAMLMerge on your local machine you can skip this and configure your specific client(s) using the sections below. If you're the first to use UnityYAMLMerge in your project or are setting up a new repo, continue reading.

Regardless of git client you need to configure your project's `.gitattributes` file to trigger UnityYAMLMerge on specific file patterns. Generally you want to apply this to all YAML based project assets.

For example, to configure all `.prefab` files to be merged with UnityYAMLMerge add the following line to the `.gitattributes` file in your project.

`*.prefab merge=unityyamlmerge`

That's it!


# Client Configuration

Below are instructions for configuring each client. If you configure a client that isn't listed here send me a PR to add it!


## General

This configures UnityYAMLMerge in your git config file(s). This will work for console commands and any other git client that respects git config files (not all do!)

Clients that respect git config:
 - TBD

Add the following to the `.git/config` of your repo.

This works globally if added to your `~/.gitconfig` as well but it's not recommended unless you're certain every repo you ever work with will be a Unity project.

```
[merge]
	tool = unityyamlmerge
[mergetool "unityyamlmerge"]
	trustExitCode = false
	cmd = ~/UnityYAMLMerge/UnityYAMLMerge merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
```


## Fork

1. Open the menu item `Fork -> Settings...`
2. Select the `Integration` tab.
3. For the `Merge Tool` drop down select `Custom`.
4. Press the `Edit` button next to the drop down.
5. In the `Edit Merge Tool` dialog enter the following
    - `File Path` - `~/UnityYAMLMerge/UnityYAMLMerge`
    - `Arguments` - `merge -p $BASE $REMOTE $LOCAL $MERGED`
6. Click `Edit` to save your changes

When there is a merge conflict, select `Merge in External Tool` to have `UnityYAMLMerge` attempt to resolve the conflicts. If there are remaining conflicts it will open the fallback diff app configured in the `mergespecfile.txt` file.


### Why don't we use Fork's built-in `UnityYAMLMerge`?

We don't use Fork's built-in `UnityYAMLMerge` merge tool option because they get their binary from somewhere else (not sure if it's built into Fork or scraped from some installed Unity editor instance). This means we can't benefit from customizing the preferred fallback diff app in `mergespecfile.txt`.