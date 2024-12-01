## Main idea

**DAO (Data Access Object)** is a structural pattern that provides an API to access data from a specific data source (like a database) without revealing details of the data’s underlying structure or storage.
* _DAO allows you to separate data access logic from business logic, making your codebase_ **_cleaner, modular, and easier to test_**_._
* By using this pattern we sort of convert the database data into object so that we can use it in our programs and then convert the objects back to database. There are frameworks available which helps us to achieve this like Hibernate which is the most popular one.

## Benefits

_DAO makes your code more flexible and maintainable, especially in projects with frequent changes or large codebases._

**Separation of Concerns (SoC)** 🔄

- It separates the data layer from the business layer, making code more modular and easier to maintain.

**Maintainability and Flexibility** 🛠️

- Since database interactions are abstracted, it becomes easier to modify and maintain the code when switching databases.

**Improved Testability** 🧪

- DAO provides an interface that can be mocked or stubbed for unit testing, allowing developers to test business logic independently of data logic.


Sources

1.  https://medium.com/@devcorner/dao-design-pattern-the-complete-guide-f8246f227091
