# changelog-principle

<p align="center">
  <strong>Rješavanje problema pisanja CHANGELOG-a polazeći od konačnog stanja promjena. Usklađeno sa standardom Keep a Changelog: evidencija promjena nije i ne smije biti hronika commitova.</strong>
</p>

<p align="center">
  <a href="../LICENSE"><img src="https://img.shields.io/badge/Licenca-CC_BY_4.0-blue.svg" alt="Licenca: CC BY 4.0"></a>
  <a href="https://keepachangelog.com/en/1.1.0/"><img src="https://img.shields.io/badge/Standard-Keep%20a%20Changelog-orange.svg" alt="Keep a Changelog"></a>
</p>

<p align="center">
  <a href="../README.md">English</a> | <a href="README.zh-CN.md">简体中文</a> | <a href="README.ru.md">Русский</a> | <strong>Srpskohrvatski</strong>
</p>

---

## Šta ova vještina rješava

Kada se od AI agenata za programiranje (Claude Code, Cursor, Windsurf, Antigravity itd.) zatraži da ažuriraju CHANGELOG.md, oni obično po automatizmu pregledaju git commit zapise i doslovno ih prepišu u CHANGELOG.

Zbog toga se pregled izmjena pretvara u interni dnevnik programera:
- Sitni commitovi puni šuma: `fix typo`, `wip`, `format with prettier`, `fix tests`.
- Prelazna stanja: mogućnost dodata u commitu A, izmijenjena u commitu B i refaktorisana u commitu C prikazuje se kao tri razdvojene stavke.
- Korisniku nevidljive promjene: refaktorisanje koda, izdvajanje funkcija i premještanje datoteka koje korisnici i integratori uopšte ne mogu primijetiti.
- Pogrešno evidentiranje dorađivanja neobjavljenih funkcija: fino podešavanje mogućnosti koja još nije objavljena pogrešno se svrstava u `Fixed` ili `Changed` stavke, unoseći zabunu kod čitalaca.

---

## Osnovni principi

> Naglašavamo: evidencija promjena je spisak suštinskih izmjena namijenjen korisnicima i programerima, a ne hronika git commitova. U eri vještačke inteligencije tome moramo posvetiti još veću pažnju.

### Stvarna promjena iz ugla korisnika jedina je osnova za unos

Svaka stavka odgovara samo na jedno pitanje: „Šta će korisnik ili programer primijetiti da je drugačije u odnosu na prethodno zvanično izdanje?” Ako je odgovor „ništa”, stavka se ne zapisuje.

### Razlika u odnosu na git log

Sve stavke se grade isključivo na osnovu čiste razlike u odnosu na prethodno stabilno izdanje (npr. `git diff <last-tag>..HEAD`) i namjere koja stoji iza nje. Naredba `git log` koristi se najviše radi provjere koje su datoteke mijenjane, a nikada kao tekstualni izvor za pisanje stavki.

---

## Poređenje rezultata

| Pristup | Tipičan izlaz agenta |
| :--- | :--- |
| Uobičajeni pristup na osnovu git log-a | <ul><li>refactor(viewer): extract tabs into composable and tweak spacing</li><li>fix: resolve broken avatar hover state on mobile</li><li>Improved the profile viewer UX with better hover handling and updated tab styles</li><li>wip: add tests for viewer tabs</li></ul> |
| changelog-principle na osnovu čiste razlike | <ul><li>Prikaz profila mijenja avatare prelaskom kursora miša.</li></ul> |

---

## Pravila odabira

| Izbaciti | Obavezno zadržati |
| :--- | :--- |
| Refaktorisanje, izdvajanje pomoćnih funkcija, preimenovanja, premještanje datoteka | Ponašanje koje korisnik ili programer može neposredno uočiti |
| Ispravke tipova, lintera, formatiranja, komentara | Nove ili uklonjene komande, parametri, stranice, skripte, podešavanja |
| Izmjene unutar build procesa i razvojnog servera | Promijenjene podrazumijevane vrijednosti ili sistemska ograničenja |
| Zapisi o odlukama, dokumentacija, interne datoteke | Zastarjevanja, uklanjanja i prekidajuće izmjene (obavezno navesti) |
| Podešavanje još neobjavljene funkcije (spojiti u prvobitni unos) | Ispravka greške na već objavljenom kodu sa kojom se korisnik mogao susresti |
| Greška napravljena i ispravljena unutar istog razvojnog ciklusa | Suštinski nov sadržaj ili nova mogućnost |

---

## Instalacija i podešavanje

### Preko Skills CLI
```bash
npx skills add NBDatsuya/changelog-principle -g -y
```

### Ručna instalacija
Kopirajte [`SKILL.md`](../SKILL.md) u direktorijum sa vještinama ili pravilima vašeg agenta:
- **Antigravity / Skills**: `skills/changelog-principle/SKILL.md`
- **Claude Code**: `.claude/skills/changelog-principle/SKILL.md`
- **Cursor**: `.cursor/rules/changelog-principle.mdc`
- **Windsurf**: `.windsurf/rules/changelog-principle.md`

---

## Kontrolna lista prije čuvanja

Prije čuvanja zapisa provjerite:
1. Svaka stavka potiče iz vidljive razlike u čistom diff-u, uz obavezno navođenje konkretne promjene.
2. Nema opisa nepostojećih funkcija; svaka rečenica odražava stvarno implementirano ponašanje.
3. Ako je funkcija dorađivana, stavka je ažurirana u prvobitnom unosu kako se ne bi pojavljivali duplikati.
4. Ako bi se prelazni commitovi spojili (squash), sve prelazne stavke koje više ne odgovaraju krajnjem stanju moraju biti uklonjene.
5. Stil je jednostavan i direktan, bez suvišnih opisa i praznih pohvala („poboljšano”, „uglađenije”).

---

## Zasluge i napomene

- Osnovne ideje oslanjaju se na koncept čiste razlike iz projekta [samber/developer-relations-skills](https://github.com/samber/developer-relations-skills) (vještina `changelog-writing`).
- Format u potpunosti prati specifikaciju [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/).
- Ova specifikacija je sastavljena i provjerena pomoću alata [blader/humanizer](https://github.com/blader/humanizer), [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) i [LifelongLazyLearner/qu-ai-wei](https://github.com/LifelongLazyLearner/qu-ai-wei) radi pouzdanog razumijevanja od strane ljudi i AI modela, bez stvaranja suvišnog sadržaja.
- Licencirano pod [Creative Commons Attribution 4.0 International](../LICENSE) (`CC BY 4.0`).
