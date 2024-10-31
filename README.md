using System;
using System.Collections.Generic;

namespace DiscountGenerator
{
    public class Item
    {
        public string Name { get; set; }
        public double Price { get; set; }
    }

    public class DiscountGenerator
    {
        private readonly List<Item> _items;
        private readonly Random _random = new Random();

        public DiscountGenerator(List<Item> items)
        {
            _items = items;
        }

        public void GenerateDiscounts(int discountCount)
        {
            if (discountCount > _items.Count)
            {
                Console.WriteLine("Error: Cannot generate more discounts than items.");
                return;
            }

            var discountedItems = new List<Item>();

            // Select random items for discounts
            while (discountedItems.Count < discountCount)
            {
                int randomIndex = _random.Next(_items.Count);
                if (!discountedItems.Contains(_items[randomIndex]))
                {
                    discountedItems.Add(_items[randomIndex]);
                }
            }

            // Apply discounts
            foreach (var item in discountedItems)
            {
                double discountPercentage = _random.Next(5, 30); // Random discount between 5% and 30%
                double discountAmount = item.Price * (discountPercentage / 100);
                item.Price -= discountAmount;

                Console.WriteLine($"Discount applied to {item.Name}: {discountPercentage}% off. New price: {item.Price:C}");
            }
        }
    }

    public class Program
    {
        static void Main(string[] args)
        {
            // Create a list of items
            List<Item> items = new List<Item>()
            {
                new Item { Name = "Laptop", Price = 1200.00 },
                new Item { Name = "Smartphone", Price = 800.00 },
                new Item { Name = "Headphones", Price = 150.00 },
                new Item { Name = "Tablet", Price = 300.00 },
                new Item { Name = "Keyboard", Price = 75.00 },
                new Item { Name = "Mouse", Price = 30.00 },
                new Item { Name = "Charger", Price = 25.00 }
            };

            // Create a discount generator
            var discountGenerator = new DiscountGenerator(items);

            // Generate 3 random discounts
            discountGenerator.GenerateDiscounts(3);

            Console.ReadKey();
        }
    }
}
