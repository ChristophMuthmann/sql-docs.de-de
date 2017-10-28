---
title: Projekteinstellungen (Synchronisierung) (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b6533ce1774dec4967c9d43ea27902281d5bf756
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-synchronization-sybasetosql"></a>Projekteinstellungen (Synchronisierung) (SybaseToSQL)
Die Seite "Synchronisierung", der die **Projekteinstellungen** Dialogfeld enthält Einstellungen, anpassen, wie SSMA-Datenbankobjekte wie Tabellen und gespeicherte Prozeduren in lädt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
Sie können zwei unterschiedliche Synchronisierung Seiten zugreifen, die die gleichen Einstellungen enthalten:  
  
-   Wenn Sie Einstellungen für alle zukünftigen SSMA-Projekte auf angeben möchten die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden **Migration Zielversion** Dropdown-Liste, und wählen Sie dann **Synchronisierung** unten im linken Bereich.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, und wählen Sie dann **Synchronisierung** unten im linken Bereich.  
  
## <a name="options"></a>enthalten  
**Versuche**  
Gibt die Anzahl der Versuche, die beim Laden von Objekten in SSMA nehmen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Objekte, die nicht geladen werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in der aktuellen Versuch wird wiederholt werden bis SSMA die maximale Anzahl von versuchen, in die aktuelle Synchronisierung erreicht.  
  
## <a name="synchronization-for-sql-server"></a>Synchronisierung für SQLServer  
**Aktualisieren Sie Lokales Objekt bei Änderung der lokale und remote-Objekt**  
Gibt an, ob es sich bei SSMA die lokalen Objektmetadaten mit remote Objektmetadaten ersetzen soll, falls die lokalen und remote-Objekte ändern.  
Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
Bei Auswahl des **in Datenbank schreiben**, SSMA werden Objekte in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.   
Standard-Option festgelegt ist **in Datenbank schreiben.**  
  
**Lokales Objekt bei Änderung der lokale Objekt aktualisieren**  
Gibt an, ob es sich bei SSMA die lokalen Objektmetadaten mit remote Objektmetadaten ersetzen soll, falls das Remoteobjekt ändert.  
Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.   
Standard-Option festgelegt ist **in Datenbank schreiben**.  
  
**Lokales Objekt bei Änderung des Remoteobjekts aktualisieren**  
Gibt an, ob es sich bei SSMA die lokalen Objektmetadaten mit remote Objektmetadaten ersetzen soll, falls das Remoteobjekt ändert.  
Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.   
Standard-Option festgelegt ist **aus der Datenbank aktualisieren**.  
  
**Aktualisieren Sie, wenn lokale Objektmetadaten fehlt**  
Gibt an, ob SSMA lokalen Metadaten erstellen soll, wenn ein Objekt in der Zieldatenbank, aber nicht lokal vorhanden ist.  
Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA-Datenbankoption die Aktualisierung auswählt, wenn die Bedingung erfüllt ist.  
Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt aus der Datenbank löschen, wenn die Bedingung erfüllt ist.  
Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.   
Standard-Option festgelegt ist **aus der Datenbank aktualisieren**.  
  

