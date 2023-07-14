# SpringFinancial
Coding Test for Spring Financial by Ajay Ramasubramanian for Full Stack Developer position

## Frontend Implementation:
- The frontend code is implemented using the Vue.js framework.
- The main page is the "HomeView.vue" component, which represents the leaderboard screen.
- It displays a list of players with their names, points, and buttons to add or subtract points.
- The leaderboard can be sorted by name or points by clicking the corresponding headers.
- There is a search input box to filter players by name.
- Clicking on a player's name toggles the display of their details, including name, age, points, and address.
- There is a button to add a new player, which navigates to the "RegistrationForm.vue" component.
- In the registration form, the user can enter the player's name, age, and address. Points are automatically set to 0.
- The form performs client-side validation, checking the length of the name and age range.
- When the form is submitted, an HTTP POST request is made to the backend API to add the player.
- The API endpoints are defined in the Laravel backend.

## Backend Implementation:
- The backend is implemented using the Laravel framework.
- The table is created in schema 'spring_ajay' and the table name is players.
- The "Players" model represents the players table in the database and defines the fillable fields.
- The fields used were Name, Age, Points and Address.
- The "AddPlayerRequest" class defines the validation rules for adding and updating players.
  - All the fields are required.
  - Age and Points are integer, and Name and Address are String.
  - Age must be between 3 to 150.
  - Name must have 3-20 characters and must be unique for every players.
- The API endpoints are defined in the "PlayerController" class in the "Api" namespace.
  - The "index" method returns all players from the database.
  - The "show" method retrieves a specific player based on the provided ID.
  - The "store" method receives a request with player data and creates a new player in the database.
  - The "update" method receives a request with player data and updates the corresponding player in the database.
  - The "destroy" method deletes a player from the database.

###   PHP ARTISAN commands that were used:-
The following commands were used during the backend implementation to create the necessary files, set up the database, define the API endpoints, and handle the validation of player data.
- To create the Players model and migration, the following command was executed: 
     php artisan make:model Players -m
   This command generates the Players model class and creates a corresponding migration file.
- The migration file created in the previous step was used to define the players table structure. To migrate the database and create the players table, the following command was executed:  
     php artisan migrate
- To create the PlayerController, which handles the API endpoints for players, the following command was executed:  
     php artisan make:controller Api/PlayerController
   This command generates the PlayerController class in the `Api` namespace.
- The `route:list` command was used to view the list of registered routes in the application. It provides an overview of the available API endpoints and their corresponding controller methods. The command was executed as follows:
     php artisan route:list
- The AddPlayerRequest class was created to define the validation rules for adding and updating players. This request class extends the FormRequest class provided by Laravel. The following command was executed to generate the AddPlayerRequest class:
     php artisan make:request AddPlayerRequest
- To generate the PlayerFactory class, which is used for seeding the players table with dummy data, the following command was executed:
     php artisan make:factory PlayerFactory --model=Players
  This command generates the PlayerFactory class and associates it with the Players model.

## Instructions to Run the Application:
- Clone this repository and navigate to the project directory.
### In backend/
- Make sure you have Node.js and Composer installed on your system.
- Install the frontend dependencies by running the following command:
    npm install
- Install the backend dependencies by running the following command:
    composer install
- Create a copy of the .env.example file and rename it to .env.
- Generate a new application key by running the following command:
    php artisan key:generate
- Create a new MySQL database for the application.
- Update the database configuration in the .env file with your MySQL database credentials.
- Migrate the database by running the following command:
    php artisan migrate
- Start the Laravel development server by running the following command:
    php artisan serve
### In vue-frontend/
- In a separate terminal, start the frontend development server by running the following command:
    npm run serve
- Open your web browser and access the application at the provided URL (e.g., http://localhost:8080).

## Unit Test Cases for both frontend and backend

### For Backend

The provided test cases demonstrate how to write feature tests for the Laravel backend. These tests ensure that the API endpoints for player operations are functioning correctly. Here's a breakdown of the test cases:

-testGetAllPlayers:
  - This test case verifies that the API endpoint for retrieving all players returns a successful response with the correct JSON structure.
  - It uses the Players model factory to create three player records in the database.
  - The test sends a GET request to the /api/players endpoint and asserts that the response status is 200 (OK) and that the JSON response contains three players.

-testGetSinglePlayer:
  - This test case verifies that the API endpoint for retrieving a single player returns a successful response with the correct JSON structure.
  - It uses the Players model factory to create a player record in the database.
  - The test sends a GET request to the /api/players/{id} endpoint, where {id} is the ID of the created player, and asserts that the response status is 200 (OK) and that the JSON response matches the player's name, age, points, and address.

- testCreatePlayer:
  - This test case verifies that the API endpoint for creating a new player returns a successful response.
  - It sends a POST request to the /api/players endpoint with the required player data.
  - The test asserts that the response status is 200 (OK) and that the JSON response contains the message "Player added".

- testUpdatePlayer:
  - This test case verifies that the API endpoint for updating a player returns a successful response.
  -  It uses the Players model factory to create a player record in the database.
  - The test sends a PUT request to the /api/players/{id} endpoint, where {id} is the ID of the created player, with the updated player data.
  - The test asserts that the response status is 200 (OK) and that the JSON response contains the message "Player updated".

-testDeletePlayer:
  - This test case verifies that the API endpoint for deleting a player returns a successful response.
  - It uses the Players model factory to create a player record in the database.
  - The test sends a DELETE request to the /api/players/{id} endpoint, where {id} is the ID of the created player.
  - The test asserts that the response status is 200 (OK) and that the JSON response contains the message "Player deleted".

### For frontend

The provided test cases demonstrate how to write unit tests for the frontend components using Vue Test Utils and the `vitest` testing library. Here's a breakdown of the test cases for both the HomeView and RegistrationForm components:

- HomeView Test Cases:
  - `renders leaderboard heading correctly`: This test verifies that the leaderboard heading is rendered correctly in the HomeView component. It mounts the HomeView component, finds the heading element, and asserts that its text matches the expected value.
  - `filters players by name correctly`: This test simulates filtering players by name in the HomeView component. It sets a search query in the input field, retrieves the filtered players, and checks if all filtered players have names that include the search query.
  - `clears filter when "Clear Filter" button is clicked`: This test verifies that the filter is cleared correctly when the "Clear Filter" button is clicked. It sets a search query, triggers the click event on the clear filter button, and checks if the filtered players array is reset to the original list of all players.
  - `sorts players by name correctly`: This test checks if the players are sorted by name correctly when the "Sort by Name" button is clicked. It triggers the click event on the sort by name button and compares the sorted players array with the expected sorted array.

- RegistrationForm Test Cases:
  - `displays the "Player Registration" heading correctly`: This test ensures that the "Player Registration" heading is displayed correctly in the RegistrationForm component. It mounts the RegistrationForm component, finds the heading element, and asserts that its text matches the expected value.
  - `correctly binds form fields to the player data object`: This test checks if the form fields in the RegistrationForm component correctly bind to the player data object. It sets values for the form fields, triggers the input events, and asserts that the player object's properties are updated accordingly.

These test cases cover various aspects of the frontend components, such as rendering, filtering, clearing filters, sorting, and form field binding. They help ensure that the components behave as expected and provide the desired functionality.
