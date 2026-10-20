---
topic: Mutual Exclusion & Condition Synchronisation
date: 2026-03-16
course: OSVO
tags:
  - studies
  - Betriebssysteme
  - "#Mutex"
  - "#ConditionSynchronisation"
---
## VO
Beispiele siehe die Folien:
- [[bs03_mutex-sync.pdf#page=2&selection=58,0,59,1|bs03_mutex-sync, page 2]]

### Gemeinsame Ressourcen
BS und Prozesse sind parallel laufende Prozesse
- verwenden dieselben Daten bzw. Ressourcen (Puffer, Shared Memory, Files, Geräte)
- tauschen Daten aus und/oder interagieren

Um Prozess-Konflikte zu vermeiden, braucht man einen *disziplinierten Zugriff*, auf gemeinsame Daten und oder Ressourcen _und_ **geordnete Abarbeitung** verteilter Aktionsfolgen. 

Falls man dies misachtet:
1. Inkonsistente Daten
2. Indeterministisches Verhalten (Ereignisfolge, Werte)

### Race   Condition

Ergebnis einer Operation hängt ab vom
- zetiliche Verhalten oder
- der Reihenfolge von Operattionen oder Ereignissen

außerhalb der Kontrolle eines Prozesses 

Fehler: ein oder mehrere der möglichen Ergebnisse sind falsch, bzw führen zu falschem Verhalten. 






#### Links
- [[Learn Lean]]
