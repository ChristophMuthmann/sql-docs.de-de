---
title: Datenvorschau (Dialogfeld) (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
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
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4d0f0772336614e81e1b29c8a4e54fb73d2ed5c2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>Datenvorschau (Dialogfeld) (SQL Server-Import/Export-Assistent)
  Nachdem Sie die Daten angegeben haben, die Sie kopieren möchten, können Sie optional auf **Vorschau** klicken, um das Dialogfeld **Vorschaudaten** zu öffnen. Auf dieser Seite können Sie bis zu 200 Zeilen mit Beispieldaten aus Ihrer Datenquelle in der Vorschau anzeigen. Dadurch können Sie sicherstellen, dass der Assistent die Daten kopieren wird, die Sie kopieren möchten.
  
## <a name="screen-shot-of-the-preview-data-page"></a>Screenshot der Seite „Vorschaudaten“ 
 Der folgende Screenshot zeigt das Dialogfeld **Vorschaudaten** des Assistenten an.  
 
![Seite „Vorschaudaten“ des Import/Export-Assistenten](../../integration-services/import-export-data/media/preview-data.png "Seite „Vorschaudaten“ des Import/Export-Assistenten")  
  
## <a name="preview-sample-data"></a>Anzeigen einer Beispieldatenvorschau  
 **Source**  
Zeigt die Abfrage an, die der Assistent zum Laden der Daten aus der Datenquelle verwendet.

Wenn Sie eine Tabelle zum Kopieren ausgewählt haben, wird im Feld **Quelle** eine `SELECT * FROM <table>`-Abfrage statt des Tabellennamens angezeigt. 
  
 **Sample data grid**  
 Zeigt bis zu 200 Zeilen von Beispieldaten an, die von der Abfrage aus der Datenquelle zurückgegeben wurden  


## <a name="thats-not-right-i-want-to-change-something"></a>Das ist nicht richtig, ich möchte etwas ändern.
Nachdem Sie die Daten in der Vorschau anzeigen, sollten Sie die Optionen ändern, die Sie auf den vorherigen Seiten des Assistenten ausgewählt haben. Um diese Änderungen vorzunehmen, klicken Sie auf **OK**, um zurück auf die Seite **Quelltabellen und -sichten auswählen** zu wechseln, und klicken Sie dann auf **Zurück**, um zu vorherigen Seiten zurückzukehren, auf denen Sie Ihre jeweilige Auswahl ändern können.

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie eine Vorschau der Daten, die Sie kopieren möchten, erstellt haben und auf **OK**klicken, leitet Sie das Dialogfeld **Vorschaudaten** zurück zu den Seiten **Quelltabellen und Sichten auswählen** oder **Flatfileziel konfigurieren** . Weitere Informationen finden Sie unter [Quelltabellen und -sichten auswählen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) oder [Flatfileziel konfigurieren](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Siehe auch
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)
