---
title: Shift DMS API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <span> &copy2017, Developed @ Andela </span>

includes:
  - documents
  - users
  - roles

search: true
---

# Shift DMS API Documentation

## Introduction
The Shift-DMS API contains several end points that allow the user to create, modify, fetch and delete documents. There are also a couple of endpoints strictly for the OVERLORD to manage roles and users on the platform.
Some of the endpoints are protected as such only registered and authenticated users can have access.
Generally, a user belongs in a role which he picks while creating his account. He has access to create documents, edit those documents, make them public or private and share them with the available roles. 
The Overlord can delete existing users and also public documents. He also has rights to create new public documents.

## Development
The application was developed with [NodeJs](http://nodejs.org/) and [Express](http://expressjs.com/) is used for routing. The [Postgres](http://postgresql.com/) database was used with sequelize as the ORM.

## Installation
Follow the steps below to setup a local development environment. First ensure you have [Postgresql](https://www.postgresql.org/) installed with an empty database instance named `shift-dms` created. A version of [Node.js](http://nodejs.org/) equal or greater than v6.8.0. should also be installed and properly set up.

1. Clone the repository to your local machine: `git clone https://github.com/andela-ifatoki/CP2-Shift-DMS.git`.
2. cd into the project directory using:  `cd CP2-Shift-DMS`
3. Rename `.env.sample` to `.env` and add the required environment variables.
4. Install project dependencies `npm install`
5. Start the express server in development mode: `npm run dev`.

## API Summary
### Users
EndPoint                           |   Functionality
-----------------------------------|------------------------
POST /auth/api/users/login         |   Logs in a user.
POST /api/users/logout             |   Logs out a user.
POST /auth/api/users/              |   Creates a new user.
GET /api/users/                    |   Gets all registered users (available only to the Overlord).
GET /api/users/:id                 |   Finds a particular user by his/her id.
PUT /api/users/:id                 |   Updates a user's attributes based on the id specified (available to the profile owner)
DELETE /api/users/:id              |   Deletes a user (available only to the Overlord)
GET /api/users/:id/documents       |   Gets all documents belonging to a particular user

### Documents
EndPoint                      |   Functionality
------------------------------|------------------------
POST /api/documents/          |   Creates a new document.
GET /api/documents/           |   Gets all documents (uses queries to specify document type e.g `type=private`, `type=public`, `type=role`)
GET /api/documents/:id        |   Find a particular document by it's id.
PUT /api/documents/:id        |   Updates a document attributes. (available only to the owner)
DELETE /api/documents/:id     |   Delete a particular document. (available only to the owner and if public, the Overlord)
GET /api/search/documents/?q=${query} | Get all documents with title containing the search query

### Roles
EndPoint                          |   Functionality
----------------------------------|------------------------
GET /api/roles/                   |   Get all created Roles.
POST /api/roles/                  |   Create a new Role (available only to the Admin)
DELETE /api/roles/:id             |   Delete a Role (available only to the Admin)