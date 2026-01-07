# Roblox Event API

This API manages in-game events and messaging for Roblox experiences using Open Cloud.

## Endpoints

### 1. Start Event
**POST** `/events/start`

Starts a specific game event.

**Body (JSON):**
```json
{
  "universe_id": 12345678,
  "event_name": "Alien",  // Options: Alien, Blizzard, Lightning, Rainbow
  "expire_in": 120        // Optional: Duration in seconds (default: 120)
}
```

### 2. Global Message
**POST** `/global-message`

Broadcasts a message to all servers in the universe.

**Body (JSON):**
```json
{
  "universe_id": 12345678,
  "message": "Hello everyone! An event is starting soon."
}
```

### 3. Admin Event
**POST** `/events/admin`

Spawns a special admin item for a specific user.

**Body (JSON):**
```json
{
  "universe_id": 12345678,
  "item_type": "AdminEgg", // Options: AdminEgg, AdminCrate
  "target_user_id": 987654321
}
```

### 4. Stop Event
**POST** `/events/stop`

Stops a specific event or all active events.

**Body (JSON):**
```json
{
  "universe_id": 12345678,
  "event_name": "Alien"   // Options: Specific event name OR "all"
}
```
