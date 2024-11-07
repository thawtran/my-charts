# my-charts
The Helm charts repository


## HomePage
https://thawtran.github.io/my-charts


## RepoIndexUrl
https://thawtran.github.io/my-charts/index.yaml


## How to work

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

## Helm repo commands
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
