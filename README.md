# Stardew Valley Multiplayer Docker Compose

This project aims to autostart a Stardew Valley Multiplayer Server as easy as possible. Updated for 1.6!

## Notes

- Updating to most recent version requires a rebuild: `git pull` and `docker-compose build --no-cache`
- Although I'm trying to put out updates, I don't have the time for testing thoroughly, so if you find issues, including
  game updates, please put in an issue request and I will try to help.
- Thanks printfuck for the base code and baolatui for helping with hosting files.

## Setup

### git clone
```
git clone https://github.com/norimicry/stardew-multiplayer-docker.git
```

### Download game files from GOG
go to gog.com, \
login with your account, \
go to Stardew Valley game and download linux version \
open terminal go to directory of downloaded file, \
there will be a file that looks like
```
stardew_valley_1_6_6_24117_6728858633_72932.sh
```
then unzip file
```
unzip stardew_valley_1_6_6_24117_6728858633_72932.sh
```
then copy game files directory to `docker/gamefiles`
```
cp -r data/noarch [replace with path to project root]/docker/gamefiles
```
game files directory should look like
```
docs  game  gameinfo  start.sh  support
```

### Docker-Compose
current version of docker includes docker compose, so command is
```
docker compose
```

build docker container
```
docker compose build
```
start docker container
```
docker compose up
```

### Configuration

Edit the docker-compose.yml with your desired configuration settings. Setting values are quite descriptive as to what
they set.

```
environment:
      # VNC
      - VNC_PASSWORD=insecure
      - DISPLAY_HEIGHT=900
      - DISPLAY_WIDTH=1200
      
      # Always On Server mod
      ## Removing this will probably defeat the point of ever using this?
      - ENABLE_ALWAYSONSERVER_MOD=${ENABLE_ALWAYSONSERVER_MOD-true}
      - ALWAYS_ON_SERVER_HOTKEY=${ALWAYS_ON_SERVER_HOTKEY-F9}
      - ALWAYS_ON_SERVER_PROFIT_MARGIN=${ALWAYS_ON_SERVER_PROFIT_MARGIN-100}
      - ALWAYS_ON_SERVER_UPGRADE_HOUSE=${ALWAYS_ON_SERVER_UPGRADE_HOUSE-0}
      - ALWAYS_ON_SERVER_PET_NAME=${ALWAYS_ON_SERVER_PET_NAME-Rufus}
      - ALWAYS_ON_SERVER_FARM_CAVE_CHOICE_MUSHROOMS=${ALWAYS_ON_SERVER_FARM_CAVE_CHOICE_MUSHROOMS-true}
      - ALWAYS_ON_SERVER_COMMUNITY_CENTER_RUN=${ALWAYS_ON_SERVER_COMMUNITY_CENTER_RUN-true}
      - ALWAYS_ON_SERVER_TIME_OF_DAY_TO_SLEEP=${ALWAYS_ON_SERVER_TIME_OF_DAY_TO_SLEEP-2200}
      - ALWAYS_ON_SERVER_LOCK_PLAYER_CHESTS=${ALWAYS_ON_SERVER_LOCK_PLAYER_CHESTS-false}
      - ALWAYS_ON_SERVER_CLIENTS_CAN_PAUSE=${ALWAYS_ON_SERVER_CLIENTS_CAN_PAUSE-true}
      - ALWAYS_ON_SERVER_COPY_INVITE_CODE_TO_CLIPBOARD=${ALWAYS_ON_SERVER_COPY_INVITE_CODE_TO_CLIPBOARD-false}

      - ALWAYS_ON_SERVER_FESTIVALS_ON=${ALWAYS_ON_SERVER_FESTIVALS_ON-true}
      - ALWAYS_ON_SERVER_EGG_HUNT_COUNT_DOWN=${ALWAYS_ON_SERVER_EGG_HUNT_COUNT_DOWN-600}
      - ALWAYS_ON_SERVER_FLOWER_DANCE_COUNT_DOWN=${ALWAYS_ON_SERVER_FLOWER_DANCE_COUNT_DOWN-600}
      - ALWAYS_ON_SERVER_LUAU_SOUP_COUNT_DOWN=${ALWAYS_ON_SERVER_LUAU_SOUP_COUNT_DOWN-600}
      - ALWAYS_ON_SERVER_JELLY_DANCE_COUNT_DOWN=${ALWAYS_ON_SERVER_JELLY_DANCE_COUNT_DOWN-600}
      - ALWAYS_ON_SERVER_GRANGE_DISPLAY_COUNT_DOWN=${ALWAYS_ON_SERVER_GRANGE_DISPLAY_COUNT_DOWN-600}
      - ALWAYS_ON_SERVER_ICE_FISHING_COUNT_DOWN=${ALWAYS_ON_SERVER_ICE_FISHING_COUNT_DOWN-600}

      - ALWAYS_ON_SERVER_END_OF_DAY_TIMEOUT=${ALWAYS_ON_SERVER_END_OF_DAY_TIMEOUT-300}
      - ALWAYS_ON_SERVER_FAIR_TIMEOUT=${ALWAYS_ON_SERVER_FAIR_TIMEOUT-1200}
      - ALWAYS_ON_SERVER_SPIRITS_EVE_TIMEOUT=${ALWAYS_ON_SERVER_SPIRITS_EVE_TIMEOUT-900}
      - ALWAYS_ON_SERVER_WINTER_STAR_TIMEOUT=${ALWAYS_ON_SERVER_WINTER_STAR_TIMEOUT-900}

      - ALWAYS_ON_SERVER_EGG_FESTIVAL_TIMEOUT=${ALWAYS_ON_SERVER_EGG_FESTIVAL_TIMEOUT-120}
      - ALWAYS_ON_SERVER_FLOWER_DANCE_TIMEOUT=${ALWAYS_ON_SERVER_FLOWER_DANCE_TIMEOUT-120}
      - ALWAYS_ON_SERVER_LUAU_TIMEOUT=${ALWAYS_ON_SERVER_LUAU_TIMEOUT-120}
      - ALWAYS_ON_SERVER_DANCE_OF_JELLIES_TIMEOUT=${ALWAYS_ON_SERVER_DANCE_OF_JELLIES_TIMEOUT-120}
      - ALWAYS_ON_SERVER_FESTIVAL_OF_ICE_TIMEOUT=${ALWAYS_ON_SERVER_FESTIVAL_OF_ICE_TIMEOUT-120 }

      # Auto Load Game mod
      ## Removing this will mean you need to VNC in to manually start the game each boot
      - ENABLE_AUTOLOADGAME_MOD=${ENABLE_AUTOLOADGAME-null}
      - AUTO_LOAD_GAME_LAST_FILE_LOADED=${AUTO_LOAD_GAME_LAST_FILE_LOADED-null}
      - AUTO_LOAD_GAME_FORGET_LAST_FILE_ON_TITLE=${AUTO_LOAD_GAME_FORGET_LAST_FILE_ON_TITLE-true}
      - AUTO_LOAD_GAME_LOAD_INTO_MULTIPLAYER=${AUTO_LOAD_GAME_LOAD_INTO_MULTIPLAYER-true}

      # Save Backup mod
      ## Disabling this will stop saves being backed up
      - ENABLE_SAVEBACKUP_MOD=${ENABLE_SAVEBACKUP_MOD-true}

      # Chat Commands mod
      - ENABLE_CHATCOMMANDS_MOD=${ENABLE_CHATCOMMANDS_MOD-false}

      # Console Commands mod
      - ENABLE_CONSOLECOMMANDS_MOD=${ENABLE_CONSOLECOMMANDS_MOD-false}

      # Time Speed mod
      - ENABLE_TIMESPEED_MOD=${ENABLE_TIMESPEED_MOD-false}

      ## Days are only 20 hours long
      ##   7.0 = 14 mins per in game day (default)
      ##  10.0 = 20 mins
      ##  15.0 = 30 mins
      ##  20.0 = 40 mins
      ##  30.0 = 1 hour
      ## 120.0 = 4 hours
      ## 300.0 = 10 hours
      ## 600.0 = 20 hours (realtime)

      - TIME_SPEED_DEFAULT_TICK_LENGTH=${TIME_SPEED_DEFAULT_TICK_LENGTH-7.0}
      - TIME_SPEED_TICK_LENGTH_BY_LOCATION_INDOORS=${TIME_SPEED_TICK_LENGTH_BY_LOCATION_INDOORS-7.0}
      - TIME_SPEED_TICK_LENGTH_BY_LOCATION_OUTDOORS=${TIME_SPEED_TICK_LENGTH_BY_LOCATION_OUTDOORS-7.0}
      - TIME_SPEED_TICK_LENGTH_BY_LOCATION_MINE=${TIME_SPEED_TICK_LENGTH_BY_LOCATION_MINE-7.0}

      - TIME_SPEED_ENABLE_ON_FESTIVAL_DAYS=${TIME_SPEED_ENABLE_ON_FESTIVAL_DAYS-false}
      - TIME_SPEED_FREEZE_TIME_AT=${TIME_SPEED_FREEZE_TIME_AT-null}
      - TIME_SPEED_LOCATION_NOTIFY=${TIME_SPEED_LOCATION_NOTIFY-false}

      - TIME_SPEED_KEYS_FREEZE_TIME=${TIME_SPEED_KEYS_FREEZE_TIME-N}
      - TIME_SPEED_KEYS_INCREASE_TICK_INTERVAL=${TIME_SPEED_KEYS_INCREASE_TICK_INTERVAL-OemPeriod}
      - TIME_SPEED_KEYS_DECREASE_TICK_INTERVAL=${TIME_SPEED_KEYS_DECREASE_TICK_INTERVAL-OemComma}
      - TIME_SPEED_KEYS_RELOAD_CONFIG=${TIME_SPEED_KEYS_RELOAD_CONFIG-B}

      # Crops Anytime Anywhere mod
      - ENABLE_CROPSANYTIMEANYWHERE_MOD=${ENABLE_CROPSANYTIMEANYWHERE_MOD-false}

      - CROPS_ANYTIME_ANYWHERE_ENABLE_IN_SEASONS_SPRING=${CROPS_ANYTIME_ANYWHERE_ENABLE_IN_SEASONS_SPRING-true}
      - CROPS_ANYTIME_ANYWHERE_ENABLE_IN_SEASONS_SUMMER=${CROPS_ANYTIME_ANYWHERE_ENABLE_IN_SEASONS_SUMMER-true}
      - CROPS_ANYTIME_ANYWHERE_ENABLE_IN_SEASONS_FALL=${CROPS_ANYTIME_ANYWHERE_ENABLE_IN_SEASONS_FALL-true}
      - CROPS_ANYTIME_ANYWHERE_ENABLE_IN_SEASONS_WINTER=${CROPS_ANYTIME_ANYWHERE_ENABLE_IN_SEASONS_WINTER-true}

      - CROPS_ANYTIME_ANYWHERE_FARM_ANY_LOCATION=${CROPS_ANYTIME_ANYWHERE_FARM_ANY_LOCATION-true}

      - CROPS_ANYTIME_ANYWHERE_FORCE_TILLABLE_DIRT=${CROPS_ANYTIME_ANYWHERE_FORCE_TILLABLE_DIRT-true}
      - CROPS_ANYTIME_ANYWHERE_FORCE_TILLABLE_GRASS=${CROPS_ANYTIME_ANYWHERE_FORCE_TILLABLE_GRASS-true}
      - CROPS_ANYTIME_ANYWHERE_FORCE_TILLABLE_STONE=${CROPS_ANYTIME_ANYWHERE_FORCE_TILLABLE_STONE-false}
      - CROPS_ANYTIME_ANYWHERE_FORCE_TILLABLE_OTHER=${CROPS_ANYTIME_ANYWHERE_FORCE_TILLABLE_OTHER-false}

      # Friends Forever mod
      - ENABLE_FRIENDSFOREVER_MOD=${ENABLE_FRIENDSFOREVER_MOD-false}

      - FRIENDS_FOREVER_AFFECT_SPOUSE=${FRIENDS_FOREVER_AFFECT_SPOUSE-false}
      - FRIENDS_FOREVER_AFFECT_DATES=${FRIENDS_FOREVER_AFFECT_DATES-true}
      - FRIENDS_FOREVER_AFFECT_EVERYONE_ELSE=${FRIENDS_FOREVER_AFFECT_EVERYONE_ELSE-true}
      - FRIENDS_FOREVER_AFFECT_ANIMALS=${FRIENDS_FOREVER_AFFECT_ANIMALS-true}

      # No Fence Decay mod
      - ENABLE_NOFENCEDECAY_MOD=${ENABLE_NOFENCEDECAY_MOD-false}

      # Non-destructive NPCs mod
      - ENABLE_NONDESTRUCTIVENPCS_MOD=${ENABLE_NONDESTRUCTIVENPCS_MOD-false}
```

## Game Setup

Initially, you have to create or load a game once via VNC or web interface. After that, the Autoload Mod jumps into the
previously loaded game save everytime you restart or rebuild the container. The AutoLoad Mod config file is by default
mounted as a volume, since it keeps the state of the ongoing game save, but you can also copy your existing game save to
the `Saves` volume and define the game save's name in the environment variables. Once started, press the Always On
Hotkey (default F9) to enter server mode.

### VNC

Use a VNC client like `TightVNC` on Windows or plain `vncviewer` on any Linux distribution to connect to the server. You
can modify the VNC Port and IP address and Password in the `docker-compose.yml` file like this:

Localhost:

```
   # Server is only reachable on localhost on port 5902...
   ports:
     - 127.0.0.1:5902:5900
   # ... with the password "insecure"
   environment:
     - VNCPASS=insecure
```

### Web Interface

On port 5800 (mapped to 5801 by default) inside the container is a web interface. This is a bit easier and more
accessible than just the VNC interface. Although you will be asked for the vnc password, I wouldn't recommend exposing
the port to the outside world.

![img](https://store.eris.cc/uploads/859865e1ab5b23fb223923d9a7e4806b.PNG)

## Accessing the server

- Direct IP: You will need to set a up direct IP access over the internet "Join LAN Game" by opening (or forwarding)
  port 24642. Or use Server Port Changer to choose a different port. People can then "Join LAN Game" via your external IP.

(Taken from mod description. See [Always On Server](https://www.nexusmods.com/stardewvalley/mods/2677?tab=description)
for more info.)

## Mods

- [Always On Server](https://www.nexusmods.com/stardewvalley/mods/2677) (Default: Required)
- [Auto Load Game](https://www.nexusmods.com/stardewvalley/mods/2509) (Default: On)
- [Crops Anytime Anywhere](https://www.nexusmods.com/stardewvalley/mods/3000) (Default: Off)
- [Friends Forever](https://www.nexusmods.com/stardewvalley/mods/1738) (Default: Off)
- [No Fence Decay](https://www.nexusmods.com/stardewvalley/mods/1180) (Default: Off)
- [Non Destructive NPCs](https://www.nexusmods.com/stardewvalley/mods/5176) (Default: Off)
- [Remote Control](https://github.com/Novex/stardew-remote-control) (Default: On)
- [TimeSpeed](https://www.nexusmods.com/stardewvalley/mods/169) (Default: Off)

## Troubleshooting

### Waiting for Day to End

Check VNC just to make sure the host hasn't gotten stuck on a prompt.

### Error Messages in Console

Usually you should be able to ignore any message there. If the game doesn't start or any errors appear, you should look
for messages like "cannot open display", which would most likely indicate permission errors.

### VNC

Access the game via VNC to initially load or start a pre-generated savegame. You can control the server from there or
edit the config.json files in the configs folder.

## Disclaimer

This multiplayer server container is designed to distribute game files for the purpose of facilitating multiplayer
gaming experiences. By utilizing this server container, you acknowledge and agree that you are expected to possess a
legal copy of the game for which the files are being distributed. These files are intended solely for the purpose of
running a multiplayer server and should not be used in any other manner. The distributed game files are to be strictly
used for the operation of multiplayer servers. Any other use, including but not limited to reproduction, modification,
or distribution for personal or commercial gain, is strictly prohibited. The distribution of these game files does not
imply endorsement or sponsorship by the creators or owners of the game. We are solely providing a platform for
multiplayer gaming experiences.