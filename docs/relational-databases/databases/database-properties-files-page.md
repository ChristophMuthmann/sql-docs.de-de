---
title: Datenbankeigenschaften (Seite Dateien) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.databaseproperties.files.f1
ms.assetid: 3c030e51-db82-4b43-b1e5-8547ddd3de87
caps.latest.revision: "42"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a9c11a4593e3712083513d5edc9374edd392022
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="database-properties-files-page"></a>Datenbankeigenschaften (Seite Dateien)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Auf dieser Seite können Sie eine neue Datenbank erstellen bzw. die Eigenschaften einer ausgewählten Datenbank anzeigen oder ändern. Dieses Thema bezieht sich auf die Option **Datenbankeigenschaften (Seite 'Dateien')** für vorhandene Datenbanken und auf die Option **Neue Datenbank (Seite 'Allgemein')**.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Datenbankname**  
 Fügen Sie den Namen der Datenbank hinzu, oder zeigen Sie ihn an.  
  
 **Besitzer**  
 Geben Sie den Besitzer der Datenbank durch Auswahl aus der Liste an.  
  
 **Volltextindizierung verwenden**  
 Dieses Kontrollkästchen ist mit einem Häkchen versehen und abgeblendet, da die Volltextindizierung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]immer aktiviert ist. Weitere Informationen finden Sie unter [Aktualisieren der Volltextsuche](../../relational-databases/search/full-text-search.md).  
  
 **Datenbankdateien**  
 Damit können Sie Datenbankdateien für die zugeordnete Datenbank hinzufügen, anzeigen, ändern oder entfernen. Datenbankdateien haben folgende Eigenschaften:  
  
 **Logischer Name**  
 Geben Sie den Namen der Datei ein, oder ändern Sie ihn.  
  
 **Dateityp**  
 Wählen Sie den Dateityp aus der Liste aus. Der Dateityp kann **Daten**, **Protokoll**oder **Filestream-Daten**lauten. Den Dateityp einer vorhandenen Datei können Sie nicht ändern.  
  
 Wählen Sie **Filestream-Daten** aus, wenn Sie einer speicheroptimierten Dateigruppe Dateien (Container) hinzufügen.  
  
 Um Dateien (Container) einer Filestream-Datendateigruppe hinzuzufügen, muss FILESTREAM aktiviert sein. Sie können FILESTREAM aktivieren, indem Sie das Dialogfeld [Servereigenschaften (Seite „Erweitert“)](../../database-engine/configure-windows/server-properties-advanced-page.md) verwenden.  
  
 **Dateigruppe**  
 Wählen Sie die Dateigruppe für die Datei aus der Liste aus. Standardmäßig lautet die Dateigruppe PRIMARY. Sie können eine neue Dateigruppe erstellen, indem Sie **\<neue Dateigruppe>** auswählen und im Dialogfeld **Neue Dateigruppe** Informationen zu der Dateigruppe eingeben. Eine neue Dateigruppe kann auch auf der Seite **Dateigruppe** erstellt werden. Die Dateigruppe einer vorhandenen Datei können Sie nicht ändern.  
  
 Wenn Sie Dateien (Container) einer speicheroptimierten Dateigruppe hinzufügen, wird in das Feld **Dateigruppe** der Name der speicheroptimierten Dateigruppe der Datenbank eingefügt.  
  
 **Anfangsgröße**  
 Geben Sie die Anfangsgröße für die Datei in Megabytes ein, oder ändern Sie sie. Standardmäßig wird dieser Wert auf den Wert der **model** -Datenbank gesetzt.  
  
 Dieses Feld ist für FILESTREAM-Dateien nicht gültig.  
  
 Bei Dateien in speicheroptimierten Dateigruppen kann dieses Feld nicht geändert werden.  
  
 **Automatische Vergrößerung**  
 Wählen Sie die Eigenschaften der automatischen Vergrößerung der Datei aus, oder zeigen Sie sie an. Diese Eigenschaften steuern, wie die Datei erweitert wird, wenn die maximale Dateigröße erreicht ist. Um die Werte für die automatische Vergrößerung zu bearbeiten, klicken Sie für die gewünschte Datei auf die Bearbeitungsschaltfläche neben den Eigenschaften für die automatischen Vergrößerung, und ändern Sie die Werte im Dialogfeld **Automatische Vergrößerung ändern** . Standardmäßig werden diese Werte auf die Werte der **model** -Datenbank gesetzt.  
  
 Dieses Feld ist für FILESTREAM-Dateien nicht gültig.  
  
 Bei Dateien in speicheroptimierten Dateigruppen sollte dieses Feld **Unbegrenzt**lauten.  
  
 **Pfad**  
 Zeigt den Pfad der ausgewählten Datei an. Um einen Pfad für eine neue Datei anzugeben, klicken Sie auf die Bearbeitungsschaltfläche neben dem Pfad für die Datei, und navigieren Sie dann zum Zielordner. Den Pfad einer vorhandenen Datei können Sie nicht ändern.  
  
 Für FILESTREAM-Dateien ist der Pfad ein Ordner. Das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] erstellt die zugrunde liegenden Dateien in diesem Ordner.  
  
 **Dateiname**  
 Zeigt den Namen der Datei an.  
  
 Dieses Feld ist für FILESTREAM-Dateien, einschließlich Dateien in speicheroptimierten Dateigruppen, nicht gültig.  
  
 **Hinzufügen**  
 Fügt der Datenbank eine neue Datei hinzu.  
  
 **Entfernen**  
 Löscht die ausgewählte Datei aus der Datenbank. Eine Datei kann nur entfernt werden, wenn sie leer ist. Die primäre Datendatei und die Protokolldatei können nicht entfernt werden.  
  
 Weitere Informationen zu Dateien finden Sie unter [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  
