# 🔊 SoundCloud Cast Remote

Zdalne sterowanie odtwarzaczem SoundCloud na komputerze bezpośrednio z telefonu — bez logowania się do żadnego konta, bez chmury poza publicznym serwerem sygnalizacyjnym PeerJS. Połączenie telefon ↔ komputer idzie peer-to-peer przez WebRTC.

**Strona zdalna:** https://polini121.github.io/SoundCloud-Cast-Remote/

## Jak to działa

Projekt składa się z dwóch części:

1. **Rozszerzenie do Chrome** (folder rozszerzenia, instalowane lokalnie w przeglądarce na komputerze) — działa w tle na karcie soundcloud.com, steruje odtwarzaczem i wystawia połączenie PeerJS.
2. **Strona zdalna** (`index.html` w tym repo, hostowana przez GitHub Pages) — otwierana w przeglądarce telefonu, łączy się z komputerem po krótkim kodzie parowania pokazywanym w popupie rozszerzenia.

```
[Telefon: strona index.html] <--WebRTC (PeerJS)--> [Rozszerzenie Chrome: offscreen document] <--chrome.tabs--> [Karta soundcloud.com]
```

Rozszerzenie w tle nie hostuje samego połączenia WebRTC (service worker w Manifest V3 nie ma do tego dostępu) — do tego celu używa dokumentu offscreen (`chrome.offscreen`), który ma pełne wsparcie WebRTC.

## Funkcje

- ▶️ Play / pauza, następny / poprzedni utwór
- 🔀 Losowo, 🔁 Powtarzaj — z odczytem prawdziwego stanu z SoundCloud
- ❤️ Lubię to — zsynchronizowane z rzeczywistym stanem na komputerze
- 🔊 Głośność góra/dół, wyciszenie
- ⏱️ Pasek przewijania z aktualnym/całkowitym czasem
- 🖼️ Podgląd okładki, tytułu i wykonawcy na bieżąco

## Instalacja

### 1. Rozszerzenie (na komputerze)

1. Pobierz i rozpakuj `soundcloud-cast-fixed.zip` (z sekcji [Releases](../../releases)).
2. Wejdź w `chrome://extensions`.
3. Włącz **Tryb dewelopera** (prawy górny róg).
4. Kliknij **Załaduj rozpakowane** i wskaż rozpakowany folder.
5. Otwórz [soundcloud.com](https://soundcloud.com) i puść jakiś utwór.

### 2. Parowanie z telefonem

1. Kliknij ikonę rozszerzenia w pasku Chrome — pokaże się kod parowania i link.
2. Otwórz ten link na telefonie (np. przez zeskanowanie/wklejenie) albo wejdź na https://polini121.github.io/SoundCloud-Cast-Remote/ i wpisz kod ręcznie.
3. Gotowe — sterowanie z telefonu powinno działać na żywo.

> Kod parowania zmienia się po kliknięciu "Wygeneruj nowy kod" w popupie rozszerzenia.

## Wymagania

- Google Chrome (lub przeglądarka oparta na Chromium) na komputerze, z otwartą kartą soundcloud.com.
- Dowolna przeglądarka na telefonie z dostępem do internetu.

## Znane ograniczenia

- Rozszerzenie musi mieć otwartą kartę soundcloud.com na komputerze, żeby sterowanie działało.
- Sterowanie opiera się o selektory CSS strony SoundCloud — zmiana układu strony przez SoundCloud może wymagać aktualizacji `content.js`.
- Połączenie działa przez publiczny serwer sygnalizacyjny PeerJS (`0.peerjs.com`) — sam strumień sterowania idzie peer-to-peer, ale wymaga dostępu do internetu po obu stronach.

## Stack technologiczny

- [PeerJS](https://peerjs.com/) (WebRTC) — połączenie telefon ↔ komputer
- Manifest V3 (Chrome Extensions) — `background.js` (service worker) + `offscreen.js` (dokument offscreen hostujący WebRTC)
- Zwykły HTML/CSS/JS — bez frameworków, bez buildów

## Licencja

Projekt hobbystyczny / na własny użytek.
