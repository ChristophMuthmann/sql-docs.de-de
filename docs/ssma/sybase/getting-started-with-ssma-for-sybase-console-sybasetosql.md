---
title: "Erste Schritte mit SSMA für Sybase-Konsole (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 239b7a8f4dbc3069e67d680b319bf426a0f917e6
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-sybase-console-sybasetosql"></a>Erste Schritte mit SSMA für Sybase-Konsole (SybaseToSQL)
Dieser Abschnitt beschreibt die Vorgehensweise zum Starten und erste Schritte mit der Sybase-Konsolenanwendung. Ebenfalls aufgeführt sind, die Konventionen in einem typischen SSMA Ausgabe Konsolenfenster verwendet.  
  
## <a name="launching-ssma-console"></a>SSMA-Konsole zu starten  
Verwenden Sie die folgenden Schritte aus, um die SSMA-Konsolenanwendung starten:  
  
1.  Wechseln Sie zu starten, und zeigen Sie auf alle Programme.  
  
2.  Klicken Sie auf die **SQL Server Migration Assistant für Sybase Command Prompt** Verknüpfung.  
  
    Es zeigt die Verwendung von SSMA Konsolenmenü und `(/? Help)`, damit Sie den Einstieg in die Konsolenanwendung.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Verfahren für die Verwendung der SSMA-Konsole  
Nachdem die-Konsole wurde erfolgreich auf Ihrem Windows-System gestartet wird, können Sie die folgenden Schritte aus, um sie zu bearbeiten:  
  
1.  Konfigurieren Sie SSMA-Konsole, über die Skriptdateien. Weitere Informationen in diesem Abschnitt finden Sie unter [Skriptdateien erstellen &#40; SybaseToSQL &#41; ](../../ssma/sybase/creating-script-files-sybasetosql.md) .  
  
2.  [Erstellen Variablenwert Dateien &#40; SybaseToSQL &#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Erstellen die Server-Connection-Dateien &#40; SybaseToSQL &#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Ausführen der Konsole SSMA &#40; SybaseToSQL &#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) basierend auf Ihren Anforderungen Projekt  
  
Zusätzliche Funktionen:  
  
1.  [Geben Sie ein Kennwort](http://msdn.microsoft.com/en-us/9b6a70f9-6840-4140-a059-bb7bd7ccc67c) und exportieren / importieren Sie ihn auf anderen Computern Fenster  
  
2.  [Generieren von Berichten](http://msdn.microsoft.com/en-us/19278f6a-6d58-4867-9d71-c6228040466e) Ausgabe Berichte für die Bewertung /conversion und Datenmigration detaillierte Xml anzeigen. Detaillierte Fehlerberichte können auch für die Aktualisierung und Synchronisierung Befehle generiert werden.  
  
## <a name="ssma-console-output-conventions"></a>SSMA-Konsole Ausgabe Konventionen  
Bei der Ausführung der SSMA-Befehle und Optionen an, das Konsolenprogramm zeigt die Ergebnisse und Meldungen (Informationen, Fehler usw.) für den Benutzer in der Konsole oder falls erforderlich, leitet an eine XML-Ausgabedatei. Jede Art von Nachricht in der Ausgabe wird durch eine eindeutige Farbe gekennzeichnet. Die Textnachricht in Weiß kennzeichnet z. B. Datei Skriptbefehle; in Grün stellt eine Eingabeaufforderung für Benutzer zur Eingabe und So weiter.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
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
[Installieren SSMA für Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
  

