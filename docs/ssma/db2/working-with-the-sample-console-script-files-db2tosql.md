---
title: Arbeiten mit der Konsole-Skriptdateien (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5c3080c3-d074-4f99-a5f5-219ebeddc474
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18787dab013e29427743b0712a9d56b28fbddd3e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="working-with-the-sample-console-script-files-db2tosql"></a>Arbeiten mit der Konsole-Skriptdateien (DB2ToSQL)
Einige Beispieldateien wurden zusammen mit dem Produkt für die Benutzer-Verweis und die Verwendung bereitgestellt. Dieser Abschnitt beschreibt die Möglichkeit, diese Skripts, sodass die Endbenutzer Bedürfnissen problemlos anzupassen.  
  
## <a name="sample-console-script-files"></a>Beispiel-Konsole-Skriptdateien  
Referenz für den Benutzer haben die folgenden Konsole Skript Beispieldateien für verschiedene Szenarien bereitgestellt wurde:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
1.  **ServersConnectionFileSample.xml:**  
  
    -   In diesem Beispiel gibt die verschiedenen Modi des Verbindung verfügbar mit der Quelle und Ziel-Datenbank und der Benutzer kann jedem Modus gemäß der Anforderung auswählen. Dieses Beispiel enthält die Serverdefinitionen.  
  
    -   Der Benutzer kann mit der erforderlichen Datenbank einfach die Werte ändern, um die erforderlichen Quell- und Ziel-Serverdefinitionen verbinden. In das bereitgestellte Beispiel alle Werte bereitgestellt wie Variablenwerte in zur Verfügung stehen die **VariableValueFileSample.xml**.  Alle anderen Verbindungsparameter können aus der Verbindung des Benutzers arbeiten Serverdatei entfernt werden.  
  
    -   Weitere Informationen zum Herstellen einer Verbindung mit dem Quell- und Ziel-Server finden Sie unter [erstellen, die Server-Connection-Dateien &#40; DB2ToSQL &#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md) .  
  
2.  **VariableValueFileSample.xml:** alle Variablen, die in der Beispielkonsole verwendet wurden, Skriptdateien und `ServersConnectionFileSample.xml` haben in dieser Datei sortiert wurden. Beispielskripts-Konsole ausführen, die ersetzen Sie die Beispiel-Variable der Benutzer muss, Werte mit Benutzer definierten Argumente und übergeben Sie diese Datei als ein zusätzliches Befehlszeilenargument zusammen mit der Skriptdatei.  
  
    Weitere Informationen zu Wert Variablendatei, finden Sie unter [erstellen Variable Wertdateien &#40; DB2ToSQL &#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md).  
  
3.  **AssessmentReportGenerationSample.xml:** dieses Beispiel ermöglicht dem Benutzer um einen XML-Bewertung-Bericht zu generieren, die verwendet werden, können vom Benutzer für die Analyse bevor er beginnt, konvertieren und Migrieren von Daten.  
  
    In der `generate-assessment-report` Befehl, der Benutzer hat den Wert den Variablen Zwischenschritte ändern (finden Sie unter **VariableValueFileSample.xml**) in der `object-name` -Attribut auf die Datenbank Namen an, von dem Benutzer verwendet. Je nach Art des Objekts angegeben wird die `object-type` Wert auch geändert werden müssen.  
  
    Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `generate-assessment-report` des Befehls Beispiel 4 von der Konsole Beispielskriptdatei.  
  
    Weitere Informationen zum Erstellen von Berichten finden Sie unter [Generieren von Berichten &#40; DB2ToSQL &#41;](../../ssma/db2/generating-reports-db2tosql.md).  
  
    **Hinweise:**  
  
    Stellen Sie sicher, dass der Wert der Variablen Befehlszeilenargument-Datei an die Konsolenanwendung übergeben wird und VariableValueFileSample.xml wird mit den angegebenen Benutzer aktualisiert Werte.  
  
    Stellen Sie sicher, dass die Server-Verbindung über die Befehlszeile Dateiargument an die Konsolenanwendung übergeben wird und die ServersConnectionFileSample.xml mit Parameterwerten für die richtigen Server aktualisiert wird.  
  
4.  **SqlStatementConversionSample.xml:** in diesem Beispiel kann der Benutzer die entsprechenden generieren `t-sql` Skript für die Quelldatenbank `sql` Befehls als Eingabe bereitgestellt.  
  
    In der `convert-sql-statement` Befehl, der Benutzer hat den Wert den Variablen Zwischenschritte ändern (finden Sie unter **VariableValueFileSample.xml**) in der `context` -Attribut auf den Namen der Datenbank, die vom Benutzer verwendet wird. Die Benutzer benötigen Sie auch so ändern Sie die `sql` -Attributwert auf die Quelldatenbank `sql` -Befehl, der er erforderlich ist, konvertiert werden soll.  
  
    Der Benutzer bieten auch Sql-Dateien konvertiert werden. Dies wurde im veranschaulicht wurde die `convert-sql-statement` des Befehls Beispiel 4 von der Konsole Beispielskriptdatei.  
  
    > [!NOTE]  
    > Stellen Sie sicher, dass der Wert der Variablen Befehlszeilenargument-Datei an die Konsolenanwendung übergeben wird und VariableValueFileSample.xml wird mit den angegebenen Benutzer aktualisiert Werte.  
  
5.  **ConversionAndDataMigrationSample.xml:** in diesem Beispiel kann der Benutzer eine End-to-End-Migration von der Konvertierung in die Datenmigration ausgeführt werden. Die Liste der erforderlichen Attributwerte, die sie ändern, wird im folgenden aufgeführt:  
  
    |Befehlsname|Description|attribute|  
    |----------------|---------------|-------------|  
    |`map-schema`|Schemazuordnung der Quelldatenbank mit dem Zielschema.|`source-schema:`Gibt die Quelldatenbank, die erforderlich sind, konvertiert werden soll.<br /><br />`sql-server-schema`: Gibt an, die Zieldatenbank, die migriert werden|  
    |`convert-schema`|Schemakonvertierung von der Quelle in das Zielschema durchgeführt.<br /><br />Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `convert-schema` des Befehls Beispiel 4 von der Konsole Beispielskriptdatei.|`object-name`: Geben Sie die Quelldatenbank / Objektnamen Sie, die erforderlich sind, konvertiert werden soll. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`|  
    |`synchronize-target`|Synchronisiert die Zielobjekte mit der Zieldatenbank an.<br /><br />Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `synchronize-target` des Befehls Beispiel 3 der Beispielskriptdatei für die Konsole.|`object-name:`Geben Sie die Sql Server-Datenbank / Objektname, der um zu erstellenden erfordert. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`|  
    |`migrate-data`|Migriert die Quelldaten zum Ziel.<br /><br />Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `migrate-data` des Befehls Beispiel 2 dieses der Beispielskriptdatei für die Konsole.|`object-name:`Gibt an, die Quelldatenbank / Tabellen Namen, die für die Migration erforderlich sind. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`|  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen Variablenwert Dateien &#40; DB2ToSQL &#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
[Erstellen die Server-Connection-Dateien &#40; DB2ToSQL &#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
[Generieren von Berichten &#40; DB2ToSQL &#41;](../../ssma/db2/generating-reports-db2tosql.md)  
  
