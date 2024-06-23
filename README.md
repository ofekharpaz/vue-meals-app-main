# Recipe App

Welcome to Recipe App! This application suggests recipes sourced from TheMealDB API. It allows users to explore recipes randomly, sort them by name, ingredients, or by a specific letter. The frontend is built with Vue.js, providing a seamless user experience for discovering and managing recipes.

## Features

- **Random Recipes**: Get random recipe suggestions to discover new dishes.
- **Sort Recipes**: Sort recipes by name, ingredients, or filter by a specific letter.
- **Explore Ingredients**: Browse recipes based on available ingredients.
- **Detailed Recipe Information**: View detailed information about each recipe, including ingredients and instructions.
- **Responsive Design**: Enjoy a responsive and intuitive user interface across devices.

## Technologies Used

- **Frontend**: Vue.js, Vuex (for state management), Vue Router (for routing)
- **Backend**: TheMealDB API (https://www.themealdb.com/)
- **Deployment**: Render

## Installation

To run this application locally, follow these steps:

1. Clone the repository:

`git clone https://github.com/your-username/recipe-app.git`

2. Install dependencies:

`npm install`

3. Create a `.env` file in the root directory and add your API key:

`VUE_APP_MEALDB_API_KEY=https://www.themealdb.com/api/json/v1/1/`

4. Start the development server:

`npm run serve`

5. Open your browser and visit `http://localhost:8080` to view the app.