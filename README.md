# Observer - Патерн Проєктування

Патерн Observer визначає залежність типу "один-до-багатьох", у якій при зміні стану одного об’єкта інші отримують повідомлення і автоматично оновлюються.

## Ідея

Є об’єкт **Subject**, який зберігає список спостерігачів.  
Коли в ньому відбувається якась подія, він повідомляє всі об’єкти **Observer**, викликаючи їх метод `Update`.

## Структура

| Елемент         | Опис |
|----------------|------|
| `Subject`      | Зберігає спостерігачів та надсилає їм повідомлення |
| `IObserver`    | Інтерфейс для об'єктів, які мають реагувати на зміни |
| `ConcreteObserver` | Реагує на повідомлення |
| Клієнт         | Налаштовує: додає спостерігачів до суб’єкта |

## Код

```csharp
interface IObserver { void Update(string msg); }

class Subject {
    List<IObserver> obs = new();
    public void Attach(IObserver o) => obs.Add(o);
    public void Notify(string m) { foreach (var o in obs) o.Update(m); }
}

class ConcreteObserver : IObserver {
    public void Update(string msg) => Console.WriteLine("Received: " + msg);
}

class Program {
    static void Main() {
        var s = new Subject();
        s.Attach(new ConcreteObserver());
        s.Notify("Event happened");
    }
}
