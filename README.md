# List of inventory
inventory = {
    "laptop": {"price": 999.99, "quantity": 15},
    "mouse": {"price": 29.99, "quantity": 50},
    "keyboard": {"price": 45.99, "quantity": 8},
    "monitor": {"price": 300.00, "quantity": 5}
}

# Display header and inventory and quantities
def display_inventory():
    """Print all inventory in a formatted way."""
    print("\n" + "=" * 45)
    print("              Store Inventory")
    print("=" * 45)
    print(f"{'Product':<14} {'Price':<12} {'Quantity':<10}")
    print("-" * 45)
     
    # Display for if no products in inventory
    if not inventory:
        print("No inventory yet.")
        return
    else:
        item_totals = []
        quantity_totals = []

        # Display formatted inventory and calculate each product's totals
        for name, details in inventory.items():
            price = details["price"]
            quantity = details["quantity"]

            # Multiply price by quantity for single product
            product_total = price * quantity

            # Append the calculated total to list
            item_totals.append(product_total)
            quantity_totals.append(quantity)

            # Print formatted totals of amt of products in inventory, price of all items and quantities
            print(f"{name.capitalize():<12}   ${price:<9}   {quantity:<10}")    

        # Use sum() to get overall total $ amount of inventory
        total_inventory_value = sum(item_totals)

        # Use sum() to get total sum of all quantities
        total_quantity = sum(quantity_totals)

        print("-" * 45)
        print(f"Total Inventory Value: ${total_inventory_value:.2f}")
        print("=" * 45)
        print(f"\nTotal inventory: {len(inventory)}")
        print(f"\nTotal Items in stock:  {total_quantity}")

display_inventory()
# Track low stock with a set (< 10)
low_stock_items = set()

for name, details in inventory.items():
    if details["quantity"] < 10:
        low_stock_items.add(name.capitalize())

    print("\n" + "=" * 45)
    print("             Low Stock Alert (< 10)")
    print("=" * 45)

if low_stock_items:
    for item in low_stock_items:
        print(f"   {item} needs restocking!")
else:
    print(f"All items are sufficiently stocked.")

    # --- Menu options ---
print("\nWhat would you like to do?")
print("1. Look up a product")
print("2. Update product quantity")
choice = input("\nEnter choice #: ")   

    # Option 1: Look up a product using .get()
if choice == "1":
    search = input("\nEnter product name to search: ").lower()
    product = inventory.get(search)

    if product:
        print(f"\nFound '{search.capitalize()}':")
        print(f" Price: ${product['price']:.2f}")
        print(f" Quantity: {product['quantity']}")
    else:
        print(f"\nProduct '{search}' not found in inventory.")

    display_inventory()
    # Option 2: Update quantity of a product with error handling
if choice == "2":
    update_item = input("\nEnter product name to update quantity: ").lower()

    if update_item in inventory:
        try:
            new_qty = int(input(f"Enter new quantity for {update_item}: "))
            inventory[update_item]["quantity"] = new_qty
            print(f"Updated {update_item} quantity to {new_qty}.")
        except ValueError:
            print(f"Invalid number entered. Quantity not changed.")
        else:
            print(f"Cannot update: '{update_item}' is not in inventory.")

display_inventory()
