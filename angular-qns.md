# Angular Interview Questions
1. What is Angular?
- Angular is a javascript framework for building scalable single-page web applications. It is typescrip based.
- It includes features such as components, directives, dependency injection, etc. making it easier to build large-scale apps.

2. What is typescript?
- It is a strongly typed superset of javascript. It compiles to plain js. 
- It has a lot of helpful warning and errors that it indicates us and enable us to write better code.

3. What are Single Page Applications?
- It is a web app that loads content dynamically without having to refresh the whole page. 
- It makes our application faster, more responsive and a good user experience.
- Some examples are gmail, outlook, instagram, etc. - many modern applications.

4. package.json vs package-lock.json?
- package.json is the main configuration file with list of dependencies and script.
- It lists the package and the versions used.
- package-lock.json provides a snapshot of all dependencies and sub-dependencies.
- Used for consistent setup across all systems.
- main.ts -> entry point of every angular application. It bootstraps(starts) the application.

5. What is the app-root selector?
- It is a placeholder used in Angular to define the root component of the angular app. Angular replaces app-root with the content of AppComponent.

6. What are components in angular?
- Components are the basic building blocks of our angular application.
- three main parts - class file, the template, the styles.
- @component decorator is used to define these.

7. What are modules in angular?
- It is a container that groups all the related components, directives, pipes into one cohesive block. 
- Declared using the @NgModule decorator.
- Now due to standalone apps as default, they are no longer widely used.

8. What are directives in angular?
- Directives are classes with additional behavior to the elements in the templates.
- Three main directives - Components, structural directives and attribute directives.
- Component directive - They are directives with template and view. They encapsulate UI logic. 

9. What is a component? Three main parts?
- It is a fundamental block of the application. 
- It is a ts class with @Component decorator. 
- Three main parts - template(view), styles, class file.
- ng g c component-name to create it in cli

10. Component vs Directive - what's the difference?
- Component is a directive with a view. It creates a UI building block along with modifying the behaviors.
- Directives modify the appearance,behavior of existing elements. 
- Multiple directives can be applied to a component.

11. Lifecycle hooks - list all and their execution order
- Lifecycle hooks are set of interfaces that allows us to tap into the execution of component - from initialization to destruction.
- It is very useful and gives control over the initialization, change detection, memory management.
- Change detection cycle - Mechanism by which the view is kept in sync with the component class.
- Angular knows every change as it runs change detection cycle on the DOM looking for changes. Whenever @Input properties changes, whenever DOM events(click) occurs, whenever timer properties (setTimeout, setTimeInverval) occurs, http request is made.
- Execution order and list of lifecycle hooks:
  - ngOnChanges: It is a lifecycle hook that is executed at the start whenever a component is initialized and an input bound property changes. 
  - ngOnInit: It is a commonly used lifecycle hook that is called right after the ngOnChanges is done (after the input properties changes are updated). It is fired only once. By this time, none of the child components projected contents, views will be updated. Perfect place to add initialization logic as it will be called only once.
  - ngDoCheck: This lifecycle hook runs on every change detection cycle, even if no input properties are changed. It runs after ngOnChanges and ngOnInit. It is a good place to have logic that should be run on every change detection cycle or user interaction as it will always run.
  - ngAfterContentInit: This lifecycle hook is called only after the projected content is fully initialized and rendered in View. Content projection is where when parent component has the child selector called and specifies additional lines(contents) within it, and the child component has a placeholder to recieve that (<ng-content>). Similar to ngOnInit, this is only called during the first change detection cycle after content is projected.
  - ngAfterContentChecked: This lifecycle hook is called during every change detection cycle after the projection content has been initialized and checked. This runs multiple times (whenever change detection cycle runs).
  - ngAfterViewInit: This lifecycle hook is called after all the component's view and all the child's view has been fully initialized. Angular also updates properties with @ViewChild and @ViewChildren decorator before raising this hook. It is only called during the first change detection cycle.
  - ngAfterViewChecked: This hook is called after angular checks and updates all the components view and child's view. It is called during successive change detection cycles.
  - ngOnDestroy: Angular fires this lifecycle hook just before the component is destroyed/removed from the DOM. Great place to clean up resources, unsubscribe to observables, detach event handler, etc. 

12. Constructor vs ngOnInit - when to use what?
- Constructor is not an angular feature, it is a part of js and many prog languages. It is the first thing that runs when the class is instantiated.
- NgOnInit is a lifecycle hook that runs after the first ngOnChanges. It runs only once, so it is ideal for initialization logic such as fetching api data, setting up initial values, handling complex logic that requires UI elements to be ready.

13. ngOnChanges - when does it fire and what parameter does it receive?
- ngOnChanges is called when there is a change in the input bound properties. It recieves a SimpleChanges argument, which has the previousValue, currentValue, firstChange boolean value.

14. ngAfterViewInit vs ngAfterContentInit - difference?
- The ngAfterContentInit fires after external content is projected in the component's view via <ng-content>. It is called once after the first ngDoCheck. It handles content that comes from external component.
- The ngAfterViewInit is called after ngAfterContentChecked when the template's view and all of its child components are fully initialized. It is called once. It handles the component's own html and it's child components.

15. Can you access @ViewChild in ngOnInit? When can you access it?
- No, we cannot access the @ViewChild in ngOnInit as the ngOnInit fires when the component's input bound properties are ready but not the template. We can access it in ngAfterViewInit where all the child components are fully initialized.

16. What is ngOnDestroy used for? Give practical examples.
- It is the last lifecycle hook that is called when the component is to be removed/destroyed from the DOM. 
- Useful to unsubscribe to observables, remove listening to event listeners, clearing timeouts, timeintervals, etc.

17. What is ngDoCheck? When would you use it?
- It is a lifecycle hook that is executed after ngOnInit. (3rd lifecycle hook).
- Useful to write any custom change detection logic as this runs during every change detection cycle whether any input properties have changed or not.

18. What are the content projection lifecycle hooks?
- There are two main lifecycle hooks - ngAfterContentInit and ngAfterContentChecked.
- ngAfterContentInit is invoked after ngDoCheck when there is an external content projected in the component. It runs only once.
- Earliest place to use @ContentChild/@ContentChildren.
- ngAfterContentChecked is invoked whenever there is changes in projected content. Checked hooks fires very frequently and if not properly used, can cause performance issues.

19. What are the types of data binding in Angular?
- Angular mainly supports two types of data binding - one-way and two-way data binding.
- One-way -> from view to component or component to view.
- View to component -> Event binding.
- Component to view -> attribute binding, property binding, interpolation
- Two-way data binding -> Data flows both ways. NgModel directive is used to achieve this.

20. Interpolation vs Property Binding - when to use which?
- Interpolation is used to render the text or strings in the HTML template. They are given inside curly braces and angular converts these expressions into strings and renders it in view. Best use case is to display dynamic data.
- Property binding is used to set the property of HTML element or a component's @Input. It directly communicates with the DOM object. Used in href, disabled, src, value. Also commonly used to pass data from parent to child. It is done with property binding.

21. Event Binding - how does it work? Can you pass $event?
- Event binding is a one-way data binding method that data flows from view to the component. (event)
- (click), (submit), (keyup), etc are commonly used.
- The $event argument can be passed. It is a special variable used in angular events that have important values that can be accessed with target.value.

22. Two-way binding - how does [(ngModel)] work internally?
- So the two-way data binding uses both property binding and event binding syntaxes. So it first uses property binding syntax [] where it flows data from component to view. Next is the () syntax of event binding to make data flow from view to component.

23. What is template reference variable? How to use it?
- A template ref variable is a handler used in specific DOM element within HTML so that it can be easly referenced elsewhere.
- <element #variablename> is the syntax used for it.
- These values can be passed as args inside the click events to get the variable value dynamically.

24. Safe navigation operator (?.) - what problem does it solve?
- Also known as optional chaining, it is commonly used to solve the problem of runtime errors, where if we access a variable with null or undefined values and try accessing it's properties, the error is thrown. This can be avoided with safe navigation operator.

25. What is the difference between [innerHTML] and interpolation?
- Interpolation - Most common way to display data as plain text. Useful for displaying simple dynamic values.
- [innerHTML] - Specific type of property binding that displays text as actual HTML content. Angular also has built-in sanitation to prevent script tags (cross-site scripting). It can be useful to display the dynamic text with formatting.

26. Can you bind to custom events? How?
- Yes, we can bind to custom events using @Output decorator which is useful for passing data from child back to the parent component.
    ```
    // child.component.ts
    @Output itemClicked = new EventEmitter<string>();
    onButtonClicked(){
        this.itemClicked.emit('Clicked the item');
    }
    // parent.component.ts
    <app-child (itemClicked)="handleSelection($event)"/>
    ```

27. What is @Input() and @Output()? How do they enable component communication?
- These are decorators commonly used for communication between the parent and child component.
- @Input is used to pass data from parent to child with the help of property binding and @Output is used to pass data from child to parent with the help of event binding.

28. What is EventEmitter? How does it work?
- EventEmitter is a class used by the @Output decorator to emit events from the child component to the parent.
- It is declared by creating: @Output item = new EventEmitter<datatype>();
- It has the emit method by which it transmits the data to be captured by the parent using the $event variable.

29. Can we use EventEmitter in a Service?
- While we can, it is generally binded with the @Output decorator. To share data with services, we commonly use RxJs Subjects/BehaviorSubject.

30. What are the three types of directives?
- Component directive, structural directives and attribute directives are the three types of directives. 
- Component directive is a directive with view (UI encapsulated). Given with @Component decorator.
- Structural directives are defined with astericks (*ngIf, *ngFor). They are used to modify the DOM elements.
- Attribute directives are those used to modify the appearance of the elements (ngClass, ngStyle). They are used with property binding syntax.
- There are also custom directives that we can use for our specific use as they can be imported in the components that we need them.

31. Structural directives (*ngIf, *ngFor) - how do they work?
- Used to modify the DOM elements, can have loops or specific conditions to render the UI and make the code cleaner and dynamic.
- When we use the structual directives with *, angular is performing syntactic sugar, underneath, these are wrapped in <ng-template>. 
- *ngIf - used for conditional rendering based on truthy/falsy values.
- *ngFor - used to repeat a code for every item in the array/collection.

32. Attribute directives (ngClass, ngStyle) - explain with examples
- These are the directives used to modify the appearance of the elements by adding, removing classes, styles based on the requirements.
- ngClass is used to apply classes based on conditions. If truthy, set this class else this one.
- ngStyle is used similar to inline styles based on conditions.

33. How to create a custom attribute directive?
- First, we can create a directive file with ng generate directive directive-name.
- We can provide the functionality for it. For example, if we want to have highlighting feature, provide the functionality inside the directive.
- To modify underlying html elements, we must inject ElementRef into the constructor. And with HostListener, we can listen to the events such as mouseleave, mouseenter.
- Then, we should import the directive and with the attribute binding syntax, [appHighlight], we can use the custom attribute directive we created.

34. ngFor - what is trackBy and why is it important?
- By default when ngFor is used to render a list, Angular tracks object by their object reference. So even if the data hasn't changed when fetching the list again, it treats it as a new object(list), deletes the existing one in DOM and replaces it. 
- When trackBy is used, we indicate angular to check not only with obj reference, but with the id of the elements if it has really changed. 
- This is really helpful in performance optimization.

35. ngIf with else - how to implement?
- ngIf with else is used for conditional rendering. 
- The statement with if condition is used with *ngIf, the statement with else is assigned with a template ref variable.
- This is used in <ng-template #referenceVariable>else logic</ng-template>

36. ngSwitch - when to use it over ngIf?
- ngSwitch can be used when there are multiple conditions to check and if we want the structure to be optimal. 
- We use *ngSwitchCase for the series of statements and *ngSwitchDefault at the end.

37. What is HostListener and HostBinding in directives?
- HostListener and HostBinding are used in creating custom attribute directives. These are particularly helpful in listening to events such as mouseenter, mouseleave and bind the custom directive to the element.
- HostListener can be used to subscribe to events without having to manually work with DOM.
- HostBinding can be used to dynamically set properties like css styles or classes on the host element.

38. What are pipes? Built-in pipes examples?
- Pipes are used to transform/format data before displaying it in the view. It takes data as input and transforms it before displaying it in the template.
- Some of the common built in pipes are uppercase,lowercase pipes, currency pipes, Json pipes.
- Syntax: {{value | pipename: parameters}}

39. How to create a custom pipe?
- A custom pipe can be defined by creating a typescript class with the @Pipe decorator. The class should implement the PipeTransform interface and we can use the transform method to set up the parameters as per our requirements and call it where we require.

40. Why is a pipe better than calling a function in the template like {{ getFormattedDate(date) }}?
- A function call is triggered during every change detection cycle whereas a pure pipe is only called when the input properties changes. So it is more optimal for performance related purposes to use a pipe when it can be done.

41. Pure vs Impure pipes - what's the difference?
- These are two types of pipes. Pure pipe is the default pipe which is only called when there is change in input properties. Pure change is the change to primitive values like string, number and also change to the object's reference. These results are cached and reused if there is no change in these values.
- Impure pipes are called during every change detection cycle and can be heavy on memory. We set pure: false to make a pipe impure.

42. When would you use an impure pipe?
- When we perform any operations/activity and for example if there is an element pushed to the array, and the array reference does not change, we would need an impure pipe to write any logic based on the change detection cycle. But should be careful about the memory optimization part when using impure pipes.

43. Async pipe - what does it do and why is it useful?
- The async pipe allows us to handle asychronous data. It allows us to subscribe to observable or promise from the view template and return the value emitted.
- It is a built-in impure pipe that makes working with asynchronous data very easy and safe.
- It does three main tasks:
    - Subscribes to an observable or promise as soon as the component loads.
    - Returns latest value emitted by the stream.
    - Unsubscribes automatically when component is destroyed.
- It prevents memory leak, helps write cleaner code.

44. Can you chain multiple pipes? How?
- Yes, it is possible to chain multiple pipes by separating them with the pipe | operator. 
- {{ value | date: mm/yy | uppercase | async}}

45. Parameterized pipes - how to pass parameters?
- We can pass parameters in pipes with the : operator.
- {{ value | pipename: parameters}} - {{ dateVal | date: 'longDate'}}
- It is very useful to create custom pipes.

46. What happens if you don't unsubscribe from an Observable but use async pipe?
- Async pipe automatically unsubscribes once the component is destroyed. It is one of the key features of async pipe as it is useful in preventing memory leaks.

47. How does pipe performance impact your app?
- The performance purely depends on whether we are using a pure or impure pipe. When using a pure pipe, it is far better for performance than impure ones as they run change detection only when input property or object references changes.

48. What is NgModule? What are its main properties?
- NgModule is a class defined by the @NgModule decorator. It bundles all the components, directives, pipes together and tells angular how they interact with other parts of the application.
- Declarations: This contains all the components, directives, pipes listed here in an array.
- Standalone: this is a boolean property which indicates whether the app is standalone or not.
- imports: this array contains all the components on which the component class is dependent on.
- exports: this contains all the components that can be exported to other components.
- providers: this array is to register all services that can be injected within that module.

49. bootstrap property - what is it for?
- The bootstrap property tells angular which component to load first. It is usually AppComponent as it's the first component to be loaded.
- Bootstrapping process - Browser loads the app, angular looks at bootstrap property and finds AppComponent. It then looks for selector of the component in index.html (<app-root>). Angular inserts the component template into the tag.

50. What is a feature module? When to create one?
- A feature module can be created in angular to group specific set of related functionalities together (components related are grouped together). 
- This is preferred when the application size grows and we need to split the NgModule into smaller sub functionalities.
- It is also used as a lazy loading feature by calling the module only when user clicks the related ones.

51. Shared module vs Core module - best practices?
- Core Module is for shared, singleton services and components that should only be instantialized once in the application.
- Shared module is for services, pipes, directives that are to be shared across multiple components. For example, custom button, loader spinners, etc.

52. Lazy loading modules - how does it work?
- Lazy loading is a design pattern in angular that allws to load modules/components only user navigates to a specific route.
- Useful for performance optimization.

53. What is forRoot() and forChild() pattern?
- When there is module with services, we need to ensure that only one instance is registered. We can call the forRoot() to register once in root module.
- forChild() - Configures module for use in lazy-loaded modules or feature modules. Can be used multiple times. 

54. What is preloading strategy?
- These are set of strategies to load all the lazy-loading modules behind the application processes after the initial setup is done. For example, the basic starter modules are loaded and the user is in the home component. Now behind scenes, all the lazy loaded features can be loaded to be ready when the user interacts with it. 
- This is done to give a faster user experience.

55. What is Dependency Injection in Angular?
- DI is a coding pattern in which a class recieves its dependencies from external sources instead of creating them by their own.
- Three parts:
    - The Dependency: The service that needs to be used.
    - The Provider: It tells angular how to create the dependency.(providedIn: root)
    - The Injector: It is responsible for maintaining container of service instances and delivering them to components as they request them.

56. What is an injector and injection token?
- Injector is responsible for maintaining instances and delivering them when needed, injection token is used when the dependency is not a class.
    ```
    import { InjectionToken } from '@angular/core';

    export const API_URL = new InjectionToken<string>('API_URL');
    ```

57. What is providedIn: 'root'?
- It is the easiest and most efficient way to inject dependencies. It follows singleton pattern, instance is defined in the root and can be accessed throughout the application.
- When you provide the service at the root level, Angular creates a single, shared instance of service and injects it into any class that asks for it.

58. Difference between providedIn root vs module vs component level?
- ProvidedIn root - can be used to declare a single instance and can be used throughout the application.
- module and component level as the name suggests can only be used inside those parts of the application.

59. What is @Injectable decorator?
- The @Injectable() decorator is a piece of metadata that tells Angular compiler that a class is a service and is intended to be used with DI system.
- It is useful to provide th scope (root or component or module).

60. What is multi provider?
- They have multiple instances in the provider and is used as an array instead of a single value.
    ```
    providers: [
        { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true },
        { provide: HTTP_INTERCEPTORS, useClass: ErrorInterceptor, multi: true }
    ]
    ```

61. What is hierarchical dependency injection?
- When we use a provider array inside the component, and specify the service to be injected, a new instance is created instead of using the same instance for DI.
- Any changes made here are not reflected in other dependencies.
- Hierarchical injection - When we provide dependency for a class, that same dependency is injected in component class and all its child and grandchild components too.
- When we provide a dependency on a component, and we also provide dependency on the child component, the child dependency will override the parent. This is known as dependency override.

62. How does Angular routing work?
- Angular routing enables navigation by mapping URL paths to components within a Single Page Application. 
- We define these mappings in the routes array and use the router-outlet as a dynamic placeholder for rendering.
    ```
    export const routes: Routes = [
        { path: 'Home', component: HomeComponent}
    ]
    ```
    ```
    // configuring routes in standalone apps
    bootstrapApplication(AppComponent, {
    providers: [
        provideRouter(routes) // This replaces RouterModule.forRoot()
    ]
    });
    // configuring them in module-based approach
    @NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule]
    })
    export class AppRoutingModule { }
    ```

63. What is router-outlet?
- Router outlet (<router-outlet>) is the placeholder used by angular where it sees the path match to the component and renders it in place of the outlet. It tells Angular exactly where to render the component that matches the current URL path.
- Without the router-outlet, Angular would know which component to load based on your routes, but it wouldn't know where to put it on the screen.

64. What is routerLink vs router.navigate()?
- routerLink is used for navigating between different routes from the view, whereas router.navigate() is used inside the component file.
- routerLink - best used for static links, menus, etc.
- router.navigate() - best for dynamic navigation based on logic or any parameters from api call to be added.

65. What are route parameters and query parameters?
- In angular, both route parameters and query parameters allows us to pass data in the url, but route parameter is primarily to identify the route, whereas the query parameters are for filter logics.
- Route parameters syntax: ``` { path: 'transaction/:id', component: DetailComponent } ```
- Query parameters syntax: ``` this.router.navigate(['/transactions'], { queryParams: { sort: 'date' } }); // savify.com/transactions?sort=date&filter=food```

66. What is ActivatedRoute?
- ActivatedRoute is a service in angular that provides us the information on the current route that is hosted.
- It holds info on the: parameters(:id, :name), query parameters(?sort=date), static data in route config.
    ``` constructor(private route: ActivatedRoute) ```
- To access data, there are two ways:
    - snapshot - synchronous way, can be used if user will not change the url params value or navigate to another page.
    - observable - async way.

67. What is a child route?
- A child route in angular is a route that is nested inside another route. It is useful to create hierarchy in the UI where the parent component stays and child routes are swapped in and out. Mainly useful for modular grouping and code reusability.
- To define child routes, the children property is used:
    ```
        const routes: Routes = [
        {
            path: 'reports',
            component: ReportsComponent, // The "Parent"
            children: [
            { path: 'monthly', component: MonthlyReportComponent }, // Child 1
            { path: 'yearly', component: YearlyReportComponent },   // Child 2
            { path: '', redirectTo: 'monthly', pathMatch: 'full' }  // Default child
            ]
        }
        ];
    ```

68. What is a named router outlet?
- There can be more than one router outlets in a program when we want the primary default outlet to render the selected component's view but also have any other components(like sidenav, popups) displayed in the page at the same time.
- We can mention multiple outlets with the name attribute.
    ``` <router-outlet name="sidebar"></router-outlet> ```
- In ts file, we need to mention the outlet there too.
    ```
        const routes: Routes = [
        { path: 'dashboard', component: DashboardComponent }, // Primary
        { 
            path: 'summary', 
            component: MiniSummaryComponent, 
            outlet: 'sidebar' // Targets the named outlet
        }
        ];
    ```

69. What are route guards? Types?
- Angular route guards can be used to control whether the user can navigate to or away from the route based on a given condition.
- Some of the use cases of route guards:
    - To restrict a user from accessing a protected route.
    - To save changes before moving away from view.
    - Validate route parameters before navigating to the route.
- CanActivate/CanActivateChild - Decides if a route can be accessed or not. Can set only the users with access (like logged in users) to access the routes.
- CanDeactivate - we can base this on certain conditions, like whether the user wants to save changes or not and based on that we can deactivate the routes too.
- Resolve - This guard delays the navigation of the route until some tasks are complete. It pre-fetches the data from backend api, before activating the route.
- CanLoad - This route guard prevents the lazy loaded modules from loading.

70. What is CanActivate?
- CanActivate route guard can be used in routes to protect o restrict it from users with unauthorized access.
     ``` { path: 'Courses', Component: CoursesComponent, canActivate: [AuthGuardService]} ```

71. What is CanDeactivate?
- CanDeactivate is the route guard that can be used to allow users to leave a route with any specified conditions.

72. What is lazy loading in routing?
- Lazy loading is an optimization technique that splits the application into smaller bundles. Instead of loading the entire application/modules/components at the initial setup, it loads oly the required portions.

73. What is a wildcard route?
- A wildcard route is the catch-all route that is set to catch any routes that doesn't match the list. It is defined by two **.

74. What is route redirects?
- It tells the user to redirect from one path to another. Usually used as the first route in the list. 
- Defined with the redirectTo property.

75. What is RouterLinkActive?
- It is a built-in angular directive that helps user providing visual feedbacks on the route they're currently in.
    ``` <a routerLink="/dashboard" routerLinkActive="active-link">Dashboard</a> ```

76. How do you pass data to the routes?
- So the common ways to pass data to routes are route parameters, query parameters, state (to pass complex objects to not be shown in url).

77. What is an Observable?
- Observable is a wrapper around asynchronous data. We use it primarily in angular to handle async code.
- It returns a promise after some time, which we can subscribe and make us of the data in it.
- It is a stream of data that can observed over time. It can handle asynchronous data sources like user inputs, network request, timers, etc.
- Creation of observables: Different methods, can be created like a class contructor with the new keyword, with rxjs operators with of keyword.
    ```
    // with new keyword
    const myObservable = new Observable(observer => {
    observer.next(1);
    observer.next(2);
    observer.next(3);
    });
    // with of operator
    const myObservable = of(1,2,3)
    ```

78. Difference between Observable and Promise?
- A promise cannot handle stream of asynchronous data. It always returns a single value. 
- Observables can be used to handle stream of data. It can return multiple values.
- In promise,we would get the data returned even if no one uses that data. In observables, only when a user requests it(subscribes to it), we get the data returned for us to use.
- Observable (Event Emitter) -> Observer(Event Listener/Subscriber) -> Event Handler

79. What is of() and from()?
- The of() operator creates an observable from the arguments we pass onto it. Any number of parameters can be passed.
- It is a RxJS operator. Each argument is sent separately from one another.
- from() operator takes in a single value as parameter (which is an iterable) and that is iterated and their values are streamed one after the other.
- They both return an Observable, but the way they handle data is different.

80. what are map() and tap() operators in RxJS?
- Both are pipeable operators that are used to handle data that flows through an observable stream.
- map() changes/transforms the data, tap() looks into it.
- Use case: map() -> to extract just the username from the api data.
            tap() -> logging, debugging data (console logs)

81. What are operators in RxJS?
- Operators are simply functions that allows us to manipulate, filter, transform data as they are flowing through the stream.
- map(), filter(), of(), from(), tap() are some examples of operators.

82. What is a Subject?
- Subject is a special type of Observable allowing multiple users to use the data. It is similar to EventEmitters where the emitted event can be seen by all the subscribers.
- It is a part of reactive programming where a new value when emitted (with next()) will immediately be updated to the subscribers.

83. Difference between Subject, BehaviorSubject, ReplaySubject, AsyncSubject?
- These are the variants of subject used to control how data is shared and remembered.
- Subject - does not remember previously emitted values. Only the latest value can be read.
- BehaviorSubject - it always requires an initial value. when a value is emitted(latest value), all the subscribers get noticed of that value.
- ReplaySubject - Has more history. Can store some previous values that can be seen.
- AsyncSubject - Only emits the last value it has recieved after the complete() method.

84. What is mergeMap vs switchMap vs concatMap vs exhaustMap?
- These are flattening operators. They are primarily used when an outer observable we have triggers an inner observable and how these are handled.
- mergeMap - allows multiple inner observables to run simultaneously. Can be used to delete multiple items back to back.
- switchMap - when the inner observable changes, it allows for switching to the new one and forgetting the current one.
- concatMap - it queues the new one and waits for current one to complete.
- exhaustMap - when a current observable is there, it ignores new ones.

85. What are forkJoin and combineLatest?
- These are combination Operators. These are used when we have multiple observables and we want to join them into a single stream.
- forkJoin - (Similar to Promise.all()). Waits for all observables to complete and emits their final values as an array.
- If any one fails, whole thing fails.
    ```
        forkJoin({
        income: this.api.getIncome(),
        expenses: this.api.getExpenses()
        }).subscribe(({ income, expenses }) => {
        this.totalSavings = income - expenses;
        });
    ```
- combineLatest - waits for every observable to emit atleast a single value. After that, whenever an observable emits a new value, it emits the latest value from every stream.
    ```
        combineLatest([this.searchTerm$, this.category$, this.dateRange$])
        .subscribe(([term, cat, range]) => {
            this.filterTransactions(term, cat, range);
        });
    ```

86. Retry and retrywith operators.
- These are operators to handle errors and allows us to resubscribe automatically to the source Observable.
- We can pass the number of retries as parameters to the method. (retry(3)).

87. What is a state?
- State refers to the data that the application manages and displays to the user. It is like a snapshot of the current application's data.
- Why do we need state management - Sharing data between components become much easier. Using services/Subjects can become complex in large applications.
- With state manageent, we can have all the data in one place and can read it from anywhere inside our application.

88. What is NgRx?
- It is a reactive state management Library for Angular that provides a structured, predictable and scalable way to manage state (data) of the application.
- Store: Single source of truth for application state. Its a js object that can be accessed throughout the application.
- Actions: These are plain objects that describe unique events that have happened (user clicks, api fetches). This signals an intent to change the state.
- Reducer: The actions are handled by the reducer. It takes the current state and an action, and returns a new immutable state. 
- Selectors: Pure functions that are used to get a specific slice of data from the store. It prevents re-rendering unless the exact data they depend on has changed.
- Effects: These handles events that happen outside of angular like api calls, logging. They listen for a action, performs a task and dispatches the result.
- The state within the store are never directly modified. Only new states are created.
- The store exposes the state as observable, allowing components to subscribe to changes and react accordingly.
- Action is created by: ``` export const increment = createAction('increment') ```
    ``` export const addProduct = createAction('addProduct', props<Product[]>()) ```

89. What is a Reducer?
- In NgRx, a reducer is a pure function which determines how the application state should change in response to an action. It returns a new state with the store and action passed, the state is immutable.
- CreateReducer method is used to create reducer, it takes two arguments, current state and action as inputs.
    ```
        export const initialState: ProductState = {
            counter: 0
        }

        export const counterReducer = createReducer(
            initialState,
            on(increment, (state) => state + 1),
            on(decrement, (state) => state - 1)
        )
    ```
- on() is a helper function used inside Reducer to define how the state should change when specific action is performed.
- Effects are for side effects such as async api calls, timers, logging. Used to perform additional actions on the state.

90. What are signals?
- Signals are wrapper around a value that can notify consumers when the value changes. It can store any values from primitive ones to data structures.
- Without signals, angular uses change detection mechanism to find out if a value has changed and updates it.
- But change detection happens very frequently and affects the performance of the app.
- We can declare signals by: ``` let counterVal = signal(0) ```
    ``` this.counterVal.set(this.counterVal() + 1); ```
- Signal returns a function type, so use () in component and view to access the values of a signal.

91. What are RxJS operators?
- They are functions that takes an Observable as input and returns a new Observable.
- They are the building blocks of reactive programming, used to manipulate, transform, and combine streams of data in a functional way.

92. What is pipe() operator?
- It is a method that allows us to chain multiple RxJS operators together. Most crucial for composing complex data transformations.
    ```
    of (1,2,3,4,5).pipe(
        filter(el => el % 2 == 0),
        map(el => el * 10)
    )
    .subscribe(result => console.log(result))
    ```

93. What is map() operator?
- The map() operator transforms each item emitted by an Observable into a new item based on the provided function. 
- Mainly to transform all the data in the stream on any specific conditions.

94. What is mergeMap()?
- mergeMap() is a RxJS flattening operator that chains async operations.
- When the source observable emits a value, mergeMap() creates a new inner observable for that value and subscribes to it automatically.
- If the source emits multiple values, mergeMap() processes them all concurrently (parallel execution), and results arrive in the order they complete, not the original order.
- For example, if we want to fetch all users and then get posts for each user: first we receive the users array, then we use from() to convert it into individual emissions, then mergeMap() fetches posts for each user in parallel. We receive results as each request completes.

95. What is exhaustMap()?
- It is another RxJS flattening operator. It maps each value from the source observable to the inner observable.
- It ignores all new emissions from the source observable while the current projected inner observable is still active.

96. take operator()
- It allows to take only the first n values emitted by the observable and then completes the stream. Useful in retry logic.

97. What is switchMap()?
- Switchmap() is an RxJS operator that chains async operations, but it cancels the current inner observable when a new one arrives. It always keeps the latest operation running. 
- It is perfect for scenarios like search or autocomplete where we only care the latest user input.

98. What is an Effect?
- An effect refers to the change made to the external variables, asynchronous HTTP calls or file manipulation. Any change made to external variables other than application state is an effect.
- Some examples: To load data from backend API or save/update data on server, authentication/authorization - login, logout, refreshing tokens, interacting with browser apis.
- They are used to manage and execute side effects. After the side effect is completed, they dispatch a new action (success/failure) to update the store with the result.
- NgRX effects are angular injectable services. Similar to reducers, they listens for a dispatched action and performs a side effect.
- It doesn't handle state directly, it just dispatches another action, which is handled by reducer, which updates the state.

99. Reducer vs Effect
- Reducers are pure functions, they are used to update state changes and they are consistent.
- Effects handle side effects ensuring that the components remain pure and app logic is more organized and testable.
- When the action is tere in both reducer and effect, both of them is triggered, reducer is triggered first.

100. What are Interceptors?
- Interceptors is a middleware provided by the HTTPClient module. They allow us to hook into the HTTP call process and perform actions before the request is sent and right after recieving response. 
- Examples - applying auth headers, caching data, setting up global loading state. 
- They are registered with the help of withInterceptors().

101. What is lazy loading and how does it improve performance of the application?
- Lazy loading is a design pattern in angular that delays the initialization or loading of the component or module until it is used by the user. 
- Instead of loading the entire app at once, we break it into smaller chunks as the user navigates.
    ```
        export const routes: Routes = [
        {
            path: 'courses',
            loadComponent: () => import('./courses/courses.component').then(m => m.CoursesComponent)
        }
        ]; 
    ```

102. What is OnPush change detection strategy?
- It is a change detection strategy used in angular to improve the overall performance of application. It tells angular to skip checking a component and its children from running change detection unless any specific action has occured (like click events, events, input changes, signal updates).
- If we change a property of object inside the existing one, angular sees the reference and skips it from change detection. So, we can create a new object with spread operator and change the property. Now, angular will run change detection on the changes.

103. What is the async pipe and why is it better?
- async pipe is a feature in angular that can be used in templates to automatically handle promises/Observables.
- It subscribes to the data source, retrieves latest value and renders it in the view.
- It automatically subscribes and unsubscribes, so it is better for performance as it avoids memory leaks.

104. What is trackBy in ngFor?
- trackBy is a function used with *ngFor directive to optimize rendering performance when dealing with lists of dynamic data. 
- It provides unique identifier for each item (eg. trackBy id), allowing angular to efficiently track which items have been added, removed, removing unnecessary DOM manipulation.
- By default, angular uses object identity to track items.
- Syntax in modern @for:
    ```
        <ul>
        @for (item of items; track item.id) {
            <li>{{ item.name }}</li>
        }
        </ul> 
    ```

105. What is pure vs impure pipe?
- Pipes are pure by default. A pure pipe has the transform() method which is only invoked if there is a change to its input value. Triggers when a primitive value or an object reference changes.
- It is highly efficient. Angular uses memoization on this transform method and caches the result for next use. Eg. CurrencyPipe, DataPipe
- It runs during every change detection cycle even if values has not changed. Eg. AsyncPipe, JSONPipe.

106. What is tree shaking?
- Tree shaking is a step in the build process that identifies and removes dead code (unused code) from final js bundle. 
- The build tool (webpack, esbuild) looks at the import export statements to see which part of code is actually being called.

107. What is AOT compilation?
- In AOT, the compilation happens on machine (build server) during the build process. Since browser doesn't have to render code, it is much faster to load.
- It catches the template errors in the build stage itself. And smaller bundle size.

108. What is the Angular build optimizer?
- It is a tool used during the production build process to further reduce size of js bundles by making them easier to tree-shake.

109. What is code splitting?
- Technique that breaks application's large js bundles into smaller chunks, that can be loaded on demand. 

110. What is preloading strategy for lazy modules?
- Preloading strategy is a technique that loads the other lazy-loaded modules in the background after the initial bundle has loaded. 
- The app doesn't wait for user to interact for lazy loading. It is interactive immediately.
- we can specify the property - withPreloading(PreloadAllModules). 
- Only a specific component/module can also be preloaded.
    ```
    import { routes } from './app.routes';

    export const appConfig: ApplicationConfig = {
    providers: [
        provideRouter(
        routes,
        // This tells Angular to download all lazy routes in the background
        withPreloading(PreloadAllModules) 
        )
    ]
    };
    ```

111. How do you use Chrome DevTools to debug Angular performance?
- We can debug angular performance with the profiler tab in angular devtools extension to detect changes and time to run.
- We can record/start profiler and interact with the app.

112. What is Ivy renderer?
- It is the rendering engine for angular.
- Key architecture - Designed to make Angular tree-shaking, smaller bundle size for standalone components as default, stricter type checking for templates.

113. What is SlicePipe and KeyValuePipe?
- SlicePipe - produces new slice/subset of array. template version of slice() method.
- ``` {{ collection | slice:start:end }} ```
- KeyValuePipe - converts objects or map to array for being able to iterate it in template with @for/ngFor.
    ```
    @for (item of settings | keyvalue; track item.key) {
        <p>{{ item.key }}: {{ item.value }}</p>
    }
    ```
