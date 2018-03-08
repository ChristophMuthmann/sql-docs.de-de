---
title: "Vornehmen von Änderungen an den zum Aufzeichnen von Änderungen ausgewählten Tabellen | Microsoft-Dokumentation"
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
- makChanToTab
ms.assetid: a309f82a-c6ef-464d-a6ef-df555bfb609a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ed1da57a1599bd386b8eed3d23db92dd427b36b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="make-changes-to-the-tables-selected-for-capturing-changes"></a>Vornehmen von Änderungen an den zum Aufzeichnen von Änderungen ausgewählten Tabellen
  In diesem Dialogfeld können Sie bestimmte Spalten aus der ausgewählten Tabelle auswählen, um dafür Änderungen aufzuzeichnen. Sie können auch die Informationen unter **Security Role** und **Capture Instance** bearbeiten.  
  
 In den Tabellen, die Sie in diesem Dialogfeld für die Aufzeichnung von Änderungen ausgewählt haben, können Sie die folgenden Änderungen vornehmen.  
  
 **Ändern Sie, welche Spalten in die CDC-Instanz eingeschlossen sind:**  
  
 Führen Sie einen oder beide der folgenden Schritte aus:  
  
-   Aktivieren Sie das Kontrollkästchen neben einer beliebigen zusätzlichen Spalte, die Sie einschließen möchten.  
  
-   Deaktivieren Sie das Kontrollkästchen neben den Spalten, die nicht mehr enthalten sein sollen.  
  
 **Ändern Sie den Datentyp für eine bestimmte Spalte**:  
  
 Sie können einen anderen Datentyp für eine bestimmte Spalte auswählen. Der Datentyp kann jedoch nur in einen Datentyp geändert werden, der mit dem ursprünglichen Datentyp kompatibel ist.  
  
 Klicken Sie zum Ändern des Datentyps in die Spalte **Datentyp** , und wählen Sie einen anderen Datentyp aus. Es sind nur Datentypen verfügbar, die mit dem ursprünglichen Datentyp kompatibel sind.  
  
> [!NOTE]  
>  Wenn keine zusätzlichen Datentypen ausgewählt werden können, ist die Dropdownliste nicht verfügbar.  
  
 **Ändern der Sicherheitsrolle**  
  
 Geben Sie im Feld **Security Role** einen neuen Namen ein, oder bearbeiten Sie den Namen der Sicherheitsgatingrolle.  
  
 **Ändern oder Hinzufügen einer Aufzeichnungsinstanz**  
  
 Geben Sie im Feld **Capture Instance** einen Namen für die Aufzeichnungsinstanz ein.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen der Instanz für die SQL Server-Änderungsdatenbank](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Auswählen von Oracle-Tabellen und -Spalten](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
