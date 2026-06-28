# Player Movement

This document briefly discusses how to modify player movement. It covers changes that can be made without code changes or a rebuild of the game, and then walks through a small source-code example that adds double jumping.

## Movement Properties

Several movement-related values are located in the `Player` section of `serverbutes.txt`. Changing these values affects player velocity and acceleration.

You can also affect gravity through the console variable `PlayerGravity`.

Relevant `serverbutes.txt` properties:

| Property | Description |
| --- | --- |
| `WalkSpeed` | Maximum walking velocity. |
| `RunSpeed` | Maximum running velocity. |
| `JumpSpeed` | Upward velocity applied when the player jumps. |
| `LadderSpeed` | Maximum velocity while climbing a ladder. |
| `SwimSpeed` | Maximum velocity while swimming. |

## Source Changes

For anything more advanced than simple velocity changes, you will need to edit the source files for player movement. Most of the movement code is contained in the `CMoveMgr` module.

This example shows a simple double-jump implementation.

### 1. Add a member variable

Edit `Game\ClientShellDLL\ClientShellShared\CMoveMgr.h` and add a boolean member:

```cpp
bool m_bCanDoubleJump;
```

Place it within the protected member section of the `CMoveMgr` class.

### 2. Initialize the variable

In `Game\ClientShellDLL\ClientShellShared\CMoveMgr.cpp`, initialize the new variable in the `CMoveMgr` constructor:

```cpp
m_bCanDoubleJump = true;
```

### 3. Allow a second jump request

Most player movement happens in `CMoveMgr::UpdateNormalMotion()`.

Change this line:

```cpp
bJumping = g_bJumpRequested && !m_bJumped;
```

to:

```cpp
bJumping = g_bJumpRequested && (!m_bJumped || m_bCanDoubleJump);
```

### 4. Allow jumping while already airborne

For this example, we assume it is valid to jump again if the player has already jumped and is allowed to double jump.

Change this line:

```cpp
bOkayToJump = (m_bSwimmingJump || (m_bOnGround && !m_bBodyInLiquid && !m_bBodyOnLadder));
```

to:

```cpp
bOkayToJump = (m_bSwimmingJump || (m_bCanDoubleJump && m_bJumped) || (m_bOnGround && !m_bBodyInLiquid && !m_bBodyOnLadder));
```

### 5. Prevent more than two jumps

Now that a second jump is allowed, make sure we do not allow more than two jumps total.

Change this block:

```cpp
vel.y = fJumpVel;

m_bJumped = LTTRUE;

m_bSwimmingOnSurface = LTFALSE;

g_bJumpRequested = LTFALSE;
```

to:

```cpp
vel.y = fJumpVel;

if (m_bCanDoubleJump && m_bJumped)
{
    // Can't double jump more than once...
    m_bCanDoubleJump = false;
}

m_bJumped = LTTRUE;

m_bSwimmingOnSurface = LTFALSE;

g_bJumpRequested = LTFALSE;
```

### 6. Re-enable double jumping after landing

Now look at `CMoveMgr::UpdateOnGround()`. If the player is back on the ground after jumping, it is safe to allow double jumping again.

Change this block:

```cpp
// Handle landing after jumping...

if (m_bJumped)
{
    m_bJumped = LTFALSE;
    UpdateStartMotion(LTTRUE);
}
```

to:

```cpp
// Handle landing after jumping...

if (m_bJumped)
{
    // We can double jump again...
    m_bCanDoubleJump = true;
    m_bJumped = LTFALSE;
    UpdateStartMotion(LTTRUE);
}
```

## Wrap-up

That is all you need to do to add a double jump to the game. Compile and build `CShell.dll`, then test your changes.

Keep in mind that this is a very simple implementation and probably not the best long-term solution. The point of the example is to make the movement code easier to approach and show where this kind of functionality is added.

Once you are comfortable with this example, a natural next step would be experimenting with something more advanced, such as long jumping.
