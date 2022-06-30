# Flask-SQLAlchemy

This repository extends the [Flask-REST-API](https://github.com/mhoward91/flask-rest-api) project. Please review this project's documentation for complete context.

## Description

The following enhancements have been made:
- SQLAlchemy is used as a Object Relational Mapper (ORM) to faciliate communication between the app & the SQLite database. It substitutes the need to manually create db tables, write SQL query statements, and convert db rows to python objects
- A stores table has been added to the database schema, allowing groupings of items to be arranged in a store
- The app incorporates token refreshing and additional Flask-JWT-extended features
- The app is deployed using Heroku

_README development in progress_
