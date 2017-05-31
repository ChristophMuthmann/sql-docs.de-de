---
title: Datenbankeigenschaften (Seite Protokollversand) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.logshipping.f1
ms.assetid: 72c4e539-fe11-4d57-b977-65b418d5916f
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 11d0b9d1cde11ab1f3a0944c313d4d800e5039b0
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="database-properties-transaction-log-shipping-page"></a>Datenbankeigenschaften (Seite Protokollversand)
  Mithilfe dieser Seite können Sie die Eigenschaften des Protokollversands einer Datenbank konfigurieren und ändern.  
  
 Eine Erklärung zu den Konzepten des Protokollversands finden Sie unter [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>enthalten  
 **Diese Datenbank als primäre Datenbank in einer Protokollversandkonfiguration aktivieren**  
 Aktiviert diese Datenbank als primäre Datenbank im Protokollversand. Aktivieren Sie dieses Kontrollkästchen, und konfigurieren Sie anschließend die übrigen Optionen auf dieser Seite. Wenn Sie dieses Kontrollkästchen deaktivieren, wird die Protokollversandkonfiguration für diese Datenbank aufgehoben.  
  
 **Sicherungseinstellungen**  
 Klicken Sie auf **Sicherungseinstellungen** , um die Parameter für Sicherungszeitplan, Speicherort, Warnung und Archivierung zu konfigurieren.  
  
 **Sicherungszeitplan**  
 Zeigt den zurzeit ausgewählten Sicherungszeitplan der primären Datenbank an. Zum Ändern dieser Einstellungen klicken Sie auf **Sicherungseinstellungen** .  
  
 **Letzte erstellte Sicherung**  
 Zeigt Uhrzeit und Datum der letzten Transaktionsprotokollsicherung an, die für die primäre Datenbank vorgenommen wurde.  
  
 **Sekundäre Serverinstanzen und Datenbanken**  
 Führt die für die primäre Datenbank zurzeit konfigurierten sekundären Serverinstanzen und Datenbanken auf. Markieren Sie eine Datenbank, und klicken Sie dann auf **...** , um Änderungen an den für diese sekundäre Datenbank verfügbaren Parametern vorzunehmen.  
  
 **Hinzufügen**  
 Klicken Sie auf **Hinzufügen** , um der Protokollversandkonfiguration der primären Datenbank eine sekundäre Datenbank hinzuzufügen.  
  
 **Entfernen**  
 Entfernt eine ausgewählte Datenbank aus dieser Protokollversandkonfiguration. Wählen Sie zuerst die Datenbank aus, und klicken Sie dann auf **Entfernen**.  
  
 **Überwachungsserverinstanz verwenden**  
 Richtet eine Überwachungsserverinstanz für die Protokollversandkonfiguration ein. Aktivieren Sie das Kontrollkästchen **Überwachungsserverinstanz verwenden** , und klicken Sie dann auf **Einstellungen** , um die Überwachungsserverinstanz anzugeben.  
  
 **Überwachungsserverinstanz**  
 Zeigt die für die Protokollversandkonfiguration zurzeit konfigurierte Überwachungsserverinstanz an.  
  
 **Einstellungen**  
 Konfiguriert die Überwachungsserverinstanz für eine Protokollversandkonfiguration. Klicken Sie auf **Einstellungen** , um die Überwachungsserverinstanz zu konfigurieren.  
  
 **Skript für Konfiguration erstellen**  
 Generiert ein Skript, das den Protokollversand mit den ausgewählten Parametern konfiguriert. Klicken Sie auf **Skript für Konfiguration erstellen**, und wählen Sie dann ein Ausgabeziel für das Skript aus.  
  
> [!IMPORTANT]  
>  Bevor Sie ein Skript für die Einstellungen einer sekundären Datenbank erstellen, müssen Sie das Dialogfeld **Einstellungen für die sekundäre Datenbank** aufrufen. Durch das Aufrufen dieses Dialogfelds wird eine Verbindung mit dem sekundären Server hergestellt, und die aktuellen Eigenschaften der sekundären Datenbank, die zum Generieren des Skripts erforderlich sind, werden abgerufen.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für den Protokollversand &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)   
 [Protokollversandtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)  
  
  
