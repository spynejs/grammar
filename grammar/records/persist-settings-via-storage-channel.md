### persist-settings-via-storage-channel
`record:persist-settings-via-storage-channel` · standard

**Recognize when:** "remember my settings," "survive a refresh," "save preferences locally."

Application settings persistence and restoration: a UI/settings event enters CHANNEL_APP (CHANNEL_APP_SETTING_EVENT); ChannelLocalStorage SUBSCRIBES and persists autonomously (settings ride the behavior stream — intent captured with state; no module 'requests' a write); on boot, a null-appended view reads the store and transmits CHANNEL_LOCAL_STORAGE_APP_SETTINGS_INITIALIZED_EVENT (the channel cannot transmit into itself — the null view is the bridge); consumers apply state (AppContainer sets the html data-theme).

**Composes:** op:state-machine-in-channel, op:acquire-and-conform, op:null-appended-behavior-view, op:bridge-channel-output-to-transmit, op:choose-replay-semantics, op:dataset-as-payload, record:theme-or-mode-toggle
