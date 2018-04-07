---
title: Erste Schritte mit SSMA für Sybase-Konsole (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d63e1c4e3ecf3cd5f2537ec54db24be59a4d8ad5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Erste Schritte mit SSMA für Sybase-Konsole (SybaseToSQL)
Dieser Abschnitt beschreibt das Verfahren zum Starten und erste Schritte mit SSMA für Sybase-Konsolenanwendung. Ebenfalls aufgeführt Hierin werden die Konventionen in einem typischen SSMA Ausgabe Konsolenfenster verwendet.  
  
## <a name="launching-the-ssma-console"></a>Die SSMA-Konsole zu starten  
Verwenden Sie die folgenden Schritte aus, um die SSMA-Konsolenanwendung starten:  
  
1.  Wechseln Sie zu starten, und klicken Sie dann nacheinander auf alle Programme.  
  
2.  Klicken Sie auf die **SQL Server Migration Assistant für Sybase Command Prompt** Verknüpfung.  
  
    Es zeigt die Verwendung von SSMA Konsolenmenü und `(/? Help)`, damit Sie den Einstieg in die Konsolenanwendung.  
  
## <a name="using-the-ssma-console"></a>Mithilfe der SSMA-Konsole  
Nachdem Sie die Konsole erfolgreich auf Ihrem Windows-System gestartet wird, können Sie die folgenden Schritte aus, um sie zu bearbeiten:  
  
1.  Konfigurieren Sie SSMA-Konsole, über die Skriptdateien. Weitere Informationen in diesem Abschnitt finden Sie unter [Skriptdateien erstellen &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
2.  [Erstellen von Dateien Variablenwert &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Erstellen die Server-Verbindungsdateien &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Ausführen der Konsole SSMA &#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) basierend auf Ihren Anforderungen Projekt. 
  
Zusätzliche Funktionen:  
  
1.  [Geben Sie ein Kennwort](http://msdn.microsoft.com/en-us/9b6a70f9-6840-4140-a059-bb7bd7ccc67c) und Export/Import es auf anderen Computern Fenster.  
  
2.  [Generieren von Berichten](http://msdn.microsoft.com/en-us/19278f6a-6d58-4867-9d71-c6228040466e) detaillierte Xml anzeigen Ausgabe Berichte für die Migration von Assessment-Konvertierung und Daten. Sie können auch detaillierte Fehlerberichte für Aktualisierung und Synchronisierung-Befehle generieren.  
  
## <a name="ssma-console-output-conventions"></a>SSMA-Konsole Ausgabe Konventionen  
Bei der Ausführung der SSMA-Befehle und Optionen an, das Konsolenprogramm zeigt die Ergebnisse und Meldungen (Informationen, Fehler usw.) für den Benutzer in der Konsole oder bei Bedarf leitet in eine XML-Ausgabedatei. Jede Art von Nachricht in der Ausgabe wird durch eine eindeutige Farbe gekennzeichnet. Die Textnachricht in Weiß kennzeichnet z. B. Datei Skriptbefehle; in Grün stellt eine Eingabeaufforderung für Benutzer zur Eingabe und So weiter.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
Farbe-Interpretation von der Konsolenausgabe wird in der folgenden Tabelle angezeigt:  
  
|Farbe|Description|  
|---------|---------------|  
|Red|Schwerwiegender Fehler während der Ausführung|  
|Grau|Datum- und Zeitstempel, die Nachricht an den Benutzer|  
|White|Datei Skriptbefehle, Nachrichtentyp|  
|Gelb|Warnung|  
|Green|Eingabeaufforderung für Benutzer zur Eingabe|  
|Cyan|Starten, beenden und Ergebnis eines Vorgangs|  
  
## <a name="see-also"></a>Siehe auch  
[Installieren von SSMA für SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
