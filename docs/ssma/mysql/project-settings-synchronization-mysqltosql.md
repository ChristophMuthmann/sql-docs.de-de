---
title: Projekteinstellungen (Synchronisierung) (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
caps.latest.revision: 3
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2b2fcc99f40b7d06cdb9bb831cee5b5bf7490f7e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-synchronization-mysqltosql"></a>Projekteinstellungen (Synchronisierung) (MySQLToSQL)
Die Synchronisierung **projekteinstellungen** können Sie konfigurieren, wie Objekte von MySQL-Datenbank mit SQL Server-Datenbankobjekte synchronisiert werden.  
  
Die Standardaktionen geben Standardeinstellungen für die Aktualisierung von Objekten aus der MySQL-Datenbank und zum Synchronisieren von Objekten mit SQL Server-Datenbank. Weitere Informationen finden Sie unter [aus Datenbank &#40; aktualisieren MySQLToSQL &#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
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
  

