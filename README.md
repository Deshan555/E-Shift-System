# Statement of Work (SOW) for e-Shift Household Goods Shifting System

## 1. Project Overview
e-Shift, a household goods shifting company, requires an automated system to manage daily operational activities, including customer management, transport job operations, and administrative tasks. This Statement of Work outlines the development of a web-based application using Laravel, HTML, CSS, JSON, MySQL, and additional libraries to meet the business requirements specified in the CS6004ES coursework. The system will include role-based permission management, a user-friendly interface, and robust programming practices to ensure scalability, maintainability, and efficiency.

## 2. Objectives
- Develop a web-based application to automate e-Shift's operational activities.
- Implement role-based permission management for admin and customer roles.
- Provide a user-friendly interface with intuitive navigation and responsive design.
- Use MySQL for persistent data storage and JSON for data interchange.
- Incorporate good programming practices, including clear code structure, sensible naming, and comprehensive error handling.
- Support management decision-making with reporting features and dashboards.

## 3. Scope of Work
The system will include the following features, aligned with the CS6004ES coursework requirements:

### 3.1 Functional Requirements
1. **Customer Management**:
   - Register and manage customer details (e.g., name, contact, address, unique customer ID).
   - Allow customers to log in and view their transport job history and status.
2. **Transport Job Management**:
   - Create and manage transport jobs, including pickup and delivery locations, and assign a unique job ID.
   - Track job details, including associated lorry, driver, assistant, and container.
3. **Admin Management**:
   - Allow only admins to manage admin details and product details.
   - Implement admin login with secure authentication.
   - Provide admin dashboard with comprehensive job and customer insights.
4. **Role-Based Permission Management**:
   - Restrict actions based on user roles (Admin vs. Customer).
   - Only admins can accept/decline transport jobs, manage products, and generate reports.
5. **Reporting**:
   - Generate reports (e.g., job summaries, customer activity) accessible only to admins.
6. **Customer Dashboard**:
   - Display job status, history, and profile details for customers.
7. **Data Validation and Exception Handling**:
   - Ensure robust input validation and error handling to prevent system crashes and data corruption.

### 3.2 Technical Requirements
- **Framework**: Laravel (PHP) for backend development, leveraging MVC architecture.
- **Frontend**: HTML, CSS (with Tailwind CSS for responsive design), and JavaScript for interactivity.
- **Database**: MySQL for relational data storage.
- **Data Interchange**: JSON for API responses and data exchange.
- **Libraries**:
  - Laravel Breeze for authentication and role-based access control.
  - Tailwind CSS for styling and responsive design.
  - DataTables.js for interactive tables in dashboards.
  - Laravel Eloquent ORM for database interactions.
- **Search Algorithms**:
  - Implement basic search functionality using MySQL queries for filtering customers and jobs.
  - Optional: Use Laravel Scout with Algolia for advanced search (if performance optimization is needed).
- **Security**:
  - Implement CSRF protection, input sanitization, and secure password hashing (via Laravel's built-in features).
  - Use Laravel's middleware for role-based access control.
- **User Interface**:
  - Responsive design compatible with desktop and mobile devices.
  - Intuitive navigation with clear menus and dashboards.
  - Accessible design adhering to WCAG 2.1 guidelines.

## 4. System Architecture
The system will follow a modular architecture to ensure maintainability and scalability:

- **Frontend**:
  - HTML/CSS/JavaScript for rendering views.
  - Tailwind CSS for styling, ensuring responsive and modern UI.
  - Blade templates for dynamic content rendering.
- **Backend**:
  - Laravel controllers to handle business logic.
  - Eloquent models for Customer, Job, Admin, Product, and TransportUnit entities.
  - Middleware for role-based permissions (e.g., `admin-only`, `customer-only`).
- **Database**:
  - MySQL tables: `customers`, `jobs`, `admins`, `products`, `transport_units`, `users` (for authentication).
  - Relationships: One-to-Many (Customer to Jobs), Many-to-One (Jobs to TransportUnit).
- **APIs**:
  - RESTful APIs for fetching job/customer data and generating reports.
  - JSON responses for frontend-backend communication.

### 4.1 Class Structure
- **Customer**:
  - Properties: `customer_id`, `name`, `email`, `phone`, `address`.
  - Methods: `create()`, `update()`, `getJobs()`.
- **Job**:
  - Properties: `job_id`, `customer_id`, `pickup_location`, `delivery_location`, `status`, `transport_unit_id`.
  - Methods: `create()`, `updateStatus()`, `assignTransportUnit()`.
- **Admin**:
  - Properties: `admin_id`, `name`, `email`.
  - Methods: `manageAdmins()`, `generateReports()`, `manageProducts()`.
- **TransportUnit**:
  - Properties: `unit_id`, `lorry_details`, `driver_details`, `assistant_details`, `container_details`.
  - Methods: `assignToJob()`, `getStatus()`.
- **Product**:
  - Properties: `product_id`, `name`, `description`, `weight`.
  - Methods: `create()`, `update()`, `delete()`.

## 5. Development Approach
- **Methodology**: Agile with iterative development and testing.
- **Tools**:
  - Visual Studio Code for coding.
  - MySQL Workbench for database design.
  - Git for version control.
- **Testing**:
  - Unit tests for backend logic using PHPUnit.
  - Integration tests for API endpoints.
  - Manual testing for UI usability.
- **Seeding**:
  - Use Laravel seeders to populate the database with sample data:
    - 10 customers with dummy details.
    - 20 transport jobs with varying statuses.
    - 5 admins with predefined roles.
    - 50 products with random weights and descriptions.
    - 10 transport units with mock lorry/driver details.

## 6. Deliverables
1. **Software Artifact**:
   - Laravel project with source code, compiled assets, and executable application.
   - MySQL database schema and seed scripts.
   - Configuration files for Laravel environment.
2. **Documentation**:
   - Detailed instructions to run the application (e.g., `php artisan serve`, database setup).
   - Software architecture diagram and class descriptions.
   - Reflective essay (1000+ words) covering:
     - Installation and execution instructions.
     - Architecture and class details.
     - Experience using Laravel and Visual Studio Code, including challenges (e.g., debugging middleware) and solutions (e.g., using Laravel logs).
3. **Database Schema** (example):
   ```sql
   CREATE TABLE users (
       id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
       email VARCHAR(255) UNIQUE,
       password VARCHAR(255),
       role ENUM('admin', 'customer') DEFAULT 'customer',
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );

   CREATE TABLE customers (
       customer_id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
       user_id BIGINT UNSIGNED,
       name VARCHAR(255),
       phone VARCHAR(20),
       address TEXT,
       FOREIGN KEY (user_id) REFERENCES users(id)
   );

   CREATE TABLE jobs (
       job_id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
       customer_id BIGINT UNSIGNED,
       pickup_location TEXT,
       delivery_location TEXT,
       status ENUM('pending', 'accepted', 'declined', 'completed') DEFAULT 'pending',
       transport_unit_id BIGINT UNSIGNED,
       FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
   );
   ```

## 7. Implementation Plan
- **Phase 1: Setup and Design (1 week)**:
  - Set up Laravel project with Breeze and Tailwind CSS.
  - Design MySQL schema and create seeders.
- **Phase 2: Backend Development (2 weeks)**:
  - Implement Eloquent models, controllers, and middleware.
  - Develop RESTful APIs for job/customer management.
- **Phase 3: Frontend Development (2 weeks)**:
  - Create Blade templates for dashboards and forms.
  - Integrate Tailwind CSS and DataTables.js for UI.
- **Phase 4: Testing and Documentation (1 week)**:
  - Write unit and integration tests.
  - Document architecture, classes, and setup instructions.
- **Phase 5: Final Submission (1 week)**:
  - Package project with source code and executable.
  - Finalize reflective essay.

## 8. Programming Standards
- **Code Clarity**: Use meaningful variable/class names (e.g., `CustomerController`, `createJob`).
- **Comments**: Include docblocks for classes/methods and inline comments for complex logic.
- **Error Handling**: Use try-catch blocks and Laravel's validation rules.
- **Search Algorithm**: Use MySQL `LIKE` queries for basic search; consider Laravel Scout for scalability.
- **UI Design**: Follow Tailwind CSS conventions for consistent styling.

## 9. Assumptions
- The system will be hosted locally for development (e.g., via `php artisan serve`).
- Users have basic knowledge of running Laravel applications.
- MySQL is installed and configured on the development machine.

## 10. Risks and Mitigation
- **Risk**: Complex role-based permissions may lead to bugs.
  - **Mitigation**: Use Laravel's Gate and middleware for robust access control.
- **Risk**: UI may not be responsive across all devices.
  - **Mitigation**: Test with Tailwind CSS responsive classes and browser dev tools.
- **Risk**: Database performance issues with large datasets.
  - **Mitigation**: Optimize queries with indexing and consider Laravel Scout for search.

## 11. Acceptance Criteria
- The application meets all functional requirements (customer/job management, role-based access, dashboards).
- The UI is responsive, intuitive, and adheres to WCAG 2.1.
- The code is well-documented, follows naming conventions, and includes error handling.
- The system runs without errors on a standard Laravel setup.
- The reflective essay addresses all required points (instructions, architecture, experience).

## 12. Conclusion
This SOW outlines the development of a robust, user-friendly system for e-Shift using Laravel, MySQL, and modern web technologies. The project will adhere to the CS6004ES coursework requirements, delivering a functional application and comprehensive documentation to support operational efficiency and management decision-making.
