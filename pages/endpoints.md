## <-- [Back](../README.md) <!-- omit in toc -->

# Endpoints <!-- omit in toc -->
This is a list of all endpoints you can send requests to.

## NAV

- [Houses](#houses)
  - [Categories](#categories)
  - [Invites](#invites)
- [Rooms](#rooms)
  - [Actions](#actions)
  - [Members](#members)
- [Messages](#messages)
- [Users](#users)
- [\@me](#me)
  - [Account](#account)
  - [DM Rooms](#dm-rooms)
  - [House](#house)
  - [Relationships](#relationships)

# Houses

### `POST /houses`
creates a house
```
d: {
  name: string,
  icon: base64?
}
```

### `PATCH /houses/:id`
edit a house
```
d: {
  name: string,
  icon: base64
}
```

### `DELETE /houses/:id`
deletes a house

## Categories
### `POST /houses/:id/entities`
adds an entity (only category so far)
```
d: {
  name: string,
  type: int{1: 'category'}
}
```

### ?`PATCH /houses/:id/entities/:id`
adds an entity (only category so far)
```
d: {
  name: string,
  type: int{1: 'category'}
}
```

### `DELETE /houses/:id/entities/:id`
deletes a category, has to be empty

## Invites
### `POST /houses/:id/invites`
creates an invite
```
d: {
  max_uses: int,
  max_age: int
}
```

### `GET /invites/:code`
fetches an invite

### `POST /invites/:code`
uses an invite
```
d: { }
```


# Rooms

### `POST /houses/:id/rooms`
creates a room
```
d: {
  name: string,
  parent_entity_id?: string
}
```

### `PATCH /rooms/:id`
edits a room
```
d: {
  name: string
}
```

### `DELETE /houses/:id/rooms/:id`
deletes a room

## Actions
### `POST /rooms/:id/typing`
starts typing in a room
```
d: { }
```
### `POST /rooms/:id/call`

start a call
```
d: { }
```

### `POST /rooms/:id/call/decline`
decline a call
```
d: { }
```

## Members
### `PUT /rooms/:id/recipients/:id`
adds a user to a group DM

### `DELETE /rooms/:id/recipients/:id`
removes a user from a group DM

### `PATCH /rooms/:id/default-permissions`
changes default permissions for a room
```
d: {
  allow: bitfield,
  deny: bitfield
}
```


# Messages

### `POST /rooms/:id/messages`
creates a text message
```
d: {
  content: string
}
```

### `POST /rooms/:id/media_messages`
creates an attachment message
```
d: form {
  file: named file
}
```

### `PATCH /rooms/:id/messages/:id`
edits a message
```
d: {
  content: string
}
```

### `DELETE /rooms/:id/messages/:id` / ` DELETE /houses/:id/rooms/:id/messages/:id`
deletes a message

### `GET /rooms/:id/messages?before=id`
gets messages from a room

### `POST /rooms/:id/messages/:id/ack`
mark as read, probably
```
d: { }
```


# Users
### `GET /users/:username`
gets an account

### `GET /relationships/:id/mutual-friends`
gets your mutual friends with an account


# \@me

## Account
### `PATCH /users/@me`
edits your account
```
d: {
  bio: string,
  name: string,
  icon: base64?,
  header: base64?,
  location: string,
  website: string
}
```

### `GET /users/@me`
gets your account

### `GET /streams/@me/mentions`
gets your mentions

### `GET /streams/@me/feed`
gets your feed

### `PUT /users/@me/settings/room_overrides/:id`
changes room settings
```
d: {
  notification_preference: int{ 0: 'all', 1: 'mentions', 2: 'none' }
}
```

## DM Rooms
### `POST /users/@me/rooms`
adds a DM room
```
d: {
  recipient: string
}
```

### `POST /users/@me/rooms`
adds a group DM room
```
d: {
  recipients: string[]
}
```

### `DELETE /users/@me/rooms/:id`
leaves a group DM

## House
### `DELETE /users/@me/houses/:id`
leaves a house

## Relationships
### `GET /relationships/@me/friends`
get your friends

### `DELETE /relationships/@me/friends/:id`
unfriends someone

### `GET /relationships/@me/friend-requests`
get your current friend requests

### `POST /relationships/@me/friend-requests`
sends a friend request to someone
```
d: {
  user_id: string
}
```

### `DELETE /relationships/@me/friend-requests/:id`
cancels a friend request

### `PUT /relationships/@me/blocked/:id`
blocks a user

### `DELETE /relationships/@me/blocked/:id`
unblocks a user

### `PUT relationships/@me/restricted/:id`
restricts a user
### ?`DELETE relationships/@me/restricted/:id`
unrestricts a user