# COP2664-1-Lesson-8-Programming-Assignment
This is a GitHub repository link for the Programming Assignment of Module 8.

// This program is created for an electronic restaurant ordering system that presents the user with the food items they ordered and the total price of the order.

import Foundation

protocol MenuItem {
    var name: String { get }
    var price: Double { get }
    func itemDescription() -> String
}
// This protocol defines the MenuItem protocol, which is used to represent the different types of menu items. It has two properties, name and price, which are both strings and return the name and price of the menu item, respectively. It also has a function itemDescription() that returns a string describing the menu item.
struct Food: MenuItem {
    var name: String
    var price: Double
    var cuisine: String
    func itemDescription() -> String {
        return "\(name) - $\(price) - Cuisine: \(cuisine)"
    }
}
// This struct represents a food item, which is a subclass of MenuItem. It has a property name, price, and cuisine, which are all strings. The itemDescription() function returns a string describing the food item, including its name, price, and cuisine.
struct Beverage: MenuItem {
    var name: String
    var price: Double
    var isAlcoholic: Bool
    func itemDescription() -> String {
        return "\(name) - $\(price) - Alcoholic: \(isAlcoholic ? "Yes" : "No")"
    }
}
// This struct represents a beverage item, which is a subclass of MenuItem. It has a property name, price, and isAlcoholic, which are all strings. The itemDescription() function returns a string describing the beverage item.
extension MenuItem {
    func calculateTax(rate: Double) -> Double {
        return price * rate
    }
}
// This extension adds a function calculateTax() to the MenuItem protocol, which takes a rate parameter and returns the tax amount for the menu item.
class Order {
    var items: [MenuItem] = []
    func addItem(_ item: MenuItem) {
        items.append(item)
    }
    func calculateTotalCost() -> Double {
        return items.reduce(0.0) { $0 + $1.price }
    }
    func listItems() {
        for item in items {
            print(item.itemDescription())
        }
    }
}
// This class represents an order, which has an array of menu items and functions to add items to the order and calculate the total cost. It also has a function listItems() that prints out the description of each item in the order.
enum OrderError: Error {
    case invalidItem
    case emptyOrder
}
// This enum represents the possible errors that can occur when adding items to an order. It has a case for each error type, and it is used in the addItem() function.
func main() {
    let food1 = Food(name: "Lomo Saltado", price: 23.00, cuisine: "Peru")
    let food2 = Food(name: "Philly CheeseSteak", price: 19.95, cuisine: "American")
    let beverage1 = Beverage(name: "MilkShake", price: 10.50, isAlcoholic: false)
    let beverage2 = Beverage(name: "Apple Martini", price: 12.36, isAlcoholic: true)
    // These are the two menu items that will be added to the order.
  let order = Order()
    order.addItem(food1)
    order.addItem(food2)
    order.addItem(beverage1)
    order.addItem(beverage2)
    print("Order Items:")
    order.listItems()
    print("Total Cost: $\(order.calculateTotalCost())")
// This is the main function that creates an order object, adds the two menu items to it, and prints out the description of each item in the order. It also prints out the total cost of the order.
    do {
        let totalCost = order.calculateTotalCost()
        print("Total Cost (with tax): $\(totalCost + totalCost * 0.1)")
    } catch OrderError.invalidItem {
        print("Error: Invalid item added to the order.")
    } catch OrderError.emptyOrder {
        print("Error: The order is empty.")
    } catch {
        print("Error: \(error)")
    }
    // This is a do-catch block that calculates the total cost of the order, including tax. If an error occurs, it prints out the error message.
}

main ()
