# Virheen-hallinta-ja-raportointi_V2
Uudelleenkäytettävä aliprosessi virheiden hallintaan ja raportointiin. Soveltuu erityisesti käyttötapauksiin, joissa samoja virheitä voi toistua usein. Aliprosessin parametrien avulla voi joustavasti konfiguroida kuinka toistuvasta virheestä raportoidaan sähköpostilla.

Tarkoituksena ottaa huomioon haluttaessa, ettei samasta virheestä hälytettäisi liian usein ja/tai suoritetaan raportointi vasta kun tarpeeksi monta samaa virhettä esiintynyt määritellyssä ajassa.

Aliprosessi hyödyntää Frendsin sisäistä Shared State -välimuistia, joka on käytettävissä Frends 5.4 -versiosta lähtien.

Parametrit:
- Recipients: vastaanottajat, puolipistein eroteltu lista
- Id: virheen/prosessin tunniste
- Subject: virheviestin otsikko
- Message: virheviesti
- ExecutionId: Pääprosessin suorittaman instanssin Id (suorituslinkin rakennusta varten)
- LogMessage: Tarkempi virhekuvaus / stacktrace, käytetään vain mahdolliseen lokitukseen
- ErrorSettingsJson: Raportointiasetukset (mm. mute timespan, error threshold), ks. esimerkki pääprossessista "Demo Virheenhallinta ja raportointi v2.json"

Palauttaa informatiivisen tekstin, jossa seuraavat osat pilkulla eroteltuina:
- Id = virheen/kutsujan tunniste
- Alerted = true/false, suoritettiinko raportointia
- Type = lisätieto raportoinnin suorittamisesta / ohituksesta ja syystä

![Virheenhallinta ja raportointi v2](https://github.com/user-attachments/assets/79db95f7-d4f4-4131-b1e6-aef697c93f00)


Mukana tässä hakemistossa on demoprosessi "**Demo Virheenhallinta ja raportointi v2.json**", joka simuloi peräkkäisissä integraatiosuorituksissa tapahtuvan saman virheen käsittelyä kutsumalla suoraan virheenhallinta-aliprosessia.

![Demo Virheenhallinta ja raportointi v2](https://github.com/user-attachments/assets/dbd31bda-d301-4b0f-8ff9-c119dc516782)
