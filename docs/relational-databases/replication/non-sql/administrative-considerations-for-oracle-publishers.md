---
title: "Überlegungen zu administrativen Aufgaben bei Oracle-Verlegern | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], administrative considerations
- administering replication, Oracle publishing
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 058c10375ed15b5375f814199a57d032c5291018
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="administrative-considerations-for-oracle-publishers"></a>Überlegungen zu administrativen Aufgaben bei Oracle-Verlegern
  Auch nach dem Konfigurieren eines Oracle-Verlegers und dem Einrichten der Replikationsmechanismen zur Änderungsnachverfolgung können Administratoren von Oracle-Datenbanksystemen noch die üblichen Oracle-Datenbankhilfsprogamme nutzen und typische Systemverwaltungsaufgaben ausführen. Dabei sollte jedoch berücksichtigt werden, wie sich die Ausführung bestimmter Verwaltungsaufgaben auf die veröffentlichten Daten auswirkt.  
  
 Mit Ausnahme des Löschens oder Änderns einer Spalte, die für eine Replikation veröffentlicht wurde, bzw. des Löschens oder Änderns von Replikationsobjekten spielen die folgenden Überlegungen bei Momentaufnahmeveröffentlichungen keine Rolle.  
  
## <a name="importing-and-loading-data"></a>Importieren und Laden von Daten  
 Die Änderungsnachverfolgung bei Transaktionsveröffentlichungen in Oracle erfolgt mithilfe von Triggern. Änderungen an veröffentlichten Tabellen können nur dann auf Abonnenten repliziert werden, wenn die Replikation beim Aktualisieren, Einfügen oder Löschen Trigger auslöst. Die Oracle-Hilfsprogramme Oracle Import und SQL*Loader verfügen beide über Optionen, die sich darauf auswirken, ob Trigger ausgelöst werden, wenn mithilfe dieser Hilfsprogramme Zeilen in replizierte Tabellen eingefügt werden.  
  
### <a name="oracle-import"></a>Oracle Import  
 Mit Oracle Import können Sie für die Option **ignore** 'y' oder 'n' festlegen (die Standardeinstellung ist 'n'). Wenn für **ignore** 'n' festgelegt ist, wird die Tabelle gelöscht und beim Importieren neu erstellt. Dabei werden die Replikationstrigger entfernt, und die Replikation wird deaktiviert. Wenn für **ignore** 'y' festgelegt ist, wird beim Importieren versucht, die Zeilen in die vorhandene Tabelle zu laden, wodurch die Replikationstrigger ausgelöst werden. Stellen Sie daher sicher, dass beim Importieren in eine replizierte Tabelle mit dem Import-Hilfsprogramm für **ignore** 'y' festgelegt ist.  
  
### <a name="sqlloader"></a>SQL*Loader  
 Mit SQL\*-Loader können Sie die Option **direct** auf TRUE oder FALSE festlegen (der Standardwert ist FALSE). Wenn für **direct** 'false' festgelegt ist, werden die Zeilen mithilfe herkömmlicher INSERT-Anweisungen eingefügt, die die Replikationstrigger auslösen. Wenn für **direct** 'true' festgelegt ist, wird die Last optimiert, und die Trigger werden nicht ausgelöst. Stellen Sie daher sicher, dass beim Laden in eine replizierte Tabelle mit SQL*Loader für **direct** 'false' festgelegt ist.  
  
## <a name="making-changes-to-published-objects"></a>Ändern von veröffentlichten Objekten  
 Die folgenden Aktionen bedürfen keiner speziellen Überlegungen:  
  
-   Erneutes Erstellen von Indizes für veröffentlichte Tabellen  
  
-   Hinzufügen von Benutzertriggern zu veröffentlichten Tabellen  
  
 Bei der folgenden Aktion müssen Sie alle Aktivitäten an den veröffentlichten Tabellen einstellen:  
  
-   Verschieben einer veröffentlichten Tabelle  
  
 Bei den folgenden Aktionen müssen Sie die Veröffentlichung löschen, die Operation ausführen und die Veröffentlichung dann erneut erstellen:  
  
-   Abschneiden von Daten in einer veröffentlichten Tabelle  
  
-   Umbenennen einer veröffentlichten Tabelle  
  
-   Hinzufügen einer Spalte zu einer veröffentlichten Tabelle  
  
-   Löschen oder Ändern einer Spalte, die für Replikationszwecke veröffentlicht wurde  
  
-   Ausführen nicht protokollierter Operationen  
  
## <a name="dropping-or-modifying-replication-objects"></a>Löschen oder Ändern von Replikationsobjekten  
 Sie müssen den Verleger löschen und neu konfigurieren, wenn Sie Nachverfolgungstabellen, Trigger, Sequenzen oder gespeicherte Prozeduren auf Verlegerebene löschen oder ändern. Eine Teilliste dieser Objekte finden Sie unter [Auf dem Oracle-Verleger erstellte Objekte](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md).  
  
 Informationen zum Löschen und Neukonfigurieren des Verlegers finden Sie im Abschnitt zu Änderungen, die eine Neukonfiguration des Verlegers erforderlich machen, im Thema [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Überlegungen zum Entwurf und Einschränkungen für Oracle-Verleger](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
