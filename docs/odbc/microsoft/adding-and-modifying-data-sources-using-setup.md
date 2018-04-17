---
title: Hinzufügen und Ändern von Daten Datenquellen mithilfe von Setup | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f820e7790f60dc7f293b97340eea8eb228972f50
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Hinzufügen und Ändern von Datenquellen mithilfe von Setup
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Eine Datenquelle gibt einen Pfad zu Daten, die eine Netzwerkbibliothek, Server, Datenbank und andere Attribute enthalten können – in diesem Fall ist die Datenquelle für den Pfad zu einer Oracle-Datenbank. Um eine Verbindung mit einer Datenquelle herzustellen, überprüft der Treiber-Manager die Windows-Registrierung für bestimmte Verbindungsinformationen.  
  
 Der Registrierungseintrag, der von der ODBC-Datenquellen-Administrator erstellt, wird von der ODBC-Treiber-Manager und ODBC-Treiber verwendet. Dieser Eintrag enthält Informationen über jede Datenquelle und den zugehörigen Treiber. Bevor Sie eine Verbindung mit einer Datenquelle herstellen können, muss die Verbindungsinformationen zur Registrierung hinzugefügt werden.  
  
 Verwenden Sie zum Hinzufügen und Konfigurieren von Datenquellen, die [ODBC-Datenquellenadministrator](../../odbc/admin/odbc-data-source-administrator.md). Der ODBC-Administrator aktualisiert die Datenquellen-Verbindungsinformationen. Hinzufügen von Datenquellen aktualisiert den ODBC-Administrator die Informationen in der Registrierung für Sie.  
  
### <a name="to-add-a-data-source-for-windows"></a>So fügen Sie eine Datenquelle für Windows hinzu  
  
1.  Öffnen Sie den ODBC-Datenquellen-Administrator.  
  
2.  Klicken Sie auf "hinzufügen", klicken Sie im Dialogfeld ODBC-Datenquellen-Administrator. Das Dialogfeld "neue Datenquelle erstellen" angezeigt wird.  
  
3.  Wählen Sie Microsoft ODBC für Oracle, und klicken Sie dann auf ' Fertig stellen '. Microsoft ODBC für Oracle-Setup-Dialogfeld wird angezeigt.  
  
4.  Geben Sie im Feld Data Source Name den Namen der Datenquelle, die Sie zugreifen möchten. Es kann ein beliebiger Name sein, die Sie auswählen.  
  
5.  Geben Sie im Feld Beschreibung die Beschreibung für den Treiber. Dieses optionale Feld beschreibt den ODBC-Treiber, dem mit die Datenquelle verbindet. Es kann ein beliebiger Name sein, die Sie auswählen.  
  
6.  Geben Sie im Feld Benutzername der Datenbank-Benutzername (die Datenbankbenutzer-ID).  
  
7.  Geben Sie den Datenbank-Alias oder Verbindungszeichenfolge für die Oracle-Server-Datenbankmoduls, die Sie zugreifen möchten, in das Serverfeld.  
  
8.  Klicken Sie auf OK, um diese Datenquelle hinzuzufügen.  
  
> [!NOTE]  
>  Die Datenquellen-Dialogfeld wird angezeigt, und der ODBC-Administrator aktualisiert die Informationen in der Registrierung. Der Benutzer benennen und die Verbindungszeichenfolge, die Sie eingegeben werden Sie die Standardwerte für die Verbindung für diese Datenquelle aus, wenn Sie eine Verbindung damit herstellen.  
  
1.  Klicken Sie auf Optionen stellen weitere Spezifikationen zum ODBC-Treiber für Oracle-Setup:  
  
    -   **Übersetzung** – klicken Sie auf auswählen, um ein Konvertierungsprogramm geladenen Daten zu wählen. Die Standardeinstellung ist \<Nein Konvertierer >.  
  
    -   **Leistung** – der enthalten Hinweise Katalogfunktionen Kontrollkästchen gibt an, ob der Treiber "Hinweise" Spalten für zurückgibt der [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) Resultset. Der ODBC-Treiber für Oracle bietet schnelleren Zugriff auf, wenn dieser Wert nicht festgelegt ist.  
  
         Die SYNONYME enthalten in SQL-Spalten Kontrollkästchen gibt an, ob der Treiber gibt Spalteninformationen zurück. **Puffergröße** gibt die Größe in Bytes, belegt, um die abgerufene Daten zu erhalten. Der Treiber wird optimiert, abrufen, sodass ein Abrufen von Daten aus dem Oracle-Server genügend Zeilen um einen Puffer, der die angegebene Größe auszufüllen zurückgegeben. Größere Werte tendenziell Leistung zu steigern, wenn eine große Datenmenge abrufen.  
  
    -   **Anpassung** – im erzwingen ODBC DayOfWeek Standard Kontrollkästchen gibt an, ob das Resultset im ODBC-Format der angegebenen Tag der Woche entspricht (Sonntag = 1; Samstag = 7). Wenn dieses Kontrollkästchen deaktiviert ist, wird der Gebietsschema-spezifische Oracle-Wert zurückgegeben.  
  
         Die SQLDescribeCol **gibt immer einen Wert für Genauigkeit** Kontrollkästchen gibt an, und zwar unabhängig davon, ob der Treiber einen Wert ungleich NULL für zurückgeben soll die *CbColDef* Argument **SQLDescribeCol**. Dieses Verbindungszeichenfolgenattribut gilt nur für Spalten, in denen es keine Skalierung Oracle definiert ist z. B. berechnete numerische, Spalten und Spalten als Zahl ohne eine Genauigkeit oder Dezimalstellenanzahl. Ein **SQLDescribeCol** gibt 130 für die Genauigkeit aufgerufen wird, wenn Oracle diese Informationen nicht bereitstellt. Wenn dieses Kontrollkästchen deaktiviert ist, wird der Treiber stattdessen für diese Spaltentypen 0 zurück.  
  
2.  Klicken Sie auf Hinzufügen, um eine andere Datenquelle hinzuzufügen, oder klicken Sie auf Schließen zu beenden.  
  
### <a name="to-modify-a-data-source-for-windows"></a>So ändern eine Datenquelle für Windows  
  
1.  Öffnen Sie den ODBC-Datenquellen-Administrator. Klicken Sie auf die entsprechende Registerkarte aus DSN.  
  
2.  Wählen Sie die Oracle-Datenquelle, die Sie ändern, und klicken Sie dann auf konfigurieren möchten. Microsoft ODBC für Oracle-Setup-Dialogfeld wird angezeigt.  
  
3.  Ändern Sie die entsprechenden Datenquellenfeldern, und klicken Sie dann auf OK.  
  
 Wenn Sie das Ändern der Informationen in diesem Dialogfeld abgeschlossen haben, aktualisiert der ODBC-Administrator die Informationen in der Registrierung.
