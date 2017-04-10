---
title: "&#220;berlegungen zu administrativen Aufgaben bei Oracle-Verlegern | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Oracle-Veröffentlichung [SQL Server-Replikation], Überlegungen zur Verwaltung"
  - "Verwalten der Replikation, Oracle-Veröffentlichung"
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# &#220;berlegungen zu administrativen Aufgaben bei Oracle-Verlegern
  Auch nach dem Konfigurieren eines Oracle-Verlegers und dem Einrichten der Replikationsmechanismen zur Änderungsnachverfolgung können Administratoren von Oracle-Datenbanksystemen noch die üblichen Oracle-Datenbankhilfsprogamme nutzen und typische Systemverwaltungsaufgaben ausführen. Dabei sollte jedoch berücksichtigt werden, wie sich die Ausführung bestimmter Verwaltungsaufgaben auf die veröffentlichten Daten auswirkt.  
  
 Mit Ausnahme des Löschens oder Änderns einer Spalte, die für eine Replikation veröffentlicht wurde, bzw. des Löschens oder Änderns von Replikationsobjekten spielen die folgenden Überlegungen bei Momentaufnahmeveröffentlichungen keine Rolle.  
  
## Importieren und Laden von Daten  
 Die Änderungsnachverfolgung bei Transaktionsveröffentlichungen in Oracle erfolgt mithilfe von Triggern. Änderungen an veröffentlichten Tabellen können nur dann auf Abonnenten repliziert werden, wenn die Replikation beim Aktualisieren, Einfügen oder Löschen Trigger auslöst. Die Oracle-Hilfsprogramme Oracle Import und SQL*Loader verfügen beide über Optionen, die sich darauf auswirken, ob Trigger ausgelöst werden, wenn mithilfe dieser Hilfsprogramme Zeilen in replizierte Tabellen eingefügt werden.  
  
### Oracle Import  
 Mit Oracle Import können Sie die Option festlegen können **ignorieren** 'y' oder ' n ' (der Standardwert ist ' n '). Wenn **ignorieren** Wert ' n ', in der Tabelle gelöscht und beim Importieren neu erstellt. Dabei werden die Replikationstrigger entfernt, und die Replikation wird deaktiviert. Wenn für **ignore** 'y' festgelegt ist, wird beim Importieren versucht, die Zeilen in die vorhandene Tabelle zu laden, wodurch die Replikationstrigger ausgelöst werden. Stellen Sie daher sicher, dass beim Importieren in eine replizierte Tabelle mit dem Import-Hilfsprogramm für **ignore** 'y' festgelegt ist.  
  
### SQL*Loader  
 Mit SQL\*Loader, können Sie die Option festlegen **direkte** auf 'true' oder 'false' (der Standardwert ist "false"). Wenn für **direct** 'false' festgelegt ist, werden die Zeilen mithilfe herkömmlicher INSERT-Anweisungen eingefügt, die die Replikationstrigger auslösen. Wenn für **direct** 'true' festgelegt ist, wird die Last optimiert, und die Trigger werden nicht ausgelöst. Stellen Sie daher sicher **direkte** auf 'False' festgelegt ist, beim Laden in eine replizierte Tabelle mit SQL * Loader-Tool.  
  
## Ändern von veröffentlichten Objekten  
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
  
## Löschen oder Ändern von Replikationsobjekten  
 Sie müssen den Verleger löschen und neu konfigurieren, wenn Sie Nachverfolgungstabellen, Trigger, Sequenzen oder gespeicherte Prozeduren auf Verlegerebene löschen oder ändern. Eine partielle Liste dieser Objekte finden Sie unter [Objekte erstellt, auf dem Oracle-Verleger](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md).  
  
 Informationen zum Löschen und Neukonfigurieren des Verlegers finden Sie im Abschnitt zu Änderungen, die eine Neukonfiguration des Verlegers erforderlich machen, im Thema [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
## Siehe auch  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Überlegungen zum Entwurf und Einschränkungen für Oracle-Verleger](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  