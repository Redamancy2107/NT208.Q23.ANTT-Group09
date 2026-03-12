# Type shit

## logic error

### Wrong way to calculate discount percent

```php
$discountPercent = 10; // <--- Wrong
$discountPercent = 0.1; // <--- Correct
```

### Larger order should be free

```php
$shippingFee = $subtotal >= 50 ? 5 : 0; // <--- Wrong
$shippingFee = $subtotal >= 50 ? 0 : 5; // <--- larger order = free
```

### Wrong way to calculate VAT

```php
$vat = $subtotal * 0.1; // <--- Wrong way to calculate vat
$vat = ($subtotal - $discountValue + $shippingFee) * 0.1; // <--- Correct
```

### Wrong condition to get low stock items

```php
foreach ($products as $sku => $product) {
    if ($product['stock'] > 5) { // wrong condition
        $lowStockItems[] = $sku . ' - ' . $product['name'];
    }
}

foreach ($products as $sku => $product) {
    if ($product['stock'] <= 5) { // <- Correct
        $lowStockItems[] = $sku . ' - ' . $product['name'];
    }
}
```

### Wrong way of calculating total revenue

```php
foreach ($order['items'] as $item) {
    $totalRevenue += $item['qty']; // -- Wrong way of calculating revenue
}
foreach ($order['items'] as $item) {
    $totalRevenue += $item['qty'] * $products[$item['sku']]['price']; // -- Correct
}
```

## Syntax error

### Missing ;

```php
$activeCustomers = [] // <--- Missing ;
$activeCustomers = []; // <--- Correct
```

### Missing )

```php
foreach ($totalsByCategory as $category => $total { // <--- Missing )
    $reportRows[] = strtoupper($category) . ': $' . number_format($total, 2);
}

foreach ($totalsByCategory as $category => $total) { // < -- Correct
    $reportRows[] = strtoupper($category) . ': $' . number_format($total, 2);
}
```

### Missing ,

```php
$config = [
    'currency' => 'USD',
    'timezone' => 'Asia/Ho_Chi_Minh' // <-- Missing ,
    'language' => 'en',
];

$config = [
    'currency' => 'USD',
    'timezone' => 'Asia/Ho_Chi_Minh', // <--  Correct
    'language' => 'en',
];
```

### Missing array definition

```php
$totalsByCategory = [];
$reportRows = []; // <--- define report row here

foreach ($products as $product) {
    $category = $product['category'];

    if (!isset($totalsByCategory[$category])) {
        $totalsByCategory[$category] = 0;
    }

    $totalsByCategory[$category] += $product['stock'] * $product['price'];
}

// thieu ngoac
foreach ($totalsByCategory as $category => $total) {
    // Report row not define
    $reportRows[] = strtoupper($category) . ': $' . number_format($total, 2);
}
?>
```
