---
title: Festlegen von Konvertierung und Migrationsoptionen (AccessToSQL) | Microsoft Docs
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
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a060c0c1890a007ad14e21f526f436d03bb6c481
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Festlegen von Konvertierung und Migrationsoptionen (AccessToSQL)
Für jedes Projekt SSMA können Sie das Projekt auf Dokumentebene Optionen festlegen. Diese Optionen angeben, wie Objekte umgewandelt werden, wie die Daten migriert werden und wie Quelldatentypen Ziel-Datentypen zugeordnet. Bevor Sie Objekte konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure oder Migrieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, stellen Sie sicher, dass die Konfigurationsoptionen für das Projekt geeignet sind.  
  
## <a name="configuration-options-and-modes"></a>Modi "und"-Konfigurationsoptionen  
SSMA verfügt über vier Sätze von Konfigurationseinstellungen und vier Modi für die Konfiguration dieser Einstellungen: Standard, Optimistic, vollständig und Benutzerdefiniert. Der Standardmodus ist für die meisten Benutzer empfohlen. Verwenden Sie der optimistische Modus für einfache Konvertierungen. Verwenden Sie den Vollbildmodus, wenn alle Nachrichten angezeigt werden soll. In den benutzerdefinierten Modus legen Sie die Optionen an.  
  
Die Einstellungen werden im Abschnitt "Referenz zur Benutzeroberfläche" in dieser Dokumentation beschrieben. Weitere Informationen zu den Einstellungen und wie die Einstellungen in jedem Modus angewendet werden finden Sie unter den folgenden Themen:  
  
-   [Projekteinstellungen (Konvertierung)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [Projekteinstellungen (Migration)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [Projekteinstellungen (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Projekteinstellungen (Zuordnung)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [Projekteinstellungen (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>Einstellung Projektoptionen  
In SSMA können Sie die Standardeinstellungen für alle Projekte konfigurieren. Diese Einstellungen sind der SSMA-Konfigurationsdatei gespeichert und angewendet wird, zu einem neuen Projekt, das Sie erstellen.  
  
**Zum Festlegen von standardmäßigen Projektoptionen**  
  
1.  Auf der **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**.  
  
2.  In der **Projekt Standardeinstellungen** (Dialogfeld), führen Sie einen der folgenden:  
  
    -   Wählen Sie die Migration-Projekttyp, die für die Einstellungen angezeigt oder geändert werden, erforderlich sind **Migration Zielversion** Dropdown-Liste, klicken Sie auf **allgemeine** am unteren Rand des linken Bereich, und klicken Sie dann wählen **Konvertierung oder Migration oder SQL Azure**.  
  
        > [!NOTE]  
        > SQL Azure-Option steht in der **allgemeine** Registerkarte nur, wenn der Projekttyp erstellt SQL Azure ist.  
  
    -   Wählen Sie zum Auswählen eines vordefinierten Modus **Standard**, **Optimistic**, oder **vollständige** in der **Modus** Dropdown-Menü.  
  
    -   Wählen Sie zum Angeben eines benutzerdefinierten Modus **benutzerdefinierte** in der **Modus** Feld, wählen Sie eine Option im linken Bereich, klicken Sie auf der Einstellung oder Wert im rechten Bereich, und klicken Sie dann wählen, oder geben Sie die neue Einstellung oder einen Wert.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
Sie können auch die Einstellungen für das aktuelle Projekt anpassen. Diese Einstellungen werden in der aktuellen Projektdatei gespeichert.  
  
**Einstellungen für das aktuelle Projekt anpassen**  
  
1.  Auf der **Tools** klicken Sie im Menü **Projekteinstellungen**.  
  
2.  In der **Projekteinstellungen** (Dialogfeld), führen Sie einen der folgenden:  
  
    -   Wählen Sie zum Auswählen eines vordefinierten Modus **Standard**, **Optimistic**, oder **vollständige** in der **Modus** Dropdown-Menü.  
  
    -   Wählen Sie zum Angeben eines benutzerdefinierten Modus **benutzerdefinierte** in der **Modus** Feld, wählen Sie eine Option im linken Bereich, klicken Sie auf der Einstellung oder Wert im rechten Bereich, und klicken Sie dann wählen, oder geben Sie die neue Einstellung oder einen Wert.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
## <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnungsquelle und Ziel-Datentypen](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
  
-   Wenn Sie die Zuordnung der Quell-und Zieldatenbanken anpassen zu können, finden Sie unter [Zuordnung Quell- und Zieldatenbanken](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
-   Konvertieren Sie Sie andernfalls die Access-Datenbank-Objektdefinitionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objektdefinitionen. Weitere Informationen finden Sie unter [den Zugriff auf Datenbankobjekte konvertieren](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

