# SA-MP Interaction Menu Documentation

## Table of Contents

- [SA-MP Interaction Menu Documentation](#sa-mp-interaction-menu-documentation)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
  - [Defines](#defines)
  - [⚙️ Functions](#️-functions)
    - [`ResyncActor`](#resyncactor)
      - [Example usage of ResyncActor](#example-usage-of-resyncactor)
    - [`RestoreActor`](#restoreactor)
      - [Example usage of RestoreActor](#example-usage-of-restoreactor)
    - [`RespawnActor`](#respawnactor)
      - [Example usage of RespawnActor](#example-usage-of-respawnactor)
    - [`IsActorDead`](#isactordead)
    - [`SetActorRespawnTime`](#setactorrespawntime)
    - [`IsPlayerInRangeOfActor`](#isplayerinrangeofactor)
    - [`Attach3DTextLabelToActor`](#attach3dtextlabeltoactor)
    - [`SetActorName`](#setactorname)
      - [Example usage of SetActorName](#example-usage-of-setactorname)
    - [`GetActorName`](#getactorname)
      - [Example usage of GetActorName](#example-usage-of-getactorname)
    - [`SetActorColor`](#setactorcolor)
      - [Example usage of SetActorColor](#example-usage-of-setactorcolor)
    - [`ToggleActorName`](#toggleactorname)
      - [Example usage of ToggleActorName](#example-usage-of-toggleactorname)
    - [`SetActorChatBubble`](#setactorchatbubble)
      - [Example usage of SetActorChatBubble](#example-usage-of-setactorchatbubble)
    - [`DestroyChatBubble`](#destroychatbubble)
      - [Example usage of DestroyChatBubble](#example-usage-of-destroychatbubble)
    - [`KillActor`](#killactor)
      - [Example usage of KillActor](#example-usage-of-killactor)
  - [🔄 CallBacks](#-callbacks)
    - [`OnActorDeath`](#onactordeath)
      - [Example usage of OnActorDeath](#example-usage-of-onactordeath)
    - [`OnActorSpawn`](#onactorspawn)
      - [Example usage of OnActorSpawn](#example-usage-of-onactorspawn)
    - [`OnPlayerTargetActor`](#onplayertargetactor)
      - [Example usage of OnPlayerTargetActor](#example-usage-of-onplayertargetactor)

---

## Installation

1. Include the script in your SA-MP gamemode:

```pawn
#include <actors>
```

## Defines

| Define                     | Description                              | Default value |
| -------------------------- | ---------------------------------------- | ------------- |
| `MAX_ACTOR_NAME`           | Maximum length of an actor's name.       | 24            |
| `ACTOR_NAME_DRAW_DISTANCE` | Max distance to draw an actor's name tag | 10.0          |

## ⚙️ Functions

### `ResyncActor`

```pawn
ResyncActor(actorid)
```

> Resyncs the actor's state.
>
> - **actorid**: The ID of the actor to resync.
>
> - **Returns**: `1` on success, `0` if the actor ID is invalid.

#### Example usage of ResyncActor

```pawn
new actorid = CreateActor(0, 0.0, 0.0, 0.0, 0.0);
ResyncActor(actorid);
```

### `RestoreActor`

```pawn
RestoreActor(actorid, worldid, Float:x, Float:y, Float:z)
```

> Restores an actor to a specific position and virtual world.
>
> - **actorid**: The ID of the actor to restore.  
> - **worldid**: The virtual world to set for the actor.  
> - **x / y / z**: The coordinates to place the actor at.

#### Example usage of RestoreActor

```pawn
new actorid = CreateActor(0, 0.0, 0.0, 0.0, 0.0);
CallLocalFunction("RestoreActor", "iiffff", actorid, 1, 100.0, 100.0, 10.0);
```

> [!NOTE]
> This function is public because it needs to be called from `ResyncActor`. We recommend using `CallLocalFunction` to call it, as shown in the example above, to avoid potential issues with forward declarations.

### `RespawnActor`

> Respawns the actor at its original position.
>
> - **actorid**: The ID of the actor to respawn.
>
> - **Returns**: `1` on success, `0` if the actor ID is invalid.

#### Example usage of RespawnActor

```pawn
new actorid = CreateActor(0, 0.0, 0.0, 0.0, 0.0);
CallLocalFunction("RespawnActor", "i", actorid);
```

> [!NOTE]
> This function is public because it needs to be called from a timer when the automatic respawn time is set using `SetActorRespawnTime`. We recommend using `CallLocalFunction` to call it, as shown in the example above, to avoid potential issues with forward declarations.

### `IsActorDead`

```pawn
IsActorDead(actorid)
```

> Checks whether an actor is dead.
>
> - **actorid**: The ID of the actor to check.  
>
> - **Returns**: `1` if dead, `0` if the actor is alive or if the actor ID is invalid.

### `SetActorRespawnTime`

```pawn
SetActorRespawnTime(actorid, time)
```

> Sets the actor respawn delay after death.
>
> - **actorid**: The ID of the actor.  
> - **time**: Respawn time in milliseconds.
>
> - **Returns**: `1` on success, `0` if the actor ID is invalid.

### `IsPlayerInRangeOfActor`

```pawn
IsPlayerInRangeOfActor(playerid, actorid, Float:radius = 5.0)
```

> Checks if a player is within a radius of an actor.
>
> - **playerid**: The player ID.  
> - **actorid**: The actor ID.  
> - **radius**: Range to check (default `5.0`).  
>
> - **Returns**: `1` if in range, `0` otherwise.

### `Attach3DTextLabelToActor`

```pawn
Text3D:Attach3DTextLabelToActor(actorid, text[], color, Float:fOffsetX, Float:fOffsetY, Float:fOffsetZ, Float:distance = 10.0, worldid = 0, testlos = 0)
```

> Attaches a 3D text label to an actor.
>
> - **actorid**: The actor ID.  
> - **text[]**: Label text.  
> - **color**: Text color.  
> - **fOffsetX / fOffsetY / fOffsetZ**: Position offsets from actor origin.  
> - **distance**: Visibility distance (default `10.0`).  
> - **worldid**: Virtual world (default `0`).  
> - **testlos**: Line-of-sight check flag (default `0`).  
>
> - **Returns**: `Text3D` label handle.

### `SetActorName`

```pawn
SetActorName(actorid, name[])
```

> Sets a custom display name for an actor.
>
> - **actorid**: The actor ID.  
> - **name[]**: Name text (max `MAX_ACTOR_NAME` chars).

#### Example usage of SetActorName

```pawn
new actorid = CreateActor(7, 100.0, 100.0, 10.0, 90.0);
SetActorName(actorid, "Security Guard");
```

### `GetActorName`

```pawn
GetActorName(actorid)
```

> Gets the current actor name.
>
> - **actorid**: The actor ID.
>
> - **Returns**: The actor name string, or an empty string if the actor has no name or if the actor ID is invalid.

#### Example usage of GetActorName

```pawn
new actorid = CreateActor(7, 100.0, 100.0, 10.0, 90.0);
SetActorName(actorid, "Vendor");

printf("Actor name: %s", GetActorName(actorid));
```

### `SetActorColor`

```pawn
SetActorColor(actorid, color)
```

> Sets the actor name-tag/chat color.
>
> - **actorid**: The actor ID.  
> - **color**: RGBA color (e.g. `0xFFFFFFFF`).

#### Example usage of SetActorColor

```pawn
new actorid = CreateActor(7, 100.0, 100.0, 10.0, 90.0);
SetActorColor(actorid, 0xFFAA00FF);
```

### `ToggleActorName`

```pawn
ToggleActorName(actorid, bool:toggle)
```

> Shows or hides the actor name tag.
>
> - **actorid**: The actor ID.  
> - **toggle**: `true` to show, `false` to hide.

#### Example usage of ToggleActorName

```pawn
new actorid = CreateActor(7, 100.0, 100.0, 10.0, 90.0);
ToggleActorName(actorid, false);
```

### `SetActorChatBubble`

```pawn
SetActorChatBubble(actorid, text[], color, Float:drawdistance, expiretime)
```

> Displays a chat bubble above an actor.
>
> - **actorid**: The actor ID.  
> - **text[]**: Bubble text.  
> - **color**: Text color.  
> - **drawdistance**: Visible distance.  
> - **expiretime**: Duration in milliseconds.

#### Example usage of SetActorChatBubble

```pawn
new actorid = CreateActor(7, 100.0, 100.0, 10.0, 90.0);
SetActorChatBubble(actorid, "Welcome!", 0xFFFFFFFF, 20.0, 5000);
```

### `DestroyChatBubble`

```pawn
DestroyChatBubble(actorid)
```

> Destroys the chat bubble attached to an actor.
>
> - **actorid**: The actor ID.

#### Example usage of DestroyChatBubble

```pawn
new actorid = CreateActor(7, 100.0, 100.0, 10.0, 90.0);
SetActorChatBubble(actorid, "This will disappear soon...", 0xFFFFFFFF, 20.0, 5000);
// Destroy the chat bubble after 3 seconds
SetTimerEx("DestroyChatBubble", 3000, false, "i", actorid);
```

> [!NOTE]
> The `DestroyChatBubble` function is public because it needs to be called from a timer to remove the chat bubble after a certain duration. We recommend using `CallLocalFunction` if you want to call it immediately, to avoid potential issues with forward declarations.

### `KillActor`

```pawn
KillActor(actorid, killerid = INVALID_PLAYER_ID, reason = 0)
```

> Kills an actor with an optional killer and reason.
>
> - **actorid**: The actor ID.
> - **killerid**: The player ID of the killer (default `INVALID_PLAYER_ID` for no killer).
> - **reason**: The weapon or death reason (default `0`).
>
> - **Returns**: `1` on success, `0` if the actor ID is invalid.

#### Example usage of KillActor

```pawn
new actorid = CreateActor(7, 100.0, 100.0, 10.0, 90.0);
KillActor(actorid, INVALID_PLAYER_ID, REASON_SUICIDE);
```

## 🔄 CallBacks

### `OnActorDeath`

```pawn
OnActorDeath(actorid, killerid, reason)
```

> Called when an actor dies.
>
> - **actorid**: Dead actor ID.  
> - **killerid**: Killer player ID (`INVALID_PLAYER_ID` if none).  
> - **reason**: Weapon or death reason.

#### Example usage of OnActorDeath

```pawn
public OnActorDeath(actorid, killerid, reason)
{
    printf("Actor %d died. Killer: %d, Reason: %d", actorid, killerid, reason);
    return 1;
}
```

### `OnActorSpawn`

```pawn
OnActorSpawn(actorid)
```

> Called when an actor spawns.
>
> - **actorid**: Spawned actor ID.

#### Example usage of OnActorSpawn

```pawn
public OnActorSpawn(actorid)
{
    printf("Actor %d spawned.", actorid);
    return 1;
}
```

### `OnPlayerTargetActor`

```pawn
OnPlayerTargetActor(playerid, newtarget, oldtarget)
```

> Called when a player changes targeted actor.
>
> - **playerid**: Player ID.  
> - **newtarget**: New targeted actor ID.  
> - **oldtarget**: Previous targeted actor ID.

#### Example usage of OnPlayerTargetActor

```pawn
public OnPlayerTargetActor(playerid, newtarget, oldtarget)
{
  printf("Player %d changed target from actor %d to actor %d", playerid, oldtarget, newtarget);
  return 1;
}
```
