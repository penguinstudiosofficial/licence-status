# licence-status

Un solo file, firmato: [`licence-status.json`](./licence-status.json).

Serve a una cosa sola. I prodotti PenguinStudios chiedono a `penguinstudios.eu` se possono
funzionare. Quando quel server non risponde continuano a funzionare per il periodo di grazia
che avevano in mano all'ultima validazione riuscita — ma **un plugin che non riesce a
raggiungerci non può essere avvisato da noi che siamo noi a essere giù**, né sapere quanto
durerà.

Questo file lo dice, da un posto che non è il nostro server. Non contiene licenze, non può
concederne né revocarne, e non sa nemmeno chi lo sta leggendo. Dice soltanto: *lo studio sa,
dura tanto così, continua a funzionare*.

## Come si legge

```json
{
  "document": {
    "schema": "penguinstudios.licence-status/1",
    "status": "operational | incident | resolved",
    "issuedAt": "...",
    "expiresAt": "...",
    "message": "una frase in inglese",
    "graceDays": null,
    "resolvedGraceDays": null,
    "contact": "https://discord.penguinstudios.eu"
  },
  "signature": "...",
  "algorithm": "ed25519"
}
```

Regole per chi lo consuma:

1. **Si legge solo dopo un fallimento.** Mai al posto della validazione normale.
2. **Si verifica la firma** sul `document` serializzato in forma canonica, con questa chiave
   pubblica Ed25519 (32 byte, raw):

   ```
   h1LHctxUd3/bA/ELLpNVwOEAqbocfy3b3YvLpCLg+/o=
   ```

   Una firma che non torna vale come nessuna risposta. Chiunque controlli questo host può
   cambiare il file; non può firmarlo.
3. **Scaduto è come assente.** Passato `expiresAt`, il documento non vale più: un "va tutto
   bene" vecchio tiene in piedi i prodotti di uno studio che non esiste più.
4. **`graceDays` allunga, non accorcia.** Un valore più basso della grazia che il plugin sta
   già contando va ignorato. Un documento che può ridurre una grazia è un documento che può
   spegnere prodotti da remoto.

## Perché è qui e non su penguinstudios.eu

Perché è l'unico host garantito irraggiungibile nel momento in cui questo file serve.

## Contatti

[discord.penguinstudios.eu](https://discord.penguinstudios.eu)
