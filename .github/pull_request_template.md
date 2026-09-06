<!-- MAS PR template (2026-09-05). Jeden ekran. -->

## Zmiany (co + dlaczego, 1-3 linie)


## Zakres
Jeden temat. Zmiany niezwiazane -> osobny PR. Tier (z `node ~/.claude/hooks/lib/risk-tier.js`): **T1**

## Checklista
- [ ] Brak `package.json`/build w tym repo (statyczny `index.html`) — zmiana sprawdzona recznie w przegladarce
- [ ] Zero sekretow w diffie
- [ ] Zero nowych zaleznosci runtime (albo uzasadnienie + ADR ponizej)
- [ ] T2+: `pg-review` odpalony — link do `aggregated.md` ponizej

## Wplyw na release
- [ ] widoczne dla usera -> wpis w `CHANGELOG.md [Unreleased]`
- [ ] tylko docs/CI/dev -> bez changelogu
- [ ] deploy: push na `main` -> Vercel buduje automatycznie (bez recznego kroku)
- [ ] rollback: `git revert <sha> && git push` na `main`

## Jak zweryfikowalem (komenda + obserwowany wynik, nie „dziala")
```
```

## Pominiete / zalozenia / do decyzji Kamila
