---
title: Projekteinstellungen (Synchronisierung) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba0fa7c4b3273ae3b4e38409789e109f495c41fb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="project-settings-synchronization-mysqltosql"></a>Projekteinstellungen (Synchronisierung) (MySQLToSQL)
Die Synchronisierung **projekteinstellungen** können Sie konfigurieren, wie Objekte von MySQL-Datenbank mit SQL Server-Datenbankobjekte synchronisiert werden.  
  
Die Standardaktionen geben Standardeinstellungen für die Aktualisierung von Objekten aus der MySQL-Datenbank und zum Synchronisieren von Objekten mit SQL Server-Datenbank. Weitere Informationen finden Sie unter [aus der Datenbank aktualisieren &#40;MySQLToSQL&#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
Sie können zwei unterschiedliche Synchronisierung Seiten zugreifen, die die gleichen Einstellungen enthalten:  
  
-   Zum Angeben von Einstellungen für alle zukünftigen SSMA-Projekte, auf die **Tools** Menü klicken Sie auf **DefaultProject Einstellungen**, und klicken Sie dann auf **Synchronisierung** unten im linken Bereich.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** Menü klicken Sie auf **Projekteinstellungen**, und klicken Sie dann auf **Synchronisierung** unten im linken Bereich.  
  
## <a name="options"></a>enthalten  
  
##### <a name="misc"></a>Sonstiges  
  
##### <a name="attempts"></a>Versuche  
Enthält Informationen über die Anzahl von Durchläufen Objekte in SQL Server laden in Anspruch nehmen. Laden von Objekten in SQL Server wird normalerweise in mehrere Durchläufe ausgeführt. Objekte, die Fehler beim Laden der im ersten Durchlauf, z. B. Fremdschlüsseln, möglicherweise im nächsten Schritt erfolgreich geladen.  
  
Standardmäßig ist der Wert 2.  
  
## <a name="synchronization-for-mysql"></a>Synchronisierung für MySQL  
  
##### <a name="action-on-local-and-remote-object-change"></a>Aktion bei Änderung der lokale und remote-Objekt  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn sich die Objektdefinition in SSMA und auf dem Datenbankserver ändert.  
  
-   Wenn Sie eine Aktualisierung aus Datenbank auswählen, lädt das SSMA Datenbankdefinitionen in die Metadaten an, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl von Skip wird SSMA Maßnahmen, die Aktualisierung nicht ausgeführt.  
  
##### <a name="action-on-local-object-change"></a>Aktion bei Änderung der lokale-Objekt  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn das Objekt im SSMA ändert.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
##### <a name="action-on-remote-object-change"></a>Aktion bei Änderung der Remote-Objekt  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn die Objekte auf dem Datenbankserver ändern.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Aktion beim lokalen Objektmetadaten nicht vorhanden ist.  
Gibt die Standardeinstellung im Dialogfeld Synchronisierung, bei die lokale Metadaten nicht vorhanden ist.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktionen aktualisieren  
  
## <a name="synchronization-for-sql-server"></a>Synchronisierung für SQLServer  
  
##### <a name="action-on-local-and-remote-object-change"></a>Aktion bei Änderung der lokale und Remote-Objekt  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn sich die Objektdefinition in SSMA und auf dem Datenbankserver ändert.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **in Datenbank schreiben**, SSMA werden Objekte in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
##### <a name="action-on-local-object-change"></a>Aktion bei Änderung der lokale-Objekt  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn das Objekt im SSMA ändert.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
##### <a name="action-on-remote-object-change"></a>Aktion bei Änderung der remote-Objekt  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn die Objekte auf dem Datenbankserver ändern.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Aktion beim lokalen Objektmetadaten nicht vorhanden ist.  
Gibt die Standardeinstellung im Dialogfeld Synchronisierung, bei der lokalen Metadaten fehlen.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA-Datenbankoption die Aktualisierung auswählt, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt aus der Datenbank löschen, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
