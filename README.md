# kdobystavelsilnice-signal

Relé mezi studiem a webem [kdobystavelsilnice.cz](https://kdobystavelsilnice.cz).

- Studio při změně archivu (zveřejnění, úprava, odvolání) zapíše `signal.json`.
- Workflow `.github/workflows/relay.yml` pak spustí import webu, ale jen když má web co doručit.
- Plánované importy webu (denně v 0:23 UTC a pak po 6 h) a hodinovou kontrolu výpadku studia spouští také toto relé.

Workflow nemá přístup k obsahu repozitáře (žádný checkout) ani žádná oprávnění kromě tokenu
`WEB_IMPORT_TOKEN`, který smí jen spouštět workflow webu. Zdroj workflow je ve studiu
v `deploy/relay/relay.yml`.
