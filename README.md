# 🚧 Mapotip – Odstávková stránka

Dočasná informační stránka pro zákazníky během plánovaného výpadku internetového připojení.

## Důvod

Společnost CETIN provádí plánované práce na optické síti, které přeruší konektivitu v naší lokalitě. Tato stránka informuje uživatele mapových portálů o výpadku.

**Termín výpadku:** 26. 3. 2026, 09:00 – 16:00

---

## 1. Nasazení na GitHub Pages

1. Nahraj `index.html` do tohoto repozitáře (branch `main`)
2. Jdi do **Settings → Pages**
3. Source: **Deploy from a branch**
4. Branch: `main`, folder: `/ (root)` → **Save**
5. Za 1–2 minuty bude stránka na: `https://mapotip.github.io/maintenance/`

---

## 2. Nastavení DNS (Český hosting)

### Přihlášení

Přihlas se do klientské sekce: [muj.cesky-hosting.cz](https://muj.cesky-hosting.cz)

Jdi do: **Správa domény → DNS**

### Varianta A – Přesměrování subdomény (např. `portal.mapotip.cz`)

Pokud přesměrováváš subdoménu, stačí jeden CNAME záznam:

| Typ   | Jméno   | Cíl                              |
|-------|---------|----------------------------------|
| CNAME | portal  | mapotip.github.io             |

### Varianta B – Přesměrování celé domény (apex, např. `mapotip.cz`)

Apex doména (bez www) nepodporuje CNAME. Musíš nastavit A záznamy na IP adresy GitHub Pages:

| Typ | Jméno | Cíl              |
|-----|-------|------------------|
| A   | @     | 185.199.108.153  |
| A   | @     | 185.199.109.153  |
| A   | @     | 185.199.110.153  |
| A   | @     | 185.199.111.153  |

Pokud chceš i `www` variantu, přidej navíc:

| Typ   | Jméno | Cíl                              |
|-------|-------|----------------------------------|
| CNAME | www   | mapotip.github.io             |

### Vlastní doména v GitHub Pages

Po změně DNS nastav vlastní doménu i na GitHubu:

1. V repozitáři jdi do **Settings → Pages → Custom domain**
2. Zadej svou doménu (např. `portal.mapotip.cz`) a klikni **Save**
3. GitHub automaticky vytvoří soubor `CNAME` v repozitáři
4. Počkej na DNS ověření (zelená fajfka)
5. Zaškrtni **Enforce HTTPS** (může trvat až 24 hodin)

---

## 3. Časový plán

### Den před odstávkou (25. 3. 2026)

- [ ] Ověřit, že stránka na GitHub Pages funguje
- [ ] Zapsat si **původní DNS záznamy** (A záznamy, IP adresy) — budeš je potřebovat na vrácení zpět!

### Ráno před odstávkou (26. 3. 2026, cca 7:00–8:00)

- [ ] V klientské sekci Českého hostingu změnit DNS záznamy (viz tabulky výše)
- [ ] Ověřit, že stránka se zobrazuje (TTL u Českého hostingu je 60 minut, takže max do hodiny)

### Po obnovení (26. 3. 2026, po 16:00)

- [ ] Vrátit DNS záznamy zpět na **původní hodnoty**
- [ ] Ověřit, že mapové portály opět fungují
- [ ] Odebrat vlastní doménu z GitHub Pages (Settings → Pages → Custom domain → smazat)

---

## 4. Ověření DNS

Po změně DNS můžeš ověřit správnost příkazem v terminálu:

```bash
# Linux / macOS
dig vase-domena.cz +noall +answer

# Windows (PowerShell)
Resolve-DnsName vase-domena.cz
```

Nebo online nástroj: [dnschecker.org](https://dnschecker.org)

---

## 5. Důležité poznámky

- **TTL u Českého hostingu je 60 minut** — změny se projeví do hodiny
- **Měň jen A / CNAME záznamy pro web** — MX záznamy (email) nechávej beze změny!
- Pokud si nebudeš jistý, napiš podporu Českého hostingu přes klientskou sekci → Zákaznická podpora
- Repozitář musí být **public**, aby GitHub Pages fungovaly zdarma

---

## Kontakt

Mapotip Česko s.r.o.  
📧 mapotip@mapotip.cz  
🌐 [mapotip.cz](https://mapotip.cz)
