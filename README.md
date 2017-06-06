# json-server many-to-many example

This many-to-many example for json-server has two modes.

## Embed as nested resource

First, there's a many-to-many embedded mode which pulls the many-many relationship as a nested resource. The function for this is an ad-hoc function which demonstrates the logic pretty clearly.

### Start server

```
yarn run nested
```

### Embed users within groups

http://localhost:3000/groups/1/users

Result:

```
{
  "id": 1,
  "name": "user",
  "users": [
    {
      "id": 0,
      "name": "Emmett Okuneva"
    },
    {
      "id": 1,
      "name": "Maryse Goodwin"
    }
  ]
}
```

### Embed groups within users

http://localhost:3000/users/1/groups

Result:

```
{
  "id": 1,
  "name": "Maryse Goodwin",
  "groups": [
    {
      "id": 0,
      "name": "admin"
    }
  ]
}
```

## Embed as filter

Alternatively, you may pass the query parameter `_include` with the intended many-to-many side to be included. This example presents a solution that does not act as middleware because other pre-bound routes don't account for existing `res.locals.data`.

### Start server

```
yarn run included
```

### Users + groups

http://localhost:3000/users?_include=groups

```
[
  {
    "id": 0,
    "name": "Emmett Okuneva",
    "groups": [
      {
        "id": 0,
        "name": "admin"
      }
    ]
  },
  {
    "id": 1,
    "name": "Maryse Goodwin",
    "groups": [
      {
        "id": 1,
        "name": "user"
      }
    ]
  },
  {
    "id": 2,
    "name": "Naomi Koch",
    "groups": [
      {
        "id": 0,
        "name": "admin"
      },
      {
        "id": 1,
        "name": "user"
      }
    ]
  }
]
```

### Groups + users

http://localhost:3000/groups?_include=users

```
[
  {
    "id": 0,
    "name": "admin",
    "users": [
      {
        "id": 0,
        "name": "Emmett Okuneva"
      },
      {
        "id": 2,
        "name": "Naomi Koch"
      }
    ]
  },
  {
    "id": 1,
    "name": "user",
    "users": [
      {
        "id": 1,
        "name": "Maryse Goodwin"
      },
      {
        "id": 2,
        "name": "Naomi Koch"
      }
    ]
  }
]
```
