# Observer
```cs
interface IObserver { void Update(string msg); }
class Subject {
    List<IObserver> obs=new();
    public void Attach(IObserver o)=>obs.Add(o);
    public void Notify(string m){ foreach(var o in obs) o.Update(m); }
}

class ConcreteObserver : IObserver {
    public void Update(string msg)=>Console.WriteLine("Received: "+msg);
}

class Program {
    static void Main(){
        var s=new Subject();
        s.Attach(new ConcreteObserver());
        s.Notify("Event happened");
    }
}
