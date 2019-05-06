# API Versioning Best Practices
Change is inevitable and growth is a good thing. When your API reaches the point where it expands beyond its 
original purpose and capacity, it's time to consider the next **version**.

Whether the next iteration is an major version or just a feature extension, it's important to consider 
the pros and cons of informing your developers about it. Unlike traditional software versioning, API 
versioning can have significant effects on the products it uses downstream.

## One URI to Rule Them All
One school of thought is to focus on one unchanging URI with just one set of criteria for consumption. 
If the API structure is changed, resources altered, or parameter set modified, then the product is 
re-launched with the same URI. **This pushes the obligation to refactor code to downstream developers.**
This approach is not particularly easy to use in a world dominated by microservices.

## Semantic Versioning in the URI
What can we learn from the versioning practices of established web API providers? 
[Google](https://cloud.google.com/apis/design/versioning) comes out of the gate with a blunt affirmation 
of numbered versioning: **Networked APIs should use Semantic Versioning.**

##
Which approach is now called **Best Practices** has evolved over time and is also shaped by the choice of 
platform. When it comes to choosing an approach for versioning a HTTP REST interface, Kubernetes uses the 
approach of encoding it in the URL. If you wonder - kubernetes is strongly influenced by Google and here 
URI encoding was nominated as **best practice**.

Example REST enpoints in a kubernetes cluster:

```
elasticsearch-logging is running at https://104.197.5.247/api/v1/namespaces/kube-system/services/elasticsearch-logging/proxy
kibana-logging is running at https://104.197.5.247/api/v1/namespaces/kube-system/services/kibana-logging/proxy
kube-dns is running at https://104.197.5.247/api/v1/namespaces/kube-system/services/kube-dns/proxy
grafana is running at https://104.197.5.247/api/v1/namespaces/kube-system/services/monitoring-grafana/proxy
heapster is running at https://104.197.5.247/api/v1/namespaces/kube-system/services/monitoring-heapster/proxy
```


**So if you want to go this way, Kubernetes offers excellent support to version your API endpoints and you are able to 
run your services in different versions separately.**


1. Replace in the ingress file `<GARDENER-CLUSTER>.<GARDENER-PROJECT>` accordingly and deploy the yaml files.
```
kubectl apply -f yaml
```
2. Call the following URLs and you will see that the response is different.
- api.ingress.`<GARDENER-CLUSTER>.<GARDENER-PROJECT>`.shoot.canary.k8s-hana.ondemand.com/api/v1/user
- api.ingress.`<GARDENER-CLUSTER>.<GARDENER-PROJECT>`.shoot.canary.k8s-hana.ondemand.com/api/v2/user
