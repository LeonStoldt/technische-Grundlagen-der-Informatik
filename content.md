> # Inhaltsverzeichnis
> ## 1. Das OSI-Schichtenmodell
> ## 2. Physical Layer
> ### 2.1 Einführung
> ### 2.2 Nachrichten und Informationen
> ### 2.3 Signale
> ### 2.4 Kodierung und Impulsformung
> ### 2.5 Übertragungsmedien
> ## 3. //to be continued

---

## 1. Das OSI-Schichtenmodell

Das OSI-Modell [Open Systems Interconnection Model] stellt ein Referenzmodell für Netzwerkprotokolle dar und ist folgendermaßen aufgebaut:

[![OSI-Schichtenmodell - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/8/80/ISO-OSI-7-Schichten-Modell%28in_Deutsch%29.svg/2560px-ISO-OSI-7-Schichten-Modell%28in_Deutsch%29.svg.png)](https://upload.wikimedia.org/wikipedia/commons/thumb/8/80/ISO-OSI-7-Schichten-Modell%28in_Deutsch%29.svg/2560px-ISO-OSI-7-Schichten-Modell%28in_Deutsch%29.svg.png)

## 2. Physical Layer
### 2.1 Einführung
 
Der Physical Layer ist die erste Schicht des OSI-Schichtenmodells und wird auch Bitübertragungsschicht genannt.
Hier findet die Erzeugung der Signale in den entsprechenden Frequenzen durch elektromagnetische Wellen statt.

### 2.2 Nachrichten und Informationen

-	Nachrichten bestehen aus Zeichen bzw. Zeichenketten, denen eine Semantik zugewiesen ist
-	Zeichen bzw. Symbole sind atomare Elemente (z.B. Buchstaben des Alphabets)
-	Wörter bzw. Zeichenketten entstehen durch die Verkettung mithilfe der transitiv-reflexiven Hülle
-	Der Rechner kennt jedoch nur das Alphabet $\Sigma = \{0,1\}$

#### Informationstheorie nach Shannon
-	Ansatz zur statistischen Erfassung von Informationen
-	Informationsgehalt pro Zeichen
-	Je seltener ein Zeichen, desto größer der Informationsgehalt
-	Ein vorhersagbares Zeichen hat keinen Informationsgehalt

> $I = \text{Informationsgehalt in bit}$
> $P(a) = \text{Wahrscheinlichkeit eines Zeichens zum Zeitpunkt } t$
> 
> $I(P(a)) = -log_2 (P(a))$
> 
> Beispiel (es wird konstant "a" gesendet): $I_a(1) = -log_2 (1) = 0 bit$

#### Entropie
-	der mittlere Informationsgehalt wird als Entropie $H$ bezeichnet
-	berechnet sich durch 
$H = \sum\limits_{a \in \Sigma} P(a) * I(a) = - \sum\limits_{a \in \Sigma} P(a) * log_2(P(a))$
-	s

### 2.3 Signale

Ein Signal $x$ ist
-	eine zeitabhängige, physikalische Größe
-	messbar

Symbole können einer definierten Signaländerung $\Delta x$ zugewiesen werden.

Signale lassen sich in folgende Kategorien unterteilen:

|  | Wertkontinuierlich | Wertdiskret |
|--|--|--|
| **Zeitkontinuierlich** | $x = x(t), x \in \R, t \in \R$ | $x = x(t), x \in \N, t \in \R$ |
| **Zeitdiskret** | $x = x(t), x \in \R, t \in \N$ | $x = x(t), x \in \N, t \in \N$ |

Analogsignale werden durch den `ÀDC = Analog Digital Converter` in eine zeit- und wertdiskrete Repräsentation überführt ($x = x(t), x \in \N, t \in \N$).

#### Analoge Signale

-	stetig (nicht abzählbar)
-	Beispiele
	-	Schallplatte
	-	analoges Telefon
	-	VHS Magnetband
	-	reden

#### Digitale Signale

-	diskret (abzählbar)
-	Beispiele:
	-	Ampel
	-	mechanische Uhr
	-	Handy-Foto



### 2.4 Kodierung und Impulsformung


### 2.5 Übertragungsmedien
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1NzQxNTA1OCwtMTc1NDYxMjg2NywtMj
E0NDI5MjMwOCwxMTE4ODM4NjA4LC02NTYwMTc2MDMsMTUyMzIy
MzA5OSwzNzkxNDIyMTEsMTQzMjI5MTI4LDE1NjY5MDU4NjVdfQ
==
-->