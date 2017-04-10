---
title: "Problembehandlung von Verarbeitungsdaten (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 678f523c-e181-4456-9a54-7b7bf044b8d2
caps.latest.revision: 12
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 12
---
# Problembehandlung von Verarbeitungsdaten (SSAS – tabellarisch)
  Dieses Thema enthält Informationen zur Verarbeitung (Aktualisierung) von Modelldaten, wenn ein Modell mit [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] erstellt wird. Das Thema enthält keine Informationen zur Verarbeitung von Daten in Modellen, die für eine Analysis Services-Serverinstanz bereitgestellt wurden. Weitere Informationen zur Verarbeitung von Daten in einem bereitgestellten Modell finden Sie unter [Skriptverwaltungsaufgaben in Analysis Services](../analysis-services/instances/script-administrative-tasks-in-analysis-services.md).  
  
 Abschnitte in diesem Thema:  
  
-   [Funktionsweise der Datenverarbeitung](#bkmk_how_df_works)  
  
-   [Auswirkungen der Datenverarbeitung](#bkmk_impact_of_df)  
  
-   [Bestimmen der Datenquelle](#bkmk_det_source)  
  
-   [Bestimmen, wann die Daten zuletzt aktualisiert wurden](#bkmk_det_last_ref)  
  
-   [Einschränkungen für aktualisierbare Datenquellen](#bkmk_restrictions)  
  
-   [Einschränkungen für Änderungen an einer Datenquelle](#bkmk_rest_changes)  
  
##  <a name="bkmk_how_df_works"></a> Funktionsweise der Datenverarbeitung  
 Wenn Sie Daten verarbeiten, werden die Daten im Modell-Designer durch neue Daten ersetzt. Sie können nicht einfach neue Datenzeilen importieren oder Daten ändern. Der Modell-Designer kann nicht nachverfolgen, welche Zeilen zuvor hinzugefügt wurden.  
  
 Die Verarbeitung der Daten findet als Transaktion statt. Das bedeutet, sobald Sie mit dem Aktualisieren der Daten beginnen, kann das gesamte Update entweder erfolgreich sein oder fehlschlagen. Sie haben also nie Daten, die teilweise richtig sind.  
  
 Die manuelle Datenverarbeitung, die Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] initiieren, wird von der lokalen Analysis Services-Instanz im Arbeitsspeicher ausgeführt. Daher kann der Datenverarbeitungsvorgang die Leistung anderer Aufgaben auf dem Computer beeinträchtigen. Wenn Sie jedoch die automatische Verarbeitung der Daten mittels eines Skripts in einem bereitgestellten Modell planen, verwaltet die Analysis Services-Instanz den Importvorgang einschließlich seiner zeitlichen Steuerung.  
  
##  <a name="bkmk_impact_of_df"></a> Auswirkungen der Datenverarbeitung  
 Durch die Datenverarbeitung wird normalerweise die Neuberechnung der Daten ausgelöst.  Verarbeiten von Daten bedeutet, dass aktuelle Daten aus den externen Quellen abgerufen werden; Neuberechnen bedeutet, dass das Ergebnis aller Formeln aktualisiert wird, für die sich die Daten geändert haben. Ein Verarbeitungsvorgang löst normalerweise eine Neuberechnung aus.  
  
 Daher sollten Sie immer die möglichen Auswirkungen beachten, bevor Sie Datenquellen ändern oder die Daten verarbeiten, die aus der Datenquelle abgerufen werden. Zudem sollten Sie sich über die möglichen Folgen im Klaren sein:  
  
-   Möglicherweise sind einige der Modelldaten aufgrund der Änderungen an der Datenquelle beschädigt. Wenn nicht alle Spalten aus der Datenquelle abgerufen werden können (da sie z. B. gelöscht oder geändert wurden), schlägt die Verarbeitung fehl, und Sie müssen die Zuordnungen zwischen den Quell- und Modelldaten aktualisieren. Weitere Informationen finden Sie unter [Bearbeiten einer vorhandenen Datenquellenverbindung &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/edit-an-existing-data-source-connection-ssas-tabular.md).  
  
-   Nach der Verarbeitung wird ggf. angezeigt, dass einige Spalten einen Fehler enthalten. Dies kann folgende Ursachen haben: Die DAX-Formel in der Spalte verwendet Daten, die bei der Verarbeitung nicht verfügbar wurden, der Datentyp einer Spalte hat sich geändert oder den externen Daten wurde ein ungültiger Wert hinzugefügt. Um das Problem zu beheben, können Sie die Formel bearbeiten, oder Sie können die Spalte löschen, wenn diese auf nicht mehr verfügbaren Daten basiert.  
  
-   Formeln, die die aktualisierten Daten verwenden, müssen neu berechnet werden. Je nach Größe des Modells kann dies einige Zeit in Anspruch nehmen.  
  
-   Wenn das Modell mehrere Datenquellen enthält, müssen Sie ggf. das ganze Modell (Alles verarbeiten) verarbeiten, auch wenn sich nur eine externe Datenquelle geändert hat. Dies kann z. B. der Fall sein, wenn Sie Measures erstellen, die berechnete Spalten benötigen und die berechneten Spalten Werte aus anderen berechneten Spalten verwenden. Der Modell-Designer analysiert dann zuerst die Abhängigkeiten und verarbeitet anschließend der Reihe nach die ganze Kette verbundener Objekte. Je nach Komplexität der Abhängigkeiten kann dies sehr lange dauern.  
  
-   Wenn Sie einen Filter ändern, muss das ganze Modell neu berechnet werden.  
  
##  <a name="bkmk_det_source"></a> Bestimmen der Datenquelle  
 Wenn Sie nicht sicher sind, woher die Daten im Modell stammen, können Sie mithilfe der Tools in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] Details wie den Quelldateinamen und den Pfad abrufen.  
  
#### So ermitteln Sie die Quelle der vorhandenen Daten  
  
1.  Wählen Sie im Modell-Designer die Tabelle mit den Daten aus, deren Quelle Sie ermitteln möchten.  
  
2.  Klicken Sie im Menü **Tabelle** auf **Tabelleneigenschaften**.  
  
3.  Notieren Sie im Dialogfeld **Tabelleneigenschaften bearbeiten** den Wert, der für **Verbindungsname**aufgeführt ist.  
  
4.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]auf das Menü **Modell** und dann auf **Vorhandene Verbindungen**.  
  
5.  Wählen Sie im Dialogfeld **Vorhandene Verbindungen** die Datenquelle mit dem Namen aus, den Sie in Schritt 3 ermittelt haben. Klicken Sie dann auf **Bearbeiten**.  
  
6.  Im Dialogfeld **Verbindungen bearbeiten** werden die Verbindungsinformationen angezeigt, z. B. Datenbankname, Dateipfad oder Berichtspfad.  
  
##  <a name="bkmk_det_last_ref"></a> Bestimmen, wann die Daten zuletzt aktualisiert wurden  
 Anhand der Tabelleneigenschaften können Sie feststellen, wann die Daten zuletzt aktualisiert wurden.  
  
#### So suchen Sie das Datum und die Uhrzeit der letzten Verarbeitung einer Tabelle  
  
1.  Wählen Sie im Modell-Designer die Tabelle mit den Daten aus, deren Aktualisierungszeitpunkt Sie ermitteln möchten.  
  
2.  Klicken Sie im Menü **Tabelle** auf **Tabelleneigenschaften**.  
  
3.  Im Dialogfeld **Tabelleneigenschaften bearbeiten** wird unter **Letzte Aktualisierung** das Datum angezeigt, an dem die Tabelle zuletzt aktualisiert wurde.  
  
##  <a name="bkmk_restrictions"></a> Einschränkungen für aktualisierbare Datenquellen  
 Einige Einschränkungen gelten für die Datenquellen, die von einem bereitgestellten Modell auf einer Analysis Services-Instanz automatisch verarbeitet werden können. Sie sollten nur Datenquellen auswählen, die die folgenden Kriterien erfüllen:  
  
-   Die Datenquelle muss zum Zeitpunkt der Datenverarbeitung sowie am angegebenen Speicherort verfügbar sein. Wenn sich die ursprüngliche Datenquelle auf einem lokalen Laufwerk des Benutzers befindet, der das Modell erstellt hat, müssen Sie diese Datenquelle entweder aus dem Datenverarbeitungsvorgang ausschließen oder eine Möglichkeit finden, die Datenquelle an einem Speicherort zu veröffentlichen, auf den über eine Netzwerkverbindung zugegriffen werden kann. Wenn Sie eine Datenquelle an einen Netzwerkspeicherort verschieben, müssen Sie das Modell im Modell-Designer öffnen und die Schritte zum Abrufen der Daten wiederholen. Dies ist notwendig, um die in den Eigenschaften der Datenquellenverbindung gespeicherten Verbindungsinformationen wiederherzustellen.  
  
-   Auf die Datenquelle muss über die Anmeldeinformationen zugegriffen werden, die in die Datenquellenverbindung eingebettet sind. Eingebettete Anmeldeinformationen werden in der Datenquellenverbindung erstellt, wenn Sie eine Verbindung mit der externen Datenquelle herstellen.  
  
-   Die Datenverarbeitung muss für alle angegebenen Datenquellen erfolgreich verlaufen. Andernfalls werden die verarbeiteten Daten verworfen und die zuletzt gespeicherte Version des Modells verwendet. Schließen Sie alle Datenquellen, bei denen Sie unsicher sind, aus.  
  
-   Durch die Datenverarbeitung dürfen keine anderen Daten im Modell ungültig werden. Wenn Sie eine Teilmenge der Daten verarbeiten, ist es wichtig zu wissen, ob das Modell weiterhin gültig ist, sobald neuere Daten mit statischen Daten aggregiert werden, die nicht aus dem gleichen Zeitraum stammen. Als Modell-Designer sollten Sie die Datenabhängigkeiten genau kennen und sicherstellen, dass die Datenverarbeitung auch für das Modell geeignet ist.  
  
     Auf eine externe Datenquelle wird über eine eingebettete Verbindungszeichenfolge, eine URL oder einen UNC-Pfad zugegriffen, die Sie beim Importieren der ursprünglichen Daten in das Modell unter Verwendung des Tabellenimport-Assistenten angegeben haben. Die ursprünglichen, in der Datenquellenverbindung gespeicherten Verbindungsinformationen werden für nachfolgende Datenaktualisierungsvorgänge wiederverwendet. Es werden keine separaten Verbindungsinformationen zu Datenverarbeitungszwecken erstellt und verwaltet, sondern nur vorhandene Verbindungsinformationen verwendet.  
  
##  <a name="bkmk_rest_changes"></a> Einschränkungen für Änderungen an einer Datenquelle  
 Für die Änderungen, die Sie an einer Datenquelle vornehmen können, gelten einige Einschränkungen:  
  
-   Die Datentypen einer Spalte können nur in einen kompatiblen Datentyp geändert werden. Wenn die Daten in der Spalte z. B. Dezimalzahlen enthalten, können Sie den Datentyp nicht in "Ganze Zahl" (Integer) ändern. Sie können jedoch numerische Daten in Text ändern. Weitere Informationen zu Datentypen finden Sie unter [Unterstützte Datentypen &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
-   Sie können nicht in verschiedenen Tabellen gleichzeitig mehrere Spalten auswählen und die Eigenschaften der Spalten ändern. Sie können nur mit jeweils einer Tabelle oder Sicht arbeiten.  
  
## Siehe auch  
 [Manuelle Verarbeitung von Daten &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/manually-process-data-ssas-tabular.md)   
 [Bearbeiten einer vorhandenen Datenquellenverbindung &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/edit-an-existing-data-source-connection-ssas-tabular.md)  
  
  