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
