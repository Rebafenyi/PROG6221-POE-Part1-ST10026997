# PROG6221-POE-Part1-ST10026997
using System.Collections.Generic;

class Recipe
{
    public List<Ingredient> Ingredients { get; set; }
    public List<string> Steps { get; set; }

    public Recipe()
    {
        Ingredients = new List<Ingredient>();
        Steps = new List<string>();
    }

    public Recipe(List<string> steps)
    {
        Steps = steps;
    }

    public void AddIngredient(string name, double quantity, string unit)
    {
        Ingredients.Add(new Ingredient(name, quantity, unit));
    }

    public void AddStep(string description)
    {
        Steps.Add(description);
    }


    public void Print()
    {
        //Prints the list of ingredients with their respective quantities and units
        Console.WriteLine("Ingredients:");
        foreach (Ingredient ingredient in Ingredients)
        {
            Console.WriteLine($"{ingredient.Name}: {ingredient.Quantity} {ingredient.Unit}");
        }
        Console.WriteLine("\nSteps:");

        //It uses a loop to iterate through the steps list and print each step with its corresponding number
        for (int i = 0; i < Steps.Count; i++)
        {
            Console.WriteLine($"{i + 1}. {Steps[i]}");
        }
    }

    public void Scale(double factor)
    {
        foreach (Ingredient ingredient in Ingredients)
        {
            ingredient.Quantity *= factor;
        }
    }

    public void ResetQuantities()
    {
        foreach (Ingredient ingredient in Ingredients)
        {
            ingredient.Quantity = ingredient.OriginalQuantity;
        }
    }

    public void Clear()
    {
        Ingredients.Clear();
        Steps.Clear();
    }
}

class Ingredient
{
    public string Name { get; set; }
    public double Quantity { get; set; }
    public double OriginalQuantity { get; set; }
    public string Unit { get; set; }

    //Variables that make up the recipe
    public Ingredient(string name, double quantity, string unit)
    {
        Name = name;
        Quantity = quantity;
        OriginalQuantity = quantity;
        Unit = unit;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Recipe recipe = new Recipe();

        Console.WriteLine("    ***********************************************************");
        Console.WriteLine("                 Welcome to the Big Recipe Ground...");
        Console.WriteLine("    ***********************************************************");
        Console.WriteLine("      Here you'll store recipes to whatever you'd like to eat.");
        Console.WriteLine("    ***********************************************************");

        Console.Write("\n       Enter the number of ingredients:");
        
        int numIngredients = int.Parse(Console.ReadLine());
        
        
        //The loop iterates through the number of ingredients specified by the user
        for (int i = 0; i < numIngredients; i++)
        {
            Console.Write($"\n          Enter the name of ingredient {i + 1}: ");
            string name = Console.ReadLine();

            Console.Write($"          Enter the quantity of ingredient {i + 1}: ");
            
            double v = double.Parse(Console.ReadLine());
            double quantity = v;

            Console.Write($"          Enter the unit of measurement of ingredient {i + 1}: ");
            string unit = Console.ReadLine();

            recipe.AddIngredient(name, quantity, unit);
        }
        
        Console.WriteLine("    ************************************************************");
       
        Console.Write("               Enter the number of steps: ");
        
        
        int numSteps = int.Parse(Console.ReadLine());


        //The loop iterates through the number of steps specified by the user
        for (int i = 0; i < numSteps; i++)
        {
            Console.Write($"      Enter the description of step {i + 1}: ");
           
            string description = Console.ReadLine();

            recipe.AddStep(description);
        }
        Console.WriteLine("    ************************************************************");

        
        // Display the recipe in a neat format
        Console.Write("\nRecipe:");
        recipe.Print();

        //The recipe object's methods are called
        while (true)
        {
            Console.WriteLine("    ************************************************************");
            Console.WriteLine("\nEnter a command (scale, reset, clear, or exit): ");
            string command = Console.ReadLine();

            switch (command)
            {
                case "scale":
                    Console.Write("\n              Enter the scale factor (0.5, 2, or 3): ");
                    double factor = double.Parse(Console.ReadLine());
                    recipe.Scale(factor);
                    recipe.Print();
                    break;

                case "reset":
                    recipe.ResetQuantities();
                    recipe.Print();
                    break;

                case "clear":
                    recipe.Clear();
                    Console.Write("\nRecipe cleared.");
                    break;

                case "exit":
                    Environment.Exit(0);
                    break;

                default:
                    Console.Write("\nInvalid command. Try again.");
                    break;
            }
        }
    }
}
       
