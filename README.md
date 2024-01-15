# Kubernetes-Bereitstellung für Homepage-Anwendung mit Multi-Container-Pod-Design

Dieses Repository enthält Kubernetes-Manifestdateien zur Bereitstellung einer Homepage-Anwendung mit Multi-Container-Pod-Design.

## Voraussetzungen

- Minikube installiert.
- Installiertes `kubectl`-Befehlszeilentool.

## Bereitstellung der Homepage-Anwendung

1. Minikube starten:
    ```bash
    minikube start --extra-config=kubelet.housekeeping-interval=10s
    ```
   ![grafik](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/6247b2df-4e2c-4d65-96ec-d221bd9ebb23)

2. Als nächstes den Metrics-Server starten:
    ```bash
    minikube addons enable metrics-server
    ```

3. Starten des Minikube Dashboard:
    ```bash
    minikube dashboard
    ```
![grafik](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/846b7e4c-f639-444d-9542-44b08466ba0b)

Wichtig: Dieses Fenster muss geöffnet bleiben, damit das Dashboard funktioniert!

4. In einem neuen Terminal das deployment.yaml anwenden:

    ```bash
    kubectl apply -f https://raw.githubusercontent.com/bgfhburg/Task-3-Kubernetes-Current-Topic/main/deployment.yaml
    ```

5. Sobald das Deployment erstellt wurde kann die configmap.yaml angewendet werden:

    ```bash
    kubectl apply -f https://raw.githubusercontent.com/bgfhburg/Task-3-Kubernetes-Current-Topic/main/configmap.yaml
    ```

6. Anschließend die auto.yaml für das Scaling anwenden:

    ```bash
    kubectl apply -f https://raw.githubusercontent.com/bgfhburg/Task-3-Kubernetes-Current-Topic/main/auto.yaml
    ```

7. Anschließend noch Port-Forwardign für die deployte Website:

    ```bash
    kubectl port-forward deployment/homepage-deployment 8080:80
    ```
8. Jetzt ist die Website unter folgender Adresse verfügbar:

   ```bash
   http://localhost:8080 in Ihrem Browser.
    ```

9. Folgende Website sollte dargestellt werden:

![grafik](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/f924352b-8933-48ed-bd09-275fc0113510)

10. Durchführung des Stress-Tests zur Demonstration von Auto-Scale:
Aufrufen der Commandline im Kubernetes-Dshboard:
![grafik](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/419b4e61-2945-4534-ae67-07ac9bd9ee45)
  ```bash
   apt-get update
   apt-get install apache2-utils
  ```
11. Produzieren von Auslastung

   ```bash
   ab -n 100000 -c 1000 http://localhost:80/
   ```
![stress-auf-deployment](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/90e21fe8-2ce8-482b-8349-2857550e7eb7)

12. In einer separaten Commandline mitttels:

   ```bash
   kubectl get hpa -w
   ```
die Auslastug darstellen lassen unter TARGETS, die erste Zahl zeigt die derzeitige Auslastung,
die zweite Zahl zeigt den Schwellwert, ab dem Replikas erstellt werden.

![grafik](https://github.com/bgfhburg/Task-3-Kubernetes-Current-Topic/assets/133404114/71a06242-aa37-4f0a-9af0-a029f69b49df)


13. Aufräumen

Um die bereitgestellten Ressourcen zu bereinigen und Minikube zu beenden:

```bash
kubectl delete -f deployment.yaml
kubectl delete -f configmap.yaml
kubectl delete -f auto.yaml
```
```bash
minikube delete
```


## Verzeichnisstruktur

- `auto.yaml`: Kubernetes-Bereitstellungsdefinition für HorizontalPodAutoscaler.
- `configmap.yaml`: Kubernetes-ConfigMap-Definition für HTML-Inhalte.
- `deployment.yaml`: Kubernetes-Bereitstellungsdefinition für die Homepage-Anwendung.



