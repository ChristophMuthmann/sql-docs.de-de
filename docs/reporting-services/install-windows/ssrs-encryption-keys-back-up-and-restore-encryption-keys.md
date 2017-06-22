---
title: "Sichern und Wiederherstellen von Reporting Services-Verschlüsselungsschlüsseln | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up encryption keys [Reporting Services]
- restoring encryption keys [Reporting Services]
- encryption keys [Reporting Services]
- symmetric keys [Reporting Services]
ms.assetid: 6773d5df-03ef-4781-beb7-9f6825bac979
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 670c061b0c624eb321fd00c0f4e2f372b6ba9e71
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="ssrs-encryption-keys---back-up-and-restore-encryption-keys"></a>Verschlüsselungsschlüssel für SSRS - sichern und Wiederherstellen von Verschlüsselungsschlüsseln
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Das Erstellen einer Sicherungskopie des symmetrischen Schlüssels, der zum Verschlüsseln sensibler Informationen verwendet wird, ist ein wichtiger Bestandteil der Berichtsserverkonfiguration. Eine Sicherungskopie des Schlüssels ist für viele Routinevorgänge erforderlich und ermöglicht Ihnen das Wiederverwenden einer vorhandenen Berichtsserver-Datenbank in einer neuen Installation.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Native Mode | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint mode  
  
 Das Wiederherstellen der Sicherungskopie des Verschlüsselungsschlüssels ist nach folgenden Ereignissen erforderlich:  
  
-   Ändern des Kontonamens des Report Server-Windows-Dienstes oder Zurücksetzen des Kennwortes. Wenn Sie den Reporting Services-Konfigurations-Manager verwenden, wird der Schlüssel beim Ändern des Dienstkontonamens automatisch gesichert.  
  
    > [!NOTE]
    > Das Zurücksetzen des Kennwortes ist nicht dasselbe wie das Ändern des Kennwortes. Für das Zurücksetzen eines Kennwortes ist eine Berechtigung zum Überschreiben von Kontoinformationen auf dem Domänencontroller erforderlich. Das Zurücksetzen von Kennwörtern wird von einem Systemadministrator ausgeführt, wenn Sie ein bestimmtes Kennwort vergessen oder nicht kennen. Nur das Zurücksetzen von Kennwörtern erfordert das Wiederherstellen des symmetrischen Schlüssels. Wenn Sie das Kennwort für ein Konto regelmäßig ändern, müssen Sie den symmetrischen Schlüssel nicht zurücksetzen.  
  
-   Umbenennen des Computers oder der Instanz, der bzw. die den Berichtsserver hostet (eine Berichtsserverinstanz beruht auf dem Namen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz).  
  
-   Migrieren einer Berichtsserverinstallation oder Konfigurieren eines Berichtsservers für das Verwenden einer anderen Berichtsserver-Datenbank.  
  
-   Wiederherstellen einer Berichtsserverinstallation nach einem Hardwarefehler.  
  
 Sie müssen lediglich eine einzige Kopie des symmetrischen Schlüssels sichern. Es besteht eine 1:1-Entsprechung zwischen einer Berichtsserver-Datenbank und einem symmetrischen Schlüssel. Obwohl nur eine einzige Kopie gesichert werden muss, müssen Sie den Schlüssel unter Umständen mehrmals wiederherstellen, falls mehrere Berichtsserver in einem Bereitstellungsmodell für horizontales Skalieren ausgeführt werden. Jede Berichtsserverinstanz benötigt jeweils eine Kopie des symmetrischen Schlüssels zum Sperren und Entsperren von Daten in der Berichtsserver-Datenbank.

 Beim Sichern des symmetrischen Schlüssels wird der Schlüssel in die von Ihnen angegebene Datei geschrieben. Anschließend wird der Schlüssel mithilfe des von Ihnen angegebenen Kennwortes verschlüsselt. Der symmetrische Schlüssel darf keinesfalls unverschlüsselt gespeichert werden, d. h., Sie müssen beim Speichern auf einem Datenträger ein Kennwort angeben, um den Schlüssel zu verschlüsseln. Sie sollten die erstellte Datei an einem sicheren Ort speichern und sich das Kennwort zum Entsperren der Datei **unbedingt merken** . Zum Sichern des symmetrischen Schlüssels können Sie die folgenden Tools verwenden:  
  
 **Einheitlicher Modus:** Entweder den Reporting Services-Konfigurations-Manager oder das Hilfsprogramm **rskeymgmt** .  
  
 **SharePoint-Modus:** Die Seiten der SharePoint-Zentraladministration oder PowerShell.  
  
##  <a name="bkmk_backup_sharepoint"></a> Sichern von Berichtsservern im SharePoint-Modus  
 Für Berichtsserver im SharePoint-Modus können Sie entweder PowerShell-Befehle oder die Verwaltungsseiten der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung verwenden. Weitere Informationen finden Sie im Abschnitt „Schlüsselverwaltung“ unter [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  
  
##  <a name="bkmk_backup_configuration_manager"></a> Sichern von Verschlüsselungsschlüsseln mit dem Reporting Services-Konfigurations-Manager (einheitlicher Modus)  
  
1.  Starten Sie den Reporting Services-Konfigurations-Manager, und stellen Sie anschließend eine Verbindung mit der zu konfigurierenden Berichtsserverinstanz her.  
  
2.  Klicken Sie auf **Verschlüsselungsschlüssel**, und klicken Sie dann auf **Sichern**.  
  
3.  Geben Sie ein sicheres Kennwort ein.  
  
4.  Geben Sie eine Datei an, die den gespeicherten Schlüssel enthalten soll. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fügt die Dateierweiterung .snk an die Datei an. Sie sollten die Datei auf einem Datenträger speichern, sodass sie vom Berichtsserver getrennt ist.  
  
5.  Wählen Sie **OK**.  
  
###  <a name="bkmk_backup_rskeymgmt"></a> Sichern von Verschlüsselungsschlüsseln mit rskeymgmt (einheitlicher Modus)  
  
1.  Führen Sie **rskeymgmt.exe** lokal auf dem Computer aus, der den Berichtsserver hostet. Sie müssen das Extrahierungsargument **-e** verwenden, um den Schlüssel zu kopieren, sowie einen Dateinamen und ein Kennwort angeben. Das folgende Beispiel veranschaulicht die anzugebenden Argumente:  
  
    ```  
    rskeymgmt -e -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="restore-encryption-keys"></a>Wiederherstellen von Verschlüsselungsschlüsseln  
 Beim Wiederherstellen des symmetrischen Schlüssels wird der vorhandene symmetrische Schlüssel überschrieben, der in der Berichtsserver-Datenbank gespeichert ist. Durch das Wiederherstellen eines Verschlüsselungsschlüssels wird ein unbrauchbarer Schlüssel durch eine Kopie ersetzt, die Sie vorher auf einem Datenträger gespeichert haben. Dabei werden die folgenden Aktionen durchgeführt:  
  
-   Der symmetrische Schlüssel wird über die kennwortgeschützte Sicherungsdatei geöffnet.  
  
-   Der symmetrische Schlüssel wird mithilfe des öffentlichen Schlüssels des Report Server-Windows-Dienstes verschlüsselt.  
  
-   Der verschlüsselte symmetrische Schlüssel wird in der Berichtsserver-Datenbank gespeichert.  
  
-   Die zuvor gespeicherten Daten für den symmetrischen Schlüssel (z. B. Schlüsselinformationen, die aus einer vorherigen Bereitstellung bereits in der Berichtsserver-Datenbank gespeichert waren) werden gelöscht.  
  
 Zum Wiederherstellen des Verschlüsselungsschlüssels benötigen Sie eine Kopie des Verschlüsselungsschlüssels in einer Datei. Außerdem müssen Sie das Kennwort zum Entsperren der gespeicherten Kopie kennen. Wenn Sie den Schlüssel und das Kennwort haben, können Sie den Schlüssel mithilfe des Reporting Services-Konfigurationstools oder des Hilfsprogramms **rskeymgmt** wiederherstellen. Beim symmetrischen Schlüssel muss es sich um denselben Schlüssel handeln, der zum Sperren oder Entsperren der verschlüsselten Daten verwendet werden kann, die zurzeit in der Berichtsserver-Datenbank gespeichert sind. Wenn Sie eine ungültige Kopie wiederherstellen, kann der Berichtsserver nicht auf die verschlüsselten Daten zugreifen, die zurzeit in der Berichtsserver-Datenbank gespeichert sind. In diesem Fall müssen Sie unter Umständen alle verschlüsselten Werte löschen, falls Sie keinen gültigen Schlüssel wiederherstellen können. Falls Sie den Verschlüsselungsschlüssel aus irgendeinem Grund nicht wiederherstellen können (z. B. wenn Sie nicht über eine Sicherungskopie verfügen), müssen Sie den vorhandenen Schlüssel und die verschlüsselten Inhalte löschen. Weitere Informationen finden Sie unter [Löschen und erneutes Erstellen von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md). Weitere Informationen zum Erstellen von symmetrischen Schlüsseln finden Sie unter [Initialisieren eines Berichtsservers &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
###  <a name="bkmk_restore_configuration_manager"></a> Wiederherstellen von Verschlüsselungsschlüsseln mit dem Reporting Services-Konfigurations-Manager (einheitlicher Modus)  
  
1.  Starten Sie den Reporting Services-Konfigurations-Manager, und stellen Sie anschließend eine Verbindung mit der zu konfigurierenden Berichtsserverinstanz her.  
  
2.  Klicken Sie auf der Seite „Verschlüsselungsschlüssel“ auf **Wiederherstellen**.  
  
3.  Wählen Sie die SNK-Datei aus, in der die Sicherungskopie enthalten ist.  
  
4.  Geben Sie das Kennwort zum Entsperren der Datei ein.  
  
5.  Wählen Sie **OK**. 
  
###  <a name="bkmk_restore_rskeymgmt"></a> Wiederherstellen von Verschlüsselungsschlüsseln mit rskeymgmt (einheitlicher Modus)  
  
1.  Führen Sie **rskeymgmt.exe** lokal auf dem Computer aus, der den Berichtsserver hostet. Verwenden Sie das Argument **-a** , um die Schlüssel wiederherzustellen. Sie müssen einen vollqualifizierten Dateinamen und ein Kennwort angeben. Das folgende Beispiel veranschaulicht die anzugebenden Argumente:  
  
    ```  
    rskeymgmt -a -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  

