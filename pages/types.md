## <-- [Back](../README.md) <!-- omit in toc -->

# Types <!-- omit in toc -->

## NAV

- [NAV](#nav)
- [user](#user)
- [room](#room)
- [member](#member)
- [role](#role)
- [entity](#entity)
- [Permissions](#permissions)
- [Type Integers](#type-integers)

## user
```
{
  username: string,
  user_flags: string,
  name: string,
  id: string,
  icon: string,
  header: string,
  presence: string
}
```

## room
```
{
  type: int,
  recipients: [{
    username: string,
    user_flags: string,
    name: string,
    id: string,
    icon: string,
    header: string,
    presence: string
  }],
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
}
```

## member
```
{
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
```

## role
```
{
  position: int,
  name: string,
  level: int,
  id: string,
  deny: int,
  color: string,
  allow: int
}
```

## entity
```
{
  type: int,
  resource_pointers: [{
    resource_type: string,
    resource_id: string
  }],
  position: int,
  name: string,
  id: string
}
```

## Permissions
All the permission bits in a row.
Thanks to [@rishon](https://app.hiven.io/@rishon) for this list!
- SEND_MESSAGES = 1 << 0,
- READ_MESSAGES = 1 << 1,
- ADMINISTRATOR = 1 << 2,
- MODERATE_ROOM = 1 << 3,
- EVICT_MEMBERS = 1 << 4,
- KICK_MEMBERS = 1 << 5,
- ATTACH_MEDIA = 1 << 6,
- MANAGE_ROLES = 1 << 7,
- MANAGE_BILLING = 1 << 8,
- MANAGE_BOTS = 1 << 9,
- MANAGE_INTEGRATIONS = 1 << 10,
- MANAGE_ROOMS = 1 << 11,
- START_PORTAL = 1 << 12,
- STREAM_TO_PORTAL = 1 << 13,
- TAKEOVER_PORTAL = 1 << 14,
- POST_TO_FEED = 1 << 15,
- MANAGE_USER_OVERRIDES = 1 << 16,
- CREATE_INVITES = 1 << 17,
- MANAGE_INVITES = 1 << 18

## Type Integers
### relationship types
```
{
  0: 'none',
  1: 'outgoing request',
  2: 'incoming request',
  3: 'friends',
  4: 'restricted',
  5: 'blocked'
}
```

### notification preferences
```
{
  0: 'all',
  1: 'mentions',
  2: 'none'
}
```

### room types
```
{
  0: 'House',
  1: 'DM',
  2: 'Group'
}
```