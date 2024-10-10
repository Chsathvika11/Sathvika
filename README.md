
class Product:
    def __init__(self, product_id, name, description, price, category):
        self.product_id = product_id
        self.name = name
        self.description = description
        self.price = price
        self.category = category

    def update(self, name=None, description=None, price=None, category=None):
        if name:
            self.name = name
        if description:
            self.description = description
        if price:
            self.price = price
        if category:
            self.category = category

    def __repr__(self):
        return f"Product ID: {self.product_id}, Name: {self.name}, Description: {self.description}, Price: {self.price}, Category: {self.category}"


class ProductApp:
    def __init__(self):
        self.products = []
        self.next_product_id = 1

    def add_product(self, name, description, price, category):
        new_product = Product(self.next_product_id, name, description, price, category)
        self.products.append(new_product)
        self.next_product_id += 1
        print("Product added successfully!")

    def update_product(self, product_id, name=None, description=None, price=None, category=None):
        product = self.get_product_by_id(product_id)
        if product:
            product.update(name, description, price, category)
            print("Product updated successfully!")
        else:
            print("Product not found!")

    def delete_product(self, product_id):
        product = self.get_product_by_id(product_id)
        if product:
            self.products.remove(product)
            print("Product deleted successfully!")
        else:
            print("Product not found!")

    def get_product_by_id(self, product_id):
        for product in self.products:
            if product.product_id == product_id:
                return product
        return None

    def get_all_products(self):
        if not self.products:
            print("No products available.")
        for product in self.products:
            print(product)

    def get_products_by_category(self, category):
        category_products = [product for product in self.products if product.category.lower() == category.lower()]
        if category_products:
            for product in category_products:
                print(product)
        else:
            print(f"No products found in category '{category}'")

    def get_products_by_price_range(self, min_price, max_price):
        price_range_products = [product for product in self.products if min_price <= product.price <= max_price]
        if price_range_products:
            for product in price_range_products:
                print(product)
        else:
            print(f"No products found in price range {min_price} to {max_price}")

def main():
    app = ProductApp()

    while True:
        print("\nProduct Management Menu:")
        print("1. Add Product")
        print("2. Update Product")
        print("3. Delete Product")
        print("4. Get Product by ID")
        print("5. Get All Products")
        print("6. Get Products by Category")
        print("7. Get Products by Price Range")
        print("8. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            name = input("Enter product name: ")
            description = input("Enter product description: ")
            price = float(input("Enter product price: "))
            category = input("Enter product category: ")
            app.add_product(name, description, price, category)

        elif choice == '2':
            product_id = int(input("Enter product ID to update: "))
            name = input("Enter new name (leave blank to keep current): ")
            description = input("Enter new description (leave blank to keep current): ")
            price = input("Enter new price (leave blank to keep current): ")
            category = input("Enter new category (leave blank to keep current): ")

            app.update_product(
                product_id,
                name=name if name else None,
                description=description if description else None,
                price=float(price) if price else None,
                category=category if category else None
            )

        elif choice == '3':
            product_id = int(input("Enter product ID to delete: "))
            app.delete_product(product_id)

        elif choice == '4':
            product_id = int(input("Enter product ID to retrieve: "))
            product = app.get_product_by_id(product_id)
            if product:
                print(product)
            else:
                print("Product not found.")

        elif choice == '5':
            app.get_all_products()

        elif choice == '6':
            category = input("Enter category: ")
            app.get_products_by_category(category)

        elif choice == '7':
            min_price = float(input("Enter minimum price: "))
            max_price = float(input("Enter maximum price: "))
            app.get_products_by_price_range(min_price, max_price)

        elif choice == '8':
            print("Exiting the app.")
            break

        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
    
