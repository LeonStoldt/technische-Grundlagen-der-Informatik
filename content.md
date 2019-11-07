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
-	berechnet sich durch:
$$H = \sum\limits_{a \in \Sigma} P(a) * I(a) = - \sum\limits_{a \in \Sigma} P(a) * log_2(P(a))$$

*Beispiel:*
$\Sigma = \{a, b\}, P(b) = 0,12$
$I(a) = ?, H(x) = ?$

$P(a) = 1 - P(b) = 0,88$
$I(a) = - log_2 (P(a)) = - log_2 (0,88) \approx 0,18$
$P(b) = 0,12$
$I(b) = - log_2 (P(b)) = - log_2 (0,12) \approx 3,06$

$H(x) = - \sum\limits_{a \in \Sigma} P(a) * log_2(P(a)) = P(a) * I(a) + P(b) * I(b) \approx 0,53$

#### Transinformationen (mutual information)

-	Informationen, die über einen gedächtnislosen Kanal übermittelt werden
-	gibt die Stärke des Zusammenhangs zweier Zufallsgrößen an
-	Transinformationen eines Kanals stellt den mittleren Informationsgehalt dar, der vom Sender zum Empfänger gelangt

Gedächtnisloser Kanal:
[![https://upload.wikimedia.org/wikipedia/commons/c/cf/Entroy_XY.png](https://upload.wikimedia.org/wikipedia/commons/c/cf/Entroy_XY.png)](https://upload.wikimedia.org/wikipedia/commons/c/cf/Entroy_XY.png)

-	verbindet zwei Quellen miteinander
-	die Transinformation fließt vom Sender zum Empfänger
-	je mehr Quellen voneinander abhängen, desto mehr Transinformationen gibt es
-	der Einfluss von Fehlinformationen wird durch $H(Y|X)$ abgebildet, da $Y$ die Sendequelle $X$ teilweise überlagert und es somit zum Informationsverlust kommt

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

Größen, wie die Spannung $U$ und der Strom $I$ sind Wert- und Zeitkontinuierlich

[![https://www.gut-erklaert.de/images/mathematik/ohmsches-gesetz-dreieck.jpg](https://www.gut-erklaert.de/images/mathematik/ohmsches-gesetz-dreieck.jpg)](https://www.gut-erklaert.de/images/mathematik/ohmsches-gesetz-dreieck.jpg)

**Probleme:**
-	Speicher ist begrenzt
-	Rechenleistung ist begrenzt
$\rightarrow$ Rechnerseitig müssen diese also Wert- und Zeitdiskret sein

**Lösung:**
Konvertierung des
-	Zeitbereichs durch Abtastung
-	Wertebereichs durch Quantisierung

Analogsignale werden durch den `ÀDC = Analog Digital Converter` in eine zeit- und wertdiskrete Repräsentation überführt ($x = x(t), x \in \N, t \in \N$).

#### Analoge Signale

-	**stetig** (nicht abzählbar)
-	Beispiele
	-	Schallplatte
	-	analoges Telefon
	-	VHS Magnetband
	-	reden

#### Digitale Signale

-	**diskret** (abzählbar)
-	Beispiele:
	-	Ampel
	-	mechanische Uhr
	-	Handy-Foto

#### Aspekte der Übertragung von Nachrichten

-	Periode $T$ in $ms$
-	Frequenz $f = \frac{1}{T}$ in $Hz$
-	Spektrum und Bandbreite $B$
-	Phasenwinkel $\phi$
-	Phasenverschiebung $\Delta\phi$

#### Dirac-Distribution
-	(uneigentliche Funktion)
-	ein Peek mit unbestimmter Höhe
-	Anwendungsbeispiel: Faltungsoperationen

[![https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Dirac_distribution_PDF.svg/1200px-Dirac_distribution_PDF.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Dirac_distribution_PDF.svg/1200px-Dirac_distribution_PDF.svg.png)](https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Dirac_distribution_PDF.svg/1200px-Dirac_distribution_PDF.svg.png)

#### Faltung
-	liefert für zwei Funktionen eine dritte, neue Funktion

#### Heaviside-Funktion
-	Einheitssprung
-	Eingangssignal für die Ermittlung der Systemantwort

#### Rechteckfunktion
-	hergeleitet aus der Heaviside-Funktion
-	begrenzt auf ein festes Intervall

#### Rampenfunktion
-	Integral der Heaviside-Funktion

#### Taktsignal
-	zur Synchronisation in Schaltwerken
-	im Netzwerk dient es zur Synchronisation zwischen Sender und Empfänger
-	idealerweise eine Folge von Rechtecksignalen
-	relevante Kriterien
	-	Frequenz bzw. Periode
	-	Flanke
	-	Amplitude


#### SPI und UART:
-	SPI = Serial Peripheral Interface
	-	Bussystem
	-	synchroner serieller Datenbus
	-	dient zur Verbindung zweier digitaler Schaltungen nach dem Master-Slave-Prinzip
-	UART = Universal Asynchronous Receiver Transmitter
	-	elektronische Schaltung
	-	existiert z.B. im Mikrokontroller oder als UART-Chip
	-	dient zur Realisierung digitaler serieller Schnittstellen


#### 5-4-3 Regel
In einem Netzwerk gilt:
-	maximal 5 Segmente
-	mit 4 Repeatern
-	und pro Segment maximal 3 Endstationen


#### Abtastung
Verfahren der Analog-Digital-Umwandlung
1.	Sample and hold
-	Der aktuelle Wert des Abtastzeitpunkts $f(t)$ wird genommen
[![https://upload.wikimedia.org/wikipedia/commons/thumb/1/15/Zeroorderhold.signal.svg/220px-Zeroorderhold.signal.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/1/15/Zeroorderhold.signal.svg/220px-Zeroorderhold.signal.svg.png)](https://upload.wikimedia.org/wikipedia/commons/thumb/1/15/Zeroorderhold.signal.svg/220px-Zeroorderhold.signal.svg.png)

2.	Diskretisierung und Quantisierung
-	Zeitpunkte werden in einen diskreten Raum überführt (**Zeitdiskret**)
-	Signalwerte werden ebenfalls diskretisiert und dem Wert zugeordnet, der am nächsten dran ist (**Wertdiskret**)
[![https://upload.wikimedia.org/wikipedia/commons/7/70/Quantized.signal.svg](https://upload.wikimedia.org/wikipedia/commons/7/70/Quantized.signal.svg)](https://upload.wikimedia.org/wikipedia/commons/7/70/Quantized.signal.svg)


#### Abtasttheorem nach Shannon
-	



### 2.4 Kodierung und Impulsformung


### 2.5 Übertragungsmedien
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA2NjMyOTYzNiwxMzMyNjEzMjk3LC0xMT
AwNzUzNjcwLDE1OTcwMzEyNDEsLTEyNTIwODgxMCwtMTA3NTI3
ODg5NSwtMTkwMDA1MDcwMywtNTkzMTI0MjQwLC02NTk5MjczMT
YsOTc0NjU4MTY3LC0xMTc2OTc1OTgxLDU1Njc3Mzg2LDIwMDgw
ODM5MzIsLTI2Mjg0MjIyOSwxNTU3NDE1MDU4LC0xNzU0NjEyOD
Y3LC0yMTQ0MjkyMzA4LDExMTg4Mzg2MDgsLTY1NjAxNzYwMywx
NTIzMjIzMDk5XX0=
-->