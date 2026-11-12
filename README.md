## Практическая работа №13
```Csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Practic_13;

namespace Practic_13
{
    public static class CurrencyConverter
    {
        private static double _usdRate;
        private static double _eurRate;

        public static double UsdRate => _usdRate;
        public static double EurRate => _eurRate;

        static CurrencyConverter()
        {
            _usdRate = 92.5;
            _eurRate = 100.2;
            Console.WriteLine("[CurrencyConverter]: Загрузка курсов валют...");
        }

        public static void UpdateRates(double newUsd, double newEur)
        {
            if (newUsd > 0 && newEur > 0)
            {
                _usdRate = newUsd;
                _eurRate = newEur;
                Console.WriteLine("Курсы успешно обновлены.");
            }
            else
            {
                Console.WriteLine("Ошибка: курсы валют должны быть строго больше нуля.");
            }
        }

        public static decimal ConvertToRub(decimal foreignAmount, string currencyCode)
        {
            decimal rate = currencyCode.ToUpper() switch
            {
                "USD" => (decimal)_usdRate,
                "EUR" => (decimal)_eurRate,
                _ => 1m
            };

            if (rate == 1m && currencyCode.ToUpper() != "RUB")
            {
                Console.WriteLine($"Предупреждение: валюта '{currencyCode}' не распознана.");
            }

            return foreignAmount * rate;
        }
    }
}
class Program
{
    static void Main()
    {
        decimal rubles = CurrencyConverter.ConvertToRub(100, "USD");
        Console.WriteLine($"100 USD = {rubles} RUB"); // 100 * 92.5 = 9250

        CurrencyConverter.UpdateRates(95.0, 105.0);

        CurrencyConverter.UpdateRates(-5, 110);
    }
}
```
### Результат выполнения:
<img width="1430" height="737" alt="1" src="https://github.com/user-attachments/assets/0ada42d4-d240-4520-90a5-7e9f575b07ce" />
<img width="1435" height="733" alt="2" src="https://github.com/user-attachments/assets/3366e736-7982-4d35-b2bc-d5c8afdcb789" />
// Делал Аристов Максим
