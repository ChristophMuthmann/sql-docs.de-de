---
title: Erste Schritte mit SSMA für Oracle-Konsole (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle Console, Console Output Conventions
- Oracle Console, Launching Console
ms.assetid: 667a5e4a-6848-4973-a72d-1287f64718ac
caps.latest.revision: 31
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ee95fb6ccb9ce9a50e35024d4f5754d32c734020
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-ssma--for-oracle-console-oracletosql"></a>Erste Schritte mit SSMA für Oracle-Konsole (OracleToSQL)
Dieser Abschnitt beschreibt die Vorgehensweise zum Starten und erste Schritte mit der Oracle-Konsolenanwendung. Ebenfalls aufgeführt sind, die Konventionen in einem typischen SSMA Ausgabe Konsolenfenster verwendet.  
  
## <a name="launching-ssma-console"></a>SSMA-Konsole zu starten  
Verwenden Sie die folgenden Schritte aus, um die SSMA-Konsolenanwendung starten:  
  
1.  Wechseln Sie zu **starten** und zeigen Sie auf **Programme**.  
  
2.  Klicken Sie auf die  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Oracle-Eingabeaufforderung** Verknüpfung.  
  
    Es zeigt die Verwendung von SSMA Konsolenmenü und `(/? Help)`, damit Sie den Einstieg in die Konsolenanwendung.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Verfahren für die Verwendung der SSMA-Konsole  
Nachdem die-Konsole wurde erfolgreich auf Ihrem Windows-System gestartet wird, können Sie die folgenden Schritte aus, um sie zu bearbeiten:  
  
1.  Konfigurieren Sie SSMA-Konsole, über die Skriptdateien. Weitere Informationen in diesem Abschnitt finden Sie unter [Skriptdateien erstellen &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-script-files-oracletosql.md) .  
  
2.  [Erstellen von Dateien Variablenwert &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
3.  [Erstellen die Server-Verbindungsdateien &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
4.  [Ausführen der Konsole SSMA &#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) basierend auf Ihren Anforderungen Projekt  
  
Zusätzliche Funktionen:  
  
1.  [Geben Sie ein Kennwort](http://msdn.microsoft.com/en-us/8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c) und exportieren / importieren Sie ihn auf anderen Computern Fenster  
  
2.  [Generieren von Berichten](http://msdn.microsoft.com/en-us/ccad6262-01e1-447a-bd2b-c105154c80ce) Ausgabe Berichte für die Bewertung /conversion und Datenmigration detaillierte Xml anzeigen. Detaillierte Fehlerberichte können auch für die Aktualisierung und Synchronisierung Befehle generiert werden.  
  
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
[Installieren von SSMA für Oracle](http://msdn.microsoft.com/en-us/9211013a-ab24-4c52-9b26-87994b35e502)  
  
