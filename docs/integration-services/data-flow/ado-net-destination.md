---
title: ADO NET-Ziels | Microsoft Docs
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
- sql13.dts.designer.adonetdest.f1
- sql13.dts.designer.adonetdest.connection.f1
- sql13.dts.designer.adonetdest.mappings.f1
- sql13.dts.designer.adonetdest.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 70508825dfb2bdf60bcd77bdaad9ba9dbb19e7eb
ms.contentlocale: de-de
ms.lasthandoff: 08/17/2017

---
# <a name="ado-net-destination"></a>ADO NET-Ziel
  Das ADO NET-Ziel lädt Daten in eine Reihe von [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-kompatible Datenbanken, die eine Datenbanktabelle oder -sicht verwenden. Sie haben die Möglichkeit, diese Daten in eine vorhandene Tabelle oder Sicht zu laden, oder Sie können eine neue Tabelle erstellen und die Daten in die neue Tabelle laden.  
  
 Sie können mithilfe des ADO.NET-Ziels eine Verbindung mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]herstellen. Das Herstellen einer Verbindung mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)] über OLE DB wird nicht unterstützt. Weitere Informationen zu [!INCLUDE[ssSDS](../../includes/sssds-md.md)]finden Sie unter [Allgemeine Richtlinien und Einschränkungen (Windows Azure SQL-Datenbank)](http://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="troubleshooting-the-ado-net-destination"></a>Problembehandlung des ADO NET-Ziels  
 Sie können die vom ADO NET-Ziel an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Speichern von Daten in externen Datenquellen durch das ADO NET-Ziel behandeln. Aktivieren Sie zum Protokollieren der vom ADO NET-Ziel an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ado-net-destination"></a>Konfigurieren des ADO NET-Ziels  
 Von diesem Ziel wird ein [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle verwendet, und der Verbindungs-Manager gibt den zu verwendenden [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Anbieter an. Weitere Informationen finden Sie unter [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
 Ein ADO NET-Ziel enthält Zuordnungen zwischen Eingabespalten und Spalten in der Zieldatenquelle. Sie müssen nicht allen Zielspalten eine Eingabespalten zuordnen. Die Eigenschaften einiger Zielspalten können jedoch die Zuordnung von Eingabespalten erfordern. Andernfalls könnten Fehler auftreten. Wenn z. B. eine Zielspalte keine NULL-Werte zulässt, muss dieser Zielspalte eine Eingabespalte zugeordnet werden. Darüber hinaus müssen die Datentypen zugeordneter Spalten kompatibel sein. Beispielsweise können Sie eine Eingabespalte mit einem string-Datentyp nicht einer Zielspalte mit einem numerischen Datentyp zuordnen, wenn der [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Anbieter diese Zuordnung nicht unterstützt.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt das Einfügen von Text in Spalten nicht mit dem Datentyp auf image festgelegt ist. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
> [!NOTE]  
>  Die Zuordnung einer Eingabespalte, deren Typ auf DT_DBTIME festgelegt ist, zu einer Datenbankspalte, deren Typ auf datetime festgelegt ist, wird vom ADO NET-Ziel nicht unterstützt. Weitere Informationen zu [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentypen finden Sie unter [Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Das ADO NET-Ziel weist eine reguläre Eingabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von ADO.NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="ado-net-destination-editor-connection-manager-page"></a>ADO.NET-Ziel-Editor (Seite 'Verbindungs-Manager')
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **ADO.NET-Ziel-Editor** können Sie die [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindung für das Ziel auswählen. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
 **So öffnen Sie die Seite "Verbindungs-Manager"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ADO.NET als Ziel hat.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ADO NET-Ziel.  
  
3.  Klicken Sie im **ADO.NET-Ziel-Editor**auf **Verbindungs-Manager**.  
  
### <a name="static-options"></a>Statische Optionen  
 **Connection manager**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **ADO.NET-Verbindungs-Manager konfigurieren** einen neuen Verbindungs-Manager.  
  
 **Tabelle oder Sicht verwenden**  
 Wählen Sie eine vorhandene Tabelle oder Sicht aus der Liste aus, oder erstellen Sie eine neue Tabelle, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle oder Sicht.  
  
> [!NOTE]  
>  Wenn Sie auf **Neu**klicken, generiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Standard-CREATE TABLE-Anweisung auf Grundlage der verbundenen Datenquelle. Diese Standard-CREATE TABLE-Anweisung enthält nicht das FILESTREAM-Attribut, selbst wenn die Quelltabelle eine Spalte mit der Erklärung des FILESTREAM-Attributs enthält. Um eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente mit dem FILESTREAM-Attribut auszuführen, implementieren Sie zunächst die FILESTREAM-Speicherung in der Zieldatenbank. Fügen Sie dann das FILESTREAM-Attribut der CREATE TABLE-Anweisung im Dialogfeld **Tabelle erstellen** hinzu. Weitere Informationen finden Sie unter [Blob-Daten &#40;Binary Large Object, SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
 **Masseneinfügung verwenden, falls verfügbar**  
 Geben Sie an, ob die Schnittstelle <xref:System.Data.SqlClient.SqlBulkCopy> verwendet werden soll, um die Leistung von Masseneinfügungsvorgängen zu verbessern.  
  
 Nur ADO.NET-Anbieter, die ein <xref:System.Data.SqlClient.SqlConnection> -Objekt zurückgeben, unterstützen die Verwendung der <xref:System.Data.SqlClient.SqlBulkCopy> -Schnittstelle. Der .NET-Datenanbieter für SQL Server (SqlClient) gibt ein <xref:System.Data.SqlClient.SqlConnection> -Objekt zurück, und ein benutzerdefinierter Anbieter gibt möglicherweise ein <xref:System.Data.SqlClient.SqlConnection> -Objekt zurück.  
  
 Sie können den .NET-Datenanbieter für SQL Server (SqlClient) verwenden, um eine Verbindung mit [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]herzustellen.  
  
 Wenn Sie **Masseneinfügung verwenden, falls verfügbar**auswählen und für **Zeile umleiten** die Option **Fehler**festlegen, enthält der Datenbatch, der vom Ziel an die Fehlerausgabe umgeleitet wird, möglicherweise intakte Zeilen. Weitere Informationen zur Behandlung von Fehlern in Massenvorgängen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md). Weitere Informationen zur Option **Zeile umleiten** finden Sie unter [Ziel-Editor für ADO.NET &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]  
>  Wenn eine SQL Server oder Sybase-Quelltabelle eine Identitätsspalte enthält, müssen Sie "SQL ausführen"-Tasks verwenden, um IDENTITY_INSERT vor der ADO NET-Ziel zu aktivieren und deaktivieren Sie es danach erneut. (Die identitätsspalteneigenschaft gibt einen inkrementellen Wert für die Spalte an. Die SET IDENTITY_INSERT-Anweisung kann die expliziten Werte aus der Quelltabelle in die Identitätsspalte in der Zieltabelle eingefügt werden.)  
>   
>   Um die SET IDENTITY_INSERT-Anweisungen und erfolgreich Laden der Daten auszuführen, müssen Sie folgende Schritte auszuführen.
>       1. Verwenden Sie den gleichen ADO.NET-Verbindungs-Manager aus, für die SQL ausführen-Tasks und die ADO.NET-Ziel.
>       2. Legen Sie auf den Verbindungs-Manager die **RetainSameConnection** Eigenschaft und die **MultipleActiveResultSets** Eigenschaft auf "true".
>       3. Legen Sie die ADO.NET-Ziel die **UseBulkInsertWhenPossible** Eigenschaft auf "false".
>
>  Weitere Informationen finden Sie unter [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) und [IDENTITY &#40;Eigenschaft&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md).  
  
## <a name="external-resources"></a>Externe Ressourcen  
 Technischer Artikel [Schnelles Laden von Daten in eine Windows Azure SQL-Datenbank](http://go.microsoft.com/fwlink/?LinkId=244333)auf sqlcat.com  
  
## <a name="ado-net-destination-editor-mappings-page"></a>ADO.NET-Ziel-Editor (Seite 'Zuordnungen')
  Auf der Seite **Zuordnungen** des Dialogfelds **ADO.NET-Ziel-Editor** können Sie eine Zuordnung von Eingabe- zu Zielspalten vornehmen.  
  
 **So öffnen Sie die Seite "Zuordnungen"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ADO.NET als Ziel hat.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ADO.NET-Ziel.  
  
3.  Klicken Sie im **ADO.NET-Ziel-Editor**auf **Zuordnungen**.  
  
### <a name="options"></a>enthalten  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Eingabespalten in der Tabelle Zielspalten zuordnen.  
  
 **Verfügbare Zielspalten**  
 Zeigt die Liste der verfügbaren Zielspalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Zielspalten in der Tabelle Eingabespalten zuordnen.  
  
 **Eingabespalte**  
 Zeigt die von Ihnen ausgewählten Eingabespalten an. Sie können Zuordnungen entfernen, indem Sie auswählen  **\<ignorieren >** um Spalten aus der Ausgabe auszuschließen.  
  
 **Zielspalte**  
 Zeigt alle verfügbaren Zielspalten an, ganz gleich, ob sie zugeordnet sind oder nicht.  
  
## <a name="ado-net-destination-editor-error-output-page"></a>ADO.NET-Ziel-Editor (Seite 'Fehlerausgabe')
  Auf der Seite **Fehlerausgabe** des Dialogfelds **ADO.NET-Ziel-Editor** geben Sie Optionen für die Fehlerbehandlung an.  
  
 **So öffnen Sie die Seite "Fehlerausgabe"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ADO.NET als Ziel hat.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ADO NET-Ziel.  
  
3.  Klicken Sie im **ADO.NET-Ziel-Editor**auf **Fehlerausgabe**.  
  
### <a name="options"></a>enthalten  
 **Eingabe oder Ausgabe**  
 Zeigt den Namen der Eingabe an.  
  
 **Column**  
 Wird nicht verwendet.  
  
 **Fehler**  
 Gibt an, was bei Auftreten eines Fehlers geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Wird nicht verwendet.  
  
 **Description**  
 Zeigt die Beschreibung des Vorgangs an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Gibt an, was im Falle eines Fehlers oder einer Kürzung mit den ausgewählten Zellen geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
  
