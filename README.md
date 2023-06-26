# Caller-ID API

# REST API Endpoints for User Contacts App

This is a documentation for the REST API endpoints of a User Contacts App. The app allows registered users to manage their personal contacts and search for contacts in the global database. The API endpoints are designed to be consumed by a front-end application.

## Assumptions and Terminology

- Each registered user of the app can have zero or more personal contacts.
- The "global database" refers to the combination of all registered users and their personal contacts, which may or may not be registered users themselves.
- The UI will be built separately, and this documentation focuses on the REST API endpoints.
- The implementation should consider performance and security aspects for production use.
- The application uses a web server (development server) and a database to incorporate all the concepts.

## Data Stored for Each User

Each user in the app has the following data associated with them:

- Name: The user's name.
- Phone Number: The user's phone number, which is unique to each registered user.
- Email Address: An optional email address associated with the user.

## Registration and Profile

To use the app, users need to register with at least their name, phone number, and password. They can optionally add an email address.

- **POST /api/register**: Register a new user with the required information (name, phone number, password) and optional email address.

## Authentication

Authentication is required for all subsequent operations after registration. Users must log in to access the app's functionalities.

- **POST /api/login**: Log in a user by providing the phone number and password.

## Contacts

Users can manage their personal contacts and perform operations related to contacts.

- **GET /api/contacts**: Retrieve all contacts of the logged-in user.
- **POST /api/contacts**: Add a new contact to the logged-in user's list. The request should include the contact's name and phone number.
- **PUT /api/contacts/{contactId}**: Update an existing contact by providing the contact's ID in the URL path. The request should include the updated contact's name and phone number.
- **DELETE /api/contacts/{contactId}**: Delete a contact from the logged-in user's list by providing the contact's ID in the URL path.

## Spam

Users can mark phone numbers as spam to help other users identify potential spammers.

- **POST /api/spam**: Mark a phone number as spam. The request should include the phone number to be marked.

## Search

Users can search for contacts in the global database based on name or phone number.

- **GET /api/search?name={name}**: Search for contacts by name in the global database. The request should include the name parameter to search for matching contacts. The response includes names, phone numbers, and spam likelihood for the matching results.
- **GET /api/search?phone={phoneNumber}**: Search for contacts by phone number in the global database. The request should include the phone parameter to search for matching contacts. If a registered user is found with the provided phone number, only that result is returned. Otherwise, all matching contacts' names and phone numbers are returned.

## Contact Details

Users can view detailed information about a specific contact, including spam likelihood. However, the contact's email address is only displayed if the contact is a registered user and the logged-in user is in the contact's personal contact list.

- **GET /api/contacts/{contactId}**: Retrieve the details of a specific contact by providing the contact's ID in the URL path.

## Data Population

For testing purposes, a script or facility should be implemented to populate the database with random sample data.

This documentation provides an overview of the available REST API endpoints for the User Contacts App. The API

 endpoints can be used to build the app's front-end and facilitate user registration, contact management, spam reporting, searching, and viewing contact details.
