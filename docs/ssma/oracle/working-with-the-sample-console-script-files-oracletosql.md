---
title: Arbeiten mit der Konsole-Skriptdateien (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Sample Console Script Files, ServersConnectionFileSample.xml
- Sample Console Script Files, SqlStatementConversionSample.xml
- Sample Console Script Files,VariableValueFileSample.xml
ms.assetid: c6202dcc-b994-457b-9b2f-0cd89e79792d
caps.latest.revision: "9"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 0f5b0bf819c5e4097e14bddedaee2efb8ce63c6e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="working-with-the-sample-console-script-files-oracletosql"></a>Arbeiten mit der Konsole-Skriptdateien (OracleToSQL)
Einige Beispieldateien wurden zusammen mit dem Produkt für die Benutzer-Verweis und die Verwendung bereitgestellt. Dieser Abschnitt beschreibt die Möglichkeit, diese Skripts, sodass die Endbenutzer Bedürfnissen problemlos anzupassen.  
  
## <a name="sample-console-script-files"></a>Beispiel-Konsole-Skriptdateien  
Referenz für den Benutzer haben die folgenden Konsole Skript Beispieldateien für verschiedene Szenarien bereitgestellt wurde:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   In diesem Beispiel gibt die verschiedenen Modi des Verbindung verfügbar mit der Quelle und Ziel-Datenbank und der Benutzer kann jedem Modus gemäß der Anforderung auswählen. Dieses Beispiel enthält die Serverdefinitionen.  
  
    -   Der Benutzer kann mit der erforderlichen Datenbank einfach die Werte ändern, um die erforderlichen Quell- und Ziel-Serverdefinitionen verbinden. In das bereitgestellte Beispiel alle Werte bereitgestellt wie Variablenwerte in zur Verfügung stehen die **VariableValueFileSample.xml**.  Alle anderen Verbindungsparameter können aus der Verbindung des Benutzers arbeiten Serverdatei entfernt werden.  
  
    -   Weitere Informationen zum Herstellen einer Verbindung mit dem Quell- und Ziel-Server finden Sie unter [erstellen, die Server-Connection-Dateien &#40; OracleToSQL &#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) .  
  
-   **VariableValueFileSample.xml:** alle Variablen, die in der Beispielkonsole verwendet wurden, Skriptdateien und `ServersConnectionFileSample.xml` haben in dieser Datei sortiert wurden. Beispielskripts-Konsole ausführen, die ersetzen Sie die Beispiel-Variable der Benutzer muss, Werte mit Benutzer definierten Argumente und übergeben Sie diese Datei als ein zusätzliches Befehlszeilenargument zusammen mit der Skriptdatei.  
  
    Weitere Informationen zu Wert Variablendatei, finden Sie unter [erstellen Variable Wertdateien &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
-   **AssessmentReportGenerationSample.xml:** dieses Beispiel ermöglicht dem Benutzer um einen XML-Bewertung-Bericht zu generieren, die verwendet werden, können vom Benutzer für die Analyse bevor er beginnt, konvertieren und Migrieren von Daten.  
  
    In der `generate-assessment-report` Befehl, der Benutzer hat den Wert den Variablen Zwischenschritte ändern (finden Sie unter **VariableValueFileSample.xml**) in der `object-name` -Attribut auf die Datenbank Namen an, von dem Benutzer verwendet. Je nach Art des Objekts angegeben wird die `object-type` Wert auch geändert werden müssen.  
  
    Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `generate-assessment-report` des Befehls Beispiel 4 von der Konsole Beispielskriptdatei.  
  
    Weitere Informationen zum Erstellen von Berichten finden Sie unter [Generieren von Berichten &#40; OracleToSQL &#41;](../../ssma/oracle/generating-reports-oracletosql.md).  
  
    > [!NOTE]  
    > -   Stellen Sie sicher, dass der Wert der Variablen Befehlszeilenargument-Datei an die Konsolenanwendung übergeben wird und VariableValueFileSample.xml wird mit den angegebenen Benutzer aktualisiert Werte.  
    > -   Stellen Sie sicher, dass die Server-Verbindung über die Befehlszeile Dateiargument an die Konsolenanwendung übergeben wird und die ServersConnectionFileSample.xml mit Parameterwerten für die richtigen Server aktualisiert wird.  
  
-   **SqlStatementConversionSample.xml:**  
    Dieses Beispiel ermöglicht dem Benutzer die entsprechenden generieren `t-sql` Skript für die Quelldatenbank `sql` Befehls als Eingabe bereitgestellt.  
  
    In der `convert-sql-statement` Befehl, der Benutzer hat den Wert den Variablen Zwischenschritte ändern (finden Sie unter **VariableValueFileSample.xml**) in der `context` -Attribut auf den Namen der Datenbank, die vom Benutzer verwendet wird. Die Benutzer benötigen Sie auch so ändern Sie die `sql` -Attributwert auf die Quelldatenbank `sql` -Befehl, der er erforderlich ist, konvertiert werden soll.  
  
    Der Benutzer bieten auch Sql-Dateien konvertiert werden. Dies wurde im veranschaulicht wurde die `convert-sql-statement` des Befehls Beispiel 4 von der Konsole Beispielskriptdatei.  
  
    > [!NOTE]  
    > Stellen Sie sicher, dass der Wert der Variablen Befehlszeilenargument-Datei an die Konsolenanwendung übergeben wird und VariableValueFileSample.xml wird mit den angegebenen Benutzer aktualisiert Werte.  
  
-   **ConversionAndDataMigrationSample.xml:**  
     In diesem Beispiel kann der Benutzer eine End-to-End-Migration von der Konvertierung in die Datenmigration ausgeführt werden. Die Liste der erforderlichen Attributwerte, die sie ändern, wird im folgenden aufgeführt:  
  
    **Befehlsname**  
  
    `map-schema`  
  
    Schemazuordnung der Quelldatenbank mit dem Zielschema.  
  
    **Attribut**  
  
    -   `source-schema:`Gibt die Quelldatenbank, die erforderlich sind, konvertiert werden soll.  
  
    -   `sql-server-schema`: Gibt an, die Zieldatenbank, die migriert werden  
  
    **Befehlsname**  
  
    `convert-schema`  
  
    -   Schemakonvertierung von der Quelle in das Zielschema durchgeführt.  
  
    -   Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `convert-schema` des Befehls Beispiel 4 von der Konsole Beispielskriptdatei.  
  
    **Attribut**  
  
    `object-name`: Geben Sie die Quelldatenbank / Objektnamen Sie, die erforderlich sind, konvertiert werden soll. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`  
  
    **Befehlsname**  
  
    `synchronize-target`  
  
    -   Synchronisiert die Zielobjekte mit der Zieldatenbank an.  
  
    -   Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `synchronize-target` des Befehls Beispiel 3 der Beispielskriptdatei für die Konsole.  
  
    **Attribut**  
  
    `object-name:`Geben Sie die Sql Server-Datenbank / Objektname, der um zu erstellenden erfordert. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`  
  
    **Befehlsname**  
  
    `migrate-data`  
  
    -   Migriert die Quelldaten zum Ziel.  
  
    -   Wenn der Benutzer verfügt über mehrere Objekte bewerten / Datenbanken er mehrere festlegbaren `metabase-object` Knoten wie im veranschaulicht die `migrate-data` des Befehls Beispiel 2 dieses der Beispielskriptdatei für die Konsole.  
  
    **Attribut**  
  
    `object-name:`Gibt an, die Quelldatenbank / Tabellen Namen, die für die Migration erforderlich sind. Sicherstellen, dass das entsprechende `object-type` wird basierend auf den Typ des Objekts, das im angegebenen geändert, die`object-name`  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen Variablenwert Dateien &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
[Erstellen die Server-Connection-Dateien &#40; OracleToSQL &#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
[Generieren von Berichten &#40; OracleToSQL &#41;](../../ssma/oracle/generating-reports-oracletosql.md)  
  
