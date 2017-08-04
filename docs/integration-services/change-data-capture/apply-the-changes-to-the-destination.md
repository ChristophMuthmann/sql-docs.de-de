---
title: "Die Änderungen auf das Ziel anzuwenden | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],applying changes
ms.assetid: 338a56db-cb14-4784-a692-468eabd30f41
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f2900e6903553f9eb74cd18aad0c13691073d425
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="apply-the-changes-to-the-destination"></a>Anwenden der Änderungen auf das Ziel
  Im Datenfluss eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets, das ein inkrementelles Laden von Änderungsdaten ausführt, ist der dritte und letzte Task die Anwendung der Änderungen auf Ihr Ziel. Sie benötigen jeweils eine Komponente, um Einfügungen, Updates und Löschungen anzuwenden.  
  
> [!NOTE]  
>  Der zweite Task beim Entwerfen des Datenflusses eines Pakets, das ein inkrementelles Laden von Änderungsdaten ausführt, ist die Trennung von Einfügungen, Updates und Löschungen. Weitere Informationen zu dieser Komponente finden Sie unter [Verarbeiten von Einfügungen, Updates und Löschungen](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md). Eine Beschreibung des Gesamtprozesses zur Erstellung eines Pakets, das ein inkrementelles Laden von Änderungsdaten ausführt, finden Sie unter [Change Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="applying-inserts"></a>Anwenden von Einfügungen  
 Zum Anwenden von Einfügungen verwenden Sie ein OLE DB-Ziel, da die neuen Zeilen keine besondere Behandlung erfordern.  
  
#### <a name="to-process-inserts-by-using-an-ole-db-destination"></a>So verarbeiten Sie Einfügungen mit einem OLE DB-Ziel  
  
1.  Fügen Sie auf der Registerkarte **Datenfluss** ein OLE DB-Ziel hinzu.  
  
2.  Verbinden Sie die Ausgabe, die Einfügungen aus der Transformation für bedingtes Teilen enthält, mit dem OLE DB-Ziel.  
  
3.  Aktivieren Sie im **Ziel-Editor für OLE DB**auf der Seite **Verbindungs-Manager** die folgenden Optionen:  
  
    1.  Wählen Sie einen OLE DB-Verbindungs-Manager für die Zieldatenbank aus oder erstellen Sie einen.  
  
    2.  Wählen Sie eine Option für den **Datenzugriffsmodus** aus, und wählen Sie dann die Zieltabelle aus, oder geben Sie eine SQL-Anweisung mit den Zielspalten ein.  
  
4.  Ordnen Sie auf der Seite **Zuordnungen** des Editors die entsprechenden Spalten von den Änderungsdaten der Zieltabelle zu.  
  
## <a name="applying-updates"></a>Anwenden von Updates  
 Zum Anwenden von Updates verwenden Sie eine Transformation für OLE DB-Befehl. Sie verwenden diese Transformation, da Sie eine parametrisierte UPDATE-Anweisung verwenden müssen, um jeweils eine Zeile mit den neuen Spaltenwerten zu aktualisieren.  
  
> [!NOTE]  
>  Sie können auch Zielkomponenten verwenden, um Updates anzuwenden. Bei dieser Vorgehensweise verwenden Sie die Zielkomponenten, um die Zeilen in temporäre Tabellen zu speichern, die Sie für diesen Zweck erstellen. Sie verwenden dann Tasks "SQL Ausführen", um Massenupdates und Massenlöschungen auf dem Ziel von den temporären Tabellen auszuführen.  
  
#### <a name="to-process-updates-by-using-an-ole-db-command-transformation"></a>So verarbeiten Sie Updates mit einer Transformation für OLE DB-Befehl  
  
1.  Fügen Sie auf der Registerkarte **Datenfluss** eine Transformation für OLE DB-Befehl hinzu.  
  
2.  Verbinden Sie die Ausgabe, die Updates aus der Transformation für bedingtes Teilen enthält, mit der Transformation für OLE DB-Befehl.  
  
3.  Wählen Sie auf der Registerkarte **Verbindungs-Manager**im **Erweiterten Editor für OLE DB-Befehl** für die Zieldatenbank einen OLE DB-Verbindungs-Manager aus, oder erstellen Sie einen.  
  
4.  Geben Sie auf der Registerkarte **Komponenteneigenschaften**im **Erweiterten Editor für OLE DB-Befehl** für **SqlCommand**eine parametrisierte UPDATE-Anweisung ein.  
  
     Zum Beispiel könnte eine UPDATE-Anweisung für eine Customer-Tabelle die folgende Syntax aufweisen:  
  
    ```  
    update CDCSample.Customer  
    set TerritoryID  = ?,  
        CustomerType  = ?,  
        rowguid  = ?,  
        ModifiedDate  = ?  
    where CustomerID = ?  
  
    ```  
  
5.  Ordnen Sie auf der Registerkarte **Spaltenzuordnungen** des Editors den Parametern in der UPDATE-Anweisung die entsprechenden Spalten von den Änderungsdaten zu.  
  
## <a name="applying-deletes"></a>Anwenden von Löschungen  
 Zum Anwenden von Löschungen verwenden Sie eine Transformation für OLE DB-Befehl. Sie verwenden diese Transformation, da Sie eine parametrisierte DELETE-Anweisung verwenden müssen, die jeweils eine einzelne Zeile löscht, die auf dem Spaltenwert basiert, der die Zeile eindeutig identifiziert.  
  
> [!NOTE]  
>  Sie können auch Zielkomponenten verwenden, um Löschungen anzuwenden. Bei dieser Vorgehensweise verwenden Sie die Zielkomponenten, um die Zeilen in temporäre Tabellen zu speichern, die Sie für diesen Zweck erstellen. Sie verwenden dann Tasks "SQL Ausführen", um Massenupdates und Massenlöschungen auf dem Ziel von den temporären Tabellen auszuführen.  
  
#### <a name="to-process-deletes-by-using-an-ole-db-command-transformation"></a>So verarbeiten Sie Löschungen mit einer Transformation für OLE DB-Befehl  
  
1.  Fügen Sie auf der Registerkarte **Datenfluss** eine Transformation für OLE DB-Befehl dem Datenfluss hinzu.  
  
2.  Verbinden Sie die Ausgabe, die Löschungen aus der Transformation für bedingtes Teilen enthält, mit der Transformation für OLE DB-Befehl.  
  
3.  Öffnen Sie den erweiterten Editor, um die Transformation zu konfigurieren.  
  
4.  Wählen Sie auf der Registerkarte **Verbindungs-Manager**im **Erweiterten Editor für OLE DB-Befehl** für die Zieldatenbank einen OLE DB-Verbindungs-Manager aus, oder erstellen Sie einen.  
  
5.  Geben Sie im **Erweiterten Editor für OLE DB-Befehl**auf der Registerkarte **Komponenteneigenschaften** des Editors für **SqlCommand**eine parametrisierte DELETE-Anweisung ein.  
  
     Zum Beispiel könnte eine DELETE-Anweisung für eine Customer-Tabelle die folgende Syntax aufweisen:  
  
    ```  
    delete from Customer where CustomerID = ?  
  
    ```  
  
6.  Ordnen Sie auf der Registerkarte **Spaltenzuordnungen** des Editors die entsprechende Spalte von den Änderungsdaten dem Parameter in der DELETE-Anweisung zu.  
  
## <a name="optimizing-inserts-and-updates-by-using-merge-functionality"></a>Optimieren von Einfügungen und Updates mithilfe der MERGE-Funktionalität  
 Sie können die Verarbeitung von Einfügungen und Updates optimieren, indem Sie bestimmte Change Data Capture-Optionen mit der Verwendung des Transact-SQL-MERGE-Schlüsselworts kombinieren. Weitere Informationen zum MERGE-Schlüsselwort finden Sie unter [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md).  
  
 In der Transact-SQL-Anweisung, mit der die Änderungsdaten abgerufen werden, können Sie *all with merge* als den Wert des *row_filter_option*-Parameters festlegen, wenn Sie die **cdc.fn_cdc_get_net_changes_<capture_instance>**-Funktion aufrufen. Diese Change Data Capture-Funktion arbeitet effizienter, wenn sie nicht die zusätzliche Verarbeitung ausführen muss, die erforderlich ist, um Einfügungen von Updates zu unterscheiden. Wenn Sie den *all with merge* -Parameterwert angeben, ist der **__$operation** -Wert der Änderungsdaten 1 für Löschungen oder 5 für Änderungen, die durch Einfügungen oder Updates verursacht wurden. Weitere Informationen zur Transact-SQL-Funktion, die zum Abrufen der Änderungsdaten verwendet wird, finden Sie unter [Abrufen und Verstehen der Änderungsdaten](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md). Nachdem Sie Änderungen mit dem *all with merge* -Parameterwert abgerufen haben, können Sie Löschungen anwenden und die übrigen Zeilen in eine temporäre Tabelle oder eine Stagingtabelle ausgeben. Sie können dann in einem Downstream-Task 'SQL Ausführen' eine einzelne MERGE-Anweisung verwenden, um alle Einfügungen oder Updates aus der Stagingtabelle auf das Ziel anzuwenden.  
  
  
