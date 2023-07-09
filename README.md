Make the readme file with this code.

class Transaction:
    """
    Class representing a transaction for a self-service cashier system.
    """

    def __init__(self):
        """
        Initialize a new Transaction object.
        """
        self.items = []

    def add_item(self, item):
        """
        Add an item to the transaction.

        Args:
            item (dict): A dictionary representing an item with 'name', 'qty', and 'price' keys.

        Returns:
            None
        """
        self.items.append(item)

    def update_item_name(self, old_name, new_name):
        """
        Update the name of an item in the transaction.

        Args:
            old_name (str): The current name of the item.
            new_name (str): The new name to be assigned to the item.

        Returns:
            None
        """
        try:
            for item in self.items:
                if item['name'] == old_name:
                    item['name'] = new_name
                    break
            else:
                raise ValueError(f"Item with name '{old_name}' not found.")
        except KeyError as e:
            print(f"Error updating item name: {e}")

    def update_item_qty(self, name, qty):
        """
        Update the quantity of an item in the transaction.

        Args:
            name (str): The name of the item.
            qty (int): The new quantity to be assigned to the item.

        Returns:
            None
        """
        try:
            for item in self.items:
                if item['name'] == name:
                    item['qty'] = qty
                    break
            else:
                raise ValueError(f"Item with name '{name}' not found.")
        except KeyError as e:
            print(f"Error updating item quantity: {e}")

    def update_item_price(self, name, price):
        """
        Update the price of an item in the transaction.

        Args:
            name (str): The name of the item.
            price (float): The new price to be assigned to the item.

        Returns:
            None
        """
        try:
            for item in self.items:
                if item['name'] == name:
                    item['price'] = price
                    break
            else:
                raise ValueError(f"Item with name '{name}' not found.")
        except KeyError as e:
            print(f"Error updating item price: {e}")

    def delete_item(self, name):
        """
        Delete an item from the transaction.

        Args:
            name (str): The name of the item to be deleted.

        Returns:
            None
        """
        try:
            for item in self.items:
                if item['name'] == name:
                    self.items.remove(item)
                    break
            else:
                raise ValueError(f"Item with name '{name}' not found.")
        except ValueError as e:
            print(f"Error deleting item: {e}")

    def reset_transaction(self):
        """
        Reset the transaction by removing all items.

        Returns:
            None
        """
        self.items = []

    def check_order(self):
        """
        Check the order for any missing or incomplete data.

        Returns:
            bool: True if the order is correct, False otherwise.
        """
        try:
            for item in self.items:
                if not all(key in item for key in ['name', 'qty', 'price']):
                    return False
            return True
        except Exception as e:
            print(f"Error checking order: {e}")

    def total_price(self):
        """
        Calculate the total price of the transaction.

        Returns:
            float: The total price of the transaction.
        """
        try:
            total = 0
            for item in self.items:
                total += item['qty'] * item['price']

            if total > 500000:
                total *= 0.9
            elif total > 300000:
                total *= 0.92
            elif total > 200000:
                total *= 0.95

            return total
        except Exception as e:
            print(f"Error calculating total price: {e}")


# Contoh penggunaan sistem kasir self-service
trnsct_123 = Transaction()

# Menambahkan item Mobil Mainan
trnsct_123.add_item({'name': 'Mobil Mainan', 'qty': 1, 'price': 200000})

# Menambahkan item Mie Instan
trnsct_123.add_item({'name': 'Mie Instan', 'qty': 5, 'price': 5000})

# Mengupdate item dengan menambahkan Ayam Goreng
trnsct_123.add_item({'name': 'Ayam Goreng', 'qty': 2, 'price': 20000})

# Mengupdate item dengan menambahkan Pasta Gigi
trnsct_123.add_item({'name': 'Pasta Gigi', 'qty': 3, 'price': 15000})

# Melakukan pengecekan pemesanan
if trnsct_123.check_order():
    print("Pemesanan sudah benar")
    for item in trnsct_123.items:
        print(f"Item: {item['name']}, Jumlah: {item['qty']}, Harga: {item['price']}")
else:
    print("Terdapat kesalahan input data")

# Menghitung total belanjaan
total = trnsct_123.total_price()
print(f"Total belanja: {total}")


# Menghapus item Pasta Gigi
trnsct_123.delete_item('Pasta Gigi')

# Melakukan pengecekan pemesanan
if trnsct_123.check_order():
    print("Pemesanan sudah benar")
    for item in trnsct_123.items:
        print(f"Item: {item['name']}, Jumlah: {item['qty']}, Harga: {item['price']}")
else:
    print("Terdapat kesalahan input data")

# Menghitung total belanjaan
total = trnsct_123.total_price()
print(f"Total belanja: {total}")

# Reset transaksi
trnsct_123.reset_transaction()

# Melakukan pengecekan pemesanan
if trnsct_123.check_order():
    print("Pemesanan sudah benar")
    for item in trnsct_123.items:
        print(f"Item: {item['name']}, Jumlah: {item['qty']}, Harga: {item['price']}")
else:
    print("Terdapat kesalahan input data")

# Menghitung total belanjaan
total = trnsct_123.total_price()
print(f"Total belanja: {total}")

