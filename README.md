RecipeBook

A simple ASP.NET MVC Recipe application that allows users to browse, view, create, edit and delete recipes. The project follows a clean separation of concerns using Models, Views, Controllers and a Repository layer for data access.




RecipeBook is an educational/sample web application built with ASP.NET MVC (System.Web.Mvc). It demonstrates typical patterns used in enterprise web apps: MVC architecture, a Repository layer for data access, simple CRUD operations for Recipe entities, and separation of concerns between controllers, models, and views.

Features

List all recipes

View recipe details

Create new recipes

Edit existing recipes

Delete recipes

Simple server-side validation

Technology Stack

Framework: ASP.NET MVC (System.Web.Mvc)

Language: C#

Data Access: Repository pattern (works with ADO.NET / Entity Framework—adaptable)

Database: SQL Server / LocalDB (recommended for development)

View Engine: Razor

Build/Run: Visual Studio (2017/2019/2022) or msbuild

You can replace the data access implementation with Entity Framework or another ORM if you prefer.

Project Structure
RecipeBook/
├── Controllers/
│   └── RecipeController.cs
├── Models/
│   └── Recipe.cs
├── DataAccess/
│   └── RecipeRepository.cs
├── Views/
│   └── Recipe/ (Index, Create, Edit, Details, Delete)
├── Scripts/
├── Content/
├── Web.config
└── README.md
Installation & Setup
Prerequisites

Windows (recommended for full Visual Studio support)

Visual Studio 2017/2019/2022 with ASP.NET workload, or the .NET Framework Developer Pack

SQL Server or LocalDB

Clone & Build

Clone the repository:

git clone <your-repo-url>
cd RecipeBook

Open the solution (.sln) in Visual Studio.

Restore NuGet packages (Visual Studio will usually do this automatically).

Build the solution.

Database Setup

This project expects a relational database. Two common options:

Option A — LocalDB (Development)

Open Web.config and set the connection string to a LocalDB instance:

<connectionStrings>
  <add name="DefaultConnection" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;Initial Catalog=RecipeBookDb;Integrated Security=True;" providerName="System.Data.SqlClient" />
</connectionStrings>

If you use Entity Framework, enable migrations and update the database:

Enable-Migrations
Add-Migration InitialCreate
Update-Database

Option B — Existing SQL Server

Point the DefaultConnection to your SQL Server, create the database manually or let EF create it (if using EF).

If the repository uses raw SQL/ADO.NET, run the provided schema.sql (if present) to create tables and seed data.

Run the App

Start the app from Visual Studio (IIS Express) or publish it to IIS.

Open a browser and navigate to http://localhost:{port}/Recipe (replace {port} with the port shown in Visual Studio).

Implementation Strategy
High-level Architecture

Presentation: MVC Views (Razor) provide the UI.

Controller layer: RecipeController handles HTTP requests and maps them to repository operations.

Business/Repository: RecipeRepository encapsulates all data access (CRUD). Keeps controllers thin.

Data Access & Repository Pattern

The repository exposes methods like GetAllRecipes(), GetRecipeById(id), AddRecipe(recipe), UpdateRecipe(recipe), and DeleteRecipe(id).

This makes it straightforward to swap out the persistence mechanism (e.g., EF, Dapper, or raw ADO.NET).

Views & UX

Use simple, responsive Bootstrap layout (optional) for the Views folder.

Keep forms accessible and server-validated, and perform minimal client-side validation for UX.

Validation & Error Handling

Use Data Annotations on the Recipe model for required fields and string lengths.

Controllers should check ModelState.IsValid before saving.

Centralize logging (e.g., use log4net/NLog or the built-in trace for errors).

Testing

Unit-test controllers by mocking RecipeRepository (use Moq or similar).

Add integration tests for repository methods against a test database (or in-memory DB if using EF Core).

Deployment

For Windows servers, publish to IIS using Web Deploy or a file publish profile.

Ensure connection strings and app settings are updated for production (use environment variables or transform Web.config).


License

This project is provided as-is for educational/demo purposes. Add a license (e.g., MIT) if you plan to open-source and accept contributions.

If you need the README tailored (for example, specific SQL scripts, exact connection string, or switching to Entity Framework code examples), tell me what to include and I will update it.
