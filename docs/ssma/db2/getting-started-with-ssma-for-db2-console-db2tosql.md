---
title: "Erste Schritte mit SSMA für die DB2-Konsole (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f245c017-023e-4880-8721-8908d339525e
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2f183de010387d512909580e46d6c41b9783a38f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>Erste Schritte mit SSMA für die DB2-Konsole (DB2ToSQL)
Dieser Abschnitt beschreibt die Vorgehensweise zum Starten und erste Schritte mit der DB2-Konsolenanwendung. Ebenfalls aufgeführt sind, die Konventionen in einem typischen SSMA Ausgabe Konsolenfenster verwendet.  
  
## <a name="launching-ssma-console"></a>SSMA-Konsole zu starten  
Verwenden Sie die folgenden Schritte aus, um die SSMA-Konsolenanwendung starten:  
  
1.  Wechseln Sie zu **starten** und zeigen Sie auf **Programme**.  
  
2.  Klicken Sie auf die  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für DB2 Command Prompt** Verknüpfung.  
  
    Es zeigt die Verwendung von SSMA Konsolenmenü und `(/? Help)`, damit Sie den Einstieg in die Konsolenanwendung.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Verfahren für die Verwendung der SSMA-Konsole  
Nachdem die-Konsole wurde erfolgreich auf Ihrem Windows-System gestartet wird, können Sie die folgenden Schritte aus, um sie zu bearbeiten:  
  
1.  Konfigurieren Sie SSMA-Konsole, über die Skriptdateien. Weitere Informationen in diesem Abschnitt finden Sie unter [Skriptdateien erstellen &#40; DB2ToSQL &#41;](../../ssma/db2/creating-script-files-db2tosql.md) .  
  
2.  [Erstellen Variablenwert Dateien &#40; DB2ToSQL &#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [Erstellen die Server-Connection-Dateien &#40; DB2ToSQL &#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [Ausführen der Konsole SSMA &#40; DB2ToSQL &#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) basierend auf Ihren Anforderungen Projekt  
  
Zusätzliche Funktionen:  
  
1.  [Verwalten von Kennwörtern](http://msdn.microsoft.com/en-us/56d546e3-8747-4169-aace-693302667e94) und exportieren / importieren Sie ihn auf anderen Computern Fenster  
  
2.  [Generieren von Berichten](http://msdn.microsoft.com/en-us/69ef5fd9-190d-4c58-8199-b3f77d5e1883) Ausgabe Berichte für die Bewertung /conversion und Datenmigration detaillierte Xml anzeigen. Detaillierte Fehlerberichte können auch für die Aktualisierung und Synchronisierung Befehle generiert werden.  
  
## <a name="ssma-console-output-conventions"></a>SSMA-Konsole Ausgabe Konventionen  
Bei der Ausführung der SSMA-Befehle und Optionen an, das Konsolenprogramm zeigt die Ergebnisse und Meldungen (Informationen, Fehler usw.) für den Benutzer in der Konsole oder falls erforderlich, leitet an eine XML-Ausgabedatei. Jede Art von Nachricht in der Ausgabe wird durch eine eindeutige Farbe gekennzeichnet. Die Textnachricht in Weiß kennzeichnet z. B. Datei Skriptbefehle; in Grün stellt eine Eingabeaufforderung für Benutzer zur Eingabe und So weiter.  
  
![SSMA-konsolenausgabe_oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMA-konsolenausgabe_oracle")  
  
Farbe von der Konsolenausgabe in der folgenden Tabelle interpretiert:  
  
|Farbe|Description|  
|---------|---------------|  
|Red|Schwerwiegender Fehler während der Ausführung|  
|Grau|Datum- und Zeitstempel, die Nachricht an den Benutzer|  
|White|Datei Skriptbefehle, Nachrichtentyp|  
|Gelb|Warnung|  
|Green|Eingabeaufforderung für Benutzer zur Eingabe|  
|Cyan|Starten Sie, beenden und das Ergebnis eines Vorgangs|  
  
## <a name="see-also"></a>Siehe auch  
[Installieren von SSMA für DB2](http://msdn.microsoft.com/en-us/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
