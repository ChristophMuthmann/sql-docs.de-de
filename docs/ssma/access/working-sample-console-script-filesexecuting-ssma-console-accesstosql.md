---
title: Arbeiten mit Beispiel-Konsole Skript FilesExecuting SSMA-Konsole | Microsoft Docs
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
ms.assetid: ad75b648-d119-4119-98f0-d18f058be68d
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a2ac9806e1f7577312ede0dddfcd38b3721f94f0
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="working-with-the-sample-console-script-filesexecuting-the-ssma-console-accesstosql"></a>Arbeiten mit der Beispiel-Konsole Skript FilesExecuting SSMA-Konsole (AccessToSQL)
Einige Beispieldateien wurden zusammen mit dem Produkt für die Benutzer-Verweis und die Verwendung bereitgestellt. Dieser Abschnitt beschreibt die Möglichkeit, diese Skripts, sodass die Endbenutzer Bedürfnissen problemlos anzupassen.  
  
## <a name="sample-console-script-files"></a>Beispiel-Konsole-Skriptdateien  
Referenz für den Benutzer haben die folgenden Konsole Skript Beispieldateien für verschiedene Szenarien bereitgestellt wurde:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   In diesem Beispiel gibt die verschiedenen Modi des Verbindung verfügbar mit der Quelle und Ziel-Datenbank und der Benutzer kann jedem Modus gemäß der Anforderung auswählen. Dieses Beispiel enthält die Serverdefinitionen.  
  
    -   Der Benutzer kann mit der erforderlichen Datenbank einfach die Werte ändern, um die erforderlichen Quell- und Ziel-Serverdefinitionen verbinden. In das bereitgestellte Beispiel alle Werte bereitgestellt wie Variablenwerte in zur Verfügung stehen die **VariableValueFileSample.xml**. Alle anderen Verbindungsparameter können aus der Verbindung des Benutzers arbeiten Serverdatei entfernt werden.  
  
    -   Weitere Informationen zum Herstellen einer Verbindung mit dem Quell- und Ziel-Server finden Sie unter [erstellen, die Server-Connection-Dateien &#40; AccessToSQL &#41; ](../../ssma/access/creating-the-server-connection-files-accesstosql.md) .  
  
-   **VariableValueFileSample.xml:** alle Variablen, die in der Beispielkonsole verwendet wurden, Skriptdateien und `ServersConnectionFileSample.xml` haben in dieser Datei sortiert wurden. Beispielskripts-Konsole ausführen, die ersetzen Sie die Beispiel-Variable der Benutzer muss, Werte mit Benutzer definierten Argumente und übergeben Sie diese Datei als ein zusätzliches Befehlszeilenargument zusammen mit der Skriptdatei.  
  
    Weitere Informationen zu Wert Variablendatei, finden Sie unter [erstellen Variable Wertdateien &#40; AccessToSQL &#41; ](../../ssma/access/creating-variable-value-files-accesstosql.md).  
  
-   **AssessmentReportGenerationSample.xml:** dieses Beispiel ermöglicht dem Benutzer um einen XML-Bewertung-Bericht zu generieren, die verwendet werden, können vom Benutzer für die Analyse bevor er beginnt, konvertieren und Migrieren von Daten.  
  
    In der `generate-assessment-report` Befehl, der Benutzer hat den Wert den Variablen Zwischenschritte ändern (finden Sie unter **VariableValueFileSample.xml**) in der `object-name` -Attribut auf die Datenbank Namen an, von dem Benutzer verwendet. Je nach Art des Objekts angegeben wird die `object-type` Wert auch geändert werden müssen.  
  
    Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `generate-assessment-report` des Befehls Beispiel 4 von der Konsole Beispielskriptdatei.  
  
    Weitere Informationen zum Erstellen von Berichten finden Sie unter [Generieren von Berichten &#40; AccessToSQL &#41; ](../../ssma/access/generating-reports-accesstosql.md).  
  
    > [!NOTE]  
    > -   Stellen Sie sicher, dass der Wert der Variablen Befehlszeilenargument-Datei an die Konsolenanwendung übergeben wird und VariableValueFileSample.xml wird mit den angegebenen Benutzer aktualisiert Werte.  
    > -   Stellen Sie sicher, dass die Server-Verbindung über die Befehlszeile Dateiargument an die Konsolenanwendung übergeben wird und die ServersConnectionFileSample.xml mit Parameterwerten für die richtigen Server aktualisiert wird.  
  
-   **ConversionAndDataMigrationSample.xml:** in diesem Beispiel kann der Benutzer eine End-to-End-Migration von der Konvertierung in die Datenmigration ausgeführt werden. Die Liste der erforderlichen Attributwerte, die sie ändern, wird im folgenden aufgeführt:  
  
    |Befehlsname|Description|Attribut|  
    |----------------|---------------|-------------|  
    |`map-schema`|Schemazuordnung der Quelldatenbank mit dem Zielschema.|`source-schema:`Gibt die Quelldatenbank, die erforderlich sind, konvertiert werden soll.<br /><br />`sql-server-schema`: Gibt an, die Zieldatenbank, die migriert werden|  
    |`convert-schema`|Schemakonvertierung von der Quelle in das Zielschema durchgeführt.<br /><br />Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `convert-schema` des Befehls Beispiel 4 von der Konsole Beispielskriptdatei.|`object-name`: Geben Sie die Quelldatenbank / Objektnamen Sie, die erforderlich sind, konvertiert werden soll. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`|  
    |`synchronize-target`|Synchronisiert die Zielobjekte mit der Zieldatenbank an.<br /><br />Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `synchronize-target` des Befehls Beispiel 3 der Beispielskriptdatei für die Konsole.|`object-name:`Geben Sie die Sql Server-Datenbank / Objektname, der um zu erstellenden erfordert. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`|  
    |`migrate-data`|Migriert die Quelldaten zum Ziel.<br /><br />Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `migrate-data` des Befehls Beispiel 2 dieses der Beispielskriptdatei für die Konsole.|`object-name:`Gibt an, die Quelldatenbank / Tabellen Namen, die für die Migration erforderlich sind. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`|  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen Variablenwert Dateien &#40; AccessToSQL &#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
[Erstellen die Server-Connection-Dateien &#40; AccessToSQL &#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
[Generieren von Berichten &#40; AccessToSQL &#41;](../../ssma/access/generating-reports-accesstosql.md)  
  

