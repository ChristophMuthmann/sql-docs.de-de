---
title: Bearbeiten von Tabellen | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aece26acf5992160124dfa14eda26a524e82ff5a
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="edit-tables"></a>Bearbeiten von Tabellen
  Verwenden Sie die Registerkarte **Tabellen** , um Änderungen an den Tabellen und Spalten vorzunehmen, die Sie in der Oracle-Quelldatenbank ausgewählt haben. Diese Registerkarte verfügt über die folgenden Elemente:  
  
 **Liste 'Tabelle'**  
 Die Tabellenliste enthält drei Spalten:  
  
-   **Oracle Table Name**: Der Name der Tabelle, einschließlich des Tabellenschemas.  
  
-   **Capture Instance:**Der Name der Aufzeichnungsinstanz, die für die Benennung der instanzspezifischen Change Data Capture-Objekte verwendet wird. Die Aufzeichnungsinstanz darf nicht NULL sein. Wenn der Name nicht angegeben ist, wird er vom Namen des Quellschemas sowie vom Namen der Quelltabelle im Format `<schema-name>_<table-name>.` abgeleitet. Der Name der Aufzeichnungsinstanz darf maximal 100 Zeichen umfassen und muss innerhalb der Datenbank eindeutig sein. Sie können in dieser Spalte in jede Zelle klicken, um die **capture_instance**manuell zu bearbeiten.  
  
-   **Security Role**: Der Name der Datenbankrolle, mit deren Hilfe der Zugriff auf die Änderungsdaten erlangt wird. Sie können in dieser Spalte in jede Zelle klicken, um die **security_role**manuell zu bearbeiten.  
  
 **Tabellen hinzufügen**  
 Klicken Sie auf **Tabellen hinzufügen** , um das Dialogfeld „Tabellenauswahl“ zu öffnen und den Schritt [Hinzufügen von Tabellen zu einer CDC-Instanz](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)auszuführen. Bei der ersten Sitzung, bei der Sie auf die Oracle-Datenbank zugreifen, müssen Sie den Schritt [Connect to Oracle](../../integration-services/change-data-capture/connect-to-oracle.md)ausführen.  
  
 **Bearbeiten**  
 Wählen Sie in der Liste eine Tabelle aus, und wählen Sie **Bearbeiten** aus, um das Dialogfeld **Eigenschaften** für die Tabelle zu öffnen, in dem Sie den Schritt [Bearbeiten der Tabelleneigenschaften](../../integration-services/change-data-capture/edit-the-table-properties.md)ausführen können.  
  
> [!NOTE]  
>  Sie können die Typzuordnung nicht für Tabellen bearbeiten, die bereits über Spiegeltabellen verfügen. Dies ist nur für neue Tabellen möglich.  
  
 **Entfernen**  
 Wählen Sie in der Liste eine Tabelle aus, und klicken Sie auf **Entfernen** , um die Tabelle aus der CDC-Instanz zu entfernen.  
  
## <a name="see-also"></a>Siehe auch  
 [Gewusst wie: Bearbeiten der CDC-Instanzeigenschaften](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Wählen Sie Oracle-Tabellen und Spalten](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  

