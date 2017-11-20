---
title: Spalte Konvertierung Details (Dialogfeld) (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 985ba8a478999a153b3bb32649b98c3e809fc5e8
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>Dialogfeld 'Spaltenkonvertierungsdetails' (SQL Server-Import/Export-Assistent)
  Wenn Sie auf der Seite **Datentypzuordnung überprüfen** auf die Zeile für eine einzelne Spalte doppelklicken, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import-/Export-Assistent das Dialogfeld **Spaltenkonvertierungsdetails** . Auf dieser Seite können Sie die ausführlicheren Konvertierungsinformationen für eine einzelne Spalte überprüfen. Diese Informationen umfassen die folgenden Elemente.
-   Der Datentyp der Spalte auf der Quelle und Ziel.
-   Die Konvertierung des Datentyps, die der Assistent ausführen wird, wenn eine Konvertierung erforderlich ist.
-   Die Datentypzuordnungsdateien, anhand derer der Assistent die erforderliche Datentypkonvertierung bestimmt. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>Screenshot der Seite „Spaltenkonvertierungsdetails“ 
 Der folgende Screenshot zeigt die Seite **Spaltenkonvertierungsdetails** des Assistenten, nachdem der Benutzer auf der Seite **Datentypzuordnung überprüfen** auf eine Zeile doppelt geklickt hat. Wenn Sie sich die Seite **Datentypzuordnung überprüfen** noch einmal ansehen möchten, wechseln Sie zu [Datentypzuordnung überprüfen](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).
 
In diesem Beispiel sehen Sie die folgenden Schritte aus.
-   Die `PersonID` Spalte in der Quelltabelle für die SQL Server ist vom Typ `int`. Der Assistent ordnet diesen Typ zu SQL Server Integration Services (SSIS) `DT_I4` -Datentyp, der eine vier-Byte-Ganzzahl mit Vorzeichen, wird durch einen Verweis auf die Datei datentypzuordnung MSSQLToSSIS10.xml.
-   Die `PersonID` Spalte in der SQL Server-Zieltabelle wird auch vom Typ `int`. Der Assistent ordnet dieses Typs dazu, die den gleichen SSIS-Datentyp.
-   Der Assistent abgeschlossen ist, *diese Spalte ist keine Konvertierung erforderlich*.
 
  
 ![Seite "Spalte Konvertierung" des Import / Export-Assistenten](../../integration-services/import-export-data/media/column-conversion.png "Spalte Konvertierung auf der Seite des Import / Export-Assistenten") 
  
## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie die Spaltenkonvertierungsdetails überprüft und auf **OK**geklickt haben, kehren Sie im Dialogfeld **Spaltenkonvertierungsdetails** zur Seite **Datentypzuordnung überprüfen** zurück. Weitere Informationen finden Sie unter [Datentypzuordnung überprüfen](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Siehe auch
[Zuordnung von Datentypen mit dem SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

