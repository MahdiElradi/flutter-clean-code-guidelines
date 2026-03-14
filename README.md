# Flutter Architecture & Clean Code Guide

A guide for building scalable Flutter applications using best practices.

---

# 1. Architecture

The project follows **Clean Architecture**.

Layers:

Presentation → Domain → Data

Responsibilities:

Presentation

* UI
* Widgets
* Bloc / Cubit

Domain

* Entities
* Use cases
* Repository contracts

Data

* API calls
* Models
* Repository implementations
* Local storage

Never allow dependencies from Domain → Presentation.

---

# 2. Folder Structure

lib/

core/
features/

Example:

lib/
core/
constants/
errors/
network/
utils/

features/
auth/
data/
domain/
presentation/

---

# 3. OOP Principles

Follow Object-Oriented Programming principles:

Encapsulation
Abstraction
Inheritance
Polymorphism

Classes should hide implementation details and expose only necessary interfaces.

---

# 4. SOLID Principles

S — Single Responsibility
Each class should have one responsibility.

O — Open / Closed
Classes should be open for extension but closed for modification.

L — Liskov Substitution
Child classes must be usable instead of parent classes.

I — Interface Segregation
Prefer multiple small interfaces.

D — Dependency Inversion
Depend on abstractions not implementations.

Example:

abstract class UserRepository {
Future<User> getUser();
}

---

# 5. State Management

Use **Bloc / Cubit**.

Rules:

• No business logic inside widgets
• UI must remain passive
• State changes handled by Cubit/Bloc

Flow:

UI → Cubit → UseCase → Repository → DataSource → API

---

# 6. Dependency Injection

Use dependency injection.

Recommended tools:

get_it
injectable

Rules:

• No manual dependency creation inside UI
• Register all services in DI container

---

# 7. Networking

All API calls must be handled in the **data layer**.

Recommended library:

Dio

Rules:

• Use interceptors
• Handle HTTP errors properly
• Convert responses to models

---

# 8. Error Handling

Use custom exceptions.

Examples:

ServerException
NetworkException
UnauthorizedException
NotFoundException

Convert exceptions to Failures in repository layer.

---

# 9. Pagination Pattern

Use pagination for large datasets.

Rules:

• Avoid loading large lists at once
• Use page-based API requests
• Append data instead of replacing it

---

# 10. Repository Caching

Implement caching where possible.

Examples:

Local database
Memory cache

Benefits:

• Faster UI
• Reduced API calls

---

# 11. API Versioning

Support versioning for APIs.

Example:

/api/v1/users
/api/v2/users

Never break older versions without migration strategy.

---

# 12. Performance Optimization

Best practices:

• Use const widgets
• Avoid unnecessary rebuilds
• Use ListView.builder
• Use pagination for large lists

Avoid heavy logic inside build().

---

# 13. Testing

Testing types:

Unit tests
Bloc tests
Widget tests

Rules:

• Mock repositories
• Avoid real API calls in tests

---

# 14. Git Workflow

Branch naming:

feature/login
feature/profile
bugfix/payment
refactor/home

Commit style:

feat: add login feature
fix: resolve crash in profile
refactor: improve cubit logic

---

# 15. Security

Never store sensitive information in source code.

Use:

.env files
Secure storage

Sensitive data includes:

API keys
tokens
credentials

---

# 16. Code Quality

Before merging:

• Code compiles successfully
• No unused imports
• No debug prints
• Follow architecture rules

---

# 17. Documentation

All complex logic must include documentation comments.

Example:

/// Handles user authentication
/// Returns User entity if login succeeds

---

# 18. Reusable Components

Reusable UI must be placed inside:

core/widgets/

Examples:

Custom buttons
Text fields
Dialogs

---

# 19. Logging

Use structured logging.

Recommended:

logger package

Avoid logging sensitive data.

---

# 20. General Rules

Do not:

• Mix architecture layers
• Duplicate code
• Hardcode strings
• Hardcode colors

Always:

• Follow architecture
• Keep code readable
• Write maintainable code
