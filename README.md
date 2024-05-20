<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Recipe Form</title>
</head>
<body>
    <h1>Recipe Form</h1>
    <form id="recipe-form">
        <label for="recipeId">Recipe ID:</label>
        <input type="text" id="recipeId" name="recipeId" required>
        <button type="button" onclick="getRecipe()">Get Recipe</button>
        <br><br>
        
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <br><br>

        <label for="ingredients">Ingredients:</label>
        <textarea id="ingredients" name="ingredients" required></textarea>
        <br><br>

        <label for="instructions">Instructions:</label>
        <textarea id="instructions" name="instructions" required></textarea>
        <br><br>

        <button type="submit">Update Recipe</button>
    </form>

    <script>
        async function getRecipe() {
            const recipeId = document.getElementById('recipeId').value;
            const response = await fetch(`https://api.example.com/recipes/${recipeId}`);
            const recipe = await response.json();

            document.getElementById('name').value = recipe.name;
            document.getElementById('ingredients').value = recipe.ingredients;
            document.getElementById('instructions').value = recipe.instructions;
        }

        document.getElementById('recipe-form').addEventListener('submit', async function(event) {
            event.preventDefault();

            const recipeId = document.getElementById('recipeId').value;
            const name = document.getElementById('name').value;
            const ingredients = document.getElementById('ingredients').value;
            const instructions = document.getElementById('instructions').value;

            const response = await fetch(`https://api.example.com/recipes/${recipeId}`, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    name: name,
                    ingredients: ingredients,
                    instructions: instructions
                })
            });

            if (response.ok) {
                alert('Recipe updated successfully!');
            } else {
                alert('Failed to update recipe.');
            }
        });
    </script>
</body>
</html>
