---
title: "Löschen von BLOB-Sicherungsdateien mit aktiver Lease | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8590c7e7adbf796d44347b66a790f98c13667bc
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="deleting-backup-blob-files-with-active-leases"></a>Löschen von BLOB-Sicherungsdateien mit aktiver Lease
  Wenn Sicherungs- oder Wiederherstellungsvorgänge im Windows Azure-Speicher ausgeführt werden, reserviert SQL Server eine Lease für eine unbegrenzte Dauer, um den exklusiven Zugriff auf das BLOB zu gewährleisten. Nachdem die Sicherung oder Wiederherstellung erfolgreich abgeschlossen wurde, wird die Lease wieder freigegeben. Wenn eine Sicherung oder Wiederherstellung fehlschlägt, wird im Rahmen des Sicherungsvorgangs versucht, ungültige BLOBs zu bereinigen. Kann die Sicherung jedoch aufgrund eines längeren bzw. dauerhaften Netzwerkverbindungsfehlers nicht ausgeführt werden, ist der Sicherungsvorgang u. U. nicht in der Lage, auf das BLOB zuzugreifen, sodass das BLOB verwaist ist. Dies bedeutet, dass das BLOB erst wieder beschreibbar ist bzw. gelöscht werden kann, nachdem die Lease freigegeben wurde. In diesem Thema wird beschrieben, wie die Lease freigegeben und das BLOB gelöscht wird.  
  
 Weitere Informationen zu Leasetypen finden Sie in diesem [Artikel](http://go.microsoft.com/fwlink/?LinkId=275664).  
  
 Ist der Sicherungsvorgang fehlerhaft, kann eine ungültige Sicherungsdatei generiert werden.  Außerdem kann für die BLOB-Sicherungsdatei eine aktive Lease bestehen, die verhindert, dass sie gelöscht oder überschrieben wird.  Um derartige BLOBs zu löschen oder zu überschreiben, sollte die Lease zuerst unterbrochen werden. Bei Sicherungsfehlern empfiehlt es sich, Leases zu bereinigen und BLOBs zu löschen. Sie können im Rahmen der Speicherverwaltung auch regelmäßige Cleanups ausführen.  
  
 Da bei einem Wiederherstellungsfehler nachfolgende Wiederherstellungen nicht blockiert werden, stellt eine aktive Lease u. U. kein Problem dar. Die Unterbrechung der Lease ist nur erforderlich, wenn das BLOB überschrieben oder gelöscht werden muss.  
  
## <a name="managing-orphaned-blobs"></a>Verwalten verwaister BLOBs  
 In den folgenden Schritten wird beschrieben, wie nach einem fehlerhaften Sicherungs- oder Wiederherstellungsvorgang ein Cleanup ausgeführt wird. Sämtliche Schritte können mithilfe von PowerShell-Skripts ausgeführt werden. Im folgenden Abschnitt finden Sie ein Codebeispiel:  
  
1.  **Ermitteln von BLOBs, die über Leases verfügen:** Falls Sie über ein Skript oder einen Prozess zum Ausführen der Sicherungsvorgänge verfügen, können Sie den Fehler möglicherweise innerhalb des Skripts oder Prozesses ermitteln und die BLOBs entsprechend bereinigen.   Sie können die BLOBs mit aktiven Leases auch mithilfe der LeaseStats-Eigenschaft und LeastState-Eigenschaft identifizieren. Nachdem Sie die BLOBs identifiziert haben, sollten Sie die Liste überprüfen, sicherstellen, dass die Sicherungsdatei gültig ist, und erst dann das BLOB löschen.  
  
2.  **Unterbrechen der Lease:** Durch eine autorisierte Anforderung kann die Lease ohne Angabe einer Lease-ID unterbrochen werden. Weitere Informationen finden Sie [hier](http://go.microsoft.com/fwlink/?LinkID=275664) .  
  
    > [!TIP]  
    >  SQL Server gibt eine Lease-ID aus, um während des Wiederherstellungsvorgangs einen exklusiven Zugriff zu gewährleisten. Die ID für die Wiederherstellungslease lautet BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2.  
  
3.  **Löschen des BLOBs:** Um ein BLOB zu löschen, das über eine aktive Lease verfügt, müssen Sie zunächst die Lease unterbrechen.  
  
###  <a name="Code_Example"></a> Beispiel für ein PowerShell-Skript  
  
> [!IMPORTANT]  
>  Bei Verwendung von PowerShell 2.0 können Probleme beim Laden der Assembly Microsoft.WindowsAzure.Storage.dll auftreten. Es wird empfohlen, ein Upgrade von PowerShell auszuführen, um das Problem zu beheben. Sie können auch die folgende Problemumgehung für PowerShell 2.0 verwenden:  
>   
>  -   Lassen Sie die .NET 2.0- und .NET 4.0-Assemblys zur Laufzeit laden. Dazu erstellen Sie eine Datei powershell.exe.config bzw. ändern eine bereits vorhandene Datei mit folgendem Code:  
>   
>     ```  
>     \<?xml version="1.0"?>   
>     <configuration>   
>         <startup useLegacyV2RuntimeActivationPolicy="true">   
>             <supportedRuntime version="v4.0.30319"/>   
>             <supportedRuntime version="v2.0.50727"/>   
>         </startup>   
>     </configuration>  
>   
>     ```  
  
 Das folgende Beispiel veranschaulicht, wie BLOBs mit aktiven Leases identifiziert und die Leases anschließend unterbrochen werden. Das Beispiel zeigt auch, wie Sie nach freigegebenen Lease-IDs filtern.  
  
 Tipps zum Ausführen des Skripts  
  
> [!WARNING]  
>  Wenn zeitgleich mit diesem Skript eine Sicherung im Windows Azure-BLOB-Speicherdienst ausgeführt wird, kann die Sicherung fehlschlagen, weil durch das Skript die Lease unterbrochen wird, die der Sicherungsvorgang zu reservieren versucht. Es empfiehlt sich, das Skript während eines Wartungsfensters oder in Phasen auszuführen, in denen keine Sicherungsaktivitäten zu erwarten sind.  
  
1.  Beim Ausführen des Skripts werden Sie aufgefordert, Werte für folgende Parameter anzugeben: Speicherkonto, Speicherschlüssel und Container sowie Pfad und Name der Windows Azure-Speicherassembly. Der Pfad der Speicherassembly entspricht dem Installationsverzeichnis der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Der Dateiname der Speicherassembly lautet "Microsoft.WindowsAzure.Storage.dll". Im Folgenden ein Beispiel für die angeforderten und eingegebenen Werte:  
  
    ```  
    cmdlet  at command pipeline position 1  
    Supply values for the following parameters:  
    storageAccount: mycloudstorageaccount  
    storageKey: 0BopKY7eEha3gBnistYk+904nf  
    blobContainer: mycontainer   
    storageAssemblyPath: C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Microsoft.WindowsAzure.Storage.dll  
    ```  
  
2.  Wenn keine BLOBs mit gesperrten Leases vorhanden sind, sollte eine mit der folgenden vergleichbare Meldung angezeigt werden:  
  
     **Es sind keine BLOBs mit gesperrter Lease vorhanden**  
  
     Wenn BLOBs mit gesperrten Leases vorhanden sind, sollten Meldungen ähnlich den folgenden angezeigt werden:  
  
     **Leases werden unterbrochen**  
  
     **Die Lease für die \<Blob-URL> ist eine Wiederherstellungslease: Diese Meldung wird nur bei einem Blob mit einer Wiederherstellungslease angezeigt, die noch aktiv ist.**  
  
     **Die Lease für die \<Blob-URL> ist keine Wiederherstellungslease. Die Lease für \<Blob-URL> wird unterbrochen.**  
  
```  
param(  
       [Parameter(Mandatory=$true)]  
       [string]$storageAccount,  
       [Parameter(Mandatory=$true)]  
       [string]$storageKey,  
       [Parameter(Mandatory=$true)]  
       [string]$blobContainer,  
       [Parameter(Mandatory=$true)]  
       [string]$storageAssemblyPath  
)  
  
# Well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# Load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
  
$container = $client.GetContainerReference($blobContainer)  
  
#list all the blobs  
$allBlobs = $container.ListBlobs()   
  
$lockedBlobs = @()  
# filter blobs that are have Lease Status as "locked"  
foreach($blob in $allBlobs)  
{  
    $blobProperties = $blob.Properties   
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
  
    }  
}  
  
if ($lockedBlobs.Count -eq 0)  
    {   
        Write-Host " There are no blobs with locked lease status"  
    }  
if($lockedBlobs.Count -gt 0)  
{  
    write-host "Breaking leases"  
    foreach($blob in $lockedBlobs )   
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease"  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease"  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)"  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
}  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-URL-Sicherung – bewährte Methoden und Problembehandlung](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
