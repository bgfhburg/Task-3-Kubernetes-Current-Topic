# Kubernetes-Bereitstellung für Homepage-Anwendung mit Multi-Container-Pod-Design

Dieses Repository enthält Kubernetes-Manifestdateien zur Bereitstellung einer Homepage-Anwendung mit Multi-Container-Pod-Design.

## Voraussetzungen

- Minikube installiert.
- Installiertes `kubectl`-Befehlszeilentool.

## Bereitstellung der Homepage-Anwendung

1. Minikube starten:
    ```bash
    minikube start
    ```
   ![grafik](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/6247b2df-4e2c-4d65-96ec-d221bd9ebb23)

2. Starten des Minikube Dashboard:
    ```bash
    minikube dashboard
    ```
![grafik](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/846b7e4c-f639-444d-9542-44b08466ba0b)

Wichtig: Dieses Fenster muss geöffnet bleiben, damit das Dashboard funktioniert!

3. In einem neuen Terminal das deployment.yaml anwenden:

    ```bash
    kubectl apply -f https://raw.githubusercontent.com/bgfhburg/Task-3-Kubernetes-Current-Topic/main/deployment.yaml
    ```

3. Sobald das Deployment erstellt wurde kann die configmap.yaml angewendet werden:

    ```bash
    kubectl apply -f https://raw.githubusercontent.com/bgfhburg/Task-3-Kubernetes-Current-Topic/main/configmap.yaml
    ```

4. Anschließend noch Port-Forwardign für die deployte Website:

    ```bash
    kubectl port-forward deployment/homepage-deployment 8080:80
    ```
5. Jetzt ist die Website unter folgender Adresse verfügbar:
    ```bash
   http://localhost:8080 in Ihrem Browser.
    ```

6. Folgende Website sollte dargestellt werden:

![grafik](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/f924352b-8933-48ed-bd09-275fc0113510)


    
## Verzeichnisstruktur

- `configmap.yaml`: Kubernetes-ConfigMap-Definition für HTML-Inhalte.
- `deployment.yaml`: Kubernetes-Bereitstellungsdefinition für die Homepage-Anwendung.




## Aufräumen

Um die bereitgestellten Ressourcen zu bereinigen, verwenden Sie die folgenden Befehle:

```bash
kubectl delete -f deployment.yaml
kubectl delete -f configmap.yaml
