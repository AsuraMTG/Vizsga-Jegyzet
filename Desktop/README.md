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
