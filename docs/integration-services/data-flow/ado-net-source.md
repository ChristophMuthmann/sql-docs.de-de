---
title: ADO NET-Quelle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.adonetsource.f1
- sql13.dts.designer.adonetsource.connection.f1
- sql13.dts.designer.adonetsource.columns.f1
- sql13.dts.designer.adonetsource.erroroutput.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
caps.latest.revision: 101
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 9e7aade0a21f0a77d05c0550aac8aed5b1ace4d8
ms.contentlocale: de-de
ms.lasthandoff: 08/17/2017

---
# <a name="ado-net-source"></a>ADO NET-Quelle
  Die ADO NET-Quelle verwendet Daten von einem .NET-Anbieter und stellt sie dem Datenfluss zur Verfügung.  
  
 Sie können mithilfe der ADO.NET-Quelle eine Verbindung mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]herstellen. Das Herstellen einer Verbindung mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)] über OLE DB wird nicht unterstützt. Weitere Informationen zu [!INCLUDE[ssSDS](../../includes/sssds-md.md)]finden Sie unter [Azure SQL-Datenbanken – Allgemeine Einschränkungen und Leitlinien](http://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="data-type-support"></a>Datentypunterstützung  
 Die Quelle konvertiert alle Datentypen, die nicht einem bestimmten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentyp zugeordnet sind, in den DT_NTEXT-Datentyp von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Diese Konvertierung findet auch dann statt, wenn der Datentyp **System.Object**ist.  
  
 Sie können den Datentyp DT_NTEXT in den Datentyp DT_WSTR oder DT_WSTR in DT_NTEXT ändern. Datentypen werden durch Festlegen der Eigenschaft **DataType** im Dialogfeld **Erweiterter Editor** der ADO NET-Quelle geändert. Weitere Informationen finden Sie unter [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 Der DT_NTEXT-Datentyp kann mithilfe einer Transformation für Datenkonvertierung nach der ADO NET-Quelle auch in die Datentypen DT_BYTES oder DT_STR konvertiert werden. Weitere Informationen finden Sie unter [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]werden die Datenquellentypen DT_DBDATE, DT_DBTIME, DT_DBTIMESTAMP2 und DT_DBTIMESTAMPOFFSET bestimmten Datumsdatentypen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugeordnet. Sie können die ADO NET-Quelle so konfigurieren, dass die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendeten Datumsdatentypen in die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendeten Datumsdatentypen konvertiert werden. Die ADO NET-Quelle wird zum Konvertieren dieser Datumsdatentypen konfiguriert, indem die Eigenschaft **Typsystemversion** des [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Managers auf **Neueste**festgelegt wird. (Die Eigenschaft **Typsystemversion** befindet sich auf der Seite **Alle** des Dialogfelds **Verbindungs-Manager** . Doppelklicken Sie mit der rechten Maustaste auf den **-Verbindungs-Manager, und klicken Sie anschließend auf** Bearbeiten [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , um das Dialogfeld **Verbindungs-Manager**zu öffnen.)  
  
> [!NOTE]  
>  Wenn die Eigenschaft **Typsystemversion** des [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Managers auf **SQL Server 2005**festgelegt ist, konvertiert das System die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datumsdatentypen in DT_WSTR.  
  
 Die benutzerdefinierten Datentypen (UDTs) werden vom System in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Blobs (Binary Large Objects) konvertiert, wenn der [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager den Anbieter als .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) festlegt. Das System wendet die folgenden Regeln an, wenn es den UDT-Datentyp konvertiert:  
  
-   Wenn die UDT-Daten nicht umfangreich sind, konvertiert das System die Daten in DT_BYTES.  
  
-   Sind die UDT-Daten nicht umfangreich und ist die Eigenschaft **Länge** der Datenbankspalte auf -1 oder einen Wert über 8.000 Byte festgelegt, werden die Daten vom System in DT_IMAGE konvertiert.  
  
-   Wenn die UDT-Daten umfangreich sind, konvertiert das System die Daten in DT_IMAGE.  
  
    > [!NOTE]  
    >  Ist die ADO NET-Quelle nicht zum Verwenden einer Fehlerausgabe konfiguriert, gibt das System die Daten an die DT_IMAGE-Spalte in Abschnitten von jeweils 8.000 Bytes weiter. Ist die ADO NET-Quelle zum Verwenden einer Fehlerausgabe konfiguriert, gibt das System das gesamte Array an Bytes an die DT_IMAGE-Spalte weiter. Weitere Informationen zum Konfigurieren von Komponenten zur Verwendung der Fehlerausgabe finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).  
  
 Weitere Informationen zu den Datentypen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , den unterstützten Datentypkonvertierungen sowie der Datentypzuordnung über bestimmte Datenbanken, darunter auch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [SQL Server Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Weitere Informationen zur Zuordnung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentypen zu verwalteten Datentypen finden Sie unter [Verwenden von Datentypen im Datenfluss](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="ado-net-source-troubleshooting"></a>Problembehandlung der ADO NET-Quelle  
 Sie können die von der ADO NET-Quelle an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Laden von Daten aus externen Datenquellen durch die ADO NET-Quelle behandeln. Aktivieren Sie zum Protokollieren der von der ADO NET-Quelle an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandlung von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="ado-net-source-configuration"></a>ADO NET-Quellkonfiguration  
 Zum Konfigurieren der ADO NET-Quelle geben Sie die SQL-Anweisung an, die das Resultset definiert. Beispielsweise extrahiert eine ADO NET-Quelle, die eine Verbindung mit der [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] -Datenbank herstellt und die SQL-Anweisung `SELECT * FROM Production.Product` verwendet, alle Zeilen aus der **Production.Product** -Tabelle und stellt das Dataset einer Downstreamkomponente bereit.  
  
> [!NOTE]  
>  Wenn Sie mithilfe einer SQL-Anweisung eine gespeicherte Prozedur aufrufen, die Ergebnisse von einer temporären Tabelle zurückgibt, verwenden Sie die Option WITH RESULT SETS, um Metadaten für das Resultset zu definieren.  
  
> [!NOTE]  
>  Wenn Sie zum Ausführen einer gespeicherten Prozedur eine SQL-Anweisung verwenden und der folgende Paketfehler auftritt, können Sie den Fehler u.U. beheben, indem Sie die **SET FMTONLY OFF** -Anweisung vor der EXEC-Anweisung hinzufügen.  
>   
>  **Die Spalte <Spaltenname> wurde in der Datenquelle nicht gefunden.**  
  
 Die ADO NET-Quelle verwendet den [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle, und der Verbindungs-Manager gibt den .NET-Anbieter an. Weitere Informationen finden Sie unter [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
 Die ADO NET-Quelle weist eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von ADO.NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="ado-net-source-editor-connection-manager-page"></a>ADO.NET-Quellen-Editor (Seite 'Verbindungs-Manager')
  Auf der Seite **Verbindungs-Manager** des Dialogfelds **ADO.NET-Quellen-Editor** wählen Sie den [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager für die Quelle aus. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
 Weitere Informationen zur ADO NET-Quelle finden Sie unter [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **So öffnen Sie die Seite "Verbindungs-Manager"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ADO.NET als Quelle hat.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ADO.NET-Quelle.  
  
3.  Klicken Sie im **ADO.NET-Quellen-Editor**auf **Verbindungs-Manager**.  
  
### <a name="static-options"></a>Statische Optionen  
 **ADO.NET-Verbindungs-Manager**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **ADO.NET-Verbindungs-Manager konfigurieren** einen neuen Verbindungs-Manager.  
  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Option|Beschreibung|  
|------------|-----------------|  
|Tabelle oder Sicht|Rufen Sie Daten aus einer Tabelle oder Sicht in der [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Datenquelle ab.|  
|SQL-Befehl|Rufen Sie mit SQL-Abfrage Daten aus der [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Datenquelle ab.|  
  
 **Vorschau**  
 Zeigt mithilfe des Dialogfelds **Datenansicht** eine Vorschau der Ergebnisse an. In der**Vorschau** können bis zu 200 Zeilen angezeigt werden.  
  
> [!NOTE]  
>  In der Datenvorschau enthalten Spalten mit einem CLR-benutzerdefinierten Typ keine Daten. Stattdessen die Werte \<Wert zu groß zum Anzeigen > oder System.Byte [] angezeigt. Der erste Wert wird angezeigt, wenn mithilfe des [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Anbieters auf die Datenquelle zugegriffen wird. Der zweite Wert wird bei Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Anbieters angezeigt.  
  
### <a name="data-access-mode-dynamic-options"></a>Dynamische Optionen (Datenzugriffsmodus)  
  
#### <a name="data-access-mode--table-or-view"></a>Datenzugriffsmodus = Tabelle oder Sicht  
 **Name der Tabelle oder Sicht**  
 Wählen Sie den Namen der Tabelle oder Sicht aus einer Liste der verfügbaren Namen in der Datenquelle aus.  
  
#### <a name="data-access-mode--sql-command"></a>Datenzugriffsmodus = SQL-Befehl  
 **SQL-Befehlstext**  
 Geben Sie den Text einer SQL-Abfrage ein, und erstellen Sie die Abfrage, indem Sie auf **Abfrage erstellen**klicken, oder suchen Sie nach der Datei, die den Abfragetext enthält, indem Sie auf **Durchsuchen**klicken.  
  
 **Build query**  
 Mithilfe des Dialogfelds **Abfrage-Generator** können Sie die SQL-Abfrage visuell erstellen.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie nach der Datei suchen, die den Text der SQL-Abfrage enthält.  
  
## <a name="ado-net-source-editor-columns-page"></a>ADO.NET-Quellen-Editor (Seite 'Spalten')
  Mithilfe der Seite **Spalten** des Dialogfelds **ADO.NET-Quellen-Editor** können Sie jeder externen (Quell-)Spalte eine Ausgabespalte zuordnen.  
  
 Weitere Informationen zur ADO NET-Quelle finden Sie unter [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **So öffnen Sie die Seite "Spalten"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ADO.NET als Quelle hat.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ADO.NET-Quelle.  
  
3.  Klicken Sie im **ADO.NET-Quellen-Editor**auf **Spalten**.  
  
### <a name="options"></a>enthalten  
 **Verfügbare externe Spalten**  
 Zeigt die Liste der in der Datenquelle verfügbaren externen Spalten an. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden.  
  
 **Externe Spalte**  
 Zeigt die externen (Quell-)Spalten in der gleichen Reihenfolge an wie beim Konfigurieren von Komponenten, die Daten aus dieser Quelle verwenden.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen an. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der bereitgestellte Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
## <a name="ado-net-source-editor-error-output-page"></a>ADO.NET-Quellen-Editor (Seite 'Fehlerausgabe')
  Mithilfe der Seite **Fehlerausgabe** des Dialogfelds **ADO.NET-Quellen-Editor** können Sie Fehlerbehandlungsoptionen auswählen und Eigenschaften für Fehlerausgabespalten festlegen.  
  
 Weitere Informationen zur ADO NET-Quelle finden Sie unter [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **So öffnen Sie die Seite "Fehlerausgabe"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ADO.NET als Quelle hat.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ADO NET-Quelle.  
  
3.  Klicken Sie im **ADO.NET-Quellen-Editor**auf **Fehlerausgabe**.  
  
### <a name="options"></a>enthalten  
 **Eingabe/Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen (Quell-)Spalten an, die im Dialogfeld **ADO.NET-Quellen-Editor** auf der Seite **Verbindungs-Manager** ausgewählt wurden.  
  
 **Fehler**  
 Gibt an, was bei Auftreten eines Fehlers geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Gibt an, was im Falle einer Kürzung geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Description**  
 Zeigt die Beschreibung des Fehlers an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Gibt an, was im Falle eines Fehlers oder einer Kürzung mit den ausgewählten Zellen geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
## <a name="see-also"></a>Siehe auch  
 [DataReader-Ziel](../../integration-services/data-flow/datareader-destination.md)   
 [ADO NET-Ziels](../../integration-services/data-flow/ado-net-destination.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  

