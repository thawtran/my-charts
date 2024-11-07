# my-charts
The Helm charts repository


## HomePage
https://thawtran.github.io/my-charts


## RepoIndexUrl
https://thawtran.github.io/my-charts/index.yaml


## Helm chart works

### 1. Create a chart
```shell
➜  …/Works/Tmp helm create tst-helm-chart-pkg
Creating tst-helm-chart-pkg
➜  …/Works/Tmp
```

### 2. Package a chart
```shell
➜  …/Works/Tmp grep '^version:' ~/Works/Tmp/tst-helm-chart-pkg/Chart.yaml
version: 0.1.0
➜  …/Works/Tmp

➜  …/Works/Tmp helm package tst-helm-chart-pkg
Successfully packaged chart and saved it to: /Users/thaovtran/Works/Tmp/tst-helm-chart-pkg-0.1.0.tgz
➜  …/Works/Tmp
```

### 3. Index charts
```shell
➜  …/Kubernetes/my-charts git:(gh-pages) ✗
➜  …/Kubernetes/my-charts git:(gh-pages) ✗ ls -lh
total 64
-rw-r--r--@ 1 thaovtran  1497946264   627B Nov  6 10:59 README.md
-rw-r--r--@ 1 thaovtran  1497946264   4.1K Nov  6 16:25 tst-helm-chart-pkg-0.1.0.tgz
➜  …/Kubernetes/my-charts git:(gh-pages) ✗
➜  …/Kubernetes/my-charts git:(master) ✗
➜  …/Kubernetes/my-charts git:(master) ✗ helm repo index . --url https://thawtran.github.io/my-charts
➜  …/Kubernetes/my-charts git:(master) ✗
➜  …/Kubernetes/my-charts git:(master) ✗ ll
total 32
-rw-r--r--@ 1 thaovtran  1497946264    35B Nov  6 15:54 README.md
-rw-r--r--@ 1 thaovtran  1497946264   456B Nov  6 15:59 index.yaml
-rw-r--r--@ 1 thaovtran  1497946264   4.1K Nov  6 15:53 tst-helm-chart-pkg-0.1.0.tgz
➜  …/Kubernetes/my-charts git:(master) ✗
```

### 4. Push charts to repo
```shell
$ git add -i
$ git commit -av
$ git push origin master
```

### 5.Create new version for a chart
```shell
➜  …/Works/Tmp grep '^version:' ~/Works/Tmp/tst-helm-chart-pkg/Chart.yaml
version: 0.1.1
➜  …/Works/Tmp

➜  …/Works/Tmp helm package tst-helm-chart-pkg
Successfully packaged chart and saved it to: /Users/thaovtran/Works/Tmp/tst-helm-chart-pkg-0.1.1.tgz
➜  …/Works/Tmp
```

### 6. Update charts index
```shell
➜  …/Kubernetes/my-charts git:(gh-pages) ✗
➜  …/Kubernetes/my-charts git:(gh-pages) ✗ ls -lh
total 64
-rw-r--r--@ 1 thaovtran  1497946264    35B Nov  6 15:54 README.md
-rw-r--r--@ 1 thaovtran  1497946264   456B Nov  6 15:59 index.yaml
-rw-r--r--@ 1 thaovtran  1497946264   4.1K Nov  6 16:25 tst-helm-chart-pkg-0.1.0.tgz
-rw-r--r--@ 1 thaovtran  1497946264   4.1K Nov  6 16:35 tst-helm-chart-pkg-0.1.1.tgz
➜  …/Kubernetes/my-charts git:(gh-pages) ✗
➜  …/Kubernetes/my-charts git:(master) ✗
➜  …/Kubernetes/my-charts git:(master) ✗ helm repo index . --url https://thawtran.github.io/my-charts
➜  …/Kubernetes/my-charts git:(master) ✗
➜  …/Kubernetes/my-charts git:(master) ✗ ll
total 32
-rw-r--r--@ 1 thaovtran  1497946264    35B Nov  6 15:54 README.md
-rw-r--r--@ 1 thaovtran  1497946264   456B Nov  6 16:34 index.yaml
-rw-r--r--@ 1 thaovtran  1497946264   4.1K Nov  6 16:25 tst-helm-chart-pkg-0.1.0.tgz
-rw-r--r--@ 1 thaovtran  1497946264   4.1K Nov  6 16:35 tst-helm-chart-pkg-0.1.1.tgz
➜  …/Kubernetes/my-charts git:(master) ✗
```

### 7. Repeat the step #4

### A. Helm chart syntax check
```shell
➜  …/Kubernetes/helm-myprj-01 helm lint tinyweb-app-mongo
==> Linting tinyweb-app-mongo
[INFO] Chart.yaml: icon is recommended
[ERROR] templates/deployment/mongoexp.yaml: unable to parse YAML: error converting YAML to JSON: yaml: line 20: did not find expected key

Error: 1 chart(s) linted, 1 chart(s) failed
➜  …/Kubernetes/helm-myprj-01

➜  …/Kubernetes/helm-myprj-01 helm lint tinyweb-app-mongo
==> Linting tinyweb-app-mongo
[INFO] Chart.yaml: icon is recommended
[ERROR] templates/deployment/tinyweb.yaml: unable to parse YAML: error converting YAML to JSON: yaml: line 20: did not find expected key

Error: 1 chart(s) linted, 1 chart(s) failed
➜  …/Kubernetes/helm-myprj-01
```

### B. Helm chart debug
```shell
➜  …/Kubernetes/helm-myprj-01
➜  …/Kubernetes/helm-myprj-01 helm template debug-tinyweb ./tinyweb-app-mongo --namespace my-tinyweb --debug
install.go:224: 2024-11-07 19:30:01.446957 +0700 +07 m=+0.034895626 [debug] Original chart version: ""
install.go:241: 2024-11-07 19:30:01.44744 +0700 +07 m=+0.035378251 [debug] CHART PATH: /Users/thaovtran/Learns/Kubernetes/helm-myprj-01/tinyweb-app-mongo

---
# Source: tinyweb-app-mongo/templates/ingress/tinyweb.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: debug-tinyweb-tinyweb-app-mongo-webapp-ingress
  namespace: my-tinyweb
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: "/"
...
...
...
Error: YAML parse error on tinyweb-app-mongo/templates/deployment/tinyweb.yaml: error converting YAML to JSON: yaml: line 20: did not find expected key
helm.go:86: 2024-11-07 19:30:01.454995 +0700 +07 m=+0.042934168 [debug] error converting YAML to JSON: yaml: line 20: did not find expected key
YAML parse error on tinyweb-app-mongo/templates/deployment/tinyweb.yaml
helm.sh/helm/v3/pkg/releaseutil.(*manifestFile).sort
	helm.sh/helm/v3/pkg/releaseutil/manifest_sorter.go:144
helm.sh/helm/v3/pkg/releaseutil.SortManifests
	helm.sh/helm/v3/pkg/releaseutil/manifest_sorter.go:104
helm.sh/helm/v3/pkg/action.(*Configuration).renderResources
	helm.sh/helm/v3/pkg/action/action.go:168
helm.sh/helm/v3/pkg/action.(*Install).RunWithContext
	helm.sh/helm/v3/pkg/action/install.go:316
main.runInstall
	helm.sh/helm/v3/cmd/helm/install.go:316
main.newTemplateCmd.func2
	helm.sh/helm/v3/cmd/helm/template.go:95
github.com/spf13/cobra.(*Command).execute
	github.com/spf13/cobra@v1.8.1/command.go:985
github.com/spf13/cobra.(*Command).ExecuteC
	github.com/spf13/cobra@v1.8.1/command.go:1117
github.com/spf13/cobra.(*Command).Execute
	github.com/spf13/cobra@v1.8.1/command.go:1041
main.main
	helm.sh/helm/v3/cmd/helm/helm.go:85
runtime.main
	runtime/proc.go:272
runtime.goexit
	runtime/asm_arm64.s:1223
➜  …/Kubernetes/helm-myprj-01
```

### C. Install/Upgrade a Helm chart
```shell
➜  …/Users/thaovtran helm upgrade --install tinyweb-app-mongo Kubernetes/helm-myprj-01/tinyweb-app-mongo-0.1.0.tgz --create-namespace --namespace tinyweb-app-mongo-ns
Release "tinyweb-app-mongo" has been upgraded. Happy Helming!
NAME: tinyweb-app-mongo
LAST DEPLOYED: Thu Nov  7 20:00:59 2024
NAMESPACE: tinyweb-app-mongo
STATUS: deployed
REVISION: 3
NOTES:
1. Get the application URL by running these commands:

2. Access Mongo Express using the following URL http://mongodb-helm.k8s.local if ingress is enabled.
➜  …/Users/thaovtran
```
```shell
helm upgrade --install tinyweb-app my-helm-charts/tinyweb-app-mongo --create-namespace --namespace tinyweb-app-ns
helm upgrade tinyweb-app my-helm-charts/tinyweb-app-mongo --create-namespace --namespace tinyweb-app-ns
```

### D. Uninstall/Install a Helm chart
```shell
helm uninstall tinyweb-app --namespace tinyweb-app-ns
helm install tinyweb-app my-helm-charts/tinyweb-app-mongo --create-namespace --namespace tinyweb-app-ns
helm install tinyweb-app Kubernetes/helm-myprj-01/tinyweb-app-mongo-0.1.0.tgz --create-namespace --namespace tinyweb-app-ns
```

### E. Staus check Helm chart installation
```shell
helm status tinyweb-app --namespace tinyweb-app-ns
```


## Helm repo works
### List repos
```shell
➜  …/Users/thaovtran
➜  …/Users/thaovtran helm repo list
NAME             	URL
k8s-dashboard    	https://kubernetes.github.io/dashboard/
ingress-nginx    	https://kubernetes.github.io/ingress-nginx
my-helm-charts   	https://thawtran.github.io/my-charts
➜  …/Users/thaovtran
➜  …/Users/thaovtran
```

### Update repos
```shell
➜  …/Users/thaovtran
➜  …/Users/thaovtran helm repo update my-helm-charts
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "my-helm-charts" chart repository
Update Complete. ⎈Happy Helming!⎈
➜  …/Users/thaovtran
```

### Search charts in a repo
```shell
➜  …/Users/thaovtran
➜  …/Users/thaovtran helm search repo my-helm-charts
NAME                             	CHART VERSION	APP VERSION	DESCRIPTION
my-helm-charts/helm-chart-pkg    	0.1.0        	1.16.0     	A Helm chart for Kubernetes
my-helm-charts/tst-helm-chart-pkg	0.1.1        	1.16.0     	A Helm chart for Kubernetes
➜  …/Users/thaovtran
```

### List all versions of a chart
```shell
➜  …/Users/thaovtran
➜  …/Users/thaovtran helm search repo my-helm-charts/tst-helm-chart-pkg --versions
NAME                             	CHART VERSION	APP VERSION	DESCRIPTION
my-helm-charts/tst-helm-chart-pkg	0.1.1        	1.16.0     	A Helm chart for Kubernetes
my-helm-charts/tst-helm-chart-pkg	0.1.0        	1.16.0     	A Helm chart for Kubernetes
➜  …/Users/thaovtran
```
