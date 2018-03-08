---
title: "Dialogfeld „Spaltenkonvertierungsdetails“ (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation"
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d4adb7bfee3533830b3d806b666ee8866fc57bb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>Dialogfeld 'Spaltenkonvertierungsdetails' (SQL Server-Import/Export-Assistent)
  Wenn Sie auf der Seite **Datentypzuordnung überprüfen** auf die Zeile für eine einzelne Spalte doppelklicken, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import-/Export-Assistent das Dialogfeld **Spaltenkonvertierungsdetails** . Auf dieser Seite können Sie die ausführlicheren Konvertierungsinformationen für eine einzelne Spalte überprüfen. Diese Informationen umfassen die folgenden Elemente.
-   Den Datentyp der Spalte in Quelle und Ziel.
-   Die Datentypkonvertierung, die der Assistent ausführt, falls eine Konvertierung erforderlich ist.
-   Die Datentypzuordnungsdateien, anhand derer der Assistent die erforderliche Datentypkonvertierung bestimmt. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>Screenshot der Seite „Spaltenkonvertierungsdetails“ 
 Der folgende Screenshot zeigt die Seite **Spaltenkonvertierungsdetails** des Assistenten, nachdem der Benutzer auf der Seite **Datentypzuordnung überprüfen** auf eine Zeile doppelt geklickt hat. Wenn Sie sich die Seite **Datentypzuordnung überprüfen** noch einmal ansehen möchten, wechseln Sie zu [Datentypzuordnung überprüfen](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).
 
Dieses Beispiel zeigt Ihnen die folgenden Sachverhalte.
-   Die `PersonID`-Spalte in der SQL Server-Quelltabelle hat den Typ `int`. Der Assistent ordnet diesen Typ durch Verweis auf die Datentypzuordnungs-Datei „MSSQLToSSIS10.xml“ dem SQL Server Integration Services `DT_I4`-Datentyp (SSIS) zu – einer Vier-Byte-Ganzzahl mit Vorzeichen.
-   Die `PersonID`-Spalte in der SQL Server-Zieltabelle hat auch den Typ `int`. Der Assistent ordnet diesen Typ dem gleichen SSIS-Datentyp zu.
-   Der Assistent erkennt: *Diese Spalte muss nicht konvertiert werden*.
 
  
 ![Seite „Spaltenkonvertierung“ des Import/Export-Assistenten](../../integration-services/import-export-data/media/column-conversion.png "Seite „Spaltenkonvertierung“ des Import/Export-Assistenten") 
  
## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie die Spaltenkonvertierungsdetails überprüft und auf **OK**geklickt haben, kehren Sie im Dialogfeld **Spaltenkonvertierungsdetails** zur Seite **Datentypzuordnung überprüfen** zurück. Weitere Informationen finden Sie unter [Datentypzuordnung überprüfen](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Siehe auch
[Zuordnung von Datentypen mit dem SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
