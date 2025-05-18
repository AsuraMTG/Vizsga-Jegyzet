```csharp
    internal class Ember
    {
        public int id { get; set; }
        public string nev { get; set; }
        public int kor { get; set; }
        public DateTime szulDat { get; set; }

        public Ember(int id, string nev, int kor, DateTime szulDat)
        {
            this.id = id;
            this.nev = nev;
            this.kor = kor;
            this.szulDat = szulDat;
        }

        public override string ToString()
        {
            return $"id: {id}, nev: {nev}, kor: {kor}, szuletett: {szulDat} \n";
        }
    }
```

```csharp
  List<Ember> emberek = new List<Ember>();

  Ember egyEmber = new Ember(1, Andris, 22, DateTime.Parse("2000.02.11"));
  emberek.Add(egyEmber);

  for (int i = 0; i < emberek.Count; i++)
  {
      Console.Write(emberek[i].ToString()); // --> id: 1, nev: Andris, kor: 22, szuletett: 2000. 02. 11. 0:00:00
  }
```
