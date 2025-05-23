# DESKTOP JEGYZETEK

```csharp
using System.IO;
```

```csharp
struct listaElemek
        {
            public string hegycsucsNeve;
            public string hegyseg;
            public string magassag;
        }
```

```csharp
 static void Main(string[] args)
        {   
            listaElemek hegy = new listaElemek();
            List<listaElemek> hegyek = new List<listaElemek>();
            
            FileStream folyam = new FileStream("hegyekMo.txt", FileMode.Open);
            StreamReader olvas = new StreamReader(folyam);

            string elso = olvas.ReadLine();
            string[] resz;

            while (!olvas.EndOfStream)
            {
                elso = olvas.ReadLine();

                resz = elso.Split(';');
                hegy.hegycsucsNeve = resz[0];
                hegy.hegyseg = resz[1];
                hegy.magassag = resz[2];
                hegyek.Add(hegy);
            }

            double seged = 0;
            for (int i = 0; i < hegyek.Count; i++)
            {
                seged += Convert.ToInt32(hegyek[i].magassag);
            }

            double legnagyobb = 0;
            int seged2 = 0;
            for (int i = 0; i < hegyek.Count; i++)
            {
                if (legnagyobb < Convert.ToInt32(hegyek[i].magassag))
                {
                    legnagyobb = Convert.ToInt32(hegyek[i].magassag); seged2 = i;
                }
            }

            Console.WriteLine($"3. feladat: Hegycsúcsok száma: {hegyek.Count} db");
            Console.WriteLine($"4. feladat: Hegycsúcsok átlagos magassága: {seged / hegyek.Count} m");
            Console.WriteLine($"5. feladat: Legmagasabb hegycsúcs adatai: " +
                $"\n\tNév: {hegyek[seged2].hegycsucsNeve}" +
                $"\n\tHegység: {hegyek[seged2].hegyseg}" +
                $"\n\tMagassága: {hegyek[seged2].magassag} m");
            Console.Write($"6. feladat: Kérek egy magasságot: ");
            string bekertAdat = Console.ReadLine();

            string seged3 = "Van";
            for (int i = 0; i < hegyek.Count; i++)
            {
                if ((hegyek[i].hegyseg == "Börzsöny") && (Convert.ToInt32(hegyek[i].magassag) < Convert.ToInt32(bekertAdat)))
                {
                    seged3 = "Nincs";
                }
            }

            Console.WriteLine($"\t{seged3} {bekertAdat}m-nél magasabb hegycsúcs a Börzsönyben!");

            double seged4 = 3.280839895;
            int megfeleloHegyekSzama = 0;
            for (int i = 0; i < hegyek.Count; i++)
            {
                if ((Convert.ToInt32(hegyek[i].magassag) * seged4) > 3000)
                {
                    megfeleloHegyekSzama++;
                }
            }
            Console.WriteLine($"7. feladat: 3000 lábnál magasabb hegycsúcsok száma: {megfeleloHegyekSzama}");

            string[] seged5 = {"Mátra", "Bükk-vidék", "Börzsöny", "Zempléni-hegység", "Kőszegi-hegység" };
            int matra = 0, bukk = 0, borzsony = 0, zemplen = 0, koszeg = 0;
            
            for (int i = 0; i < hegyek.Count; i++)
            {
                for (int j = 0; j < seged5.Length; j++)
                {
                    if (hegyek[i].hegyseg.Contains(seged5[j]))
                    {
                        if (seged5[j] == "Mátra")
                        {
                            matra++;
                        }
                        if (seged5[j] == "Bükk-vidék")
                        {
                            bukk++;
                        }
                        if (seged5[j] == "Börzsöny")
                        {
                            borzsony++;
                        }
                        if (seged5[j] == "Zempléni-hegység")
                        {
                            zemplen++;
                        }
                        if (seged5[j] == "Kőszegi-hegység")
                        {
                            koszeg++;
                        }
                    }
                }
            }

            Console.WriteLine($"8. feladat: Hegység statisztika" +
                $"\n\t{seged5[0]} - {matra} db" +
                $"\n\t{seged5[1]} - {bukk} db" +
                $"\n\t{seged5[2]} - {borzsony} db" +
                $"\n\t{seged5[3]} - {zemplen} db" +
                $"\n\t{seged5[4]} - {koszeg} db");

            Console.WriteLine("9. feladat: bukk-videk.txt");

            string path = "bukk-videk.txt";
            if (!File.Exists(path))
            {
                File.Create(path);
                TextWriter tw = new StreamWriter(path);
                tw.WriteLine("Hegycsúcs neve;Magasság láb");
                tw.Close();
            }
            else if (File.Exists(path))
            {
                TextWriter tw = new StreamWriter(path);
                for (int i = 0; i < hegyek.Count; i++)
                {
                    if (hegyek[i].hegyseg == "Bükk-vidék")
                    {
                        tw.WriteLine($"{hegyek[i].hegycsucsNeve};{Convert.ToInt32(hegyek[i].magassag) * seged4}");
                    }
                }
                tw.Close();
            }
            Console.ReadKey();
        }
```
---
# howToSolve

## General Guide

#### Useful Webpages
- [StackOverflow](https://stackoverflow.com/)
- [W3Schools](https://www.w3schools.com/)
- [Bootstrap](https://getbootstrap.com/)

#### VSC Extensions:
- EasyZoom
- Live Server
- Thunder Client
- Auto Rename Tag 

#### If XAMPP Won't Start
1. Navigate to: `C:\xampp\mysql\backup`
2. Press `Ctrl + X` to cut the contents
3. Navigate to: `C:\xampp\mysql\data`
4. Press `Ctrl + A` to select all, then `Ctrl + P` to paste

## Desktop 
Target finish time: **~1h 25min**

### Text manipulation
```csharp
Replace(',','-');  // 2019-2-12
Trim('-');  // 2019212 
Split(',');  // {apple, banana, orange}
Contains("YES") // returns true

char[] nameArray = {'A', 'l', 'i', 'c', 'e'};
string name = new string(nameArray);

Math.Round(number, 2)); // 5.43529 -> 5.44 (Honorable mention: Floor(), Ceiling())
```

### Classes and Constructors
```csharp
 class Person
 {
     public int id { get; set; }
     public double average { get; set; }
     public string name { get; set; }
     public DateTime date { get; set; }

     public Person(int id, double average, string name, DateTime date)
     {
         this.id = id;
         this.average = average;
         this.name = name;
         this.date = date;
     }
 }
```

### Reading a File
```csharp
List<Person> peopleList = new List<Person>();

using (StreamReader sr = new StreamReader("filename.txt"))
{
    while (!sr.EndOfStream)
    {
        string line = sr.ReadLine();
        string[] data = line.Split(';');
        int id = int.Parse(data[0]);
        data[1] = data[1].Replace(',', '.');
        double atlag = double.Parse(data[1]);
        string name = data[2];
        DateTime date = Convert.ToDateTime(data[3]);
        Person personList = new Person(id, average, name, date);
        peopleList.Add(person);
    }
}
```

### Creating a File
```csharp
using (StreamWriter sw = File.CreateText("filename.txt"))
{
    sw.WriteLine("...");
}
```
### LINQ Examples
```csharp
using System.Linq;
```

#### 1. Aggregation (Count, Sum, Average, Max, Min)
Calculate statistics.

```csharp
int count = people.Count(); // Total people
int over30Count = people.Count(p => p.Age > 30); // People over 30
double totalSalary = people.Sum(p => p.Salary); // Total salary
double avgSalary = people.Average(p => p.Salary); // Average salary
int maxAge = people.Max(p => p.Age); // Oldest age
```

#### 2. Filtering (Where)
Select people older than 25.

```csharp
var olderThan25 = people.Where(p => p.Age > 25);
```

#### 3. Sorting (OrderBy, ThenBy)
Sort people by age, then by name.


```csharp
var sortedPeople = people.OrderBy(p => p.Age).ThenBy(p => p.Name);
```

#### 4. Selecting Specific Fields (Select)
Get a list of names and salaries.

```csharp
var namesAndSalaries = people.Select(p => new { p.Name, p.Salary });
```

#### 5. Grouping (GroupBy)
Group people by age.


```csharp
var groupedByAge = people.GroupBy(p => p.Age).Select(g => new { Age = g.Key, People = g });
```


#### 6. First, Last, Single
Get specific elements.

```csharp
Person firstPerson = people.First(); // First person
Person lastPerson = people.Last(); // Last person
Person singlePerson = people.Single(p => p.Id == 1); // Person with Id 1
```

#### 7. Any and All
Check conditions.

```csharp
bool hasYoung = people.Any(p => p.Age < 25); // True if any person is under 25
bool allHighEarners = people.All(p => p.Salary > 40000); // True if all earn > 40k
```

#### Tips for Effective LINQ
- **Performance**: Avoid multiple enumerations; materialize results with `.ToList()` if needed.
- **Debugging**: Break complex queries into smaller steps.

## Backend
Target finish time: **~1h**

### Endpoints
```javascript
import express from "express";
import mysql from "mysql2";
import cors from "cors";

const app = express();
const port = 3000;

app.use(express.json());
app.use(cors());

const db = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "",
  database: "namedays",
});

// API endpoint to get nameday by date
app.get("/api/nameday/", (req, res) => {
  // Extract "date" from query parameter
  const date = req.query.date; // KEY

  // Check if date is specified
  if (!date) {
    return res.status(400).json({ error: "Date parameter is required" });
  }

  // get the month and day
  const month = date.split("-")[0];
  const monthName = convertMonthNumberToName(month);
  const day = date.split("-")[1];
  const sql = SELECT name1, name2 FROM nameday WHERE month = ${month} AND day = ${day};

db.query(sql, (err, result) => {
    if (err) {
      console.log("Server error");
    }
    if (result.length === 0) {
      console.log("No nameday found");
    }
    const nameday = result[0];

// Send response with formatted date and nameday data
    res.json({ // KEY
      date: `${monthName} ${day}.`,
      name1: nameday.name1,
      name2: nameday.name2,
    });
  });
});

// Function to convert month number to month name
function convertMonthNumberToName(monthNumber) {
  switch (monthNumber) {
    case "1":
      return "January";
    case "2":
      return "February";
    ...
  }
}

// Delete data by ID
app.delete("/api/nameday/:id", async (req, res)=>{
 const id = req.params.id; // Extracts the ID from the URL parameter, e.g., /api/nameday/123
  const sql = "DELETE FROM nameday WHERE id = ?";
  const [result] = await database.execute(sql, [id]);
  res.status(200).json(result);
})

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});

```

## Frontend
Target finish time: **~1h 30min**

### Import Bootstrap
```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4Q6Gf2aSP4eDXB8Miphtr37CMZZQ5oXLH2yaXMJ2w8e2ZtHTl7GptT4jmndRuHDT" crossorigin="anonymous">
```

### Display and submit cards dynamically using Bootstrap
```html
<div class="container">  <!-- To make the page responsive -->
   <form id="dateForm" class="mb-4">
      <div class="row g-3 align-items-end">
        <div class="col-auto">
          <label for="dateInput" class="form-label">Select Date:</label>
          <input type="date" id="dateInput" class="form-control" required>
        </div>
        <div class="col-auto">
          <button type="submit" class="btn btn-primary">Get Nameday</button>
        </div>
      </div>
    </form>
</div>


    <div id="namedayCards" class="row row-cols-1 row-cols-md-2 g-4"></div> // Place for the cards


    <script>
    // Handle form submission
    document.getElementById('dateForm').addEventListener('submit', async (e) => {
      e.preventDefault();
      const date = document.getElementById('dateInput').value;
      if (!date) return;

      // Clear previous cards
      const cardContainer = document.getElementById('namedayCards');
      cardContainer.innerHTML = '';

      // Fetch data from API
      try {
        const response = await fetch(`http://localhost:3000/api/nameday/?date=${date}`);
        if (!response.ok) {
          throw new Error('Failed to fetch nameday data');
        }
        const data = await response.json();

        // Check for error response
        if (data.error) {
          cardContainer.innerHTML = `<div class="alert alert-warning">${data.error}</div>`;
          return;
        }

        // Create Bootstrap cards for each name
        const names = [data.name1, data.name2];
        names.forEach(name => {
          const card = document.createElement('div');
          card.className = 'col';
          card.innerHTML = `
            <div class="card h-100">
              <div class="card-body">
                <h5 class="card-title">${name}</h5>
                <p class="card-text">Nameday on ${data.date}</p>
              </div>
            </div>
          `;
          cardContainer.appendChild(card);
        });
      } catch (error) {
        console.error('Error:', error);
        cardContainer.innerHTML = `<div class="alert alert-danger">Error fetching data</div>`;
      }
    });
  </script>
```
