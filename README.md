# kdobystavelsilnice-signal

Relé mezi studiem a webem [kdobystavelsilnice.cz](https://kdobystavelsilnice.cz).

- Studio při změně archivu (zveřejnění, úprava, odvolání) zapíše `signal.json`.
- Workflow `.github/workflows/relay.yml` pak spustí import webu, ale jen když má web co doručit.
- Studio zapíše `signal.json` i hodinu před koncem ověření veřejnosti videí na webu (`verifiedUntil`, platí 6 h); relé pak spustí obnovovací import (`reason=refresh`).
- Plánované importy webu (denně v 0:23 UTC a pak po 6 h) spouští také toto relé. Import v 6, 12 a 18 h přeskočí, když obnova ověření běží a web měl čerstvý import.
- Kontrola v :17 a :47 hlídá výpadek studia a je zálohou obnovy ověření.

Workflow nemá přístup k obsahu repozitáře (žádný checkout) ani žádná oprávnění kromě tokenu
`WEB_IMPORT_TOKEN`, který smí jen spouštět workflow webu. Zdroj workflow i tohoto README je ve studiu
v `deploy/relay/`.
