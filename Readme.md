# The Cashier Apps
Aplikasi ini berfungsi sebagai aplikasi cashier yang mencakup fungsi menambah item, type, jumlah dan harga kemudian mengkalkulasikan total harga semua barang 
## Scope & Funcionalities
* User dapat memasukkan item, type, jumlah dan harga barang
* User dapat menyentuh tombol tambahkan
* User mendapat jumlah total harga keseluruhan barang yang diinputkan
## How Does it works?
Diawali dengan method `MainWindow` pada class `MainWindows.xml.cs` kita mendeklarasikan `InitializeComponent()` berfugsi sebagai method yang membuat dan menginisialisasi user interface object yang telah dibuat, selanjutnya yaitu membuat object dari class `Calculator.cs` dengan syntax ` calculator = new Calculator();`

```csharp
    public MainWindow()
        {
            InitializeComponent();
            currencyController = new CurrencyController();
        }
``` 

Penjelasan Code diclass `Item.cs` yaitu menambahkan property dan merepresentasikan property sebagai get dan set method / getter dan setter 
```csharp
 private int id;
        public string title { get; set; }
        public int quantity { get; set; }
        public double price { get; set; }
        public double subtotal { get; set; }
        private string type;

        public Item(int id, string title, int quantity,   string type, double price)
        {
            this.id = id;
            this.title = title;
            this.quantity = quantity;
            this.type = type;
            this.price = price;
            this.subtotal = 0;
        }

 public Item(int id, string title, int quantity,   string type, double price)
        {
            this.id = id;
            this.title = title;
            this.quantity = quantity;
            this.type = type;
            this.price = price;
            this.subtotal = 0;
        }
```
Kemudian Pada class `MainWindow.xaml.cs` penjelasannya yaitu ketika button di klik akan menambahkan title,quantity, type dan harga yang telah diinputkan oleh kita tadi
```csharp
 private void AddButton_Click(object sender, RoutedEventArgs e)
        {
            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);

            Item item = new Item(new Random().Next(), title, quantity, type, price);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = String.Format("Rp. {0}", total);

            listBox.Items.Refresh();
        }
```


Penjelasan code selanjutnya yaitu pada `Calculator.cs` yang menerapkan prinsip Single Responsibility
```csharp
public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }
```

Code diatas menurut saya menerapkan prinsip Single Responibility dikarenakan hanya menambahkan nilai dari `getSubTotal()` ke variabel total dan kemudian menambahkan ke list item
