# Simpele TODO lijst web app
Deze repo bevat een simpele TODO web app, met een frontend, backend en db.

# Demo
![](https://github.com/AP-IT-GH/projectopdracht-TisdenHakim/blob/main/demo.gif)

### Wat uitleg:
Deze TODO-applicatie is opgezet met een docker compose file en bestaat uit drie services: `denbackend`, `denfrontend`, en `dendb`. 
Hier beneden vind je een overzicht van de configuratie en hoe je deze applicatie kunt gebruiken.

### Services:
**Let op:**
Het is de bedoeling om de URL's in het Docker Compose-bestand aan te passen naar een domein van jezelf.

1. **denbackend**:
   - Bevat de backend van de TODO-applicatie.
   - Draait op `h4kim.tech/api/{name:.*}`.    Je past alles voor `/api/{name:.*}` aan.
   - Geconfigureerd voor TLS met Let's Encrypt via Traefik.

2. **denfrontend**:
   - Bevat de frontend van de applicatie, gebaseerd op een Nginx-image.
   - Toegankelijk via `h4kim.tech`.     Zie 'let op' hierboven! 

3. **dendb**:
   - MySQL als db van de applicatie.
   - Gebruikt volumes om gegevens op te slaan en initialiseert de database met `init.sql`.

### Configuratie:

- De applicatie maakt gebruik van Traefik als reverse proxy om verkeer naar de juiste services te routeren.
- Het is dus de bedoeling dat Traefik reeds draaiende is op je machine. 
- Een extern Traefik-netwerk wordt gebruikt om TLS-certificaten te beheren en verkeer veilig te maken via HTTPS.

### Hoe te gebruiken:
**Let op 1:**
Ik ga ervan uit dat Traefik al geïnitialiseerd is op je machine voordat je deze Docker Compose-applicatie start. 
Zorg er dus voor dat Traefik correct is geconfigureerd en dat het operationeel is, aangezien deze applicatie gebruikmaakt van Traefik als reverse proxy.

**Let op 2:**
Voordat je de Docker Compose-applicatie start, dien je een `.env`-bestand aan te maken in de directory waar de docker compose zich bevind. 
Deze met de volgende variabelen en hun waarden:

- `sqlUsr`: De gebruikersnaam voor de MySQL-database.
- `sqlPass`: Het wachtwoord voor de MySQL-gebruiker.
- `sqlRootPass`: Het wachtwoord voor de root-gebruiker van de MySQL-database.
- `sqlDb`: De naam van de MySQL-database.


1. Zorg ervoor dat Docker en Docker Compose zijn geïnstalleerd op je machine.
2. Voer het volgende commando uit in de directory waar het `docker-compose.yml`-bestand zich bevindt:
    ```bash
    docker-compose up -d
    ```
   Dit zal alle bovenstaande genoemde services starten in detached mode (achtergrond).
3. De applicatie is nu bereikbaar op (In mijn geval: `h4kim.tech`) voor de frontend en (In mijn geval:`h4kim.tech/api/{name:.*}`) voor de backend.
4. De backend API kan bereikt worden door middel van: `jedomein/api/todo` <== (API) `jedomein/api/verify` <== (Status API)

### Redenen waarom de app niet zou kunnen werken:

- De environment variabelen zijn niet correct geconfigureerd voordat je de applicatie start.
- Traefik is verkeerd geconfigureerd en/of is niet operationeel.

### Het stoppen van de applicatie:

- Om de applicatie te stoppen, gebruik je:
    ```bash
    docker-compose down
    ```

