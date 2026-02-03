# Changes from Original Implementation

This document tracks custom features and modifications made to the game server.

## Build Configuration

### Tibia 7.72 by Default

The Makefile now always builds for Tibia client version 7.72 instead of 7.70.

**Files modified:**
- `Makefile` - Added `-DTIBIA772=1` to CFLAGS

---

## Configurable Rates

### Experience Rate (Staged)

Configurable experience multiplier that can be staged based on player level.

**Config syntax:**
```
# Simple fixed rate for all levels
experiencerate = 50

# Staged rates (min_level, max_level, rate) - 0 means no upper limit
experiencerate = (1, 50, 50)
experiencerate = (51, 100, 25)
experiencerate = (101, 200, 10)
experiencerate = (201, 0, 5)
```

**Default:** `1` (normal rate)

**Files modified:**
- `src/config.hh` - Added `TRateStage` struct and extern declarations
- `src/config.cc` - Added parsing and initialization
- `src/crcombat.cc` - Applied rate in `DistributeExperiencePoints()`

---

### Loot Rate

Global multiplier for item drop probability. Capped at 100% (1000).

**Config syntax:**
```
lootrate = 2
```

**Default:** `1` (normal rate)

**Files modified:**
- `src/config.hh` - Added extern declaration
- `src/config.cc` - Added parsing and initialization
- `src/crnonpl.cc` - Applied rate in monster loot generation

---

### Magic Rate

Multiplier for magic level training (mana spent = skill points gained).

**Config syntax:**
```
magicrate = 10
```

**Default:** `1` (normal rate)

**Files modified:**
- `src/config.hh` - Added extern declaration
- `src/config.cc` - Added parsing and initialization
- `src/magic.cc` - Applied rate in `CheckMana()`

---

### Melee Rate

Multiplier for melee skill training (sword, axe, club, fist).

**Config syntax:**
```
meleerate = 10
```

**Default:** `1` (normal rate)

**Files modified:**
- `src/config.hh` - Added extern declaration
- `src/config.cc` - Added parsing and initialization
- `src/crcombat.cc` - Applied rate in `GetAttackDamage()`

---

### Distance Rate

Multiplier for distance/ranged skill training.

**Config syntax:**
```
distancerate = 10
```

**Default:** `1` (normal rate)

**Files modified:**
- `src/config.hh` - Added extern declaration
- `src/config.cc` - Added parsing and initialization
- `src/crcombat.cc` - Applied rate in `DistanceAttack()`

---

### Shielding Rate

Multiplier for shielding skill training.

**Config syntax:**
```
shieldingrate = 10
```

**Default:** `1` (normal rate)

**Files modified:**
- `src/config.hh` - Added extern declaration
- `src/config.cc` - Added parsing and initialization
- `src/crcombat.cc` - Applied rate in `GetDefendDamage()`
