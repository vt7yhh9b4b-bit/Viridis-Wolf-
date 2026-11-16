# VIRIDIS WOLF

Prima base applicativa per il gestionale del centro cinofilo VIRIDIS WOLF.
Stack: Next.js + Supabase (autenticazione e database PostgreSQL con Row Level Security).

## Cosa comprende questa base
- Accesso e registrazione clienti con approvazione amministratore.
- Profili e anagrafiche clienti.
- Schede cane e note istruttore.
- Agenda settimanale con slot e prenotazioni.
- Inserimento giornate di chiusura per maltempo.
- Pubblicazione eventi e corsi.
- Tabelle predisposte per tessere, presenze e consensi.
- Interfaccia responsive e manifest PWA.

## Cosa NON è ancora pronto per uso commerciale
Questa è una base di sviluppo da configurare e collaudare, non un servizio già pubblicato.
Prima di inserire dati reali occorre completare test, gestione dei conflitti di prenotazione lato database, notifiche, QR scanner, documenti/consensi con versionamento, export report e verifiche legali/privacy. Il limite delle 48 ore nel database è una prima protezione per le prenotazioni; la gestione completa degli spostamenti e le eccezioni amministratore vanno testate e completate.
Non sono inclusi pagamenti né fatturazione elettronica.

## Avvio locale
1. Installa Node.js LTS.
2. Crea un progetto su Supabase.
3. In Supabase > SQL Editor esegui `supabase/schema.sql`.
4. Copia `.env.example` in `.env.local` e inserisci URL e anon key del progetto Supabase.
5. Esegui:
   ```bash
   npm install
   npm run dev
   ```
6. Apri `http://localhost:3000`.

## Crea il primo amministratore
1. Registrati dall'app con l'indirizzo email che userai come titolare.
2. In Supabase > Authentication > Users copia l'UUID dell'utente.
3. Nel SQL Editor esegui:
   ```sql
   update public.profiles
   set role='admin', approved=true
   where id='UUID-DEL-TUO-UTENTE';
   ```
4. Esci e rientra nell'app.

## Pubblicazione
Puoi pubblicare il progetto su un servizio hosting compatibile con Next.js (ad esempio Vercel) collegando il repository Git e impostando le stesse variabili d'ambiente. Il progetto Supabase resta il database condiviso.

## Nota privacy
I dati anagrafici, fiscali e le eventuali note relative ai cani sono informazioni da proteggere. Prima del go-live occorre definire informativa, tempi di conservazione, ruoli e autorizzazioni, backup, gestione delle richieste degli interessati e accordi con i fornitori. Non caricare dati reali finché il progetto non è configurato e verificato.
