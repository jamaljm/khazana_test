# Financial Management API 


A Flask-based API for managing user financial goals, portfolios, and assets. This API allows users to create financial goals, manage portfolios of assets (stocks, crypto, etc.), and track asset price history over time.

## Project Setup

### Prerequisites
Make sure you have the following installed on your machine:

- Python 3.7 or later
- PostgreSQL
- pip (Python package installer)

### Installation

1. **Clone the repository:**

   ```bash
   [git clone https://github.com/your-username/financial-management-api.git](https://github.com/jeffprakash/khazana_test.git)
   cd khazana_test

Create a virtual environment:
  
    ```bash
    python3 -m venv venv

Install the dependencies:

    ```bash  
    pip install -r requirements.txt

Run the flask
  
      ```bash  
      flask run


# Financial Management API - Overview of API Design

This section outlines the key endpoints, request/response formats, and the design of the API for the **Financial Management** application. The API allows users to manage their financial goals, portfolios, assets, and track asset price history over time.

## Base URL

The base URL for the API is:

https://api.example.com/



# Financial Management Database Schema

The database schema for the Financial Management API manages users, their financial goals, portfolios, assets, and asset price history. The relationships between these entities are key to providing the required functionality for financial tracking and management.

## User Model

The `User` table stores the user's personal information.

| Column        | Data Type        | Description                           |
|---------------|------------------|---------------------------------------|
| `id`          | Integer (PK)     | Primary Key, Auto-Incremented         |
| `email`       | String(120)       | User's email address, unique          |
| `password`    | String(200)       | User's hashed password                |
| `name`        | String(120)       | User's full name                      |
| `dob`         | Date             | User's date of birth (optional)       |
| `monthly_income` | Float         | User's monthly income (optional)      |
| `role`        | String(50)        | User's role (default: 'user')         |

**Indexes:**
- `idx_user_email`: Index on the `email` field for faster queries.

---

## Goal Model

The `Goal` table tracks the financial goals of users.

| Column         | Data Type        | Description                           |
|----------------|------------------|---------------------------------------|
| `id`           | Integer (PK)     | Primary Key, Auto-Incremented         |
| `user_id`      | Integer (FK)     | Foreign Key referencing `User.id`    |
| `title`        | String(120)       | Title of the goal                    |
| `target_amount`| Float            | Amount the user wants to save         |
| `current_savings` | Float         | Current amount saved towards the goal|
| `target_date`  | Date             | Date by which the goal should be achieved |
| `created_at`   | DateTime         | Timestamp when the goal was created  |

**Relationships:**
- **User**: Each goal belongs to a user.
- **Cascade delete**: Deleting a user will automatically delete all associated goals.

---

## Portfolio Model

The `Portfolio` table represents a collection of assets owned by a user.

| Column       | Data Type        | Description                           |
|--------------|------------------|---------------------------------------|
| `id`         | Integer (PK)     | Primary Key, Auto-Incremented         |
| `user_id`    | Integer (FK)     | Foreign Key referencing `User.id`    |
| `name`       | String(120)       | Name of the portfolio (e.g., "Retirement Fund") |

**Relationships:**
- **User**: Each portfolio belongs to a user.

---

## Asset Model

The `Asset` table represents an individual asset within a portfolio.

| Column           | Data Type        | Description                           |
|------------------|------------------|---------------------------------------|
| `id`             | Integer (PK)     | Primary Key, Auto-Incremented         |
| `portfolio_id`   | Integer (FK)     | Foreign Key referencing `Portfolio.id` |
| `name`           | String(120)       | Name of the asset (e.g., "Tesla Stock") |
| `type`           | String(50)        | Type of the asset (e.g., "Stock", "Crypto") |
| `amount_invested`| Float            | Amount invested in the asset          |
| `purchase_date`  | Date             | Date when the asset was purchased     |

**Relationships:**
- **Portfolio**: Each asset belongs to a portfolio.

---

## PriceHistory Model

The `PriceHistory` table stores the historical prices of assets.

| Column         | Data Type        | Description                           |
|----------------|------------------|---------------------------------------|
| `id`           | Integer (PK)     | Primary Key, Auto-Incremented         |
| `asset_id`     | Integer (FK)     | Foreign Key referencing `Asset.id`   |
| `date`         | Date             | Date of the price record              |
| `price`        | Float            | Price of the asset on the given date  |

**Relationships:**
- **Asset**: Each price history record belongs to an asset.

---

## Entity Relationships

1. **User ↔ Goal**:
   - One-to-many relationship: A user can have multiple goals.
   - Cascade delete: Deleting a user deletes all related goals.

2. **User ↔ Portfolio**:
   - One-to-many relationship: A user can have multiple portfolios.

3. **Portfolio ↔ Asset**:
   - One-to-many relationship: A portfolio can have multiple assets.

4. **Asset ↔ PriceHistory**:
   - One-to-many relationship: An asset can have multiple price history records.

---

## ER Diagram

The following is a representation of the relationships in the database schema:

![ER](https://imgur.com/pT5rUET.png)




##  API DOCUMENTATION

https://api.example.com/apidocs

  use /apidocs


##  DEPLOYED LINK
