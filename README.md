# LINQ Operators and Class Structures

## Introduction to LINQ Operators

LINQ (Language Integrated Query) operators can be used against sequences that implement the `IEnumerable` interface. These sequences can be of any data type, class, or collection. There are two main types of sequences:

1. Local Sequences
   - Static
   - XML
2. Remote Sequences

In this document, we'll focus on local sequences, both static and XML types.

## Project Structure

To organize our code, we'll create the following structure:

- Project Root
  - Data (Folder)
    - Product.cs
    - Order.cs
    - Customer.cs
  - ListGenerator.cs

## Class Definitions

### Product Class

```csharp
public class Product
{
    public long ProductID { get; set; }
    public string ProductName { get; set; }
    public string Category { get; set; }
    public decimal UnitPrice { get; set; }
    public int UnitsInStock { get; set; }

    public override string ToString()
        => $"ProductID: {ProductID}, ProductName: {ProductName}, Category: {Category}, UnitPrice: {UnitPrice}, UnitsInStock: {UnitsInStock}";
}
```

### Order Class

```csharp
internal class Order
{
    public int OrderID { get; set; }
    public DateTime OrderDate { get; set; }
    public decimal Total { get; set; }

    public Order(int orderID, DateTime orderDate, decimal total)
    {
        OrderID = orderID;
        OrderDate = orderDate;
        Total = total;
    }

    public Order() { }

    public override string ToString()
        => $"Order ID: {OrderID}, Date: {OrderDate.ToShortDateString()}, Total: {Total}";
}
```

### Customer Class

```csharp
public class Customer
{
    public string CustomerID { get; set; }
    public string CustomerName { get; set; }
    public string Address { get; set; }
    public string City { get; set; }
    public string Region { get; set; }
    public string PostalCode { get; set; }
    public string Country { get; set; }
    public string Phone { get; set; }
    public string Fax { get; set; }
    public Order[] Orders { get; set; }

    public Customer(string customerID, string customerName)
    {
        CustomerID = customerID;
        CustomerName = customerName;
        Orders = new Order[10];
    }

    public Customer() { }

    public override string ToString()
    {
        // Implementation not provided in the original code
        return $"Customer: {CustomerID}, Name: {CustomerName}";
    }
}
```

### ListGenerator Class

```csharp
internal class ListGenerator
{
    // This class will be used to generate lists of our data types
    // Implementation to be added later
}
```

## Notes

- The `Customer` class has an aggregate composition relationship with the `Order` class, represented by the `Orders` array property.
- The `ListGenerator` class is currently empty and will be implemented later to create lists of our data types for LINQ operations.
- All classes override the `ToString()` method to provide a string representation of their data.

In the next section, we'll implement the `ListGenerator` class and explore various LINQ operators using these data structures.




## ListGenerator Class

The `ListGenerator` class is designed to be a container for our data. It's implemented as a static class with static properties, which means:

- There can only be one instance of this class for the entire application.
- Its properties can be accessed without creating an instance of the class.
- It uses a static constructor to initialize its properties.

Here's the implementation of the `ListGenerator` class:

```csharp
public static class ListGenerator
{
    public static List<Customer> CustomersList { get; set; }
    public static List<Product> ProductList { get; set; }

    static ListGenerator()
    {
        ProductList = new List<Product>()
        {
            new Product() { ProductID = 1, ProductName = "Chai", Category = "Beverages", UnitPrice = 18.00M, UnitsInStock = 100 },
            new Product { ProductID = 2, ProductName = "Chang", Category = "Beverages", UnitPrice = 19.0000M, UnitsInStock = 17 },
            new Product { ProductID = 3, ProductName = "Aniseed Syrup", Category = "Condiments", UnitPrice = 10.0000M, UnitsInStock = 13 },
            // ... [The rest of the 77 products are listed here]
            new Product() { ProductID = 77, ProductName = "Original Frankfurter grüne Soße", Category = "Condiments", UnitPrice = 13.0000M, UnitsInStock = 32 }
        };

        // CustomersList initialization will be added here
    }
}
```

### Key Points about ListGenerator

1. **Static Class**: The `ListGenerator` class is declared as `static`, meaning it cannot be instantiated and all its members must also be static.

2. **Static Properties**: `CustomersList` and `ProductList` are static properties, allowing them to be accessed directly through the class name (e.g., `ListGenerator.ProductList`).

3. **Static Constructor**: The static constructor (which has no access modifier and is named after the class) is used to initialize the static properties. It's called automatically before the first use of the class.

4. **List Initialization**: The `ProductList` is initialized using a collection initializer, which provides a concise way to create and populate the list.

5. **Local Sequence of Static Data**: The product list represents a local sequence of static data, which is ideal for demonstrating LINQ operations.

### Note on CustomersList

The `CustomersList` is currently not initialized in the provided code. You may want to add customer data in a similar manner to the product list, depending on your requirements.

## Next Steps

With this `ListGenerator` class, we now have a substantial set of data to work with for demonstrating LINQ operators. In the next sections, we can explore various LINQ operations using this data, such as:

- Filtering products by category
- Sorting products by price
- Grouping products by category
- Joining products with customer orders (once customer data is added)

These operations will showcase the power and flexibility of LINQ in querying and manipulating data from local sequences.
