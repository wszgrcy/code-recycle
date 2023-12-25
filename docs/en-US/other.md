## FAQ
### Why does the content not sync in real-time after modifying the content/adding public resources?
- There may be multiple operations for modifying resources, and one operation may not cover all.
- You can force refresh all content by executing `code-recycle.refresh-all` in the command panel.

### Why does the content not sync after restarting?
- It is a problem with the synchronization mechanism of VSCode itself, which may cause the written memory not to take effect...
- You can force refresh all content by executing `code-recycle.refresh-all` in the command panel.
- Set `code-recycle.startupRefresh` to force refresh on startup.

?> Setting it will ensure that the resources are up-to-date, but some cached resources that need to be requested will also be cleared.  
 For example, actions called by other Actions, Custom Rule calls, and Code Snippet calls...

### Will the modified resources be synced to all editors?
- No, it needs to be refreshed; or waiting for the next startup.

### How to terminate the currently running action?
- Currently, it cannot be terminated. If a deadlock occurs due to custom rule design, it may be necessary to kill the process or restart the window.
- In the future, the plugin will run on independent threads, which will not affect the overall use of the plugin.

## Other More
- Feel free to ask questions in the [Issue](https://github.com/wszgrcy/code-recycle/issues) section.