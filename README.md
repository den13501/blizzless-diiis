 

![](pictures/logo.png)

# DiIiS Project

DiIiS is a fully-functional open-source local server for [Diablo III: Reaper of Souls](https://eu.diablo3.blizzard.com).

## Features

- Implemented account creation system, authorization and lobby.
- Implemented Necromancer class mechanics.
- Fully implemented chat system and friends.
- Fully implemented clan system.
- Implemented basic DRLG (dungeon generator).
- Implemented item generator with in-game affixes.
- Implemented the basic mechanics of almost all active abilities for all classes.
- Implemented a system of set items.
- Implemented all main scripts for all story quests 5 acts.
- Implemented basic scripts and generator for "Adventure Mode".
- Implemented the basis for the "Challenge Nephalem Rifts" mode.
- Implemented artificial intelligence for 80% of minions.
- Implemented personal artificial intelligence for 40% of all monsters.
- Implemented personal artificial intelligence for half of the Bosses.
- Implemented LAN

## Restrictions

- Donate Store implementation is removed.
- NAT support is hidden, but possible ;)

# Installation

## Supported Clients

Each version of the client includes changes to structures, opcodes and attributes.

The currently supported version of the client: **2.7.4.84161**

## Server Deploying

1. Install [PostgreSQL 9.5.25](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).

2. Create databases in PostgreSQL: `diiis` and `worlds`.

   ```postgresql
   -- use cli as below or use pgAdmin to create database
   CREATE DATABASE diiis;
   CREATE DATABASE worlds;
   ```

   

3. Change you account and password in <u>src/DiIiS-NA</u>/`database.Account.config` and `database.Worlds.conifg`.

4. Restore `worlds.backup` to `worlds` database.

   > I suggest using pgAdmin

5. Compile by [VS 2019/2022](https://visualstudio.microsoft.com/).

6. [Skip this stage for local game] Copy the [config.ini](configs/config.ini) file to the server folder (It overwrites the default settings):

   - Update the parameter entries with your IP record on the network: `BindIP` and `PublicIP`.

7. Launch wait until server start, it creates a hierarchy.

   > the server binary is **src\DiIiS-NA\bin\Release\net5.0\Blizzless.exe**

8. Create user account(s) using console: `!account add Login Password Tag`

   > for example:  !account add adm@adm 12345678 test

## Prepare Client

Do this for each client connecting to the server.

1. Get [supported client](#supported-clients) Diablo 3.

2. Install certificate <u>src\DiIiS-NA\</u> [bnetserver.p12](src/DiIiS-NA/bnetserver.p12), password - `123` (the game verifies the CA root certificates).

3. Setting up redirects client to your server:

   **Method #1 - Hosts**

     Add redirects to the `hosts` file (`%WinDir%\System32\drivers\etc\hosts`):  
     `127.0.0.1 us.actual.battle.net`  
     `127.0.0.1 eu.actual.battle.net`

     !After the modification the official Battle.Net application will not be able to connect to the server!

     **Method #2 - Modify main executable file**

     ```c++
   // Find null-terminated string enum and rewrite with HexEditor to your IP server.
   eu.actual.battle.net/
   us.actual.battle.net/
   cn.actual.battle.net/
   kr.actual.battle.net/
       
   Use any domain, no matter paid or free, the main thing is to create a subdomain - (eu.your domain),the main thing here is eu or us for example, to get eu.diabloiii.ru (example),and bind it to the IP where your server is located.
   open files Diablo III.exe and Diablo III64.exe in any hex editor
   
   find text "actual.battle.net"
   
   61637475616C2E626174746C652E6E6574
   to
   646961626C6F6969692E72750000000000
   
   replace it with your domain "diabloiii.ru"
   
   if your domain turned out to be shorter in length, then replace the excess with null bytes something like this ))
     ```

4. Launch client (`x64` or `x86`) with arguments `"Diablo III64.exe" -launch`

   > if you want to launch specific language, just add this parameter -locale xxxx
   >
   > Traditional Chinese = **zhTW**
   >
   > Simple Chinese = **zhCN**
   >
   > English = **enUS**
   >
   > French =  **frFR**
   >
   > German = **deDE**
   >
   > Spanish = **esES**

5. Login to the game using your credentials.

6. [Skip this stage for local game] After that, when creating a game (in client), indicate the creation of a public game. Other players, when connecting, must also indicate a public game, and at the start they will connect to you.

7. You're in the game world!

## Using Docker

Run `docker-compose up` inside [db](db) folder and continue from the 5th step in section [server](#server-deploying).

# Server Configuration

## Global configuration

Using the configuration file you can easily override the [global world parameters](docs/game-world-settings.md).

## Command system

The command system allows you to get control of the game world if you have rights. A list of commands is available [here](docs/commands-list.md).

# Issues

Check the [report form](docs/report-form.md) before submitting issue, this will help people save time!

# System requirements

|            | **Entry-level**              | **Mid-range**                | **High-end**                 |
| ---------- | ---------------------------- | ---------------------------- | ---------------------------- |
| **CPU**    | Intel Core i5 or AMD Ryzen 5 | Intel Core i7 or AMD Ryzen 7 | Intel Core i9 or AMD Ryzen 9 |
| **Memory** | 4 GB RAM                     | 16 GB RAM                    | 64 GB RAM                    |
| **Disk**   | 500 MB                       | 1 GB                         | 1 GB                         |

# Screenshots

You can see more screenshots [here](SCREENSHOTS.md)

![](pictures/ingame-screen-1.png)



## Video guide

[(15) Setting Up Blizzless DiIiS Offline Server (read desc) - YouTube](https://www.youtube.com/watch?v=DsYlZk-bMOc)

# Ragezone post

[Diablo 3 2022 Emuator by Blizzless (source code) - RaGEZONE - MMO development community](https://forum.ragezone.com/f857/diablo-3-2022-emuator-by-1207314/)
