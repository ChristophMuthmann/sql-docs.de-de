---
title: Projekt Settings(Synchronization) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 9d22a21b5599ba6a073366fcebb7023980ad95ad
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="project-settingssynchronization-oracletosql"></a>Projekt Settings(Synchronization) (OracleToSQL)
Die Seite "Synchronisierung", der die **Projekteinstellungen** das Dialogfeld enthält Einstellungen, die anpassen, wie SSMA lädt und Aktualisierungen-Datenbankobjekte, z. B. Tabellen und gespeicherten Prozeduren in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Die Standardoptionen für die Aktionen geben Standardeinstellungen für die Aktualisierung von Objekten aus der Oracle-Datenbank und zum Synchronisieren von Objekten mit SQL Server-Datenbank. Weitere Informationen finden Sie unter [Aktualisieren von Oracle-Datenbank –](../../ssma/oracle/refresh-from-database-oracletosql.md).  
  
Sie können zwei unterschiedliche Synchronisierung Seiten zugreifen, die die gleichen Einstellungen enthalten:  
  
-   Zum Angeben von Einstellungen für alle zukünftigen SSMA-Projekte, auf die **Tools** Menü klicken Sie auf **Projekt Standardeinstellungen**, und klicken Sie dann auf **Synchronisierung** unten im linken Bereich.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** Menü klicken Sie auf **Projekteinstellungen**, und klicken Sie dann auf **Synchronisierung** unten im linken Bereich.  
  
## <a name="miscellaneous-options"></a>Sonstige Optionen  
**Versuche**  
Gibt die Anzahl der Versuche, die beim Laden von Objekten in SSMA nehmen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Objekte, die nicht geladen werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in der aktuellen Versuch wird wiederholt werden bis SSMA die maximale Anzahl von versuchen, in die aktuelle Synchronisierung erreicht. Ist der Standardwert festgelegt **2**  
  
## <a name="synchronization-for-oracle-options"></a>Synchronisierung für Oracle-Optionen  
**Aktion bei Änderung der lokale und remote-Objekt**  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn sich die Objektdefinition in SSMA und auf dem Datenbankserver ändert. Ist der Standardwert festgelegt **aus der Datenbank aktualisieren**.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
**Aktion bei Änderung der lokale-Objekt**  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn das Objekt im SSMA ändert. Ist der Standardwert festgelegt **Skip**.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
**Aktion bei Änderung der remote-Objekt**  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn die Objekte auf dem Datenbankserver ändern. Ist der Standardwert festgelegt **aus der Datenbank aktualisieren**.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
**Aktion beim lokalen Objektmetadaten nicht vorhanden ist.**  
Gibt die Standardeinstellung im Dialogfeld Synchronisierung, bei der lokalen Metadaten fehlen. Ist der Standardwert festgelegt **aus der Datenbank aktualisieren**.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
## <a name="synchronization-for-sql-server-options"></a>Synchronisierung für SQL Server-Optionen  
**Aktion bei Änderung der lokale und remote-Objekt**  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn sich die Objektdefinition in SSMA und auf dem Datenbankserver ändert. Ist der Standardwert festgelegt **Schreiben in Datenbank**.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **in Datenbank schreiben**, SSMA werden Objekte in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
**Aktion bei Änderung der lokale-Objekt**  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn das Objekt im SSMA ändert. Ist der Standardwert festgelegt **Schreiben in Datenbank**.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
**Aktion bei Änderung der remote-Objekt**  
Gibt die Standardeinstellung im Dialogfeld "Synchronisierung", wenn die Objekte auf dem Datenbankserver ändern.  Ist der Standardwert festgelegt **aus der Datenbank aktualisieren**.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA laden Datenbankdefinitionen in den Metadaten ab, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt in der Datenbank gemäß SSMA-Metadaten-Inhalt aktualisiert, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
**Aktion beim lokalen Objektmetadaten nicht vorhanden ist.**  
Gibt die Standardeinstellung im Dialogfeld Synchronisierung, bei der lokalen Metadaten fehlen. Ist der Standardwert festgelegt **aus der Datenbank aktualisieren**.  
  
-   Bei Auswahl des **aus der Datenbank aktualisieren**, SSMA wählt die **aus der Datenbank aktualisieren** option, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **in Datenbank schreiben**, SSMA wird das Objekt aus der Datenbank löschen, wenn die Bedingung erfüllt ist.  
  
-   Bei Auswahl des **Skip**, SSMA wird keine Aktualisierung Aktionen ausführen.  
  
