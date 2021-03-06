# Tinder App - Users Service

User service for Tinder App. Handles and stores all the user information

## Roadmap

View the project roadmap [here](https://drive.google.com/open?id=1kAPJHYxOglYTeN3WJslR1_gGNFUneNer6oveAjPyoFA)

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.

# Table of Contents

1. [Usage](#Usage)
1. [API Usage](#api-usage)
    1. [Input](#input)
    1. [Output](#output)
1. [Requirements](#requirements)
1. [Development](#development)
    1. [Installing Dependencies](#installing-dependencies)
    1. [Tasks](#tasks)

## Usage

### API Usage

#### Input

Query will happen with one of two unique keys

```javascript
{
  type: STRING,
  query: NUMBER or STRING,
  gender: STRING,
  filter: ARRAY,
  startDate: STRING,
  endDate: STRING
}
```

- `type` Can be either __user__ or __stat__. Defaults to __user__.
- `query` Used with type __user__. User ID num or zone string. Can accept an array
- `gender` Used with type __user__. _OPTIONAL_. The gender of users to retrieve
- `filter` Used with type __user__. _OPTIONAL_. An array of userIDs to omit from results, e.g. swiped users

- `startDate` Used with _stat_. Start of period to query for stats. Takes formats supported by PostgreSQL. Defaults at first entry
- `endDate` Used with _stat_. End of period to query for stats. Takes formats supported by PostgreSQL. Defaults at last entry

##### Example User Request Parameters

Get full information on user with ID _#7443_
```javascript
{
  type: 'user',
  query: 7443
}
```

Get all females from _"Zone A"_ except userIDs _56_ and _69_
```javascript
{
  type: 'user',
  query: 'A',
  gender: 'F',
  filter: [65, 69]
}
```

##### Example Stat Request Parameters

Get stats from Oct 31 1984 to Dec 25 1984
```javascript
{
  type: 'stat',
  startDate: '1984-10-31'
  endDate: '1984-12-25'
}
```

#### Output

##### Type 'user'
```javascript
[{
  userId: NUMBER,
  name: STRING,
  email: STRING,
  gender: STRING,
  location: STRING,
  photoCount: NUMBER,
  traits: ARRAY
}]
```

The return object has been built to include information irrelevant to the MVP, for future expansion opportunity

- `userId` The user's ID number
- `name` The user's name
- `email` The user's email count
- `gender` The user's gender
- `location` Which zone the user is located in
- `photoCount` The number of photos the user has uploaded
- `traits` An array of objective terms that can be used to describe the user's physical appearance. Represents a photo of user

##### Type 'stat'

```javascript
{
  errorsCounted: NUMBER,
  entries: NUMBER,
  averageEntryTime: NUMBER,
  averageRetrieveTime: NUMBER
}
```

- `errorsCounted` The number of insertion/read errors generated in the database
- `entries` Number of entries in the database
- `averageEntryTime` Average time it takes to insert in milliseconds
- `averageRetrieveTime` Average time it takes to retrieve in milliseconds

## Requirements

- Node 6.9.x
- Postgresql 9.6.x
- express 4.16.2
- faker 4.1.0
- mocha 4.0.1
- chai 4.1.2
- pg 7.3.0
- pg-hstore 2.3.2
- sequelize 5.15.0

## Development
### Installing Dependencies
Run `npm install`

### Tasks

#### Simulation

- Simulate new user sign-ups
- Simulate account deletions
- Simulate user information pulls

#### Monitoring/Testing

- Time for insertion saved
- Time for retrieve saved
- Time for remove saved
- Errors logged out into log directory


## Other Information

### Schema

__Users__

| col | type |
| ----- | -----:|
| name | VARCHAR |
| traits | VARCHAR |
| gender | VARCHAR |
| photo_count | INT |
| email | VARCHAR |
| location | VARCHAR |
