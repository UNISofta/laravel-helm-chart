## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

```bash
helm repo add laravel-helm-chart https://unisofta.github.io/laravel-helm-chart
```

If you had already added this repo earlier, run `helm repo update` to retrieve the latest versions of the packages.   
You can then run `helm search repo laravel-helm-chart` to see the charts.

To install the nmrxiv chart:

    helm install my-nmrxiv laravel-helm-chart/nmrxiv

To uninstall the chart:

    helm delete my-nmrxiv