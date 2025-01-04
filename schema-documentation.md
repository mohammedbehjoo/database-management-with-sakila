# Sakila Database Schema Documentation

## Tables and Relationships

### 1. `actor`
- **Description**: Stores information about actors.
- **Primary Key**: `actor_id`
- **Relationships**:
  - Many-to-many with `film` via `film_actor`.

### 2. `film`
- **Description**: Stores information about films.
- **Primary Key**: `film_id`
- **Relationships**:
  - Many-to-many with `actor` via `film_actor`.
  - Many-to-many with `category` via `film_category`.
  - One-to-many with `inventory`.

### 3. `film_actor`
- **Description**: Links `actor` and `film` in a many-to-many relationship.
- **Primary Key**: (`actor_id`, `film_id`)
- **Foreign Keys**:
  - `actor_id` references `actor(actor_id)`.
  - `film_id` references `film(film_id)`.

### 4. `category`
- **Description**: Stores film categories (e.g., Action, Comedy).
- **Primary Key**: `category_id`
- **Relationships**:
  - Many-to-many with `film` via `film_category`.

### 5. `film_category`
- **Description**: Links `film` and `category` in a many-to-many relationship.
- **Primary Key**: (`film_id`, `category_id`)
- **Foreign Keys**:
  - `film_id` references `film(film_id)`.
  - `category_id` references `category(category_id)`.

### 6. `inventory`
- **Description**: Stores inventory information for each film.
- **Primary Key**: `inventory_id`
- **Foreign Keys**:
  - `film_id` references `film(film_id)`.
  - `store_id` references `store(store_id)`.
- **Relationships**:
  - One-to-many with `rental`.

### 7. `rental`
- **Description**: Stores rental transactions.
- **Primary Key**: `rental_id`
- **Foreign Keys**:
  - `inventory_id` references `inventory(inventory_id)`.
  - `customer_id` references `customer(customer_id)`.
  - `staff_id` references `staff(staff_id)`.

### 8. `customer`
- **Description**: Stores customer information.
- **Primary Key**: `customer_id`
- **Foreign Keys**:
  - `address_id` references `address(address_id)`.
  - `store_id` references `store(store_id)`.
- **Relationships**:
  - One-to-many with `rental`.
  - One-to-many with `payment`.

### 9. `payment`
- **Description**: Stores payment details for rentals.
- **Primary Key**: `payment_id`
- **Foreign Keys**:
  - `customer_id` references `customer(customer_id)`.
  - `staff_id` references `staff(staff_id)`.
  - `rental_id` references `rental(rental_id)`.

### 10. `staff`
- **Description**: Stores staff information.
- **Primary Key**: `staff_id`
- **Foreign Keys**:
  - `address_id` references `address(address_id)`.
  - `store_id` references `store(store_id)`.
- **Relationships**:
  - One-to-many with `rental`.
  - One-to-many with `payment`.

### 11. `store`
- **Description**: Stores information about rental stores.
- **Primary Key**: `store_id`
- **Foreign Keys**:
  - `manager_staff_id` references `staff(staff_id)`.
  - `address_id` references `address(address_id)`.
- **Relationships**:
  - One-to-many with `customer`.
  - One-to-many with `staff`.

### 12. `address`
- **Description**: Stores address details.
- **Primary Key**: `address_id`
- **Foreign Keys**:
  - `city_id` references `city(city_id)`.
- **Relationships**:
  - One-to-many with `customer`.
  - One-to-many with `staff`.
  - One-to-many with `store`.

### 13. `city`
- **Description**: Stores city details.
- **Primary Key**: `city_id`
- **Foreign Keys**:
  - `country_id` references `country(country_id)`.
- **Relationships**:
  - One-to-many with `address`.

### 14. `country`
- **Description**: Stores country details.
- **Primary Key**: `country_id`
- **Relationships**:
  - One-to-many with `city`.