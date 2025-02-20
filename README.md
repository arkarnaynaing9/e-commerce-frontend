# E-Commerce Frontend

This is the frontend part of the e-commerce platform built using Vue.js. It interacts with the Laravel backend API to provide users with a seamless shopping experience, including product viewing, cart management, order placement, and user authentication (register/login). It also includes an admin dashboard for managing products, orders, and users.

## Features

- **Authentication**: User registration, login, and logout functionalities.
- **Home View**: Displays the list of products available for purchase.
- **Cart View**: Allows users to view and manage items in their shopping cart.
- **Checkout View**: Lets users place an order and complete the purchase.
- **Admin Dashboard**: Admins can manage products, orders, and users.
- **Responsive Layout**: Designed with Tailwind CSS for a modern, responsive user interface.

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/yourusername/ecommerce-frontend.git
    cd ecommerce-frontend
    ```

2. Install dependencies:

    ```bash
    npm install
    ```

3. Create an `.env` file for environment variables:

    ```bash
    cp .env.example .env
    ```

    Update the `.env` file with your API URL (Laravel backend).

    ```env
    VUE_APP_API_URL=http://localhost:8000/api
    ```

4. Run the development server:

    ```bash
    npm run serve
    ```

    Your frontend should now be accessible at `http://localhost:8080`.

## Directory Structure

- **src/components**: Contains the reusable Vue components such as headers, footers, and product cards.
- **src/views**: Contains the different views for each page (e.g., `HomeView`, `CartView`, `CheckoutView`, etc.).
- **src/router**: Handles routing between different views (e.g., Home, Login, Admin).
- **src/store**: Contains the Vuex store for managing global state (e.g., user authentication, cart items).

## Vue Components & Views

### 1. **AdminView.vue**

- **Path**: `src/views/AdminView.vue`
- **Description**: The admin dashboard for managing products, orders, and users. Accessible only by users with the `admin` role.
- **Features**:
  - Manage products (CRUD operations).
  - View and manage orders.
  - View and manage users.

### 2. **AppLayout.vue**

- **Path**: `src/layouts/AppLayout.vue`
- **Description**: The main layout wrapper for the application. It contains the header, sidebar (for admins), and footer. Used across all views.
- **Features**:
  - Header with navigation.
  - Sidebar with admin-specific navigation links.
  - Footer with copyright and contact information.

### 3. **CartView.vue**

- **Path**: `src/views/CartView.vue`
- **Description**: Displays the user's shopping cart. Users can add/remove products, and proceed to checkout.
- **Features**:
  - List of products added to the cart.
  - Total price calculation.
  - Button to proceed to checkout.

### 4. **CheckoutView.vue**

- **Path**: `src/views/CheckoutView.vue`
- **Description**: Allows users to review their order and enter shipping and payment information to complete the purchase.
- **Features**:
  - Form for entering user details (e.g., shipping address, payment method).
  - Display cart summary and total price.
  - Confirmation button to place the order.

### 5. **HomeView.vue**

- **Path**: `src/views/HomeView.vue`
- **Description**: Displays a list of available products. Users can browse and view individual product details.
- **Features**:
  - List of products retrieved from the backend API.
  - Option to add products to the cart.

### 6. **LoginView.vue**

- **Path**: `src/views/LoginView.vue`
- **Description**: Provides a login form for users to authenticate.
- **Features**:
  - Fields for email and password.
  - Button to log in the user and store the authentication token.

### 7. **RegisterView.vue**

- **Path**: `src/views/RegisterView.vue`
- **Description**: A registration form for new users to sign up.
- **Features**:
  - Fields for user details (name, email, password, etc.).
  - Button to register and authenticate the user.

## Vuex Store

The store manages global application state, including:

- **User Authentication**: Stores the logged-in user's data and the authentication token.
- **Cart State**: Stores the list of products in the user's cart.
- **Product Data**: Stores the list of products retrieved from the API.

Example of the Vuex store structure for the cart:

```javascript
// src/store/modules/cart.js
export default {
  state: {
    items: [],
  },
  mutations: {
    addToCart(state, product) {
      state.items.push(product);
    },
    removeFromCart(state, productId) {
      state.items = state.items.filter(item => item.id !== productId);
    },
    clearCart(state) {
      state.items = [];
    },
  },
  actions: {
    addProductToCart({ commit }, product) {
      commit('addToCart', product);
    },
    removeProductFromCart({ commit }, productId) {
      commit('removeFromCart', productId);
    },
    clearUserCart({ commit }) {
      commit('clearCart');
    },
  },
};
