
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
