# Kubernetes-Bereitstellung für Homepage-Anwendung mit Multi-Container-Pod-Design

Dieses Repository enthält Kubernetes-Manifestdateien zur Bereitstellung einer Homepage-Anwendung mit Multi-Container-Pod-Design.

## Voraussetzungen

- Laufender Kubernetes-Cluster.
- Installiertes `kubectl`-Befehlszeilentool.

## Bereitstellung der Homepage-Anwendung

1. Konfigurationsdateien anwenden:

    ```bash
    kubectl apply -f configmap.yaml
    ```

2. Homepage-Deployment anwenden:

    ```bash
    kubectl apply -f deployment.yaml
    ```

3. Auf die Homepage zugreifen:

    - Verwenden Sie die Portweiterleitung, um auf die Homepage lokal zuzugreifen:

        ```bash
        kubectl port-forward deployment/homepage-deployment 8080:80
        ```

        Besuchen Sie http://localhost:8080 in Ihrem Browser.

## Verzeichnisstruktur

- `configmap.yaml`: Kubernetes-ConfigMap-Definition für HTML-Inhalte.
- `deployment.yaml`: Kubernetes-Bereitstellungsdefinition für die Homepage-Anwendung.

## Aufräumen

Um die bereitgestellten Ressourcen zu bereinigen, verwenden Sie die folgenden Befehle:

```bash
kubectl delete -f deployment.yaml
kubectl delete -f configmap.yaml
