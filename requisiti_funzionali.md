# Documento dei Requisiti Funzionali  
**Applicazione:** Personal Finance Manager (PFM)  
**Backend:** NestJS  
**Frontend:** React  

---

## 1. Introduzione  
L'applicazione PFM consente agli utenti di gestire spese, entrate e analizzare i propri flussi finanziari attraverso dashboard interattive.  
**Obiettivo:** Fornire un tool centralizzato per il monitoraggio finanziario personale con automazione e personalizzazione avanzata.  

---

## 2. Requisiti Funzionali  

### 2.1 Autenticazione e Gestione Profilo  
#### 2.1.1 Social Login  
- **FR-01:** L'utente deve poter accedere utilizzando account Google (OAuth 2.0).  
- **FR-02:** L'utente deve poter accedere utilizzando account Apple (Sign in with Apple).  
- **FR-03:** Il sistema deve memorizzare solo l'ID univoco fornito dal provider sociale (no password).  

#### 2.1.2 Registrazione Tradizionale  
- **FR-04:** L'utente può registrarsi con email e password (conferma via OTP).  
- **FR-05:** Il sistema deve validare la complessità della password (min. 8 caratteri, 1 numero, 1 carattere speciale).  

#### 2.1.3 Profilo Utente  
- **FR-06:** L'utente può modificare:  
  - Valuta predefinita (supporto per EUR, USD, GBP, etc.).  
  - Fuso orario.  
  - Notifiche preferite (email/push).  
- **FR-07:** L'utente può eliminare l'account (con conferma e cancellazione di tutti i dati associati).  

---

### 2.2 Gestione Transazioni  
#### 2.2.1 Inserimento Manuale  
- **FR-08:** L'utente può aggiungere una transazione (spesa/entrata) con:  
  - Importo (obbligatorio, positivo per entrate, negativo per spese).  
  - Data (default: corrente).  
  - Categoria (selezione da lista predefinita o personalizzata).  
  - Descrizione (max 200 caratteri).  
  - Tag multipli (es. #viaggio, #casa).  
- **FR-09:** Le categorie predefinite devono includere almeno:  
  `Casa, Trasporti, Alimentazione, Salute, Intrattenimento, Istruzione`.  

#### 2.2.2 Modifica/Eliminazione Transazioni  
- **FR-10:** L'utente può modificare/eliminare una transazione esistente (con conferma per l'eliminazione).  
- **FR-11:** Le modifiche devono essere registrate in un log di audit (data/ora, utente, azione).  

#### 2.2.3 Transazioni Ricorrenti (Fase 2)  
- **FR-12:** L'utente può impostare transazioni ricorrenti con:  
  - Frequenza (giornaliera, settimanale, mensile, annuale).  
  - Data di inizio/fine.  
  - Opzione di sospensione temporanea.  

---



### 2.3 Integrazione con Istituti Bancari 
<!-- NOTA: L'integrazione con gli istituti bancari verrà implementata in una release successiva. Attualmente non è disponibile. -->

#### 2.3.1 Collegamento Conti  
- **FR-13:** L'utente può collegare uno o più conti bancari tramite API (es. Plaid, Yodlee, o PSD2 per l'Europa).  
- **FR-14:** Il sistema deve supportare l'autenticazione a più fattori (2FA) richiesta dalle banche.  

#### 2.3.2 Sincronizzazione Automatica  
- **FR-15:** Le transazioni bancarie devono essere importate ogni 24h o in tempo reale (se supportato dalla banca).  
- **FR-16:** Le transazioni importate devono essere categorizzate automaticamente (basato su regole utente o machine learning).  

#### 2.3.3 Sicurezza Dati Bancari  
- **FR-17:** Le credenziali bancarie devono essere crittografate end-to-end (AES-256) e non memorizzate in plain text.  
- **FR-18:** L'utente può revocare l'accesso a un conto bancario in qualsiasi momento.  

---

### 2.4 Dashboard e Reportistica  
#### 2.4.1 Visualizzazione Dati  
- **FR-19:** La dashboard deve mostrare:  
  - Grafico a torta: Distribuzione spese/entrate per categoria.  
  - Istogramma: Confronto mensile/annuo.  
  - Totale netto (entrate - spese).  
- **FR-20:** L'utente può filtrare i dati per intervallo temporale (mese/anno/personalizzato).  

#### 2.4.2 Esportazione Dati  
- **FR-21:** L'utente può esportare transazioni in formato CSV o PDF.  
- **FR-22:** I report PDF devono includere logo personalizzato e dati utente (nome, email).  

---

### 2.5 Budgeting (Fase 2)  
- **FR-23:** L'utente può impostare un budget mensile per categoria.  
- **FR-24:** Il sistema deve mostrare un avviso visivo quando la spesa supera l'80% del budget.  
- **FR-25:** Confronto automatico tra budget e spese effettive (grafico a barre sovrapposte).  

---

### 2.6 Notifiche  
- **FR-26:** Notifiche push/email per:  
  - Transazioni ricorrenti in scadenza (24h prima).  
  - Soglie di spesa superate (configurabile dall'utente).  
  - Attività sospette (es. transazioni sopra X€ in Paesi non abituali).  

---

### 2.7 Multi-Utente (Fase 3)  
- **FR-27:** Un utente può invitare altri utenti a condividere categorie/transazioni specifiche.  
- **FR-28:** Assegnazione ruoli:  
  - **Admin:** Gestione completa.  
  - **Editor:** Aggiunta/modifica transazioni.  
  - **Viewer:** Solo lettura.  

---

## 3. Requisiti Non Funzionali  

### 3.1 Sicurezza  
- **NR-01:** Crittografia TLS 1.3 per tutte le comunicazioni client-server.  
- **NR-02:** Autenticazione JWT con refresh token (scadenza: 15 minuti).  

### 3.2 Usabilità  
- **NR-03:** Tempo di caricamento dashboard < 2 secondi (90% delle richieste).  
- **NR-04:** Supporto per lingue EN/IT (localizzazione basata su impostazioni utente).  

### 3.3 Compatibilità  
- **NR-05:** Frontend compatibile con Chrome, Safari, Firefox (ultime 3 versioni).  
- **NR-06:** App mobile-responsive (breakpoint: 320px, 768px, 1024px).  

---

## 4. Priorità  
- **MVP:** FR-01 a FR-22, NR-01 a NR-06.  
- **Fase 2:** FR-23 a FR-26.  
- **Fase 3:** FR-27, FR-28.  