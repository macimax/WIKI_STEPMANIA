Project Antenna is a proposal to revamp StepMania's netcode to offer more flexible online functionality, including the ability for passive, online service servers (akin to e-Amusement, AM.NET or NESiCAxLive) that can stream player statistics and scores to a score tracking server. Unlike SMO, this would be able to occur in the background during normal gameplay, without requiring the user to log into a network lobby server in order to take advantage of such features.

Tracking of progress related to Antenna is taking place on a [project board](https://github.com/stepmania/stepmania/projects/1).

# Comparison of current online functionality between SM and other products

## StepMania
 * Optional online connectivity to multiplayer servers (SMO).
 * Decentralized distribution of songs and other add-on content (although the main SMO server does have a repository of song packs with a search tool).
 * When SMO is active, user is prompted to login and is placed in a lobby.
 * Public and private rooms for multiple players to play the same song at once.
 * The main SMO server has a song scanning system.
 * The main SMO server manages online leaderboards and profiles for each song and player, accessible online.
 * Online functionality is exclusive to SMO mode. All other functionality is offline only unless otherwise noted.
 * The UI for SMO is rather clunky and depends on unusual variations of SM’s standard workflow, since it’s very hackish.

## Osu
 * Account required to play
 * Centralized song distribution with per-song leaderboards accessible in-game.
 * Online functionality is passive, game was built around it from the start.
 * Has multiplayer with up to 16 players on the same song/chart (no I am not calling it a “map”.)
 * Has a better editor (I know it’s not online related but it’s still an advantage)
 * Is the subject of ridicule within certain segments of the music gaming community as a whole. But the fact that all this is seamless and well-implemented is likely the reason why it's so popular.

## Some Konami games connected to e-amusement
 * Contactless card and PIN login system
 * Arcade game.
 * Rival system (compare high scores with specific friends).
 * Additional features in an app apparently (generating custom “result cards” for posting on social media, etc.)
 * Online events and updates.
 * Online functionality is passive when a machine is online-connected and the user logs in.

## Step ManiaX
 * Seems to involve results screen QR codes and a mobile app.

# Brainstorming
## Goal
Divide StepMania online functionality into two modes;
 * “Legacy”/Multiplayer Lobby server (what SMO currently is now) - SMLan, etc. (see also https://github.com/stepmania/stepmania/blob/master/Docs/Devdocs/SMLanProtocol.txt)
 * “Online Service Server” (Project Antenna, an “Antenna server”) - a passive mode that sends player results to a specified online server over the course of standard gameplay. Essentially, something more like e-Amusement or AM.NET (i.e. a remote user profile with online score saving, etc.). The latter could theoretically be used to implement the former in a saner and futureproof manner.

## Requirements
 * Ability to stream player results to a specified server over the course of normal gameplay.
 * Ability to have server-side profiles and leaderboards for players and songs associated with the server.
 * Ability to enforce/override specific settings or at least recognize and acknowledge them (i.e. specific modifiers, timings, etc.)
 * The server-side username should be separate from the user profile name in SM (this is just a personal pet peeve with the current system).
 * Ability for a server to whitelist or blacklist specific packs/playlists (mainly if it is to serve specific audiences/projects/products. I.e. just ITG official packs, just TrotMania, just StepManiaX, etc.)
 * A Packs table and a Packs_members joining table in postgres will be the most efficient way to do this
 * Server backend has to be open source. Preferably under the same license as SM itself (MIT or some other BSD-like)
 * Server backend needs an API so it can be polled for other things (such as integration with websites).
 * Possibly a way to create an account from within SM?
 * Ability to scan and verify simfiles/other configuration settings to ensure songs and other settings are not modified to abuse the system.
 * Relevant Lua bindings to allow for features such as displaying per-song leaderboards within SM (i.e. on ScreenSelectMusic)

## Possible workflow
1. The user first creates an account on the server-side’s website component.
2. The user goes into SM and accesses the “Online Options” menu in the options menu.
3. The previous Network Options menu would be replaced so that SMO-related stuff is moved to a new Multiplayer option in the main menu.
4. The user types in the Antenna server domain, and logs in with their username and password. This login would be bound to a player’s in-game profile.
5. Once SM connects to the server, they are told of anything of note (i.e. a MOTD, supported packs if applicable, etc.). This screen will then contain an on-off toggle for enabling the online connection, or disassociating the local SM profile from the online account.
6. UI elements (maybe an “ONLINE” prompt in the system overlay a la DDR) would signify the player’s online status once this is configured. If no online account is configured on the profile, these elements would not display.
7. The theme would be able to support loading selected statistics from the online server (such as on ScreenSelectMusic, Evaluation, etc.)

## Things to look into
* gRPC
   * “it has support for bidirectional streaming”
   * “so you can make a call with a stream of game events that you write to and recieve a stream of game events back”
   * “(not to mention the fact that protocol buffers are unable to be interpreted any way other than correctly, including type-safety for all things passed through)”
   * “it's over TLS by default, gRPC doesn't have to worry about session hijacking because that's TLS' job”