# Fitness App

A Java desktop app for planning meals and workouts. Users can search healthy recipes by calorie and diet goals, generate meal plans, calculate BMI and daily calorie needs, and find exercises by name or target muscle.

Built as a team project for CSC207 (Software Design) at the University of Toronto, following **Clean Architecture**.

## Features

- **Account signup and login**, with password validation and users stored in a CSV file
- **Recipe search** by calorie range and diet labels, using the Edamam Recipe API
- **Meal planning**, using the Edamam Meal Planner API
- **Calorie counter**: BMI, ideal weight, and daily calorie needs, using the Fitness Calculator API
- **Workout search** by exercise name or target muscle, using the ExerciseDB API

## Architecture

The code follows Clean Architecture. Dependencies point inward, so the business logic does not depend on the UI, the APIs, or storage.

```
src/
├── entity/             # Core business objects (User, Recipe, Workout, MealPlan)
├── use_case/           # Interactors + input/output boundaries for each feature
├── interface_adapter/  # Controllers, presenters, view models, view state
├── DataAccess/         # API clients and user storage (CSV file + in-memory)
├── view/               # Java Swing UI
└── app/                # Use-case factories and Main (dependency wiring)
TEST/                   # JUnit 5 tests
```

Each feature is its own use case. A controller builds the input data, an interactor runs the business logic through data-access interfaces, and a presenter updates the view model. Because the interactors only depend on interfaces, the storage and API layers can be swapped out. For example, the CSV-backed user store can be replaced by an in-memory one, or a mock can stand in during tests.

## Tech Stack

Java · Swing · JUnit 5 · Gson · org.json · REST APIs (Edamam, ExerciseDB, Fitness Calculator)

## Running It

1. Open the project in **IntelliJ IDEA**.
2. Make sure the Gson (`com.google.code.gson:gson:2.10.1`), `org.json:json:20231013`, and JUnit 5 libraries are added to the module.
3. Run `src/app/Main.java`.

The API calls need valid keys for Edamam and RapidAPI (ExerciseDB / Fitness Calculator).

## Tests

Tests are in `TEST/` and cover the `Recipe` entity and the recipe search interactor. The interactor tests use mock presenter and data-access classes, so they exercise the business logic without calling a real API.

Run them from IntelliJ: right-click `TEST/` and choose **Run 'All Tests'**.

## Team

A CSC207 group project. The original repository is [207project/Fitness-App](https://github.com/207project/Fitness-App).

- [Muhammad Muaawiz](https://github.com/Muaawiz1): recipe search, workout search (by name and by muscle), recipe and workout UI, and tests
- [WorthOnGit](https://github.com/WorthOnGit)
- [amonsyali](https://github.com/amonsyali)
- [spreesir](https://github.com/spreesir)
- [sarimsarfraz](https://github.com/sarimsarfraz)
