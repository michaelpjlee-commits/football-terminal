# Football Terminal

A football dashboard in the style of a trading terminal, by [@tamerton](https://x.com/tamerton). Views:

- **League overview**: Premier League 2026/27 table, form, goals, xG, results and fixtures
- **Squads**: a Football Manager-style squad page for any of the 20 Premier League clubs
- **Leagues**: "Leagues in Focus" cards for 12 English, Scottish and European leagues
- **Scotland**: squad pages for all 12 Scottish Premiership clubs
- **Managers**: every Liverpool manager since 1892 and every Celtic manager since 1897 compared (switch club at the top, or open `#managers/celtic`), split by league, domestic cups and Europe, including a first-N-games comparison with the current manager

Open it here: https://football.tamertongroup.co.uk/

The page is a single static `index.html`. It reads live data from a published Google Sheet that refreshes every night, using data from the official Fantasy Premier League API, Transfermarkt market values, ESPN, LFChistory.net, TheCelticWiki and Wikipedia. Not affiliated with Football Manager, the Premier League, Liverpool FC, Celtic FC, Transfermarkt, ESPN, LFChistory.net or TheCelticWiki.
