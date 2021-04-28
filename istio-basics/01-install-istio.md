In this lab, you will install Istio and its addons. You will validate the installation is successfully and examinate the installation artifacts.

## Download Istio

Download the istio release binary:

```bash
curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.9.3 sh -
```

Add istioctl client to your path:

```bash
cd istio-1.9.3
export PATH=$PWD/bin:$PATH
```

Check istioctl version:

```bash
istioctl version
```

Check if your Kubernetes environment meets Istio's platform requirement:

```bash
istioctl x precheck
```

## Install Istio

List available installation profiles:

```bash
istioctl profile list
```

Since this is a get started workshop, let's use the demo profile.

```bash
istioctl install --set profile=demo -y
```

Check out the resources installed by Istio:

```bash
kubectl get all,cm,secrets -n istio-system
```

Check out CRDs installed by Istio:

```bash
kubectl get crds -n istio-system
```

Check out Istio resources installed by Istio and used by Istio internally:

```bash
kubectl get istio-io -n istio-system
```

## Install Istio Telemetry Addons

Istio telemetry addons are shipped as samples because these addons are optimized for quick get started and demo purpose and not for production usage. They provides a convenient way to install these telemetry components that integrate with Istio.

```bash
kubectl apply -f samples/addons
```

Verify you can access the Prometheus dashboard:

```bash
istioctl dashboard prometheus
```

Verify you can access the Grafana dashboard:

```bash
istioctl dashboard grafana
```

Verify you can access the Jaeger dashboard:

```bash
istioctl dashboard jaeger
```

Verify you can access the Kiali dashboard:

```bash
istioctl dashboard kiali
```

Congratulations, you have installed Istio and its addon components successfully.  We'll explore expose and secure your services to Istio ingress gateway in the [next lab](./02-secure-service-ingress.md).



