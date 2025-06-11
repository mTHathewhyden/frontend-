<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Recipe Finder</title>
</head>
<style>
 *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
  }
  
  .container {
    max-width: 800px;
    margin: 50px auto;
    text-align: center;
  }
  
  h1 {
    color: #d51414b3;
    margin-bottom: 20px;
  }
  
  .search-bar {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  input {
    width: 300px;
    padding: 10px;
    font-size: 16px;
  }
  
  button {
    padding: 10px 15px;
    font-size: 16px;
    cursor: pointer;
    background-color: #28a745;
    color: white;
    border: none;
  }
  
  .recipe-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  
  .recipe-card {
    background-color: white;
    width: 250px;
    margin: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    text-align: center;
    overflow: hidden;
  }
  
  .recipe-card img {
    width: 100%;
    height: 150px;
    object-fit: cover;
  }
  
  .recipe-card h3 {
    font-size: 18px;
    color: #333;
    padding: 10px;
  }
  </style>
<body>
  <div class="container">
    <h1>Recipe Finder</h1>
    <div class="search-bar">
      <input type="text" id="ingredient" placeholder="Enter an ingredient...">
      <button id="search-btn">Search</button>
    </div>
    <div id="recipes" class="recipe-container"></div>
  </div>

<script>
    // Spoonacular API key (get yours from https://spoonacular.com/food-api)
const apiKey = 'c2b2c53009c249df8effe98f9d294fea';
const searchBtn = document.getElementById('search-btn');
const recipesContainer = document.getElementById('recipes');

searchBtn.addEventListener('click', () => {
  const ingredient = document.getElementById('ingredient').value;
  if (ingredient) {
    fetchRecipes(ingredient);
  } else {
    alert('Please enter an ingredient');
  }
});

async function fetchRecipes(ingredient) {
  const url = `https://api.spoonacular.com/recipes/findByIngredients?ingredients=${ingredient}&number=6&apiKey=${apiKey}`;
  
  try {
    const response = await fetch(url);
    const data = await response.json();
    displayRecipes(data);
  } catch (error) {
    console.error('Error fetching recipes:', error);
  }
}

function displayRecipes(recipes) {
  recipesContainer.innerHTML = ''; // Clear previous results
  
  recipes.forEach(recipe => {
    const recipeCard = document.createElement('div');
    recipeCard.classList.add('recipe-card');

    recipeCard.innerHTML = `
      <img src="${recipe.image}" alt="${recipe.title}">
      <h3>${recipe.title}</h3>
    `;

    recipeCard.addEventListener('click', () => {
      showRecipeDetails(recipe);
    });

    recipesContainer.appendChild(recipeCard);
  });
}

function showRecipeDetails(recipe) {
  alert(`Recipe: ${recipe.title}\nMissed Ingredients: ${recipe.missedIngredientCount}`);
}
  </script>
</body>
</html>

