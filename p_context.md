## Context

Als je een React applicatie bouwt, zul je regelmatig data doorgeven via properties. Je kunt data echter alleen doorgeven van boven naar beneden, <b>niet terug omhoog</b>. Daarbij kan het voorkomen, door de complexiteit van de applicatie, dat je sommige data door ontzettend veel componenten moeten laten stromen. Terwijl misschien alleen die button - 5 niveau's diep - de data nodig heeft. In sommige situaties moeten zelfs bijna alle componenten toegang hebben tot een stukje data. Dit soort situaties doen zich vaak voor wanneer je:

- Een applicatie hebt die tweetalig is, waardoor bijna alle componenten zich bewust moeten zijn van de huidige geselecteerde taal.
- Een light- en dark-mode interface hebt, waarbij alle componenten met één druk op de knop moeten wisselen van styling.
- Een applicatie hebt waarbij ingelogde gebruikers afgeschermde content kunnen bekijken. Alle pagina's moeten dan weten of de gebruiker ingelogd en geautoriseerd is om de content te bekijken.

`React Context` lost dit probleem voor ons op. Er wordt een overkoepelend stukje state aangemaakt waar ieder component in de applicatie bij zou kunnen. Als een component de informatie uit de context nodig heeft, kan het dit direct aanspreken (<i>consumer</i>), omdat een top-level component deze data in de context aanbied (<i>provider</i>).

### Voorbeeld context

Een context aanmaken voor een click-counter is alsof je een tosti doorsnijdt met een kettingzaag. Probeer je voor te stellen dat dit een ingewikkeldere applicatie zou zijn en dat we daarom Context gaan implementeren.

Er komen drie componenten in deze applicatie die allemaal toegang moeten hebben tot dezelfde data:
1. Button component die de count verhoogt
2. Button component die de count verlaagt
3. Result component die de count laat zien