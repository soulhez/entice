![Travis-CI](https://travis-ci.org/entice/web.svg?branch=master)

# Protocol definition

_Always be sure to check the appropriate source files for more details._
_Hint: We use the same server for login, char selection, playing, and so on._

---

## TODOs / Versions / Milestones

With each milestone, we will add new features in the protocol and implement them in the server and client-mod. The milestone definitions are a rough overview of the features. Details will be added in the source code directly on demand. The milestones only define

Each milestone may modify existing processes and/or create new processes and messages.

**Definition of done:
A milestone is `DONE` when all messages of the protocol are supported both in the client-mod and server, including all their features. Ideally, we will have automated tests for the messages to prove that the milestone is done.**

Generally, we need to create the following features over the single milestones:

```
* login                [DONE]
* account-create       [?]
* account-delete       [?]
* instance-load        [70%] <- long term WIP
* map-change           [DONE]
* char-create          [DONE]
* char-delete          [DONE]
* game-state-diff      [95%] <- long term WIP
* movement             [70%] <- long term WIP
* chat                 [70%]
* emotes               [DONE] (scripted)
* npc-spawns           [?]
* npc-dialogues        [?]
* ...
```

### Milestone 1 `DONE`

**Should support**

- account login and proper reply (success or error-code)
- instance load into one single map (propagation of the complete entity system)
- spawn at least one other sample entity (a player)
- movement calculations of entities (simple: no collision, client based)

**Should not support**

- any char actions (selection, creation etc.)
- any account actions (creation, management etc.)
- different entity types (everything is a player)
- character appearance and that (but might support names for entity-system testing purposes)
- movement speed

### Milestone 2 `DONE`

**Should support**

- account login, character selection (plus dispatch) based on a DB backend
- char creation (on the LS, bringing the client back to the char selection afterwards)
- chat (at least general chat and recognition of commands)
- emotes
- char appearance as component (necessary consequence of char creation and selection)
- mod: enhanced debugging and exception handling (visually etc.)

**Should not support**

- account actions such as creation etc. (might come with another 'web interface' prj later on)
- different entity types (everything still is a player, but it also has an appearance)
- any changes on the movement or collision system etc.

### Milestone 3 `DONE`

**Should support**

- different worlds, i.e. the outposts of The Battle Isles, incl. world-map based map-change
- character deletion
- quit playing and going back to char selection
- proper despawning/deletion of entities upon map-change or logout etc. (which is a fix)
- player groups, incl. invite, accept, merge, leave, etc.
_(Hint: Make sure that all groups in a world are known to all clients, either by handling them separately or by having a well designed group component... or both. The server does all the checks (group-size etc.) but the client can and should do its own soft checking when trying to merge groups etc.)_
- a 4 bytes length prefix in the protocol to support very large JSON docs

**Should not support**

- different instances and districts of one outpost
- group search window (who needs that really?)

### The following are skipped milestones, due to rework of the server branch (yet again :D)

> ### Milestone 4 `DONE`
>
> **Should support**
>
> - movement computation and collision detection, **server side**
> - group chat (introduction of channels)
> - a generally more reasonable instance-load/diffing/spawning system
>   - client side: enable spawning of incomplete entities
>   - ~~protocol: communicate when the client is ready to play after instance-load~~
>
> **Should not support**
>
> - any other chat channels than group chat and all chat
>
> ### Milestone 5
>
> **Should support**
>
> - remove PlayReady leftover code
> - animations with variable lengths
> - automatic world unloading if empty
> - server: flush should specify a world to flush (see WorldDiff controller)
> - further refinement of movement
> - NPCs (spawning and scripted AI)
> - Skillbar interactions with mock-up skills
>
> **Should not support**
>
> - skill-functionality, i.e. skill casting

### Milestone 6

**Should support**

- (probably) fix groups. if that works, add group-map-change
- add a place to store available skills and a way to work with them (check if available, lock/unlock etc.)
  - store as bitarray, transfer as base64 string
- let clients manage their current skillbars
- propagate client-side movement updates (add apropriate attributes)

### Milestone 7

**May support**

- (improvement) more maps generally
- (improvement) remove leader from groups, use list semantics `[leader|members]` only
- (old feature) explorable zones
- (old feature) movement speed
- (old feature) whisper messages
- (new feature) no skillbar changes in explorables
- (new feature) portals
- (new feature) NPC dialogues
- (new feature) items
- (new feature) friends-list
- (new feature) guilds
- (new feature) more chat channels (guild, trade)
