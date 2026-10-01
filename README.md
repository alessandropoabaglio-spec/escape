# 🕸️ L'Ombra di Pontevecchio – Escape Night

Caccia al tesoro notturna a tema horror per le vie di Pontevecchio, giocata dal browser del telefono.
Ogni tappa ha un enigma che indica un luogo reale: lì i giocatori trovano un QR code da scansionare
(o una parola da inserire a mano) per sbloccare la tappa successiva. Le iniziali delle parole
formano l'acrostico finale.

## Grafica

Atmosfera di tempesta con pioggia, nebbia e lampi; ogni risposta giusta spezza un sigillo di ceralacca.
Le animazioni si riducono automaticamente se sul telefono è attiva l'opzione "riduci movimento".

## Come si gioca

1. Aprire il link del gioco sul telefono e premere **INIZIA** (serve un tocco per attivare l'audio).
2. Risolvere l'enigma, raggiungere il luogo, scansionare il QR o scrivere il codice.
3. I progressi restano salvati sul telefono: se la pagina si ricarica si riprende con **CONTINUA**.

## Struttura

```
index.html                 gioco completo (HTML, CSS, JS)
img/tappaN.jpg             foto/indizio della tappa N (da 0)
audio/sottofondo.mp3       musica di sottofondo in loop
audio/errore.mp3           suono risposta sbagliata
audio/vittoria.mp3         suono tappa superata
audio/finale.mp3           brano della schermata finale
js/html5-qrcode.min.js     libreria scanner QR v2.3.8 (Apache-2.0)
```

## Modificare le tappe

Le tappe sono nell'array `STEPS` dentro `index.html`: numero (`num`), titolo (`name`), paragrafi dell'enigma (`paras`) e `hash` della risposta.
Le risposte non sono scritte in chiaro ma come impronta SHA-256 della parola in maiuscolo senza accenti.

Per cambiare una parola:

1. aprire il gioco nel browser, aprire la console (F12);
2. digitare `await sha256("NUOVAPAROLA")` e premere Invio;
3. copiare il risultato nel campo `hash` della tappa;
4. rigenerare il QR code con la nuova parola.

Per aggiungere una tappa basta aggiungere un elemento a `STEPS` e la foto `img/tappaN.jpg`.

> Nota: l'hash impedisce di leggere le soluzioni con un'occhiata al codice, ma non è una protezione
> assoluta. Per eventi "seri" conviene rendere il repository privato o cambiare le parole prima di ogni edizione
> (la cronologia Git contiene le versioni precedenti).

## Pubblicazione

Il gioco è statico e gira su GitHub Pages (Settings → Pages → Deploy from a branch → `main`, cartella `/ (root)`).
Indirizzo: https://alessandropoabaglio-spec.github.io/escape/
Serve HTTPS per fotocamera e controllo delle risposte, quindi non aprirlo come file locale ma da Pages
o da un server locale (`python3 -m http.server`).

## Audio

Usare solo brani di cui si hanno i diritti o royalty-free (es. Pixabay Music, Free Music Archive con licenza CC).
Per cambiare il brano finale basta sostituire `audio/finale.mp3`.
