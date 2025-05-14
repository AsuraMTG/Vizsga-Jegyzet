# BACKEND JEGYZETEK
## Create / Post
`app.post`
```js
app.post('/', async (req, res) => {
  const { ertek1, ertek2, ertek3} = req.body;
  const [result] = await pool.query(
    'INSERT INTO database (database_ertek1, database_ertek2, database_ertek3) VALUES (?, ?, ?)',
    [ertek1, ertek2, ertek3]
  );
  res.json({
    ertek1,
    ertek2,
    ertek3
  });
});
```
## Read / Get
`app.get`
```js
app.get('/', async (req, res) => {
  try {
    const [rows] = await pool.query(`SELECT * FROM database`);
    res.json(rows);
  } catch (err) {
    res.status(500).json({ message: 'Fetching from database failed.' });
  }
});
```
## Update / Put
`app.put`
```js
app.put('/:id', async (req, res) => {
  const { ertek1, ertek2, ertek3} = req.body;
  await pool.query(
    'UPDATE database SET database_ertek1 = ?, database_ertek2 = ?, database_ertek3 = ? WHERE id = ?',
    [ertek1, ertek2, ertek3, req.params.id]
  );
  res.sendStatus(204);
});
```
## Delete
`app.delete`
```js
app.delete('/:id', async (req, res) => {
  await pool.query('DELETE FROM database WHERE id = ?', [req.params.id]);
  res.sendStatus(204);
});
```
