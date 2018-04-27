---
title: Abstimmen der Änderungen von mehreren Benutzern (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- table modifications [SQL Server], multiple users
- reconciling changes made by multiple users
- modifications made by multiple users
ms.assetid: fc7ed4f2-ad3d-47fc-a3ef-51e5bb069ef0
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b85f384098ce7c01e84f561ac809f7dc9487e1b2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="reconcile-changes-made-by-multiple-users-visual-database-tools"></a>Abstimmen der Änderungen von mehreren Benutzern (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
In einer Mehrbenutzerumgebung können mehrere Benutzer gleichzeitig Änderungen an ein und demselben Objekt vornehmen. Diese Situation kann auftreten, wenn Sie an der Struktur des Objekts im Tabellen-Designer oder im Datenbankdiagramm-Designer arbeiten, oder bei Ergebniswerten, die im Ergebnisbereich des Abfrage- und Sicht-Designers zurückgegeben werden. Dies kann Konflikte verursachen, die aufgelöst werden sollten.  
  
## <a name="conflicts-in-the-table-or-database-diagram-designers"></a>Konflikte im Tabellen-Designer oder im Datenbankdiagramm-Designer  
Beispielsweise kann ein Benutzer eine Tabelle löschen oder umbenennen, während Sie gerade an derselben Tabelle oder einer verknüpften Tabelle im Tabellen-Designer arbeiten. Wenn Sie versuchen, die Tabelle zu speichern, werden Sie vom [Es wurden Änderungen in der Datenbank festgestellt (Dialogfeld) &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/database-changes-detected-dialog-box-visual-database-tools.md) darüber benachrichtigt, dass die Datenbank nach dem Öffnen der Tabelle aktualisiert wurde.  
  
In diesem Dialogfeld finden Sie auch eine Liste der Datenbankobjekte, die durch das Speichern der Tabelle beeinflusst werden. Sie können hier eine der folgenden Aktionen ausführen:  
  
-   Wählen Sie **Ja** aus, um die Tabelle zu speichern und die Datenbank mit allen Änderungen in der Liste zu aktualisieren.  
  
    Diese Aktion kann sich auch auf Tabellen auswirken, die dieselben Datenbankobjekte nutzen. Angenommen, Sie ändern beispielsweise in der Tabelle`titleauthors` die Spalte `au_id` während ein anderer Benutzer an der Tabelle `authors` arbeitet, die über die Spalte `au_id` mit der Tabelle `titleauthors` verknüpft ist. Wenn Sie Ihre Tabelle speichern, wirkt sich dies auf die Tabelle des anderen Benutzers aus. Ein ähnlicher Fall liegt vor, wenn ein anderer Benutzer in der Tabelle `qty` eine CHECK-Einschränkung für die Spalte `sales` definiert hat. Wenn Sie die Spalte `qty` löschen und die Tabelle `sales` speichern, wirkt sich dies auf die CHECK-Einschränkung des anderen Benutzers aus.  
  
-   Wählen Sie **Nein** aus, um den Speichervorgang abzubrechen.  
  
    Sie können die Tabelle jetzt schließen, ohne sie zu speichern. Wenn Sie die Tabelle erneut öffnen, wird diese mit dem Inhalt der Datenbank angepasst.  
  
-   Wählen Sie **Textdatei speichern** aus, um eine Liste der Änderungen zu speichern.  
  
    Sie können die im Dialogfeld **Es wurden Änderungen in der Datenbank festgestellt** aufgelisteten Datenbankänderungen in einer Textdatei speichern, sodass Sie die Gründe untersuchen können, die andere Benutzer für ihre Änderungen hatten. Wenn ein anderer Benutzer z. B. eine Tabelle geändert hat, die Sie zum Löschen ausgewählt haben, können Sie überprüfen, ob die Tabelle vor dem Aktualisieren der Datenbank gelöscht werden soll.  
  
## <a name="conflicts-in-the-query-and-view-designer"></a>Konflikte im Abfrage- und Sicht-Designer  
Wenn Sie eine Abfrage ausführen oder die Ergebnisse einer Ansicht zurückgeben lassen, werden die Daten im [Ergebnisbereich](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)angezeigt. Da mehrere Benutzer gleichzeitig an derselben Gruppe von Daten arbeiten können, kann es zu Konflikten kommen.  
  
Beispielsweise führen Sie und ein Kollege jeweils eine Abfrage aus, um die gesamten Daten in der Tabelle `titleauthors` anzuzeigen. Ihr Kollege ändert den ersten Namen im ersten zurückgegebenen Datensatz von Barb in Barbara. Zu diesem Zeitpunkt enthält dieses Feld in der Datenbank Barbara, während in Ihrem Resultset immer noch Barb angezeigt wird. Sie geben jetzt Barbara ein und klicken auf eine Stelle außerhalb der Zeile. Daraufhin erhalten Sie eine Meldung, in der Sie zum Auflösen des Konflikts aufgefordert werden.  
  
-   Klicken Sie auf **Ja** , um die Datenbank mit den Änderungen zu aktualisieren.  
  
    Dadurch werden die Änderungen Ihres Kollegen überschrieben.  
  
-   Klicken Sie auf **Nein** , um das Resultset mit den aktuellen Daten aus der Datenbank zu aktualisieren.  
  
    Dadurch werden Ihre Änderungen mit den Änderungen Ihres Kollegen überschrieben.  
  
-   Klicken Sie auf **Abbrechen** , um die Bearbeitung fortzusetzen, ohne den Konflikt aufzulösen.  
  
    In diesem Fall können Sie Ihre Änderungen nicht in die Datenbank übernehmen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Es wurden Änderungen in der Datenbank festgestellt (Dialogfeld) &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/database-changes-detected-dialog-box-visual-database-tools.md)  
  
