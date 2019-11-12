> # Inhaltsverzeichnis
> ## 1. Das OSI-Schichtenmodell
> ## 2. Bitübertragungsschicht
> ### 2.1 Einführung
> ### 2.2 Nachrichten und Informationen
> ### 2.3 Signale
> ### 2.4 Kodierung und Impulsformung
> ### 2.5 Übertragungsmedien
> ## 3. Sicherungsschicht
> ### 3.1 Direktverbindungsnetze
> ### 3.2 Medienzugriff
> ### 3.3 Rahmenbildung
> ## 4. Vermittlungsschicht
> ### 4.1 Vermittlungsarten
> ### 4.2 Adressierung im Internet
> ### 4.3 ICMP
> ### 4.4 DHCP
> ### 4.5 IPv6
> ### 4.6 Statisches Routing
> ### 4-7 Dynamisches Routing

---

## 1. Das OSI-Schichtenmodell

Das OSI-Modell [Open Systems Interconnection Model] stellt ein Referenzmodell für Netzwerkprotokolle dar und ist folgendermaßen aufgebaut:

[![OSI-Schichtenmodell - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/8/80/ISO-OSI-7-Schichten-Modell%28in_Deutsch%29.svg/2560px-ISO-OSI-7-Schichten-Modell%28in_Deutsch%29.svg.png)](https://upload.wikimedia.org/wikipedia/commons/thumb/8/80/ISO-OSI-7-Schichten-Modell%28in_Deutsch%29.svg/2560px-ISO-OSI-7-Schichten-Modell%28in_Deutsch%29.svg.png)

---

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
-	eine zu geringe Abtastrate führt zu verschiedenen möglichen Frequenzen
[![https://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Nyquist_Aliasing.svg/740px-Nyquist_Aliasing.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Nyquist_Aliasing.svg/740px-Nyquist_Aliasing.svg.png)](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Nyquist_Aliasing.svg/740px-Nyquist_Aliasing.svg.png)

*Die gestrichelte Linie zeigt mögliche andere Signale mit demselben Ergebnis bei der gegebenen Abtastrate*


#### Allgemeine Werte
-	Bandbreite
$$B = f_o - f_u = \text{obere Frequenz - untere Frequenz}$$
-	Rauschen
$$\bar{x} = \frac{1}{n} \sum\limits_{i=1}^{n} x_i$$


### 2.4 Kodierung und Impulsformung

-	Zwischen Signalen und der realen physikalischen Größe bestehen signifikante Unterschiede
-	kleinste Übertragungsfehler können das Ergebnis bereits unbrauchbar machen
-	um Fehler erkennen zu können, werden weitere Protokolle benötigt

#### Basisimpuls 1 - NRZ

[![https://upload.wikimedia.org/wikipedia/commons/5/55/NRZcode.png](https://upload.wikimedia.org/wikipedia/commons/5/55/NRZcode.png)](https://upload.wikimedia.org/wikipedia/commons/5/55/NRZcode.png)

-	Non-return-to-zero Leitungskodierung
-	Bsp. Kommunikation auf der Platine
-	Nachteile:
	-	nicht gleichanteilsfrei (= zeitlicher Mittelwert ist 0)
	-	keine Taktrückgewinnung
	-	unsicher bei längeren Nachrichten


#### Basisimpuls 2 - RZ

[![https://www.ijunoon.com/sw-store/images/dictionary/Return-to-zero.jpg](https://www.ijunoon.com/sw-store/images/dictionary/Return-to-zero.jpg)](https://www.ijunoon.com/sw-store/images/dictionary/Return-to-zero.jpg)

-	Return-to-zero Leitungskodierung
-	Nachricht ist zu Ende, wenn das Signal auf 0 bleibt
-	ist ebenfalls nicht gleichanteilsfrei

#### Basisimpuls 3 - Manchesterkodierung

[![https://upload.wikimedia.org/wikipedia/commons/0/0a/Manchester_code.png](https://upload.wikimedia.org/wikipedia/commons/0/0a/Manchester_code.png)](https://upload.wikimedia.org/wikipedia/commons/0/0a/Manchester_code.png)

-	logische 1 wird über eine fallende Flanke codiert
-	logische 0 wird über eine steigende Flanke codiert
-	meist Kodierung in Netzwerken und LAN
-	Vorteile:
	-	gleichanteilsfrei
	-	Taktrückgewinnung ist möglich
	-	Sener und Empfänger lassen sich galvanisch trennen (Trennung der Stromkreisläufe)
-	Nachteile:
	-	die Bandbreite ist doppelt so groß wie bei z.B. NRZ
	-	die Bitrate (= Bitübertragungsrate) ist halb so groß wie die Baudrate (= Symbolübertragungsrate)


### 2.5 Übertragungsmedien

Übertragungsmedien lassen sich unterteilen in:
-	leistungsgebundene Übertragung
-	nicht leistungsgebundene Übertragung
und unterscheiden zwischen:
-	akustischen Wellen
-	elektromagnetischen Wellen
	-	benötigen im Gegensatz zu Schall kein Medium
	-	hat eine Wellenlänge $\lambda$, die die räumliche Ausdehnung bestimmt
	-	hat eine Frequenz $f = \frac{c}{\lambda}$ (c ist die Ausbreitung)
	-	die Ausbreitungsgeschwindigkeit in Medien ergibt sich durch den Faktor $v$ in $v * c$

#### Kabel
-	straight through Kabel
	-	Netzwerkkabel von Computer zu Switch
-	crossover Kabel
	-	Twisted-Pair Kabel (gewisse Kabeladern vertauscht)
	-	verbindet zwei Computer bzw. Switches miteinander
-	Lichtwellenleiter (Glasfaserkabel)
	-	sehr hohe Datenrate
	-	geringe Dämpfung und Verluste
	-	sehr geringer Kerndurchmesser des Kabels

#### Hub
-	Kopplungselement zur Verbindung mehrerer Hosts eines Netzwerks

---

## 3. Sicherungsschicht

### 3.1 Direktverbindungsnetze

-	alle Knoten eines Netzwerks sind erreichbar
-	alle Knoten lassen sich über physikalische Adressen identifizieren
-	es findet keine Vermittlung der Pakete statt
-	**Begrifflichkeiten:**
	-	Durchmesser: maximale Entfernung zweier Knoten (auf direktem Weg)
	-	Grad: Anzahl der benachbarten Knoten
	-	Konnektivität: Mit der Entfernung wie vieler Knoten würde das Netzwerk nicht mehr funktionieren?

#### Aufgaben der Sicherungsschicht:
-	Steuerung des Medienzugriffs
-	Prüfung übertragener Nachrichten auf Fehler
-	Adressierung innerhalb des Direktverbindungsnetzwerks

#### verschiedene Aufbaustrukturen:
**1. Punkt zu Punkt:**
-	zwei direkt verbundene Knoten
-	z.B.  über crossover Kabel

**2. Stern:**
-	viele Knoten sind zu einem zentralen Knoten verbunden
-	z.B. über einen Hub oder Switch

**3. Vermaschung:**
-	vernetzte Knoten (auch untereinander)
-	keine redundanten Vernetzungen

**4. Vollvermascht:**
-	Vermaschung mit zusätzlich redundanten Vernetzungen (transitive Hülle)

**5. Baum:**
-	Binärbaum-Struktur

**6.  Bus (Binary Unit System):**
-	alle Knoten sind über eine Bus-Leitung physikalisch verbunden

#### Verbindungscharakteristik
-	Übertragungsrate $r_{ij}$ in $\frac{bit}{s}$
-	Serialisierungszeit $t_s$ für die Nachricht der Länge $L$ in $Bit$  ist definiert durch $ts = \frac{L}{r_{ij}}$
-	Ausbreitungsverzögerung $t_p$ über die Distanz $d$ ist definiert durch $t_p = \frac{d}{v * c}$


#### Nachrichtenflussdiagramm
-	Knoten $i$ mit der Distanz zu Knoten $j$ überträgt in der Serialisierungszeit $t_s$ die Nachricht, die mit einer Ausbreitungsverzögerung $t_p$ bei $j$ ankommt. Die Gesamtzeit für das Senden und Empfangen der Nachricht beträgt also $t_d = t_s + t_p$

#### Verbindungsarten
-	abhängig von
	-	Fähigkeiten des Übertragungskanals
	-	Medienzugriffsverfahren
	-	Fähigkeiten des Kommunikationspartners

**simplex, halbduplex und vollduplex:**
[![https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSkHSneyZshgPRp7iPzsxLBFQeFLQdCSaiSxcu-xyOxHan2Fjk4kA&s](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSkHSneyZshgPRp7iPzsxLBFQeFLQdCSaiSxcu-xyOxHan2Fjk4kA&s)](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSkHSneyZshgPRp7iPzsxLBFQeFLQdCSaiSxcu-xyOxHan2Fjk4kA&s)


### 3.2 Medienzugriff

- Aufteilung des Kanals in verschiedene Frequenzbänder für die Kommunikationspartner
oder
- zeitliche Aufteilung des Zugriffs auf den Kanal

**synchron**
- Probleme:
	- Kanal wird statisch aufgeteilt
	- Bandbreite steht während Ruhepausen anderer Teilnehmer nicht zur Verfügung

Verfahren:
- Slotted ALOHA
	- Funktionsweise wie bei ALOHA (*siehe asynchrone Verfahren*)
	- Zuweisung von Time Slots für das Senden von Nachrichten zur Kollisionsminimierung
	- deutlich höhere Effizienz als ALOHA, aber nicht optimal
- Token passing
	-	Kollisionsvermeidung durch Weitergabe eines Tokens
	-	Bildung eines Token-Rings
	-	nur die Station mit dem Token darf senden und gibt diesen danach weiter
	-	Problem: fehlerhafte Knoten stören das gesamte Netz

**asynchron**

Verfahren:
- ALOHA
	- Jede Station sendet an eine zentrale Station
	- Bei gleichzeitigen Nachrichten tritt eine Kollision auf
	- erfolgreiche Nachrichten werden quittiert
	- nicht optimal im Hinblick auf Effizienz
-  CSMA (Carrier Sense Multiple Access)
	- simple Verbesserung des Slotted ALOHA
	- Es wird geprüft, ob das Medium frei ist bevor die Nachricht gesendet wird
	- Die Stationen warten nach einer Kollision eine zufällige Zeit, um die Kollisionswahrscheinlichkeit zu reduzieren
	- Bei Kollisionen wird ein sog. "Jam-Signal" gesendet
	- Problem: funktioniert nicht in Funknetzen
	- Lösung:
		-	CSMA/CD (Collision Detection)
		-	Übertragung wird von der Basisstation (Bsp. Router) gesteuert
		-	Knoten senden vor der Nachricht ein *RTS - Request to send*
		-	Router antwortet idealerweise mit *CTS - Clear to send*
		-	Kollisionen werden verringert (die Datenrate allerdings auch)
		-	Bsp. Ethernet

### 3.3 Rahmenbildung

Auseinanderhalten von Nachrichten in einer Sequenz von Bits

1.	Nachrichtenlänge angeben durch
-	**Steuerzeichen:** Symbole, die nicht in der Nachricht vorkommen und Start bzw. Ende der Nachricht kodieren. (Bsp. Beispiel: **11000 10001** 10111 01011 01110 **01101 00111**)

2.	**Bitstuffing:** Anfang und Ende einer Nachricht werden mit einer bestimmten Bitfolge, die nicht Teil der Nachricht ist und zwischen Sender und Empfänger vereinbart wurde, markiert. (Bsp. **01111110** 101110101101110 **01111110**)

3. **Coderegelverletzung:** Markierung einer Nachricht durch Auslassen definierter Signalwechsel bei gleichanteilsfreien Codierungen (Bsp. Manchestercodierung) vor- und hinter der Nachricht.

Adressierung

Bedingung:
-	Eindeutige Identifikation im Direktverbindungsnetz
-	Eine *Broadcast-Adresse*, die alle Knoten im Netz adressiert werden kann.

> **MAC-Adressen (Media Access Control)** 
> -	MAC-Adresse ist im ROM (read only memory) hinterlegt
> -	bestehen aus einer Herstellerkennung (Bsp. Intel *00-07-E9*) und einer eindeutigen Gerätenummer
> -	Beispielhafte MAC-Adresse `00-07-E9-01-37-A2`

-	Aufbau der Adressierung innerhalb eines Direktverbindungsnetzes:

| Ziel MAC-Adresse | Ursprungs MAC-Adresse | (Control) | L3-PDU (Daten) | Prüfsumme |
|:--:|:--:|:--:|:--:|:--:|
| Empfänger | Sender | optional - für die Unterstützung virtueller LANs über Ethernet | PDU = Protocol Data Unit | zur Fehlererkennung |

Übertragungsfehler erkennen und korrigieren

> **Prüfsummenbildung mit Hilfe von CRC (cyclic redundancy check)**
> -	berechnet zu einem Datenblock eine Prüfsumme fester Länge
> -	Fehlererkennung von allen 1-Bit Fehlern und zusammenhängenden 2-Bit Fehlern
> 
> 1.	Die Nachricht $m$ erfüllt die Bedingung $|m| \gt k$, wobei $k$ der Grad des Generatorpolynoms $g$ ist
> 2.	Die Nachricht $m$ erhält am Ende $k$ Nullen ($w \circ 0^k$)
> 3.	Die Nachricht mit den zusätzlichen Nullen wird mit dem Generatorpolynom $g$ *XOR* verknüpft $$0 \oplus 0 = 0 \\ 0 \oplus 1 = 1 \\ 1 \oplus 0 = 1 \\ 1 \oplus 1 = 0$$
> 4.	Der Rest $r$ mit $|r| \leq k$ wird an die ursprüngliche Nachricht angehängt
> 5.	Der Empfänger der Nachricht mit Prüfsumme teilt diese durch das Generatorpolynom und sollte nach der fehlerfreien Übertragung keinen Rest erhalten.
> 
> *Beispiel*
> Generatorpolynom $g = 100111 \implies k = 5$ (da $g = x^5 + x^2 + x^1 + x^0$)
> Nachricht: $m = 10010 11100 11101 \implies |m| = 15$
> 
> 1.	$|m| \gt k = 15 \gt 5 = true$
> 2.	$m \circ 0^5 = 10010 11100 11101 00000$
> 3.	Polynomdivision:
> ``` j
> 10010111001110100000
> 100111 
> ------
> 0000101100
>     100111 
>     ------
>     00101111
>       100111 
>       ------
>       00100010
>         100111
>         ------
>         000101100
>            100111 
>            ------
>            00101100
>              100111
>              ------
>              0010110 = r
> ```
> 
> 4.	$|r| \leq k = 5 \leq 5 = true$
> $m \circ r = 10010 11100 11101 \circ 10110 = 10010 11100 11101 10110$
> 
> 5.	Empränger prüft auf Korrektheit
> ``` j
> 10010111001110110110
> 100111 
> ------
> 0000101100
>     100111
>     ------
>     00101111
>       100111
>       ------
>       00100010
>         100111
>         ------
>         000101110
>            100111
>            ------
>            00100111
>              100111
>              ------
>              0000000
> ```


Kollisionsdomäne

- Teilbereich aus Teilnehmerstationen (Knoten)
-	Ein **Hub** verbindet die Knoten physikalisch zu einer Kollisionsdomäne
-	Alle Knoten konkurrieren um den Zugriff auf ein Übertragungsmedium (geteilte Ressource)
-	**Bridge**s unterteilen Netzte in kleinere Kollisionsdomänen
-	Nachrichten aus einer Kollisionsdomäne in eine andere werden im Switch kurz zwischengespeichert und schließlich an das Ziel weitergeleitet.
-	Jeder Knoten kann in eine einzelne Kollisionsdomäne aufgeteilt werden, damit es keine Kollisionen mehr gibt. Hierbei handelt es sich dann um einen **Switch**


## 4. Vermittlungsschicht

### 4.1 Vermittlungsarten

1.	Leitungsvermittlung (verbindungsorientierte Verbindung)
-	zugeteilte Leitungen zwischen Sender und Empfänger
-	Verbindungsaufbau $\rightarrow$ Datenaustausch $\rightarrow$ Verbindungsabbau

2.	Nachrichtenvermittlung
-	Pfad im Netzwerkgraph für eine Nachricht
-	Nachricht mit vorangestelltem Header, der Informationen zu Sender und Empfänger enthält
-	Vorteil: Phasen der verbindungsorientierten Verbindung entfallen
-	Nachteil: Falls Knoten zwischendrin ausgelastet sind, müssen Nachrichten gepuffert werden. Wenn der Puffer voll ist, gehen Nachrichten verloren

3.	Paketvermittlung
-	Nachrichten werden in Einzelpakete zerlegt und nach dem Prinzip der Nachrichtenvermittlung verschickt
-	Jedes Nachrichtenpaket erhält einen eigenen Header u.a. mit Informationen zur Zusammensetzung
-	Vorteile
	-	Pufferung kleiner Pakete, statt großer Nachrichten
	-	Bei Verlust gehen nur einzelne Nachrichten verloren und können erneut gesendet werden
-	Nachteile
	-	zusätzliche Header für einzelne Pakete sorgen für Overhead
	-	Empfänger muss die Nachricht zusammenbauen

### 4.2 Adressierung im Internet

-	Internet Protokoll zur Adressierung in globalen Netzwerken
-	IP Adressen werden zur Adressierung über Netze hinweg genutzt
-	IPv4 Header 20 Bytes lang

> Checksumme berechnen (Hexadezimal)
> 1.	Alle bis auf die Checksumme addieren
> 2.	Übertrag in jedem Schritt hinzuzählen
> 3.	Einerkomplement des Ergebnis bilden
> 
> *Beispiel*
> Header:
> 0x4500 0x3621
> 0x1211 0x4000
> 0x0108 0xEEA8
> 0xB29B 0x4D3A
> 0xC0A8 0x0203
> 
> `4500 + 3621 + 1211 + 4000 + 0108 + B29B + 4D3A + C0A8 + 0203 = 90BC`
> 
> Einerkomplement (Hex in Binär, Bits flippen und in Hex zurück umwandeln): 
> $90BC_{16} = 1001 0000 1011 1100_2$
> Bits flippen: $0110 1111 0100 0011_2 = 6F43_{16}$

#### ARP - Address Resolution Protocol
-	wird von IPv4 verwendet
-	wird zur Ermittlung der MAC-Adressen zu gegebenen IP Adressen verwendet
-	hinterlegt die Zuordnung in ARP-Tabellen auf dem Rechner

ARP Spoofing
-	softwareseitige Manipulation der MAC-Adresse
-	kann zum Abfangen von Inhalten genutzt werden (Man in the middle)

#### Beispiel-Szenario:

``` mermaid
graph LR
A((A))-->G((Gateway)) 
B((B))-->G 
G-->C((C)) 
G-->D((D))
```

Angenommen Host A möchte Host D eine Nachricht schicken und es sind zwei Netze (A, B) und (C, D)
1.	$Host A$ erkennt, dass $Host D$ nicht in dem Direktnetz liegt
2.	$Host A$ löst die MAC-Adresse zu der Adresse des Gateways auf und schickt die Nachricht mit der IP Adresse von $Host D$ los
3.	Das Gateway kennt die IP Adresse des Ziels und löst diese dann im anderen Netz auf die MAC-Adresse auf und leitet die Nachricht an das Ziel $Host D$ weiter

:information_source: Beim Routing werden die Ziel-MAC-Adressen zwischendurch verändert, aber die IP-Adresse bleibt gleich.


### 4.3 ICMP - Internet Control Message Protocol

-	benachrichtigt den Sender über auftretende Probleme beim Senden von Nachrichten
-	dient zur Paketumleitung
-	überprüft die Erreichbarkeit des Hosts (*Ping*)
	-	Es wird ein Echo Request an den Zielhost geschickt
	-	Der Zielhost antwortet nach erhalt des Echo Request mit einem Echo Reply
	-	Sollte der Zielhost nichts erhalten, wird eine ICMP-Nachricht mit dem Fehlercode an den Absender zurück geschickt
		-	Dies kann durch Ablaufen der TTL (Time to live) passieren
		-	Traceroute: Die Pakete werden mit einer TTL von 1 losgeschickt und somit beim nächsten Knoten verworfen und es wird eine Time Exceeded Nachricht an den Sender geschickt. Dieser erhöht die TTL um 1 und sendet erneut. Somit kann der Pfad zum Ziel herausgefunden werden.


### 4.4 DHCP - Dynamic Host Configuration Protocol

Die Zuteilung von IP-Adressen kann auf zwei Wegen erfolgen:

1.	Statisch
-	manuelle Konfiguration

2.	Dynamisch
-	zugewiesene Adresse eines DHCP-Servers
-	Clients erneuern ihre vom DHCP-Server zugewiesene Adresse regelmäßig

``` mermaid
graph LR
H((Host)) --1. DHCP-Discover--> D((DHCP))
D --2. DHCP-Offer--> H
H --3. DHCP-Request--> D
D --4. DHCP-ACK/NACK--> H
```

-	Der Host sendet ein *DCHP-Discover* und erhält vom DHCP-Server ein *DHCP-Offer* mit der angebotenen IP-Adresse.
-	Danach fordert der Host die angebotene IP-Adresse an (*DHCP-Request*) und der DHCP-Server antwortet mit einem *DHCP-ACK*, wenn er die IP-Adresse freigibt oder einem *DHCP-NACK*, wenn er die Nutzung untersagt.


### 4.5 IPv6




### 4.6 Statisches Routing

### 4-7 Dynamisches Routing

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUwODcxODA5OCwtNzE1MjMzMzAxLC05NT
M5OTk3MDAsLTE1MzQxNDQ2ODcsMjAyMjI5NDYwOCwxODk5ODAy
MTM1LDEzOTMxMDA5NTIsLTEyOTM4MTk1MTksMzg4MzQ1OTk0LC
0yMzY5NzcyMjYsLTE3NjA0ODk1NjcsLTEyMTA0MzQ4NzQsMTAz
OTYxNjU1NiwtMTQ5MDk3OTcxOSwtMTkzODMwMDEyMSw3MTQ4Nz
A2MjcsNTQ0MzQwMTgxLC0xMDY0ODc5MzY1LDEzODA1NzU1NjQs
LTU0NzgwOTk1M119
-->