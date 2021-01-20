### Builder Design Pattern

- The builder pattern allows us to create a complex object step by step by setting it's different properties one by one.

Following is an example for making a Hamburger that need to be done step by step like choosing meat type, putting sauces,
giving diffrent type of topping ext. The example code is written in swift programming language.

public struct Hamburger {
  public let meat: Meat
  public let sauce: Sauces
  public let toppings: Toppings
}

extension Hamburger: CustomStringConvertible {
  public var description: String {
    return meat.rawValue + " burger"
  }
}

public enum Meat: String {
  case beef
  case chicken
  case kitten
  case tofu
}

public struct Sauces: OptionSet {
  public static let mayonnaise = Sauces(rawValue: 1 << 0)
  public static let mustard = Sauces(rawValue: 1 << 1)
  public static let ketchup = Sauces(rawValue: 1 << 2)
  public static let secret = Sauces(rawValue: 1 << 3)

  public let rawValue: Int
  public init(rawValue: Int) {
    self.rawValue = rawValue
  }
}

public struct Toppings: OptionSet {
  public static let cheese = Toppings(rawValue: 1 << 0)
  public static let lettuce = Toppings(rawValue: 1 << 1)
  public static let pickles = Toppings(rawValue: 1 << 2)
  public static let tomatoes = Toppings(rawValue: 1 << 3)

  public let rawValue: Int
  public init(rawValue: Int) {
    self.rawValue = rawValue
  }
}

// MARK: - Builder
public class HamburgerBuilder {

  public private(set) var meat: Meat = .beef
  public private(set) var sauces: Sauces = []
  public private(set) var toppings: Toppings = []

  public func addSauces(_ sauce: Sauces) {
    sauces.insert(sauce)
  }

  public func removeSauces(_ sauce: Sauces) {
    sauces.remove(sauce)
  }

  public func addToppings(_ topping: Toppings) {
    toppings.insert(topping)
  }

  public func removeToppings(_ topping: Toppings) {
    toppings.remove(topping)
  }

  public func setMeat(_ meat: Meat) {
    self.meat = meat
  }

  // 3
  public func build() -> Hamburger {
    return Hamburger(meat: meat,
                     sauce: sauces,
                     toppings: toppings)
  }
}
