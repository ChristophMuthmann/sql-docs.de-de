---
title: Einen SQL Server-Container in Kubernetes für hohe Verfügbarkeit konfigurieren | Microsoft Docs
description: In diesem Lernprogramm wird gezeigt, wie eine SQL Server-hochverfügbarkeitslösung mit Kubernetes auf Azure-Container-Dienst bereitgestellt wird.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux,mvc
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 9e9925268f46007155c3a6851b250a57d9b02298
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="configure-a-sql-server-container-in-kubernetes-for-high-availability"></a>Konfigurieren Sie einen SQL Server-Container in Kubernetes für hohe Verfügbarkeit

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Informationen Sie zum Konfigurieren von SQL Server-Instanz auf Kubernetes in Azure Container Service (so) mit permanenten Speicher für hohe Verfügbarkeit (HA). Die Lösung bietet Stabilität. Wenn SQL Server-Instanz ein Fehler auftritt, erstellt erneut Kubernetes automatisch im eine neue Pod. So bietet Stabilität gegenüber einem Knotenausfall Kubernetes. 

Dieses Lernprogramm veranschaulicht, wie so konfigurieren Sie eine hoch verfügbare SQL Server-Instanz in Containern, die so zu verwenden. 

> [!div class="checklist"]
> * Erstellen Sie eine SA-Kennwort
> * Erstellen von Speicher
> * Erstellen der Bereitstellung
> * Herstellen einer Verbindung mit SQL Server Management Studio (SSMS)
> * Überprüfen Sie, ob Fehler und Wiederherstellung

## <a name="ha-solution-that-uses-kubernetes-running-in-azure-container-service"></a>Mit hoher Verfügbarkeit verwendet Lösung, die Kubernetes im Azure-Container-Dienst ausgeführt wird

Kubernetes 1.6 und höher bietet Unterstützung für [Speicherklassen](http://kubernetes.io/docs/concepts/storage/storage-classes/), [persistenten Volume Ansprüche](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims), und die [Azure-Datenträger Volumetyp](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). Sie können erstellen und verwalten die SQL Server-Instanzen systemintern in Kubernetes. Im Beispiel in diesem Artikel wird gezeigt, wie zum Erstellen einer [Bereitstellung](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) ähnelt einer freigegebenen Datenträger Failoverclusterinstanz Konfiguration mit hoher Verfügbarkeit zu erzielen. In dieser Konfiguration spielt Kubernetes der Rolle für den Cluster Orchestrator. Wenn eine SQL Server-Instanz in einem Container ein Fehler auftritt, startet der Orchestrator eine andere Instanz des Containers, die den gleichen persistenten Speicher zugeordnet wird.

![Diagramm der Kubernetes SQL Server-cluster](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

Im vorigen Diagramm `mssql-server` ist ein Container in einem [Pod](http://kubernetes.io/docs/concepts/workloads/pods/pod/). Kubernetes koordiniert die Ressourcen im Cluster. Ein [Replikatsatz](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) wird sichergestellt, dass die Pod automatisch nach einem Knotenausfall wiederhergestellt wird. Clientanwendungen eine Verbindung mit dem Dienst herstellen. In diesem Fall stellt der Dienst ein Lastenausgleichsmodul, das eine IP-Adresse gehostet werden, die unverändert, Ausfall des bleibt der `mssql-server`.

In der folgenden Abbildung der `mssql-server` Container ist fehlgeschlagen. Wie die Orchestrator garantiert Kubernetes an die richtige Anzahl der fehlerfreien Instanzen im Replikat festgelegt, und startet einen neuen Container entsprechend der Konfiguration. Die Orchestrator startet eine neue Pod auf demselben Knoten und `mssql-server` erneut mit dem gleichen permanenten Speicher. Der Dienst eine Verbindung herstellt, auf das neu erstellte `mssql-server`.

![Diagramm der Kubernetes SQL Server-cluster](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

In der folgenden Abbildung der Knoten hosten die `mssql-server` Container ist fehlgeschlagen. Die Orchestrator startet die neue Pod auf einen anderen Knoten und `mssql-server` erneut mit dem gleichen permanenten Speicher. Der Dienst eine Verbindung herstellt, auf das neu erstellte `mssql-server`.

![Diagramm der Kubernetes SQL Server-cluster](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>Erforderliche Komponenten

* **Kubernetes-cluster**
   - Das Lernprogramm ist ein Kubernetes Cluster erforderlich. Verwenden Sie die Schritte [Kubectl](https://kubernetes.io/docs/user-guide/kubectl/) zum Verwalten des Clusters. 

   - Finden Sie unter [einen Azure-Container-Dienst (so)-Cluster bereitstellen](http://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster) erstellen und Herstellen einer Verbindung mit einem Einzelknotencluster Kubernetes in so mit `kubectl`. 

   >[!NOTE]
   >Zum Schutz vor dem Ausfall eines Knotens erfordert ein Kubernetes Cluster mehrere Knoten.

* **Azure-CLI 2.0.23**
   - Die Anweisungen in diesem Lernprogramm wurden für Azure-CLI 2.0.23 überprüft.

## <a name="create-an-sa-password"></a>Erstellen Sie eine SA-Kennwort

Erstellen Sie im Cluster Kubernetes SA-Kennwort ein. Kubernetes können Informationen wie Kennwörter als sensible Konfigurationen verwalten [geheime Schlüssel](http://kubernetes.io/docs/concepts/configuration/secret/).

Der folgende Befehl erstellt ein Kennwort für das SA-Konto:

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   Ersetzen Sie `MyC0m9l&xP@ssw0rd` mit einem komplexen Kennwort.

   So erstellen Sie einen geheimen Schlüssel in Kubernetes mit dem Namen `mssql` , enthält den Wert `MyC0m9l&xP@ssw0rd` für die `SA_PASSWORD`, führen Sie den Befehl.


## <a name="create-storage"></a>Erstellen von Speicher

Konfigurieren einer [persistenten Volume](http://kubernetes.io/docs/concepts/storage/persistent-volumes/) und [persistenten Volume Anspruch](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection) im Cluster Kubernetes. Führen Sie die folgenden Schritte aus: 

1. Erstellen Sie ein Manifest, um die Speicherklasse und die persistenten Volume definieren Anspruch.  Das Manifest gibt an, die Speicher-Provisioner, Parameter, und [freigeben Richtlinie](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming). Der Kubernetes-Cluster verwendet dieses Manifest den permanenten Speicher zu erstellen. 

   Im folgenden Yaml Beispiel definiert eine Speicherklasse und beständige Volume Anspruch. Der Speicher Klasse Provisioner `azure-disk`, da diese Kubernetes-Cluster in Azure befindet. Der speicherkontotyp wird `Standard_LRS`. Der Anspruch persistenten Volume ist mit dem Namen `mssql-data`. Persistente Volume Anspruch Metadaten enthält eine Anmerkung verbinden Sie sie zurück in die Speicherklasse. 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1beta1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   Speichern Sie die Datei (z. B. **pvc.yaml**).

1. Erstellen Sie den persistente Volume Anspruch in Kubernetes.

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` ist der Speicherort, in dem Sie die Datei gespeichert.

   Persistente Volume automatisch als Azure Storage-Konto erstellt und an den persistenten Volume Anspruch gebunden. 

    ![Screenshot der Befehl "permanente Lautstärke-Anspruch"](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. Überprüfen Sie den Anspruch persistenten Volume aus.

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` ist der Name des Anspruchs persistenten Volume.

   Im vorherigen Schritt, der Anspruch persistenten Volume heißt `mssql-data`. Um die Metadaten über den Anspruch persistenten Volume anzuzeigen, führen Sie den folgenden Befehl ein:

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   Die zurückgegebene Metadaten enthält einen Wert mit dem `Volume`. Dieser Wert wird auf den Namen des Blob zugeordnet.

   ![Screenshot des zurückgegebenen Metadaten, einschließlich Volumes](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   Der Wert für das Volume entspricht Teil des Namens des Blob in der folgenden Abbildung aus dem Azure-Portal: 

   ![Screenshot der Azure-Portal Blob-name](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. Überprüfen Sie die persistente Volume aus.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` Gibt Metadaten für die permanente Volume, das automatisch erstellt und an den persistenten Volume Anspruch gebunden wurde. 

## <a name="create-the-deployment"></a>Erstellen der Bereitstellung

In diesem Beispiel wird der Container, der SQL Server-Instanz als Objekt Kubernetes Bereitstellung beschrieben. Die Bereitstellung wird eine Replikatgruppe erstellt. Die Replikatgruppe erstellt die Pod. 

In diesem Schritt erstellen Sie ein Manifest, um den Container, basierend auf dem SQL Server zu beschreiben [Mssql-Server – Linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) Docker-Images. Auf das Anwendungsmanifest verweist die `mssql-server` persistenten Volume Anspruch, und die `mssql` geheimen Schlüssel, die bereits auf dem Cluster Kubernetes angewendet. Das Manifest beschreibt auch eine [Service](http://kubernetes.io/docs/concepts/services-networking/service/). Dieser Dienst ist ein Lastenausgleich. Der Load Balancer wird sichergestellt, dass die IP-Adresse erhalten bleibt, nachdem SQL Server-Instanz wiederhergestellt wird. 

1. Erstellen Sie ein Manifest (YAML-Datei), um die Bereitstellung zu beschreiben. Im folgende Beispiel wird eine Bereitstellung, z. B. einen Container, basierend auf der SQL Server-Container-Abbild beschrieben.

   ```yaml
   apiVersion: apps/v1beta1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: mssql
           image: microsoft/mssql-server-linux
           ports:
           - containerPort: 1433
           env:
           - name: ACCEPT_EULA
             value: "Y"
           - name: SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   Kopieren Sie den vorherigen Code in eine neue Datei mit dem Namen `sqldeployment.yaml`. Aktualisieren Sie die folgenden Werte an: 

   * `value: "Developer"`: Legt fest, den Container an SQL Server Developer Edition ausgeführt werden. Developer Edition ist für Produktionsdaten nicht lizenziert. Wenn die Bereitstellung für die Produktion ist, legen Sie die passende Edition (`Enterprise`, `Standard`, oder `Express`). 

      >[!NOTE]
      >Weitere Informationen finden Sie unter [wie SQL Server-Lizenz](http://www.microsoft.com/sql-server/sql-server-2017-pricing).

   * `persistentVolumeClaim`: Dieser Wert muss einen Eintrag für `claimName:` , der für den persistenten Volume Anspruch verwendeten Namen zugeordnet. Dieses Lernprogramm verwendet `mssql-data`. 

   * `name: SA_PASSWORD`: Konfiguriert das Container-Bild, um das SA-Kennwort festlegen, wie in diesem Abschnitt definiert.

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     Kubernetes Container bereitstellt, verweist auf den geheimen Schlüssel mit dem Namen `mssql` , den Wert für das Kennwort abzurufen. 

   >[!NOTE]
   >Mithilfe der `LoadBalancer` Diensttyp, der SQL Server-Instanz ist Remote (über das Internet) an Port 1433.

   Speichern Sie die Datei (z. B. **sqldeployment.yaml**).

1. Die Bereitstellung zu erstellen.

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` ist der Speicherort, in dem Sie die Datei gespeichert.

   ![Screenshot der Bereitstellungsbefehl](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   Der Bereitstellung und der Dienst erstellt werden. SQL Server-Instanz ist in einem Container, in den persistenten Speicher verbunden.

   Geben Sie zum Anzeigen des Status von der Pod `kubectl get pod`.

   ![Screenshot des Get-Pod-Befehl](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   In der vorherigen Abbildung die Pod weist den Status `Running`. Dieser Status gibt an, dass der Container bereit ist. Dies kann einige Minuten dauern.

   >[!NOTE]
   >Nachdem die Bereitstellung erstellt wurde, dauert es einige Minuten, bevor die Pod sichtbar ist. Die Verzögerung, da der Cluster abruft, wird die [Mssql-Server – Linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) Image von Docker Hub. Nachdem das Image erstmalig per Pull abgerufen wird, sind möglicherweise spätere Bereitstellungen schneller, bei einer Bereitstellung mit einem Knoten, die bereits für das Bild darauf zwischengespeichert. 

1. Stellen Sie sicher, dass die Dienste ausgeführt werden. Führen Sie den folgenden Befehl aus:

   ```azurecli
   kubectl get services 
   ```

   Dieser Befehl gibt die Dienste, die ausgeführt werden, sowie die internen und externen IP-Adressen für die Dienste zurück. Beachten Sie die externe IP-Adresse für die `mssql-deployment` Dienst. Verwenden Sie diese IP-Adresse für die Verbindung mit SQL Server. 

   ![Screenshot der Befehl "Get-Service"](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Weitere Informationen zum Status der Objekte im Cluster Kubernetes ausführen:

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>Herstellen einer Verbindung mit SQL Server-Instanz

Wenn Sie den Container wie beschrieben konfiguriert haben, können Sie mit einer Anwendung von außerhalb der virtuellen Azure-Netzwerk verbinden. Verwenden der `sa` Konto und die externe IP-Adresse für den Dienst. Verwenden Sie das Kennwort, das Sie als geheimem Schlüssel Kubernetes konfiguriert. 

Sie können die folgenden Anwendungen verwenden, für die Verbindung mit der SQL Server-Instanz. 

* [SSMS](http://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssms)

* [SSDT](http://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   Für die Verbindung mit `sqlcmd`, führen Sie den folgenden Befehl:

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   Ersetzen Sie die folgenden Werte an:
      
    - `<External IP Address>` mit der IP-Adresse für die `mssql-deployment` Service 
    - `MyC0m9l&xP@ssw0rd` mit Ihrem Kennwort

## <a name="verify-failure-and-recovery"></a>Überprüfen Sie, ob Fehler und Wiederherstellung

Um Fehler und Wiederherstellung zu überprüfen, können Sie die Pod löschen. Führen Sie die folgenden Schritte aus:

1. Liste der Pod SQL Server ausgeführt wird.

   ```azurecli
   kubectl get pods
   ```

   Notieren Sie den Namen des der Pod SQL Server ausgeführt wird.

1. Löschen Sie die Pod.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` der Wert wird aus dem vorherigen Schritt für Pod Name zurückgegeben werden. 

Kubernetes erstellt erneut automatisch die Pod zum Wiederherstellen einer SQL Server-Instanz und Herstellen einer Verbindung mit dem permanenten Speicher. Verwendung `kubectl get pods` zu überprüfen, ob eine neue Pod bereitgestellt wird. Verwendung `kubectl get services` um sicherzustellen, dass die IP-Adresse für den neuen Container identisch ist. 

## <a name="summary"></a>Zusammenfassung

In diesem Lernprogramm haben Sie gelernt, wie Sie SQL Server-Container zu einem Cluster Kubernetes für hohe Verfügbarkeit bereitstellen. 

> [!div class="checklist"]
> * Erstellen Sie eine SA-Kennwort
> * Erstellen von Speicher
> * Erstellen der Bereitstellung
> * Herstellen einer Verbindung mit SQL Server Management Studios (SSMS)
> * Überprüfen Sie, ob Fehler und Wiederherstellung

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
>[Einführung in Kubernetes](http://docs.microsoft.com/en-us/azure/aks/intro-kubernetes)


