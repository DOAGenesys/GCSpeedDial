# Genesys Cloud Speed Dial Application

## Overview

This application provides a user-friendly interface for Genesys Cloud users to search for external contacts and manage a personalized speed dial list. Users can quickly find contacts and initiate calls directly from the application, streamlining their workflow. The speed dial list is persistent, meaning a user's favorite contacts are saved and automatically loaded each time they use the application.

## Features

* **External Contact Search**: Search for external contacts stored in your Genesys Cloud organization.
* **Speed Dial List**: Add or remove contacts from a personal speed dial list for quick access.
* **Click-to-Dial**: Initiate a call to a contact directly from the speed dial list.
* **Persistent Favorites**: Your speed dial list is saved. The application intelligently tags your chosen contacts in the backend, so they are automatically loaded the next time you open the app.
* **Dynamic UI**: A clean and responsive user interface for a seamless experience.

## How It Works

The application is a client-side web app built with HTML, CSS, and JavaScript that leverages the Genesys Cloud Platform SDK to interact with the Genesys Cloud API.

1.  **Authentication**: When you first open the application, it authenticates with Genesys Cloud using an OAuth Implicit Grant flow to get a token on your behalf.
2.  **Loading Favorites**: On startup, the application fetches all external contacts and filters them to find any that you have previously marked as a "speed dial" favorite. This is done by checking a custom field on the contact record.
3.  **Searching**: When you search for a contact, the app queries the Genesys Cloud API and displays the results.
4.  **Adding a Favorite**: When you add a contact to your speed dial list, the application makes an API call to update the contact record in Genesys Cloud, setting a custom field (`speed_dial_checkbox`) to `true`. This marks the contact as a favorite.
5.  **Removing a Favorite**: When you remove a contact, the same custom field is set to `false`, and the contact is removed from your UI list.
6.  **Placing a Call**: Clicking the dial button next to a contact initiates a call through the Genesys Cloud API, using your selected phone (e.g., softphone).

## Project Structure

* `index.html`: The main HTML file that defines the structure of the user interface, including the search bar, results area, and speed dial list.
* `main.js`: This file contains the core logic of the application. It handles searching for contacts, adding/removing contacts from the speed dial list, and interacting with the Genesys Cloud API to place calls and update contact information.
* `startGCSDKs.js`: This script is responsible for initializing the Genesys Cloud Platform SDK, handling the OAuth authentication process, and retrieving user details.
* `styles.css`: This file contains all the CSS rules for styling the application, making it responsive and visually appealing.
* `api/getConfig.js`: A serverless function used to securely provide the necessary Genesys Cloud OAuth Client ID to the frontend application without exposing it directly in the client-side code.
