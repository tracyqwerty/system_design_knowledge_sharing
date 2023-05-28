# cohesion & coupling

Cohesion and coupling are two fundamental principles used in software design to evaluate and improve the quality of a software system.

## cohesion（内聚）

**Cohesion** refers to how closely the responsibilities of a module or a component in a software system are related to each other. High cohesion means that a module or a class is given a single, well-defined responsibility. This makes the system easier to understand, maintain, and modify. Low cohesion, on the other hand, means that a module or a class has multiple responsibilities that are not closely related, which can make the system more complex and harder to maintain.

For example, in an e-commerce application, you might have a `Cart` class that is responsible for adding items to a cart, removing items from the cart, and calculating the total cost of the items in the cart. These responsibilities are closely related, so this class would be considered highly cohesive.

## Coupling（耦合）

**Coupling** refers to the degree to which one module or a component depends on other modules or components within a system. **Low coupling is desirable because it means that each module or component can operate independently of the others, which makes the system as a whole easier to understand, maintain, and modify. High coupling, on the other hand, means that a change in one module can have a ripple effect on other modules, which can make the system more complex and harder to maintain.**

Continuing the e-commerce application example, suppose the `Cart` class needs to calculate sales tax for the items in the cart. If the `Cart` class calculates the sales tax itself, it would be highly coupled to the sales tax rules. If the sales tax rules change, the `Cart` class would need to be modified. To reduce this coupling, you could create a separate `TaxCalculator` class that is responsible for calculating sales tax. The `Cart` class could then use the `TaxCalculator` class to calculate sales tax. This way, if the sales tax rules change, only the `TaxCalculator` class needs to be modified.

In general, a good software design aims for high cohesion and low coupling. This makes the system easier to understand, maintain, and modify, and it makes it more robust to changes.