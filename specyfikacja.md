# Specyfikacja gry „Asteroids” (Godot Engine)

## 1. Opis funkcjonalności

### 1.1. Logika gry
Gra jest klasyczną interpretacją „Asteroids”, w której gracz steruje statkiem kosmicznym, unika asteroid i niszczy je za pomocą pocisków.

#### Funkcje główne:
- Sterowanie statkiem gracza.
- Strzelanie pociskami generowanymi przez statek.
- Kolizje pocisków z asteroidami.
- Kolizje gracza z asteroidami skutkujące utratą życia.
- Respawn gracza po śmierci (jeśli pozostały życia).
- System punktacji zależny od rozmiaru zniszczonej asteroidy.
- System żyć (domyślnie 3).
- Ekran Game Over po utracie wszystkich żyć.
- Możliwość zresetowania gry poprzez akcję „Reset”.

---

### 1.2. Asteroidy
Asteroidy występują w trzech rozmiarach:
- **LARGE**
- **MEDIUM**
- **SMALL**

#### Zachowanie asteroid:
- LARGE → po zniszczeniu generują 2 × MEDIUM  
- MEDIUM → po zniszczeniu generują 2 × SMALL  
- SMALL → nie generują nowych asteroid  
- Każda asteroida emituje sygnał `exploded`, przekazując:
  - pozycję eksplozji,
  - rozmiar,
  - liczbę punktów.

---

### 1.3. Gracz
Gracz posiada:
- możliwość strzelania (sygnał `bullet_shot`),
- możliwość śmierci (sygnał `died`),
- funkcję `respawn(position)` wywoływaną po utracie życia.

#### Zachowanie po śmierci:
- jeśli pozostały życia → respawn po 1 sekundzie,
- jeśli brak żyć → po 2 sekundach wyświetlany jest ekran Game Over.

---

### 1.4. Interfejs użytkownika (HUD)
HUD zawiera:
- aktualny wynik,
- liczbę żyć,
- ekran Game Over (domyślnie ukryty).

HUD jest aktualizowany automatycznie poprzez settery zmiennych:
- `score`,
- `lives`.

---

### 1.5. System punktacji
Punkty przyznawane są w zależności od rozmiaru asteroidy (wartości przekazywane przez sygnał `exploded`):
- LARGE → najwięcej punktów,
- MEDIUM → średnio,
- SMALL → najmniej.

---

### 1.6. Reset gry
Naciśnięcie akcji `Reset` powoduje:
- przeładowanie aktualnej sceny (`get_tree().reload_current_scene()`).

---

## 2. Wygląd aplikacji

### 2.1. Styl graficzny
Gra utrzymana jest w minimalistycznym stylu retro:
- czarne tło imitujące przestrzeń kosmiczną,
- jasne, wektorowe obiekty (statek, asteroidy, pociski),
- proste, geometryczne kształty.

---

### 2.2. Rozmieszczenie elementów
- **Statek gracza** — startuje w pozycji `PlayerSpawnPos`.
- **Asteroidy** — rozmieszczone wstępnie lub generowane dynamicznie.
- **HUD**:
  - lewy górny róg → wynik,
  - prawy górny róg → liczba żyć.
- **Game Over Screen** — wyśrodkowany, widoczny po utracie wszystkich żyć.

---

### 2.3. Animacje i efekty
- efekt eksplozji asteroid,
- płynne poruszanie obiektów,
- opcjonalny efekt pojawiania się gracza po respawnie.

---

## 3. Wymagania techniczne

### 3.1. Wymagania sprzętowe (minimalne)
- CPU: dowolny dwurdzeniowy procesor,
- RAM: 2 GB,
- GPU: obsługa OpenGL 3.3,
- System: Windows / Linux / macOS.

---

### 3.2. Wymagania silnika
- Godot Engine **4.x**,
- GDScript 2.0,
- wymagane sceny:
  - `asteroid.tscn`,
  - scena główna zawierająca:
    - Node2D (root),
    - Player,
    - Asteroids (Node2D),
    - Bullets (Node2D),
    - UI (CanvasLayer),
    - HUD,
    - GameOverScreen,
    - PlayerSpawnPos (Position2D).

---

### 3.3. Struktura projektu
res://
├─ assets/
	├─ scenes/
	│   ├─ asteroid.tscn
	│   ├─ player.tscn
	│   ├─ ul_life.tscn
	│   ├─ hud.tscn
	│   ├─ bullet.tscn
	│   ├─ game_over_scene.tscn
	│   └─ game.tscn
	├─ scripts/
	│   ├─ asteroid.gd
	│   ├─ player.gd
	│   ├─ game.gd
	│   ├─ game_over_scene.gd
	│   ├─ bullet.gd
	│   └─ hud.gd
	├─ UI/
	│   ├─ HUD.tscn
	│   └─ GameOverScreen.tscn


---

### 3.4. Wymagania dotyczące wejścia (Input Map)
| Akcja | Opis |
|-------|------|
| `Reset` | reset gry |
| `shoot` | strzał gracza |
| `move_left` / `move_right` | obrót statku |
| `thrust` | przyspieszenie statku |

---

## 4. Podsumowanie
Specyfikacja opisuje pełną logikę gry, interfejs, strukturę projektu i wymagania techniczne. Dokument może być używany jako baza do dalszego rozwoju gry lub jako dokumentacja projektowa.
