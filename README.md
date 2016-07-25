Service In AngularJS
====================

This repository is for exploring Service Providers in AngularJS.

When we are working on **MVC** (or **MVVM** for **AngularJS**) **Design-Patterns**, our application is loosely coupled because of  different independent components defined for e.g. **Controller**, **View**, **Services**, **Modal/Data** etc. All the components have their own work/role but today we will discuss only **Services**.

**Services** are that part of application where we write our business logic and load data (if it is frond-end framework Service e.g. **AngularJS** **Service** then it loads data from Web Server and if it is back-end framework Service e.g. **NodeJS** **Service** then it loads data from Database Server or other Web Server). **AngularJS** also provides many built-in **services** e.g. **$http**, **$q** etc. **$http** is very commonly used **service** which helps us to load data from Web Server, we can hit Ajax request with the help of **$http** **service**, which internally hits **XMLHTTPRequest**.

Generally, instead of writing **Services**  we do data loading from Web-Server in **Controllers**, which is obviously a bad practice. So lets try a basic program, where we will load data from Web-Server with the help of **Service** instead of writing the code into **Controller**.

```JavaScript
var serviceTestApp = angular.module('serviceTest', []);

/*
 * Defining TestService, Which will load User list Asynchronously(From Web-Server).
 * for demo purpose we are using setTimeout().
 *
 * $q is built-in Angular Service which helps us to implement Promise-Defer Design Pattern and
 * will be injected to TestService by AngularJS via DI(Dependency Injection) Design Pattern.
 * */
serviceTestApp.service('TestService', function ($q) {
    // Defining Service function: getUsers which will load user list
    this.getUsers = function () {
        var deferred = $q.defer();
        setTimeout(function () {
            var users = [
                {name: "Amit Thakkar", age: 25},
                {name: "Namita", age: 36},
                {name: "Kanika", age: 43}
            ];
            deferred.resolve(users);
        }, 2000);
        return deferred.promise;
    };
});
```

Also, **Services** must be registered with **module**(Same as **[directives](http://codechutney.in/blog/angularjs/component-in-angularjs/)**) via **module.service** API, in which first argument is the name of the **Service** and second argument is the function. Second argument function is just a constructor function that will be called with **'new'** keyword by **AngularJS** itself. And this **Service** will be injected to **Controllers** or other **Services** (**AngularJS** also implement **Dependency Injection** Design Pattern to inject **services** to **Controllers** and **Services**).

```JavaScript
/*
 * Defining TestController, who will use TestService to get User List.
 * */
function TestController($scope, TestService) {
    // Calling getUsers function on TestService.
    TestService.getUsers().
        then(function (users) {
            $scope.users = users;
        });
}
```

**AngularJS** **Services** implement **Singleton Design Pattern** so only one object is created for an application.

Follow Me
---
[Github](https://github.com/AmitThakkar)

[Twitter](https://twitter.com/amit_thakkar01)

[LinkedIn](https://in.linkedin.com/in/amitthakkar01)

[More Blogs By Me](http://amitthakkar.github.io/)
