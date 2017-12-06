---
title: rskeymgmt-Hilfsprogramm (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], encryption
- joining report server instances [SQL Server]
- report server scale-out deployments [Reporting Services]
- cryptography [Reporting Services]
- multiple report server instances
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], scale-out deployments
- encryption [Reporting Services]
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 53f1318d-bd2d-4c08-b19f-c8b698b5b3d3
caps.latest.revision: "56"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f6d98e612a8f2033cb72ab59caa6eaab94ed5754
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="rskeymgmt-utility-ssrs"></a>rskeymgmt-Hilfsprogramm (SSRS)
  Dient zum Extrahieren, Wiederherstellen, Erstellen und Löschen des symmetrischen Schlüssels, der verwendet wird, um vertrauliche Berichtsserverdaten vor nicht autorisiertem Zugriff zu schützen. Dieses Hilfsprogramm wird auch verwendet, um Berichtsserverinstanzen in einer Bereitstellung für horizontales Skalieren zu verknüpfen. Eine *Berichtsserverbereitstellung für horizontales Skalieren* bezeichnet mehrere Berichtsserverinstanzen, die gemeinsam eine einzelne Berichtsserver-Datenbank nutzen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
rskeymgmt {-?}  
{–eextract}  
{–aapply}  
{-ddeleteall}  
{–srecreatekey}  
{–rremoveinstancekey}  
{-jjoinfarm}  
{-iinstance}  
{-ffile}  
{-pencryptionpassword}  
{-mremotecomputer}  
{-ninstancenameofremotecomputer}  
{-uadministratoruseraccount}  
{-vadministratorpassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>Argumente  
 **-?**  
 Zeigt die Syntax von **rskeymgmt** -Argumenten an.  
  
 **-e**  
 Extrahiert den symmetrischen Schlüssel, der zum Verschlüsseln und Entschlüsseln von Daten für die Berichtsserverinstanz verwendet wird, sodass Sie ihn in eine Datei kopieren können.  
  
 Dieses Argument enthält keinen Wert. Sie müssen jedoch zusätzliche Argumente in der Befehlszeile einschließen, um die Extrahierung abzuschließen. Zu den Argumenten, die Sie angeben müssen, gehören **-f** und**-p**.  
  
 **-a**  
 Ersetzt einen vorhandenen symmetrischen Schlüssel durch eine Kopie, die Sie in einer kennwortgeschützten Sicherungsdatei bereitstellen. Alle Instanzen des symmetrischen Schlüssels werden aktualisiert.  
  
 Dieses Argument enthält keinen Wert. Sie müssen jedoch zusätzliche Argumente in der Befehlszeile angeben, um die Datei mit dem anzuwendenden Schlüssel auszuwählen. Zu den Argumenten, die Sie angeben können, gehören **-f** und**-p**.  
  
 **-d**  
 Löscht alle Instanzen des symmetrischen Schlüssels und alle verschlüsselten Daten in einer Berichtsserver-Datenbank. Dieses Argument enthält keinen Wert.  
  
 **-s**  
 Generiert einen neuen symmetrischen Schlüssel und verschlüsselt alle verschlüsselten Inhalte mithilfe dieses neuen Schlüssels neu. Alle Instanzen des symmetrischen Schlüssels werden neu generiert.  
  
 **-j**  
 Konfiguriert eine Remoteberichtsserver-Instanz für die gemeinsame Nutzung der Berichtsserver-Datenbank, die von der lokalen Berichtsserverinstanz verwendet wird.  
  
 **-r**  *installationID*  
 Entfernt die Informationen zu einem symmetrischen Schlüssel für eine bestimmte Berichtsserverinstanz, wodurch der Berichtsserver aus einer Bereitstellung für horizontales Skalieren entfernt wird. *installationID* ist ein GUID-Wert, der in der Datei RSReportserver.config gefunden werden kann.  
  
 **-f**  *Datei*  
 Gibt einen vollqualifizierten Pfad zu der Datei an, in der eine Sicherungskopie der symmetrischen Schlüssel gespeichert ist.  
  
 Für **rskeymgmt -e**wird der symmetrische Schüssel in die von Ihnen angegebene Datei geschrieben.  
  
 Für **rskeymgmt -a**wird der in der Datei gespeicherte Wert des symmetrischen Schlüssels auf die Berichtsserverinstanz angewendet.  
  
 **-p**  *Kennwort*  
 (Erforderlich für **-f**) Gibt das Kennwort an, das zum Sichern oder Anwenden eines symmetrischen Schlüssels verwendet wird. Dieser Wert muss angegeben sein.  
  
 **-i**  
 Gibt eine lokale Berichtsserverinstanz an. Dieses Argument ist optional, wenn Sie den Berichtsserver auf der standardmäßigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz installiert haben (der Standardwert für **-i** ist MSSQLSERVER). Wenn Sie den Berichtsserver als benannte Instanz installiert haben, ist **-i** erforderlich.  
  
 **-m**  
 Gibt den Namen des Remotecomputers an, der die Berichtsserverinstanz hostet, die Sie der Berichtsserverbereitstellung für horizontales Skalieren hinzufügen. Verwenden Sie den Namen, durch den der Computer im Netzwerk identifiziert wird.  
  
 **-n**  
 Gibt den Namen der Berichtsserverinstanz auf einem Remotecomputer an. Dieses Argument ist optional, wenn Sie den Berichtsserver auf der standardmäßigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz installiert haben (der Standardwert für **-n** ist MSSQLSERVER). Wenn Sie den Berichtsserver als benannte Instanz installiert haben, ist **-n** erforderlich.  
  
 **-u**  *Benutzerkonto*  
 Gibt das Administratorkonto auf dem Remotecomputer an, den Sie der Bereitstellung für horizontales Skalieren hinzufügen. Wird kein Konto angegeben, werden die Anmeldeinformationen des aktuellen Benutzers verwendet.  
  
 **-v**  *Kennwort*  
 (Erforderlich für **-u**) Gibt das Kennwort eines Administratorkontos auf dem Remotecomputer an, den Sie der Bereitstellung für horizontales Skalieren hinzufügen möchten.  
  
 **-t**  *Ablaufverfolgung*  
 Schreibt Fehlermeldungen in das Ablaufverfolgungsprotokoll. Dieses Argument enthält keinen Wert. Weitere Informationen finden Sie unter [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen dieses Tools müssen Sie als lokaler Administrator angemeldet sein, und das Tool muss lokal auf dem Computer ausgeführt werden, der den Berichtsserver hostet. Das Hilfsprogramm rskeymgmt arbeit mit der Windows-Instanz des lokalen Berichtsservers zusammen. (Das Hilfsprogramm kann keine Verbindung mit Remoteinstanzen des Report Server-Windows-Dienstes herstellen. Es kann daher nicht zum Verwalten der Verschlüsselungsschlüssel einer Remoteberichtsserver-Instanz verwendet werden.)  
  
> [!NOTE]  
>  Wenn Sie die Argumente **-u** und **-v** verwenden, müssen Sie sicherstellen, dass Sie ein Konto mit Administratorberechtigungen für den Remotecomputer verwenden.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen mögliche Verwendungsweisen von **rskeymgmt**. In den folgenden Beispielen wird gezeigt, wie Verschlüsselungsschlüssel extrahiert, wiederhergestellt und gelöscht werden und wie eine Berichtsserverbereitstellung für horizontales Skalieren konfiguriert wird.  
  
#### <a name="extracting-encryption-keys"></a>Extrahieren von Verschlüsselungsschlüsseln  
 In diesem Beispiel wird gezeigt, wie eine Sicherungskopie des Verschlüsselungsschlüssels erstellt und in einer kennwortgeschützten Datei auf einer Diskette gespeichert wird. Wenn der Berichtsserver als benannte Instanz installiert ist, fügen Sie das Argument **-i** hinzu.  
  
```  
rskeymgmt -e -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="restoring-encryption-keys"></a>Wiederherstellen von Verschlüsselungsschlüsseln  
 In diesem Beispiel wird gezeigt, wie der Verschlüsselungsschlüssel ersetzt wird. Sie müssen den Speicherort der Sicherungskopie des Schlüssels und das Kennwort angeben, mit dem die Dateisperre aufgehoben wird.  
  
```  
rskeymgmt -a -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="deleting-encryption-keys-and-encrypted-content"></a>Löschen von Verschlüsselungsschlüsseln und verschlüsselten Inhalten  
 In diesem Beispiel wird gezeigt, wie alle auf einem Berichtsserver gespeicherten Verschlüsselungsschlüssel gelöscht werden. Wenn es sich bei der Installation um eine Berichtsserverbereitstellung für horizontales Skalieren handelt, werden die Verschlüsselungsschlüssel für alle Berichtsserverinstanzen gelöscht, die in die Bereitstellung eingeschlossen sind. Durch das Löschen eines Verschlüsselungsschlüssels werden auch alle verschlüsselten Werte in der Berichtsserver-Datenbank gelöscht. Weitere Informationen zu verschlüsselten Inhalten finden Sie unter [Speichern verschlüsselter Berichtsserverdaten (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md).  
  
```  
rskeymgmt -d  
```  
  
#### <a name="joining-a-remote-report-server-named-instance-to-a-scale-out-deployment"></a>Hinzufügen einer benannten Remoteberichtsserver-Instanz zu einer Bereitstellung für horizontales Skalieren  
 In diesem Beispiel wird gezeigt, wie eine auf einem Remotecomputer installierte Berichtsserverinstanz zu einer Berichtsserverbereitstellung für horizontales Skalieren hinzugefügt wird. Sie müssen den Befehl auf einem der Computer ausführen, die bereits mithilfe der freigegebenen Datenbank konfiguriert sind. Mit den Befehlsargumenten wird die Remoteberichtsserver-Instanz angegeben, die Sie der Bereitstellung für horizontales Skalieren hinzufügen möchten.  
  
```  
rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
```  
  
> [!NOTE]  
>  Eine Berichtsserverbereitstellung für horizontales Skalieren bezeichnet ein Bereitstellungsmodell, bei dem mehrere Berichtsserverinstanzen dieselbe Berichtsserver-Datenbank gemeinsam nutzen. Eine Berichtsserver-Datenbank kann von jeder Berichtsserverinstanz verwendet werden, die ihre symmetrischen Schlüssel in der Datenbank speichert. Wenn eine Berichtsserver-Datenbank beispielsweise Schlüsselinformationen für drei Berichtsserverinstanzen enthält, werden alle drei Instanzen als Mitglieder derselben Bereitstellung für horizontales Skalieren betrachtet.  
  
#### <a name="joining-report-server-instances-on-the-same-computer"></a>Verknüpfen von Berichtsserverinstanzen auf demselben Computer  
 Sie können eine Bereitstellung für horizontales Skalieren von mehreren Berichtsserverinstanzen aus erstellen, die auf demselben Computer installiert sind. Legen Sie die Argumente **-u** und **-v** nicht fest, wenn Sie Berichtsserverinstanzen verknüpfen, die lokal installiert sind. Die Argumente **-u** und **-v** werden nur verwendet, wenn Sie eine Instanz von einem Remotecomputer aus hinzufügen. Wenn Sie die Argumente festlegen, wird die folgende Fehlermeldung angezeigt: "Benutzeranmeldeinformationen können nicht für lokale Verbindungen verwendet werden."  
  
 Das folgende Beispiel veranschaulicht die Syntax für eine Bereitstellung für horizontales Skalieren mithilfe mehrerer lokaler Instanzen. In diesem Beispiel ist \<**initializedinstance**> der Name einer Instanz, die bereits für die Verwendung der Berichtsserver-Datenbank initialisiert wurde, und \<**newinstance**> ist der Name der Instanz, die der Bereitstellung hinzugefügt werden soll:  
  
```  
rskeymgmt -j -i <initializedinstance> -m <computer name> -n <newinstance>  
```  
  
#### <a name="removing-encryption-keys-for-a-single-report-server-in-a-scale-out-deployment"></a>Entfernen von Verschlüsselungsschlüsseln für einzelne Berichtsserver in einer Bereitstellung für horizontales Skalieren  
 In diesem Beispiel wird gezeigt, wie die Verschlüsselungsschlüssel für einen einzelnen Berichtsserver in einer Berichtsserverbereitstellung für horizontales Skalieren entfernt werden können. Die Schlüssel werden aus der Berichtsserver-Datenbank entfernt. Sobald die Schlüssel für diese Berichtsserverinstanz entfernt wurden, kann die Berichtsserverinstanz nicht mehr auf die verschlüsselten Daten in der Datenbank zugreifen; die Instanz wurde somit faktisch aus der Bereitstellung für horizontales Skalieren entfernt.  
  
 Um eine Berichtsserverinstanz aus einer Bereitstellung für horizontales Skalieren zu entfernen, ist es erforderlich, eine Installations-ID anzugeben. Die Installations-ID ist ein GUID, der in der Datei RSReportserver.config der Berichtsserverinstanz gespeichert ist, für die Sie die Verschlüsselungsschlüssel entfernen möchten. Sie müssen den folgenden Befehl auf dem Computer ausführen, den Sie aus der Bereitstellung für horizontales Skalieren entfernen möchten. Wenn der Berichtsserver als benannte Instanz installiert ist, verwenden Sie das Argument **-i** , um die Instanz anzugeben. Weitere Informationen finden Sie unter [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
```  
rskeymgmt -r <installationID>  
```  
  
## <a name="file-location"></a>Dateispeicherort  
 Rskeymgmt.exe befindet sich unter **\<*Laufwerk*>:\Programme\Microsoft SQL Server\110\Tools\Binn *oder unter *\<*Laufwerk*>:\Programme (x86)\Microsoft SQL Server\110\Tools\Binn**. Sie können das Hilfsprogramm von einem beliebigen Ordner im Dateisystem ausführen.  
  
## <a name="remarks"></a>Hinweise  
 Ein Berichtsserver verschlüsselt gespeicherte Anmeldeinformationen und Verbindungsinformationen. Zum Verschlüsseln von Daten werden ein öffentlicher Schlüssel und ein symmetrischer Schlüssel verwendet. Eine Berichtsserver-Datenbank muss über gültige Schlüssel verfügen, damit der Berichtsserver ausgeführt werden kann. Mithilfe von **rskeymgmt** können Sie die Schlüssel sichern, löschen oder wiederherstellen. Wenn die Schlüssel nicht wiederhergestellt werden können, bietet dieses Tool eine Möglichkeit zum Löschen verschlüsselter Inhalte, die nicht mehr verwendet werden können.  
  
 Das Hilfsprogramm **rskeymgmt** wird zum Verwalten des Schlüsselsatzes verwendet, der während der Installation oder Initialisierung definiert wurde. Über einen RPC-Endpunkt (Remote Procedure Call, Remoteprozeduraufruf) stellt es eine Verbindung mit dem Windows-Dienst des lokalen Berichtsservers her. Der Windows-Dienst des Berichtsservers muss ausgeführt werden, damit dieses Hilfsprogramm funktionsfähig ist.  
  
 Weitere Informationen zu den Verschlüsselungsschlüsseln finden Sie unter [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md) und [Initialisieren eines Berichtsservers (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellung für horizontales Skalieren – Reporting Services im einheitlichen Modus &#40;Konfigurations-Manager&#41;](http://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c)   
 [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Eingabeaufforderungs-Hilfsprogramme für Berichtsserver &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
 [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
