## <-- [Back](../README.md) <!-- omit in toc -->

# Websocket <!-- omit in toc -->

## NAV

- [Events](#events)
  - [after connecting](#after-connecting)
  - [INIT_STATE](#init_state)
  - [HOUSE_JOIN](#house_join)
  - [HOUSE_MEMBERS_CHUNK](#house_members_chunk)
  - [TYPING_START](#typing_start)
  - [MESSAGE_CREATE](#message_create)
  - [MESSAGE_UPDATE](#message_update)
  - [MESSAGE_DELETE](#message_delete)
  - [ROOM_CREATE](#room_create)
  - [ROOM_UPDATE](#room_update)
  - [ROOM_DELETE](#room_delete)
  - [HOUSE_ENTITIES_UPDATE](#house_entities_update)
  - [HOUSE_MEMBER_UPDATE](#house_member_update)
  - [USER_UPDATE](#user_update)
  - [RELATIONSHIP_UPDATE](#relationship_update)
  - [PRESENCE_UPDATE](#presence_update)
  - [HOUSE_DOWN](#house_down)
  - [HOUSE_LEAVE](#house_leave)
  - [HOUSE_MEMBER_JOIN](#house_member_join)
  - [HOUSE_MEMBER_LEAVE](#house_member_leave)
  - [HOUSE_UPDATE](#house_update)
- [Data](#data)
  - [Ping](#ping)
  - [Init](#init)
  - [Request Presence Updates](#request-presence-updates)
  - [Request House Members](#request-house-members)
  - [Select A Room](#select-a-room)

# Events
a list of all websocket events

## after connecting
```
op: 1
d: {
  hbt_int: 30000
}
```

## INIT_STATE
```
{
  op: 0
  d: {
    user: {
      username: string,
      user_flags: string,
      name: string,
      id: string,
      icon: string,
      header: string,
      presence: string
    },
    settings: {
      user_id: string,
      theme: null,
      room_overrides: {
        id: { notification_preference: int }
      },
      onboarded: unknown,
      enable_desktop_notifications: unknown
    },
    relationships: {
      id: {
        user_id: string,
        user: {
          username: string,
          user_flags: string,
          name: string,
          id: string,
          icon: string,
          header: string,
          presence: string
        },
        type: int,
        last_updated_at: string
      }
    },
    read_state: {
      id: {
        message_id: string,
        mention_count: int
      },
    },
    private_rooms: room[]
    presences: {
      id: {
        username: string,
        user_flags: string,
        name: string,
        id: string,
        icon: string,
        header: string,
        presence: string
      }
    },
    house_memberships: {
      id: {
        user_id: string,
        user: {
          username: string,
          user_flags: string,
          name: string,
          id: string,
          icon: string,
          header: string,
          presence: string
        },
        roles: array,
        last_permission_update: string,
        joined_at: string,
        house_id: string
      }
    },
    house_ids: string[]
  }
}
```

## HOUSE_JOIN
```
{
  op: 0
  d: {
    rooms: room[{
      type: int,
      recipients: null
      position: int,
      permission_overrides: bits,
      owner_id: string,
      name: string,
      last_message_id: string,
      id: string,
      house_id: string,
      emoji: object,
      description: string,
      default_permission_override: int
    }],
    roles: role[{
      position: int,
      name: string,
      level: int,
      id: string,
      deny: bits,
      color: string,
      allow: bits
    }],
    owner_id: string,
    name: string,
    members: [{
      user_id: string,
      user: {
        username: string,
        user_flags: string,
        name: string,
        id: string,
        icon: string,
        header: string,
        presence: string
      },
      roles: array,
      last_permission_update: string,
      joined_at: string,
      house_id: string
    }],
    id: string,
    icon: string,
    entities: [{
      type: int,
      resource_pointers: [{
        resource_type: string,
        resource_id: string
      }],
      position: int,
      name: string,
      id: string
    }],
    default_permissions: int,
    banner: string
  }
}
```

## HOUSE_MEMBERS_CHUNK
```
{
  op: 0
  d: {
    members: {
      id: {
        user_id: string,
        user: {
          username: string,
          user_flags: string,
          name: string,
          id: string,
          icon: string,
          header: string,
          presence: string
        },
        roles: array,
        last_permission_update: string,
        joined_at: string,
        house_id: string
      }
    },
    house_id: string
  }
}
```

## TYPING_START
```
{
  op: 0
  d: {
    timestamp: int,
    room_id: string,
    house_id: string,
    author_id: string
  }
}
```

## MESSAGE_CREATE
```
{
  op: 0
  d: {
    timestamp: int,
    room_id: string,
    mentions: [{
      username: string,
      user_flags: string,
      name: string,
      id: string,
      icon: string,
      header: string,
      presence: string,
      bot: boolean
    }],
    member: {
      user_id: string,
      user: {
        username: string,
        user_flags: string,
        name: string,
        id: string,
        icon: string,
        header: string,
        presence: string
      },
      roles: array,
      last_permission_update: string,
      joined_at: string,
      house_id: string
    },
    id: string,
    house_id: string,
    exploding_age: int,
    exploding: boolean,
    device_id: string,
    content: string,
    bucket: int,
    author_id: string,
    author: {
      username: string,
      user_flags: string,
      name: string,
      id: string,
      icon: string,
      header: string,
      presence: string
    }
    attachment: {
      media_url: string,
      filename: string,
      dimensions: {
        width: int,
        type: string,
        height: int
      }
    }
  }
}
```

## MESSAGE_UPDATE
```
{
  op: 0
  d: {
    type: int,
    timestamp: string,
    room_id: string,
    metadata: unknown,
    mentions: [{
      username: string,
      user_flags: string,
      name: string,
      id: string,
      icon: string,
      header: string,
      presence: string
    }],
    id: string,
    house_id: string,
    exploding_age: int,
    exploding: boolean,
    embed: object,
    edited_at: string,
    device_id: string,
    content: string,
    bucket: int,
    author_id: string,
    attachment: {
      media_url: string,
      filename: string,
      dimensions: {
        width: int,
        type: string,
        height: int
      }
    }
  }
}
```

## MESSAGE_DELETE
```
{
  op: 0
  d: {
    room_id: string,
    message_id: string,
    house_id: string
  }
}
```

## ROOM_CREATE
```
{
  op: 0
  d: {
    type: int,
    position: int,
    name: string,
    id: string,
    house_id: string
  }
}
```

## ROOM_UPDATE
```
{
  op: 0
  d: {
    type: int,
    position: int,
    name: string,
    id: string,
    house_id: string,
    emoji: object,
    description: string
  }
}
```

## ROOM_DELETE
```
{
  op: 0
  d: {
    id: '191527742867501935',
    house_id: '182410583881021247'
  }
}
```

## HOUSE_ENTITIES_UPDATE
```
{
  op: 0
  d: {
    house_id: '182410583881021247',
    entities: [{
      type: int,
      resource_pointers: [{
        resource_type: string,
        resource_id: string
      }],
      position: int,
      name: string,
      id: string
    }]
  }
}
```

## HOUSE_MEMBER_UPDATE
```
{
  op: 0
  d: {
    user_id: string,
    user: {
      website: string,
      username: string,
      user_flags: int,
      name: string,
      location: string,
      id: string,
      icon: string,
      header: string,
      email_verified: boolean,
      bot: boolean,
      bio: string
    },
    roles: object[],
    presence: string,
    last_permission_update: unknown,
    joined_at: string,
    id: string,
    house_id: string
  }
}
```

## USER_UPDATE
```
{
  op: 0
  d: {
    website: string,
    username: string,
    user_flags: int,
    name: string,
    location: string,
    id: string,
    icon: string,
    header: string,
    email_verified: boolean,
    bot: boolean,
    bio: string
  }
}
```

## RELATIONSHIP_UPDATE
```
{
  op: 0
  d: {
    user: {
      website: string,
      username: string,
      user_flags: int,
      name: string,
      location: string,
      id: string,
      icon: string,
      bio: string
    },
    type: int,
    recipient_id: string,
    id: string
  }
}
```

## PRESENCE_UPDATE
```
{
  op: 0
  d: {
    username: string,
    user_flags: string,
    name: string,
    id: string,
    icon: string,
    header: string,
    presence: string
  }
}
```

## HOUSE_DOWN
```
{
  op: 0
  d: {
    unavailable: boolean,
    house_id: string
  }
}
```

## HOUSE_LEAVE
```
{
  op: 0
  d: {
    id: string,
    house_id: string
  }
}
```

## HOUSE_MEMBER_JOIN
```
{
  op: 0
  d: {
    user: {
      username: string,
      user_flags: string,
      name: string,
      id: string,
      icon: string,
      header: string
    },
    roles: [],
    joined_at: string,
    house_id: string
  }
}
```

## HOUSE_MEMBER_LEAVE
```
{
  op: 0
  d: {
    user: {
      username: string,
      user_flags: string,
      name: string,
      id: string,
      icon: string,
      header: string
    },
    roles: [],
    presence: string,
    joined_at: string,
    house_id: string
  }
}
```

## HOUSE_UPDATE
```
{
  op: 0
  d: {
    type: int,
    roles: [{
      position: int,
      name: string,
      level: int,
      id: string,
      deny: int,
      color: string,
      allow: int
    }],
    owner_id: string,
    name: string,
    id: string,
    icon: string,
    house_id: string,
    entities: [{
      type: int,
      resource_pointers: [{
        resource_type: string,
        resource_id: string
      }],
      position: int,
      name: string,
      id: string
    }],
    default_permissions: int,
    banner: unknown
  }
}
```


# Data
list of websocket data you can send

## Ping
```
{
  op: 3
}
```
This is to be sent on an interval of hbt_int, as received upon connection.

## Init
```
{
  op: 2,
  d: {
    token: string
  }
}
```
Authenticates you to Hiven Swarm.
Causes the server to send `INIT_STATE`, and `HOUSE_JOIN` for every house the authenticated account is in.

## Request Presence Updates
```
{
  op: 6
  d: {
    user_ids: string[]
  }
}
```
Subscribes you to presence updates for a user.
Causes the server to send `PRESENCE_UPDATE` immediately after subscribing, and whenever the presence of a user you've subscribed to changes.

## Request House Members
```
{
  op: 7,
  d: {
    house_id: string;
    user_ids: string[];
  }
}
```
Causes the server to send `HOUSE_MEMBER_CHUNK` with the member data of the requested users.

## Select A Room
```
{
  op:4,
  d:{
    id: string
  }
}
```
Haven't been able to get this working properly, but it seems to be so Hiven remembers what room you were last viewing, so you can be put back into that room next time you visit Hiven.