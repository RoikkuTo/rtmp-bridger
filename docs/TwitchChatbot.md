<h1>Twitch Chatbot Usage</h1>

-   [Configuration](#configuration)
-   [Available commands](#available-commands)

## Configuration

To interact with your twitch chat, RTMP Bridger uses a User OAuth Token which is basically an authorization for bots.

At some points you will be prompt to authorize Bridger to access your chat (and nothing else), just say yes and It will be fine.

## Available commands

The Twitch Chatbot offers you basic commands to manage the stream while reading the chat. They all starts with an `!` exclamation point/mark.

| Commands | Options                | For who  | Behavior                             |
| -------- | ---------------------- | -------- | ------------------------------------ |
| !bitrate | none                   | everyone | Return the current bitrate (in Kbps) |
| !stream  | `start, stop, on, off` | streamer | Start and stop the stream            |
| !scene   | `[scene name]`         | streamer | Change the current scene             |
| !server  | none                   | everyone | Present RTMP Bridger in short        |
