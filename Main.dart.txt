double calculateOrderTotal(String coffeeType, int cupCount, double pricePerCup) {
  if (cupCount <= 0) {
    throw ArgumentError('Cup count must be greater than zero.');
  }

  double rawTotal = cupCount * pricePerCup;
  
  if (rawTotal >= 20.0) {
    print('   -> Qualifying for 10% High-Value Order Discount!');
    rawTotal *= 0.90;
  } else {
    print('   -> Standard order total applied.');
  }

  return rawTotal;
}

void main() {
  List<Map<String, dynamic>> customerOrders = [
    {'item': 'Oat Milk Latte', 'cups': 5, 'price': 4.75},
    {'item': 'Americano', 'cups': 1, 'price': 3.00},
    {'item': 'Espresso', 'cups': -2, 'price': 2.50}, // Intentional invalid input to test try/catch
    {'item': 'Iced Caramel Macchiato', 'cups': 4, 'price': 5.25},
  ];

  print('=== CAFE ORDERS PROCESSING  ===\n');

  for (int i = 0; i < customerOrders.length; i++) {
    var order = customerOrders[i];
    print('Processing Order #${i + 1}: ${order['cups']}x ${order['item']}');

    try {
      double finalPrice = calculateOrderTotal(
        order['item'] as String,
        order['cups'] as int,
        order['price'] as double,
      );
      print('   Final Receipt Total: \$${finalPrice.toStringAsFixed(2)}\n');
    } catch (e) {
      print('   [ERROR HANDLED]: Failed to process order. Reason: ${e}\n');
    }
  }

  print('=== ALL ORDERS PROCESSED ===');
}