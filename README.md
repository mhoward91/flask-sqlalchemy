# Flask-SQLAlchemy

This repository extends the [Flask-REST-API](https://github.com/mhoward91/flask-rest-api) project, which provides the ability for registered users to retrieve and modify a database of household items for sale. Please review the original documentation for full context.

## Enhancements

The following enhancements have been made:
- SQLAlchemy is used as a Object Relational Mapper (ORM) to faciliate communication between the app & the SQLite database. It substitutes the need to manually create db tables, write SQL query statements, and convert db rows to python objects
- A stores table has been added to the database schema, allowing groupings of items to be arranged in a store
- The app is deployed using Heroku, at root URL [https://stores-flask-rest-api-mh.herokuapp.com/](https://stores-flask-rest-api-mh.herokuapp.com/)
  - the root URL itself is not used in the API - please see endpoints section below
  - the `GET` methods from the stores, store and items endpoints are publicly available without registration & authentication
- The deployed version of the app uses a PostgreSQL database as its data store, as opposed to a locally hosted SQLite database

## Planned features
- Token refreshing and additional Flask-JWT-extended security

## Endpoints

### 1. /stores

**Available methods**

| Method   | Description                              |
| -------- | ---------------------------------------- |
| `GET`    | Returns the complete stores list and their items as `json` data, displaying the names and prices of each item |

### 2. /items

**Available methods**

| Method   | Description                              |
| -------- | ---------------------------------------- |
| `GET`    | Returns a complete items list as `json` data, with items not broken down by store |

### 3. /store/\<name\>

- **URL Parameters** `GET` `POST` `DELETE`

    `name=[str]` (required) 
 
**Available methods**

| Method   | Description                              | HTTP Response
| -------- | ---------------------------------------- | -------------|
| `GET`    | Returns all items from a single store, identified by the \<name\> parameter | `200 OK` if store found, otherwise `404 Not Found` if store doesn't exist |
| `POST`    | Adds a store with name=\<name\> to the stores list | `201 Created` if store added, `400 Bad Request` if store already exists, or `500 Internal Server Error` if issue with the ORM (SQLAlchemy) |
| `DELETE`    | Deletes the store with name=\<name\> from the stores list | `200 OK` if item successfully deleted |

### 4. /item/\<name\>

- **URL Parameters** `GET` `POST` `PUT` `DELETE`

    `name=[str]` (required) 

- **Request Headers** `POST` `PUT`

    `{"Content-Type": "application/json"}`

- **Data (json payload)** `POST` `PUT`

    `{"price": <price>[float],
    "store_id": <id>[int]}`
    
 
**Available methods**

| Method   | Description                              | HTTP Response
| -------- | ---------------------------------------- | -------------|
| `GET`    | Returns data on a single item, identified by the \<name\> parameter | `200 OK` if item found, otherwise `404 Not Found` if item doesn't exist |
| `POST`    | Adds an item with name=\<name\>, to the defined store with price defined in the json payload | `201 Created` if item added, `400 Bad Request` if item already exists, or `500 Internal Server Error` if issue with the ORM (SQLAlchemy) |
| `PUT`    | Adds an item with name=\<name\>to the defined store if not present, otherwise updates the item's price with the price defined in the json payload | `200 OK` if item added or updated |
| `DELETE`    | Deletes the item with name=\<name\> from the database | `200 OK` if item successfully deleted |

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
