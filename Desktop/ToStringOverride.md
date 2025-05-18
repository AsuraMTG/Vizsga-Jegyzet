```csharp
    internal class Ember
    {
        public int id { get; set; }
        public string nev { get; set; }
        public int kor { get; set; }

        public Ember(int id, string nev, int kor)
        {
            this.id = id;
            this.nev = nev;
            this.kor = kor;
        }

        public override string ToString()
        {
            return $"id: {id}, nev: {nev}, kor: {kor}";
        }
    }
```

```csharp
  List<Ember> emberek = new List<Ember>();

  Ember egyEmber = new Ember(1, Andris, 22);
  emberek.Add(egyEmber);

  
  Console.Write(emberek[0].ToString()); // --> id: 1, nev: Andris, kor: 22
```
