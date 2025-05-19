# Vizsga-Jegyzet

**Ami várhatóan közös minden feladatban:**

> [!WARNING]  
> Az `index.js`-ben állítsd be a db portot `port: 3307` ha kell


```bash
mkdir vizsga
cd vizsga
mkdir forras
mkdir asztali
mkdir backend
cd backend
npm i express mysql2 cors
npm pkg set type=module
echo import express from 'express'; > index.js
echo import cors from 'cors'; >> index.js
echo import mysql from 'mysql2'; >> index.js
echo. >> index.js
echo const app = express(); >> index.js
echo app.use(cors()); >> index.js
echo app.use(express.json()); >> index.js
echo. >> index.js
echo const db = mysql.createConnection(^{ >> index.js
echo     host: 'localhost', >> index.js
echo     user: 'root', >> index.js
echo     password: '', >> index.js
echo     database: 'adatbazis_nev', >> index.js
echo     port: 3306 // esetenkent 3307 >> index.js
echo }); >> index.js
echo. >> index.js
echo // vegpontok >> index.js
echo. >> index.js
echo // Create / Post >> index.js
echo app.post('/', (req, res) =^> ^{  >> index.js
echo   const { value1, value2} = req.body; >> index.js
echo   db.query( >> index.js
echo     'INSERT INTO tabla_nev (value1, value2) VALUES ( ?, ?)', >> index.js
echo     [value1, value2], >> index.js
echo     (err, result) =^> ^{ >> index.js
echo       if (err) { >> index.js
echo        console.error('Create error:', err); >> index.js
echo        return res.status(500).json({ message: 'Create error.' }); >> index.js
echo      } >> index.js
echo      res.json({ value1, value2}); >> index.js
echo    } >> index.js
echo  ); >> index.js
echo }); >> index.js
echo. >> index.js
echo // Read / Get >> index.js
echo app.get('/', (req, res) =^> ^{ >> index.js
echo  db.query('SELECT * FROM tabla_nev', (err, results) =^> ^{ >> index.js
echo    if (err) { >> index.js
echo      console.error('Read error:', err); >> index.js
echo      return res.status(500).json({ message: 'Read error.' }); >> index.js
echo    } >> index.js
echo    res.json(results); >> index.js
echo  }); >> index.js
echo }); >> index.js
echo. >> index.js
echo // Update / Put >> index.js
echo app.put('/:id', (req, res) =^> ^{ >> index.js
echo  const { value1, value2} = req.body; >> index.js
echo  db.query( >> index.js
echo    'UPDATE tabla_nev SET value1 = ?, value2 = ? WHERE id = ?', >> index.js
echo    [value1, value2, req.params.id], >> index.js
echo    (err, result) =^> ^{ >> index.js
echo      if (err) { >> index.js
echo        console.error('Update error:', err); >> index.js
echo        return res.status(500).json({ message: 'Update error.' }); >> index.js
echo      } >> index.js
echo      res.sendStatus(204); >> index.js
echo    } >> index.js
echo  ); >> index.js
echo }); >> index.js
echo. >> index.js
echo // Delete >> index.js
echo app.delete('/:id', (req, res) =^> ^{ >> index.js
echo  db.query('DELETE FROM tabla_nev WHERE id = ?', [req.params.id], (err, result) =^> ^{ >> index.js
echo    if (err) { >> index.js
echo      console.error('Delete error:', err); >> index.js
echo      return res.status(500).json({ message: 'Delete error.' }); >> index.js
echo    } >> index.js
echo    res.sendStatus(204); >> index.js
echo  }); >> index.js
echo }); >> index.js
echo. >> index.js
echo app.listen(3000, () =^> ^{ >> index.js
echo     console.log('Server is running on http://localhost:3000'); >> index.js
echo }); >> index.js

cd ..
npm create vite@latest frontend -- --template react
y
cd frontend
npm install
npm pkg set type=module
npm install axios react-router-dom
npm install react-bootstrap bootstrap bootstrap-icons 
exit

```

> [!WARNING]  
> Mindkét `package.json`-ban állítsd be `"type": "module"` 
----

> [!WARNING]
> `src/main.jsx` Ha bootstrap nelkul hasznalod
```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>,
)
```
> [!WARNING]
> `src/App.jsx` Ha bootstrap nelkul hasznalod
`src/App.jsx`
```jsx
import React from 'react'
import { Routes, Route, Link } from 'react-router-dom'
import Home from './pages/Home'
import About from './pages/About'

export default function App() {
  return (
    <div>
      <nav style={{ display: 'flex', gap: '1rem' }}>
        <Link to="/">Főoldal</Link>
        <Link to="/about">Rólunk</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </div>
  )
}
```
> [!TIP]
> `src/pages/Home.jsx`
```jsx
import React, { useEffect, useState } from 'react'
import axios from 'axios'

export default function Home() {
  const [data, setData] = useState(null)

  useEffect(() => {
    axios.get('https://jsonplaceholder.typicode.com/posts/1')
      .then(response => setData(response.data))
      .catch(error => console.error('Hiba történt:', error))
  }, [])

  return (
    <div>
      <h1>Főoldal</h1>
      {data ? (
        <div>
          <h2>{data.title}</h2>
          <p>{data.body}</p>
        </div>
      ) : (
        <p>Betöltés...</p>
      )}
    </div>
  )
}
```
> [!TIP]
> `src/pages/About.jsx`
```jsx
import React from 'react'

export default function About() {
  return (
    <div>
      <h1>Rólunk</h1>
      <p>Ez egy példa React alkalmazás a Vite használatával.</p>
    </div>
  )
}
```
> [!TIP]
> `App.jsx` a menü Bootstrap-el
```jsx
import { BrowserRouter } from 'react-router-dom'
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.bundle.min'
import 'bootstrap-icons/font/bootstrap-icons.css'
import {  Routes, Route, Link } from 'react-router-dom'
import Home from './pages/Home'
import About from './pages/About'

export default function App() {
  return (
    <BrowserRouter>

      <div>
        <nav className="navbar navbar-expand-lg navbar-light bg-light">
          <div className="container-fluid">
            <Link className="navbar-brand" to="/">Weboldalam</Link>
            <button
              className="navbar-toggler"
              type="button"
              data-bs-toggle="collapse"
              data-bs-target="#navbarNav"
              aria-controls="navbarNav"
              aria-expanded="false"
              aria-label="Toggle navigation"
            >
              <span className="navbar-toggler-icon"></span>
            </button>
            <div className="collapse navbar-collapse" id="navbarNav">
              <ul className="navbar-nav">
              <li className="nav-item">
                  <Link className="nav-link" to="/">Főoldal</Link>
                </li>
                <li className="nav-item">
                  <Link className="nav-link" to="/about">Rólunk</Link>
                </li>
              </ul>
            </div>
          </div>
        </nav>

        <div className="container mt-4">
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
          </Routes>
        </div>
      </div>
    </BrowserRouter>
  )
}
```
> [!WARNING]  
> A `App.css` illetve az `index.css` tartalmat torolni kell a Bootstrap miatt.

# FRONTEND JEGYZETEK

`src/pages/CRUD.jsx`
```jsx
import React, { useEffect, useState } from 'react'
import axios from 'axios'

const API_URL = 'http://localhost:3000' // Vagy a sajat API-d

export default function CRUD() {
  const [emberek, setEmberek] = useState([])
  const [ujEmber, setUjEmber] = useState({ nev: '', kor: '' })
  const [szerkesztesId, setSzerkesztesId] = useState(null)
  const [szerkesztett, setSzerkesztett] = useState({ nev: '', kor: '' })

  useEffect(() => {
    lekertEmberek()
  }, [])

  const lekertEmberek = async () => {
    try {
      const res = await axios.get(API_URL)
      setEmberek(res.data)
    } catch (err) {
      console.error('Lekérési hiba:', err)
    }
  }

  const hozzaadas = async () => {
    try {
      await axios.post(API_URL, ujEmber)
      setUjEmber({ nev: '', kor: '' })
      lekertEmberek()
    } catch (err) {
      console.error('Hozzáadási hiba:', err)
    }
  }

  const mentes = async (id) => {
    try {
      await axios.put(`${API_URL}/${id}`, szerkesztett)
      setSzerkesztesId(null)
      setSzerkesztett({ nev: '', kor: '' })
      lekertEmberek()
    } catch (err) {
      console.error('Frissítési hiba:', err)
    }
  }

  const torles = async (id) => {
    try {
      await axios.delete(`${API_URL}/${id}`)
      lekertEmberek()
    } catch (err) {
      console.error('Törlési hiba:', err)
    }
  }

  return (
    <div>
      <h1>Emberek kezelése</h1>

      {/* Új ember hozzáadása */}
      <div>
        <h3>Új ember</h3>
        <input
          placeholder="Név"
          value={ujEmber.nev}
          onChange={(e) => setUjEmber({ ...ujEmber, nev: e.target.value })}
        />
        <input
          placeholder="Kor"
          type="number"
          value={ujEmber.kor}
          onChange={(e) => setUjEmber({ ...ujEmber, kor: e.target.value })}
        />
        <button
          style={{ backgroundColor: 'green', color: 'white' }}
          onClick={hozzaadas}
        >
          Hozzáadás
        </button>
      </div>

      <hr />

      {/* Emberek listázása */}
      {emberek.map((ember) => (
        <div key={ember.id} style={{ border: '1px solid gray', margin: '10px', padding: '10px' }}>
          {szerkesztesId === ember.id ? (
            <div>
              <input
                value={szerkesztett.nev}
                onChange={(e) => setSzerkesztett({ ...szerkesztett, nev: e.target.value })}
              />
              <input
                type="number"
                value={szerkesztett.kor}
                onChange={(e) => setSzerkesztett({ ...szerkesztett, kor: e.target.value })}
              />
              <button
                style={{ backgroundColor: 'orange', color: 'white' }}
                onClick={() => mentes(ember.id)}
              >
                Mentés
              </button>
              <button
                style={{ backgroundColor: 'gray', color: 'white' }}
                onClick={() => setSzerkesztesId(null)}
              >
                Mégse
              </button>
            </div>
          ) : (
            <div>
              <h3>{ember.nev}</h3>
              <p>Kor: {ember.kor}</p>
              <button
                style={{ backgroundColor: 'blue', color: 'white' }}
                onClick={() => {
                  setSzerkesztesId(ember.id)
                  setSzerkesztett({ nev: ember.nev, kor: ember.kor })
                }}
              >
                Szerkesztés
              </button>
              <button
                style={{ backgroundColor: 'red', color: 'white', marginLeft: '10px' }}
                onClick={() => torles(ember.id)}
              >
                Törlés
              </button>
            </div>
          )}
        </div>
      ))}
    </div>
  )
}
```

`src/App.jsx`
```jsx
import { BrowserRouter } from 'react-router-dom'
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.bundle.min'
import 'bootstrap-icons/font/bootstrap-icons.css'
import {  Routes, Route, Link } from 'react-router-dom'
import Home from './pages/Home'
import About from './pages/About'
import CRUD from './pages/CRUD'

export default function App() {
  return (
    <BrowserRouter>

      <div>
        <nav className="navbar navbar-expand-lg navbar-light bg-light">
          <div className="container-fluid">
            <Link className="navbar-brand" to="/">Weboldalam</Link>
            <button
              className="navbar-toggler"
              type="button"
              data-bs-toggle="collapse"
              data-bs-target="#navbarNav"
              aria-controls="navbarNav"
              aria-expanded="false"
              aria-label="Toggle navigation"
            >
              <span className="navbar-toggler-icon"></span>
            </button>
            <div className="collapse navbar-collapse" id="navbarNav">
              <ul className="navbar-nav">
              <li className="nav-item">
                  <Link className="nav-link" to="/">Főoldal</Link>
                </li>
                <li className="nav-item">
                  <Link className="nav-link" to="/about">Rólunk</Link>
                </li>
                <li className="nav-item">
                  <Link className="nav-link" to="/CRUD">CRUD</Link>
                </li>
              </ul>
            </div>
          </div>
        </nav>

        <div className="container mt-4">
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/CRUD" element={<CRUD />} />
          </Routes>
        </div>
      </div>
    </BrowserRouter>
  )
}
```




# Desktop
### SelectedIndex
```csharp
private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
 {
     int index = listBox1.SelectedIndex;
     if (index >= 0 && index < fuggohidak.Count)
     {
         Fuggohid kivalasztott = fuggohidak[index];

         textBox1.Text = kivalasztott.helyszin;
         textBox2.Text = kivalasztott.orszag;
         textBox3.Text = kivalasztott.ev.ToString();
         textBox4.Text = kivalasztott.hossz.ToString();
     }
 }
 
  private void button_ChoiceInsert_Click(object sender, EventArgs e)
        {
            //Átlépés másik formba
            FormGuest formGuest = new FormGuest();
            formGuest.Show();
            this.Close();

        }
```


## Hegyes feladat

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

## Emberes feladat
`ember.cs` Class
```csharp
 public int id { get; set; }
 public string nev { get; set; }
 public int kor { get; set; }

 public Ember(int id, string nev, int kor)
 {
     this.id = id;
     this.nev = nev;
     this.kor = kor;
 }
```
`program.cs`
```csharp
public Form1()
{
    InitializeComponent();
}
int id = 0; // Globális változó az ID-hez
private void Form1_Load(object sender, EventArgs e)
{

}
private void button1_Click(object sender, EventArgs e)
{
    OpenFileDialog openFileDialog = new OpenFileDialog();

    // Beállítások (opcionális)
    openFileDialog.InitialDirectory = "C:\\";
    openFileDialog.Filter = "CSV fájlok (*.csv)|*.csv|Minden fájl (*.*)|*.*";
    openFileDialog.FilterIndex = 1;
    openFileDialog.RestoreDirectory = true;

    // Ha a felhasználó kiválasztott egy fájlt
    if (openFileDialog.ShowDialog() == DialogResult.OK)
    {
        // Fájl elérési útja
        string filePath = openFileDialog.FileName;

        // Például: kiírjuk egy Label-re vagy feldolgozzuk
        MessageBox.Show("Kiválasztott fájl: " + filePath);

        List<Ember> emberek = new List<Ember>();

        FileStream folyam = new FileStream(filePath, FileMode.Open);
        StreamReader olvas = new StreamReader(folyam);

        string elso = olvas.ReadLine();
        string[] resz;

        while (!olvas.EndOfStream)
        {
            elso = olvas.ReadLine();

            resz = elso.Split(';');
            Ember personList = new Ember(int.Parse(resz[0]), resz[1], int.Parse(resz[2]));
            emberek.Add(personList);
            id++;
        }
        olvas.Close();
        folyam.Close();

        // A lista feltöltése
        for (int i = 0; i < emberek.Count; i++)
        {
            // listBox
            listBox1.Items.Add(emberek[i].id + ", " + emberek[i].nev + ", " + emberek[i].kor);
        }
    }
}

private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
{
    if (listBox1.SelectedItem != null)
    {
        // Kiválasztott sor szövege
        string selectedLine = listBox1.SelectedItem.ToString();

        // Sor feldarabolása pontosvessző mentén
        string[] parts = selectedLine.Split(',');

        if (parts.Length == 3)
        {
            textBox_id.Text = parts[0];
            textBox_nev.Text = parts[1];
            textBox_kor.Text = parts[2];
        }
    }
}

private void button_Create_Click(object sender, EventArgs e)
{
    id++;
    listBox1.Items.Add(id + ", " + textBox_nev.Text + ", " + textBox_kor.Text);
    
}

private void button_Update_Click(object sender, EventArgs e)
{
    string updatedLine = $"{textBox_id.Text}, {textBox_nev.Text}, {textBox_kor.Text}";

    // Kijelölt elem cseréje az új értékre
    int selectedIndex = listBox1.SelectedIndex;
    listBox1.Items[selectedIndex] = updatedLine;
}

private void button_Delete_Click(object sender, EventArgs e)
{
    listBox1.Items.Remove(listBox1.SelectedItem);
}
```

export to `bin/Debug`
```csharp
private void button_export_Click(object sender, EventArgs e)
{
    string fileName = "exportalt_adatok.csv";
    string exportPath = Path.Combine(Application.StartupPath, fileName);

    using (StreamWriter writer = new StreamWriter(exportPath, false, Encoding.UTF8))
    {
        // Fejléc (ha kell)
        writer.WriteLine("id;nev;kor");

        foreach (var item in listBox1.Items)
        {
            string line = item.ToString(); // "id, nev, kor"
            string[] parts = line.Split(','); // [id, nev, kor]

            // Trim miatt: szóközök eltávolítása
            string formattedLine = $"{parts[0].Trim()};{parts[1].Trim()};{parts[2].Trim()}";
            writer.WriteLine(formattedLine);
        }
        MessageBox.Show("Exportálás kész: " + exportPath);
        writer.Close();
    }
}
```
export to `kivalasztott hely`
```csharp
private void button_export_Click(object sender, EventArgs e)
{
    SaveFileDialog saveFileDialog = new SaveFileDialog();
    saveFileDialog.Filter = "CSV fájlok (*.csv)|*.csv";
    saveFileDialog.Title = "Mentés CSV fájlba";
    saveFileDialog.FileName = "kimentett_adatok.csv";

    if (saveFileDialog.ShowDialog() == DialogResult.OK)
    {
        try
        {
            using (StreamWriter writer = new StreamWriter(saveFileDialog.FileName, false, Encoding.UTF8))
            {
                // Fejléc (ha kell)
                writer.WriteLine("id;nev;kor");

                foreach (var item in listBox1.Items)
                {
                    string line = item.ToString(); // "id, nev, kor"
                    string[] parts = line.Split(','); // [id, nev, kor]

                    // Trim miatt: szóközök eltávolítása
                    string formattedLine = $"{parts[0].Trim()};{parts[1].Trim()};{parts[2].Trim()}";
                    writer.WriteLine(formattedLine);
                }
            }

            MessageBox.Show("Sikeres exportálás!");
        }
        catch (Exception ex)
        {
            MessageBox.Show("Hiba történt: " + ex.Message);
        }
    }
}
```








## String Override
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
