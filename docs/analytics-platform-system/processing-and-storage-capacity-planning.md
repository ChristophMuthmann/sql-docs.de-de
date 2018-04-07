---
title: Analytics Platform Verarbeitung und die Speicherkapazität
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Ihre geschäftlichen Anforderungen bestimmen die Anzahl der Skalierungseinheiten für Daten und die Größe der Compute-Knoten-Datenträger, die Sie in Ihrer Anwendung Analytics Platform System (APS) benötigen.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 2c32fec4-e97c-4797-b7f8-7c8d4301b7b6
caps.latest.revision: 7
ms.openlocfilehash: 68852344c65863ee051467e524eb0c3f09211483
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="analytics-platform-system-processing-and-storage-capacity"></a>Analytics Platform System Verarbeitung und die Speicherkapazität
Ihre geschäftlichen Anforderungen bestimmen die Anzahl der Skalierungseinheiten für Daten und die Größe der Compute-Knoten-Datenträger, die Sie in Ihrer Anwendung Analytics Platform System (APS) benötigen. Verwenden Sie diese Berechnungen Verarbeitung und Speicherung als Anleitung für die Kapazität Ihrer Kauf und planungsentscheidungen.  
  
  
## <a name="section1"></a>Planen der Verarbeitungskapazität  
Abfrageleistung für SQL Server Parallel Data Warehouse (PDW) hängt stark von der Anzahl der CPU-Kerne, die auf Ihre Daten gleichzeitig arbeiten. Innerhalb der Grenzen verbessert die Parallelität erhöht die abfrageleistung massive parallelverarbeitung (MPP). Auch wenn die Datengröße relativ klein ist, wird die Leistungsfähigkeit von Abfragemodul MPP erweitert, indem mit mehr Parallelität.  
  
Beispielsweise verfügt eine Einheit mit 12 Serverknoten 192 CPU-Kerne, die Ihre Daten parallel verarbeiten. Das ist schon 192-Wege-Parallelität! Eine Einheit mit 56 Serverknoten hat 896 Kerne parallel alle arbeiten. Diese Größe der Parallelität ist nicht ohne MPP computing müssen umsetzbar sein.  
  
Mit zunehmender Anzahl von Serverknoten erfordert die Appliance Ausskalieren Hinzufügen von mehreren Compute-Knoten zu einem Zeitpunkt, zu einer spürbaren nutzen zu können. Hardwarehersteller unterstützt nur an bestimmten Konfigurationen Skalierungseinheiten Daten, um sicherzustellen, dass der Vorteil, dass die Appliance Skalierung die Kosten für das Verteilen von Daten über weitere Serverknoten überwiegen.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Beispiele für Daten Skalierungseinheit-Konfiguration - HPE  
Es folgen Beispiele für die unterstützten HPE-Konfigurationen für die Skalierung Uunits Daten. Sie können von den aktuellsten unterstützten Konfigurationen abweichen, aber dienen als Beispiel dafür, wie zum Erhöhen der Kapazität von ungefähr 20 Prozent.  
  
Aufwertung ist der Gewinn Prozent Kapazität infolge einer Erhöhung der Uunits Skalierung Daten von einer Zeile zur nächsten. Erhöhen die Daten Skalierungseinheiten aus 6 bis 8 ermöglicht z. B. eine 33 % Aufwertung im CPU-Kerne und Speicher.  Es wird auch den Speicherplatz in dieser Tabelle aufgeführt ist nicht erhöht.  
  
|Skalierungseinheiten Daten|Compute-Knoten|CPU-Kerne|Arbeitsspeicher (GB)|Aufwertung|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|2|32|512|-|  
|2|4|64|1024|100%|  
|3|6|96|1536|50%|  
|4|8|128|2048|33%|  
|5|10|160|2560|25%|  
|6|12|192|3072|20%|  
|8|16|256|4096|33%|  
|10|20|320|5120|25%|  
|12|24|384|6144|20%|  
|16|32|512|8192|33%|  
|20|40|640|10240|25%|  
|24|48|768|12288|20%|  
|28|56|896|14336|17%|  
  
Erläuterung:  
  
-   **Daten-Skalierungseinheiten** pro Einheit. Weitere Informationen zu Daten Skalierungseinheiten finden Sie unter [Analytics Platform System Hardwarekomponenten](hardware-components.md).  
  
-   **Serverknoten** pro Einheit.  
  
-   **CPU-Kerne** pro Einheit. Es sind 16 Kerne pro Compute-Knoten, einen Kern pro jedes gespiegelten Datenträger-Paar. Compute-Knoten Datenträgerstruktur, finden Sie unter [Analytics Platform System Hardwarekomponenten](hardware-components.md).  
  
-   **Arbeitsspeicher** pro Einheit. Jeder Kern ist 256 GB Arbeitsspeicher.  
  
### <a name="data-scale-unit-configuration-examples--dell-quanta"></a>Skalierung Einheit Konfiguration Datenbeispiele – Dell, Quanta  
Es folgen Beispiele für die unterstützten Dell und Quanta Konfigurationen für die Skalierung Uunits Daten. Sie können von den aktuellsten unterstützten Konfigurationen abweichen, aber dienen als Beispiel dafür, wie zum Erhöhen der Kapazität von ungefähr 20 Prozent.  
  
Aufwertung ist der Gewinn Prozent Kapazität infolge einer Erhöhung der Uunits Skalierung Daten von einer Zeile zur nächsten. Erhöhen die Daten Skalierungseinheiten aus 6 bis 8 ermöglicht z. B. eine 33 % Aufwertung im CPU-Kerne und Speicher. Es wird auch den Speicherplatz in dieser Tabelle aufgeführt ist nicht erhöht.  
  
|Skalierungseinheiten Daten|Compute-Knoten|CPU-Kerne|Arbeitsspeicher (GB)|Aufwertung|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|3|48|768|-|  
|2|6|96|1536|100%|  
|3|9|144|2,304|50%|  
|4|12|192|3,072|33%|  
|5|15|240|3,840|25%|  
|6|18|288|4,608|20%|  
|7|21|336|5,376|17%|  
|8|24|384|6,144|14%|  
|9|27|432|6,912|13%|  
|12|36|576|9,216|33%|  
|15|45|720|11,520|25%|  
|18|54|864|13,824|20%|  
  
## <a name="section2"></a>Planen der Speicherkapazität  
Diese Tabelle schätzt, dass Sie laden und speichern Sie bis zu 6 Petabytes nicht komprimierten Daten auf eine vollständig integrierte Analytics Platform System Appliance konnte. 
  
|Hersteller|Laufwerkgröße|Physischen Speicher pro berechnen Datenknoten|Maximale Serverknoten pro rack|Maximale physische-Datenspeicher pro rack|Geschätzte maximale Benutzer Datenspeicher pro rack|Maximale racks|Geschätzte maximale Benutzer Datenspeicher pro Einheit|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2,240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4,480 TB|  
|HPE|3 TB|48 TB|8|384 TB|960 TB|7|6,720 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|2,160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4.320 TB|  
|DELL|3 TB|48 TB|9|432 TB|1080 TB|6|6,480 TB|  
  
Erläuterung:  
  
-   **Laufwerkgröße** ist 1, 2 oder 3 TB für jeden Hardwarehersteller.  
  
-   **Physischen Datenspeicher pro Serverknoten** = (Laufwerkgröße) * (16 Datenträger pro Compute-Knoten). Der gespiegelten Datenträgern sind nicht eingeschlossen, da sie sind jedoch für Redundanz.  
  
-   **Maximale Serverknoten pro Rack** bezieht sich auf den Hardwarehersteller.  
  
-   **Maximale physische-Datenspeicher pro Rack** = (physischen Datenspeicher pro Serverknoten) * (maximale Serverknoten pro Rack).  
  
-   **Geschätzte maximale Benutzer Datenspeicher pro Rack** = (physische maximale Datenspeicher pro Rack) * (für ein Komprimierungsverhältnis von 5:1-5) \* "50 % für Protokolle" und "TempDB". Dies ist eine konservative Schätzung für die unkomprimierten Daten, die geladen und auf dem Gerät gespeichert werden können. Dies ist eine Schätzung und wird durch die Software nicht erzwungen. Der tatsächlichen Benutzer-Datenspeicher hängt davon ab, die Daten und Ihrer Konfiguration.  
  
-   **Maximale Racks** ist eine spezifische Sicht für jede Hardwarehersteller.  
  
-   **Geschätzte maximale Datenspeicher pro Einheit** = (geschätzte maximale Daten-Speicher pro Rack) * (Maximum racks). Dies ist eine konservative Schätzung der Gesamtsumme Gesamtgröße von Benutzerdaten, die Sie laden und speichern Sie auf eine vollständig integrierte Appliance konnte.  
  
