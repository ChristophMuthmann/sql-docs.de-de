---
title: "Erste Schritte mit SSMA für Access-Konsole (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2b555cebf6fbfda157b72e8bc71b10600da54d39
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>Erste Schritte mit SSMA für Access-Konsole (AccessToSQL)
Dieser Abschnitt beschreibt die Vorgehensweise zum Starten und erste Schritte mit der Anwendung der Access-Konsole. Ebenfalls aufgeführt sind, die Konventionen in einem typischen SSMA Ausgabe Konsolenfenster verwendet.  
  
## <a name="launching-ssma-console"></a>SSMA-Konsole zu starten  
Verwenden Sie die folgenden Schritte aus, um die SSMA-Konsolenanwendung starten:  
  
1.  Wechseln Sie zu **starten** und zeigen Sie auf **Programme**.  
  
2.  Klicken Sie auf die **SQL Server Migration Assistant für Access Command Prompt** Verknüpfung.  
  
    Es zeigt die Verwendung von SSMA Konsolenmenü und `(/? Help)`, damit Sie den Einstieg in die Konsolenanwendung.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Verfahren für die Verwendung der SSMA-Konsole  
Nachdem die-Konsole wurde erfolgreich auf Ihrem Windows-System gestartet wird, können Sie die folgenden Schritte aus, um sie zu bearbeiten:  
  
1.  Konfigurieren Sie SSMA-Konsole, über die Skriptdateien. Weitere Informationen in diesem Abschnitt finden Sie unter [Skriptdateien erstellen &#40; AccessToSQL &#41; ](../../ssma/access/creating-script-files-accesstosql.md).  
  
2.  [Erstellen Variablenwert Dateien &#40; AccessToSQL &#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [Erstellen die Server-Connection-Dateien &#40; AccessToSQL &#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [Ausführen der Konsole SSMA &#40; AccessToSQL &#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) basierend auf Ihren Anforderungen Projekt  
  
Zusätzliche Funktionen:  
  
1.  [Geben Sie ein Kennwort](http://msdn.microsoft.com/en-us/b099d0f9-dd37-4c87-8b6f-ed0177881ea4) und exportieren / importieren Sie ihn auf anderen Computern Fenster  
  
2.  [Generieren von Berichten](http://msdn.microsoft.com/en-us/abb4264a-622e-4215-af5b-14e309b8a399) Ausgabe Berichte für die Bewertung /conversion und Datenmigration detaillierte Xml anzeigen. Detaillierte Fehlerberichte können auch für die Aktualisierung und Synchronisierung Befehle generiert werden.  
  
## <a name="ssma-console-output-conventions"></a>SSMA-Konsole Ausgabe Konventionen  
Bei der Ausführung der SSMA-Befehle und Optionen an, das Konsolenprogramm zeigt die Ergebnisse und Meldungen (Informationen, Fehler usw.) für den Benutzer in der Konsole oder falls erforderlich, leitet an eine XML-Ausgabedatei. Jede Art von Nachricht in der Ausgabe wird durch eine eindeutige Farbe gekennzeichnet. Die Textnachricht in Weiß kennzeichnet z. B. Datei Skriptbefehle; in Grün stellt eine Eingabeaufforderung für Benutzer zur Eingabe und So weiter.  
  
![SSMA-Konsolenausgabe](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA-Konsolenausgabe")  
  
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
[Installieren von SQL Server Migration Assistant für Access](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)  
  

