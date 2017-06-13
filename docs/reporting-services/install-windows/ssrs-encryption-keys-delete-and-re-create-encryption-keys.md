---
title: "Löschen und erneutes Erstellen von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager) | Microsoft Docs"
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
- re-creating encryption keys
- encryption keys [Reporting Services]
- deleting encryption keys
- symmetric keys [Reporting Services]
- removing encryption keys
- resetting encryption keys
ms.assetid: 201afe5f-acc9-4a37-b5ec-121dc7df2a61
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b042bef86620c773f39f81ea16a62b3d9c4c2a6a
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="ssrs-encryption-keys---delete-and-re-create-encryption-keys"></a>SSRS-Verschlüsselungsschlüssel – löschen und erneutes Erstellen von Verschlüsselungsschlüsseln
  Das Löschen und erneute Erstellen von Verschlüsselungsschlüsseln gehört nicht zu den routinemäßigen Aktivitäten bei der Verwaltung von Schlüsseln. Sie führen diese Aufgaben als Reaktion auf eine bestimmte Gefahr für den Berichtsserver oder als letzte Möglichkeit vor dem Verlust des Zugriffs auf die Datenbank des Berichtsservers aus.  
  
-   Erstellen Sie den symmetrischen Schlüssel neu, wenn Sie annehmen, dass der vorhandene symmetrische Schlüssel nicht mehr sicher ist. Sie können den Schlüssel auch regelmäßig neu erstellen. Dies ist eine bewährte Sicherheitsmethode.  
  
-   Löschen Sie vorhandene Verschlüsselungsschlüssel und nicht verwendbaren verschlüsselten Inhalt, wenn Sie den symmetrischen Schlüssel nicht wiederherstellen können.  
  
## <a name="re-creating-encryption-keys"></a>Erneutes Erstellen von Verschlüsselungsschlüsseln  
 Wenn Sie davon ausgehen müssen, dass der symmetrische Schlüssel nicht autorisierten Benutzern bekannt ist, oder wenn der Berichtsserver einem Angriff ausgesetzt war und Sie den symmetrischen Schlüssel als Vorsichtsmaßnahme zurücksetzen möchten, dann können Sie ihn erneut erstellen. Beim erneuten Erstellen des symmetrischen Schlüssels werden alle verschlüsselten Werte mit dem neuen Wert wieder verschlüsselt. Wenn Sie mehrere Berichtsserver in einer Bereitstellung für horizontales Skalieren ausführen, werden alle Kopien des symmetrischen Schlüssels neu aktualisiert. Der Berichtsserver verwendet verfügbare öffentliche Schlüssel zum Aktualisieren des symmetrischen Schlüssels für jeden Server in der Bereitstellung.  
  
 Sie können den symmetrischen Schlüssel nur dann erneut erstellen, wenn der Server ausgeführt wird. Das erneute Erstellen der Verschlüsselungsschlüssel und das erneute Verschlüsseln des Inhalts unterbricht die Serveroperationen. Sie müssen den Server offline nehmen, während die erneute Verschlüsselung ausgeführt wird. Während dieser Zeit sollten keine Anforderungen an den Server gestellt werden.  
  
 Sie können das Reporting Services-Konfigurationstool oder das Hilfsprogramm **rskeymgmt** verwenden, um den symmetrischen Schlüssel und die verschlüsselten Daten zurückzusetzen. Weitere Informationen dazu, wie der symmetrische Schlüssel erstellt wird, finden Sie unter [Initialisieren eines Berichtsservers &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
### <a name="how-to-re-create-encryption-keys-reporting-services-configuration-tool"></a>Erneutes Erstellen der Verschlüsselungsschlüssel (Reporting Services-Konfigurationstool)  
  
1.  Deaktivieren Sie den Report Server-Webdienst und HTTP-Zugriff, indem Sie die **IsWebServiceEnabled** -Eigenschaft in der Datei rsreportserver.config ändern. Mit diesem Schritt werden Authentifizierungsanforderungen vorübergehend nicht mehr an den Berichtsserver gesendet, ohne dass der Server vollständig herunterfährt. Sie müssen minimale Berechtigungen haben, damit Sie die Schlüssel neu erstellen können.  
  
     Wenn Sie Verschlüsselungsschlüssel für eine Berichtsserverbereitstellung durch dezentrales Skalieren erneut erstellen, deaktivieren Sie diese Eigenschaft für alle Instanzen in der Bereitstellung.  
  
    1.  Öffnen Sie Windows-Explorer, und navigieren Sie zu *Laufwerk*:\Programme\Microsoft SQL Server\\*Berichtsserverinstanz*\Reporting Services. Ersetzen Sie *Laufwerk* durch den Laufwerkbuchstaben und *Berichtsserverinstanz* durch den Ordnernamen, der der Berichtsserverinstanz entspricht, für die Sie den Webdienst und den HTTP-Zugriff deaktivieren möchten. Beispiel: C:\Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services.  
  
    2.  Öffnen Sie die Datei rsreportserver.config.  
  
    3.  Geben Sie für die **IsWebServiceEnabled** -Eigenschaft **False**an, und speichern Sie dann die Änderungen.  
  
2.  Starten Sie das Reporting Services-Konfigurationstool, und stellen Sie anschließend eine Verbindung zu der zu konfigurierenden Berichtsserverinstanz her.  
  
3.  Klicken Sie auf der Seite Verschlüsselungsschlüssel auf **Ändern**. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Starten Sie den Windows-Dienst des Berichtsservers erneut. Wenn Sie Verschlüsselungsschlüssel für eine Bereitstellung für horizontales Skalieren erneut erstellen, starten Sie den Dienst auf allen Instanzen erneut.  
  
5.  Aktivieren Sie den Webdienst und HTTP-Zugriff erneut, indem Sie die Eigenschaft **IsWebServiceEnabled** in der Datei „rsreportserver.config“ ändern. Wiederholen Sie diesen Schritt für alle Instanzen, wenn Sie mit einer Bereitstellung für horizontales Skalieren arbeiten.  
  
### <a name="how-to-re-create-encryption-keys-rskeymgmt"></a>Erneutes Erstellen von Verschlüsselungsschlüsseln (rskeymgmt)  
  
1.  Deaktivieren Sie den Berichtsserver-Webdienst und den HTTP-Zugriff. Verwenden Sie die Anweisungen in der vorherigen Vorgehensweise, um den Webdienst zu stoppen.  
  
2.  Führen Sie **rskeymgmt.exe** lokal auf dem Computer aus, der den Berichtsserver hostet. Verwenden Sie das Argument **-s** zum Zurücksetzen des symmetrischen Schlüssels. Es sind keine anderen Argumente erforderlich:  
  
    ```  
    rskeymgmt -s  
    ```  
  
3.  Starten Sie den Reporting Services-Windows-Diensts neu.  
  
## <a name="deleting-unusable-encrypted-content"></a>Löschen von nicht verwendbarem verschlüsseltem Inhalt  
 Wenn Sie den Verschlüsselungsschlüssel auf irgendeinem Grund nicht wiederherstellen können, ist der Berichtsserver nicht mehr in der Lage, Daten, die mit diesem Schlüssel verschlüsselt wurden, zu entschlüsseln und zu verwenden. Um den Berichtsserver wieder betriebsbereit zu machen, müssen Sie die verschlüsselten Werte löschen, die aktuell in der Datenbank des Berichtsservers gespeichert sind, und anschließend die benötigten Werte manuell neu angeben.  
  
 Durch das Löschen der Verschlüsselungsschlüssel werden sämtliche Informationen des symmetrischen Schlüssels aus der Datenbank des Berichtsservers sowie alle verschlüsselten Inhalte gelöscht. Alle nicht verschlüsselten Daten bleiben intakt, verschlüsselter Inhalt wird entfernt. Beim Löschen von Verschlüsselungsschlüsseln initialisiert sich der Berichtsserver selbst wieder automatisch, indem er einen neuen symmetrischen Schlüssel hinzufügt. Folgendes passiert beim Löschen von verschlüsseltem Inhalt:  
  
-   Verbindungszeichenfolgen in freigegebenen Datenquellen werden gelöscht. Benutzer, die Berichte ausführen, erhalten die Fehlermeldung "Die ConnectionString-Eigenschaft wurde nicht initialisiert."  
  
-   Gespeicherte Anmeldeinformationen werden gelöscht. Berichte und freigegebene Datenquellen werden rekonfiguriert und fordern zur Eingabe von Anmeldeinformationen auf.  
  
-   Berichte, die auf Modellen basieren (und freigegebene Datenquellen erfordern, die mit gespeicherten oder keinen Anmeldeinformationen konfiguriert sind), können nicht ausgeführt werden.  
  
-   Abonnements werden deaktiviert.  
  
 Nachdem Sie verschlüsselten Inhalt einmal gelöscht haben, können Sie ihn nicht wiederherstellen. Sie müssen erneut Verbindungszeichenfolgen und gespeicherte Anmeldeinformationen angeben und die Abonnements aktivieren.  
  
 Sie können das Reporting Services-Konfigurationstool oder das Hilfsprogramm **rskeymgmt** verwenden, um die Werte zu entfernen.  
  
### <a name="how-to-delete-encryption-keys-reporting-services-configuration-tool"></a>Löschen der Verschlüsselungsschlüssel (Reporting Services-Konfigurationstool)  
  
1.  Starten Sie das Reporting Services-Konfigurationstool, und stellen Sie anschließend eine Verbindung zu der zu konfigurierenden Berichtsserverinstanz her.  
  
2.  Klicken Sie auf **Verschlüsselungsschlüssel**, und klicken Sie dann auf **Löschen**. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Starten Sie den Windows-Dienst des Berichtsservers erneut. Wiederholen Sie diesen Schritt für alle Instanzen des Berichtsservers, wenn Sie mit einer Bereitstellung für horizontales Skalieren arbeiten.  
  
### <a name="how-to-delete-encryption-keys-rskeymmgt"></a>Löschen von Verschlüsselungsschlüsseln (rskeymmgt)  
  
1.  Führen Sie **rskeymgmt.exe** lokal auf dem Computer aus, der den Berichtsserver hostet. Sie müssen das Anwendungsargument **-d** verwenden. Das folgende Beispiel veranschaulicht das erforderliche Argument:  
  
    ```  
    rskeymgmt -d  
    ```  
  
2.  Starten Sie den Windows-Dienst des Berichtsservers erneut. Wiederholen Sie diesen Schritt für alle Instanzen des Berichtsservers, wenn Sie mit einer Bereitstellung für horizontales Skalieren arbeiten.  
  
### <a name="how-to-re-specify-encrypted-values"></a>Erneutes Angeben von verschlüsselten Werten  
  
1.  Sie müssen für jede freigegebene Datenquelle die Verbindungszeichenfolge erneut eingeben.  
  
2.  Für jeden Bericht und jede freigegebene Datenquelle, der bzw. die gespeicherte Anmeldeinformationen verwendet, müssen Sie den Benutzernamen und das Kennwort erneut eingeben und dann speichern. Weitere Informationen finden Sie unter [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
3.  Für datengesteuerte Abonnements öffnen Sie jedes Abonnement, und geben Sie die Anmeldeinformationen für die Abonnementdatenbank erneut ein.  
  
4.  Für Abonnements, die verschlüsselte Daten verwenden (d. h. die Dateifreigabe-Übermittlungserweiterung und alle verschlüsselten Übermittlungserweiterungen von Drittanbietern) öffnen Sie jedes Abonnement, und geben Sie die Anmeldeinformationen erneut ein. Abonnements, die Übermittlungsoption Berichtsserver-E-Mail verwenden, verwenden keine verschlüsselten Daten und sind bei einer Schlüsseländerung nicht betroffen.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [Speichern verschlüsselter Berichtsserverdaten &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  

