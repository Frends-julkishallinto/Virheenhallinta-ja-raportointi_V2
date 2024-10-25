# Virheenhallinta-ja-raportointi_V2

Uudelleenkäytettävä aliprosessi virheiden hallintaan ja raportointiin, joka soveltuu käytettäväksi erityisesti sellaisten pääprosessien kanssa, joissa samoja virheitä toistuu säännöllisesti ja/tai tiheästi. Aliprosessin parametrien avulla voi joustavasti konfiguroida kuinka toistuvasta virheestä raportoidaan sähköpostilla.

Tarkoituksena ottaa huomioon haluttaessa, ettei samasta virheestä hälytettäisi liian usein ja/tai suoritetaan raportointi vasta kun tarpeeksi monta samaa virhettä esiintynyt määritellyssä ajassa.

Kuva aliprosessista:
![Virheenhallinta ja raportointi v2](https://github.com/user-attachments/assets/79db95f7-d4f4-4131-b1e6-aef697c93f00)

## Ennakkovaatimukset
- Frends 5.4 tai uudempi
  - Aliprosessi hyödyntää Frendsin sisäistä Shared State -välimuistia, joka on käytettävissä Frends 5.4 -versiosta lähtien.
- Taski Frends.Community.Email.EmailTask.SendEmail on asennettu.
  - Jos käytössä on uudempi Frends.SMTP.SendEmail, voit vaihtoehtoisesti käyttöönoton yhteydessä muutta prosessin target framework:ksi .NET 6.0/8.0 ja käyttää sähköpostin lähetykseen SMTP.SendEmail -taskia.
 
## Aliprosessin tarvitsemat ympäristömuuttujat
Voit tarvittaessa hyödyntää olemassa olevia muuttujia. Oletuksena aliprosessi käyttää seuraavia muuttujia:
  - #env.Reporting.EmailFrom = lähettäjän sähköpostiosoite
  - #env.Reporting.EmailSenderName = lähettäjän nimi
  - #env.Reporting.SmtpServer = SMTP-palvelimen osoite
  - #env.Reporting.SmtpUsername = SMTP-käyttäjätunnus, jolla ei ole MFA käytössä
  - #env.Reporting.SmtpPassword = SMTP-käyttäjätunnuksen salasana

## Parametrit:
- Recipients: vastaanottajat, puolipistein eroteltu lista
- Id: virheen/prosessin tunniste
- Subject: virheviestin otsikko
- Message: virheviesti
- ExecutionId: Pääprosessin suorittaman instanssin Id (suorituslinkin rakennusta varten)
- LogMessage: Tarkempi virhekuvaus / stacktrace, käytetään vain mahdolliseen lokitukseen
- ErrorSettingsJson: Raportointiasetukset (mm. mute timespan, error threshold), ks. esimerkki pääprossessista "ESIMERKKIPROSESSI Demo Virheenhallinta ja raportointi v2.json"

## Paluudata
Aliprosessi palauttaa informatiivisen tekstin, jossa seuraavat osat pilkulla eroteltuina:
- Id = virheen/kutsujan tunniste
- Alerted = true/false, suoritettiinko raportointia
- Type = lisätieto raportoinnin suorittamisesta / ohituksesta ja syystä

## Esimerkkiprosessi

Mukana tässä hakemistossa on esimerkkiprosessi "**ESIMERKKIPROSESSI Demo Virheenhallinta ja raportointi v2.json**", joka simuloi peräkkäisissä integraatiosuorituksissa tapahtuvan saman virheen käsittelyä kutsumalla suoraan virheenhallinta-aliprosessia. Prosessi sisältää myös esimerkin kuinka virheenhallintaa voi käyttää odottamattomien virheiden käsittelyssä.

![Demo Virheenhallinta ja raportointi v2](https://github.com/user-attachments/assets/dbd31bda-d301-4b0f-8ff9-c119dc516782)

# Asennus

Linkki interaktiiviseen esitykseen miten aliprosessi importoidaan ja sovitetaan kohde-Frends-ympäristöön: [Aliprosessin asennus import-tiedostosta](https://app.storylane.io/share/pzxc3znytx5j)
