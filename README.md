# Kubernetes-PlantUML

These are the PlantUML sprites, macros and stereotypes for creating PlantUML diagrams with the Kubernetes components.
The official Kubernetes Icons Set (where this work is based) can be found ![here](https://github.com/kubernetes/community/tree/master/icons)

This repo is heavily influenced by the awesome work from Ricardo Niepel on ![Azure-PlantUML](https://github.com/RicardoNiepel/Azure-PlantUML)

## Getting Started

If you're familiar with PlantUML this is what you need:
```vim
' Kubernetes
!define KubernetesC4 https://raw.githubusercontent.com/dcasati/kubernetes-PlantUML/master/
!includeurl KubernetesC4/kubernetes_C4.puml  
!includeurl KubernetesC4/kubernetes_Container.puml
!includeurl KubernetesC4/kubernetes_Context.puml

!define KubernetesPuml https://raw.githubusercontent.com/dcasati/kubernetes-PlantUML/master/dist
!includeurl KubernetesPuml/OSS/KubernetesPod.puml
!includeurl KubernetesPuml/OSS/KubernetesPsp.puml
!includeurl KubernetesPuml/OSS/KubernetesPv.puml
!includeurl KubernetesPuml/OSS/KubernetesPvc.puml

[...]
```
A basic `hello world` would look like this:

```vim
@startuml kubernetes

footer Kubernetes Plant-UML
scale max 1024 width

skinparam nodesep 10
skinparam ranksep 10

' Azure
!define AzurePuml https://raw.githubusercontent.com/RicardoNiepel/Azure-PlantUML/release/2-1/dist

!includeurl AzurePuml/AzureCommon.puml
!includeurl AzurePuml/AzureSimplified.puml

' Kubernetes
!define KubernetesC4 https://raw.githubusercontent.com/dcasati/kubernetes-PlantUML/master
!includeurl KubernetesC4/kubernetes_Context.puml

!define KubernetesPuml https://raw.githubusercontent.com/dcasati/kubernetes-PlantUML/master/dist

!includeurl KubernetesPuml/OSS/KubernetesSvc.puml
!includeurl KubernetesPuml/OSS/KubernetesPod.puml

actor "User" as userAlias
left to right direction

' Kubernetes Components
Cluster_Boundary(cluster, "Kubernetes Cluster") {
    Namespace_Boundary(ns, "Web") {
        KubernetesSvc(svc, "service", "")
        KubernetesPod(pod1, "web-pod1", "")
        KubernetesPod(pod2, "web-pod2", "")
    }
}

Rel(userAlias,svc,"get HTTP/1.1 index.html", "1")
Rel(svc,pod1,"load Balances to Pods", "2")
Rel(svc,pod2,"load Balances to Pods", "2")
Rel_U(pod1, svc, "serves content", "3")
Rel(svc, userAlias, "return content to", "4")
@enduml
```

A more complete example

```vim
@startuml kubernetes

footer Kubernetes Plant-UML
scale max 1024 width

skinparam nodesep 10
skinparam ranksep 10

' Azure
!define AzurePuml https://raw.githubusercontent.com/RicardoNiepel/Azure-PlantUML/release/2-1/dist

!includeurl AzurePuml/AzureCommon.puml
!includeurl AzurePuml/AzureSimplified.puml

' Kubernetes
!define KubernetesC4 https://raw.githubusercontent.com/dcasati/kubernetes-PlantUML/master
'!includeurl KubernetesC4/kubernetes_C4.puml
'!includeurl KubernetesC4/kubernetes_Container.puml
!includeurl KubernetesC4/kubernetes_Context.puml

!define KubernetesPuml https://raw.githubusercontent.com/dcasati/kubernetes-PlantUML/master/dist

!includeurl KubernetesPuml/OSS/KubernetesApi.puml
!includeurl KubernetesPuml/OSS/KubernetesSvc.puml
!includeurl KubernetesPuml/OSS/KubernetesIng.puml
!includeurl KubernetesPuml/OSS/KubernetesPod.puml
!includeurl KubernetesPuml/OSS/KubernetesRs.puml
!includeurl KubernetesPuml/OSS/KubernetesDeploy.puml
!includeurl KubernetesPuml/OSS/KubernetesHpa.puml

actor "User" as userAlias
left to right direction

' Kubernetes Components
Cluster_Boundary(cluster, "Kubernetes Cluster") {
    Namespace_Boundary(ns, "Back End") {
        KubernetesIng(ingress, "your.domain.com", "")
        KubernetesSvc(svc, "service", "")
        KubernetesPod(pod1, "", "")
        KubernetesPod(pod2, "", "")
        KubernetesPod(pod3, "", "")
        KubernetesRs(rs,"","")
        KubernetesDeploy(deploy,"deployment","")
        KubernetesHpa(hpa, "HPA", "")
    }
}

Rel(userAlias,ingress," ")
Rel(ingress,svc," ")

Rel(svc,pod1," ")
Rel(svc,pod2," ")
Rel(svc,pod3," ")

Rel_U(rs,pod1," ")
Rel_U(rs,pod2," ")
Rel_U(rs,pod3," ")

Rel_U(deploy,rs, " ")
Rel_U(hpa,deploy, " ")

@enduml
```

## List of Supported Symbols
Category | Macro (Name) | <pre>Color</pre> | <pre>Mono </pre> | Url
  ---    |  ---  | :---:  | :---: | ---
**OSS** | | | | **OSS/all.puml**
OSS | KubernetesCronjob </br> (Kubernetes Cronjob) |  |![KubernetesCronjob](dist/OSS/KubernetesCronjob(m).png?raw=true) | OSS/KubernetesCronjob.puml
OSS | KubernetesGroup </br> (Kubernetes Group) |  |![KubernetesGroup](dist/OSS/KubernetesGroup(m).png?raw=true) | OSS/KubernetesGroup.puml
OSS | KubernetesPsp </br> (Kubernetes Psp) |  |![KubernetesPsp](dist/OSS/KubernetesPsp(m).png?raw=true) | OSS/KubernetesPsp.puml
OSS | KubernetesRole </br> (Kubernetes Role) |  |![KubernetesRole](dist/OSS/KubernetesRole(m).png?raw=true) | OSS/KubernetesRole.puml
OSS | KubernetesApi </br> (Kubernetes Api) |  |![KubernetesApi](dist/OSS/KubernetesApi(m).png?raw=true) | OSS/KubernetesApi.puml
OSS | KubernetesJob </br> (Kubernetes Job) |  |![KubernetesJob](dist/OSS/KubernetesJob(m).png?raw=true) | OSS/KubernetesJob.puml
OSS | KubernetesCm </br> (Kubernetes Cm) |  |![KubernetesCm](dist/OSS/KubernetesCm(m).png?raw=true) | OSS/KubernetesCm.puml
OSS | KubernetesMaster </br> (Kubernetes Master) |  |![KubernetesMaster](dist/OSS/KubernetesMaster(m).png?raw=true) | OSS/KubernetesMaster.puml
OSS | KubernetesKproxy </br> (Kubernetes Kproxy) |  |![KubernetesKproxy](dist/OSS/KubernetesKproxy(m).png?raw=true) | OSS/KubernetesKproxy.puml
OSS | KubernetesCrd </br> (Kubernetes Crd) |  |![KubernetesCrd](dist/OSS/KubernetesCrd(m).png?raw=true) | OSS/KubernetesCrd.puml
OSS | KubernetesDs </br> (Kubernetes Ds) |  |![KubernetesDs](dist/OSS/KubernetesDs(m).png?raw=true) | OSS/KubernetesDs.puml
OSS | KubernetesSc </br> (Kubernetes Sc) |  |![KubernetesSc](dist/OSS/KubernetesSc(m).png?raw=true) | OSS/KubernetesSc.puml
OSS | KubernetesCrb </br> (Kubernetes Crb) |  |![KubernetesCrb](dist/OSS/KubernetesCrb(m).png?raw=true) | OSS/KubernetesCrb.puml
OSS | KubernetesSched </br> (Kubernetes Sched) |  |![KubernetesSched](dist/OSS/KubernetesSched(m).png?raw=true) | OSS/KubernetesSched.puml
OSS | KubernetesLimits </br> (Kubernetes Limits) |  |![KubernetesLimits](dist/OSS/KubernetesLimits(m).png?raw=true) | OSS/KubernetesLimits.puml
OSS | KubernetesQuota </br> (Kubernetes Quota) |  |![KubernetesQuota](dist/OSS/KubernetesQuota(m).png?raw=true) | OSS/KubernetesQuota.puml
OSS | KubernetesVol </br> (Kubernetes Vol) |  |![KubernetesVol](dist/OSS/KubernetesVol(m).png?raw=true) | OSS/KubernetesVol.puml
OSS | KubernetesSa </br> (Kubernetes Sa) |  |![KubernetesSa](dist/OSS/KubernetesSa(m).png?raw=true) | OSS/KubernetesSa.puml
OSS | KubernetesKubelet </br> (Kubernetes Kubelet) |  |![KubernetesKubelet](dist/OSS/KubernetesKubelet(m).png?raw=true) | OSS/KubernetesKubelet.puml
OSS | KubernetesPvc </br> (Kubernetes Pvc) |  |![KubernetesPvc](dist/OSS/KubernetesPvc(m).png?raw=true) | OSS/KubernetesPvc.puml
OSS | KubernetesCcm </br> (Kubernetes Ccm) |  |![KubernetesCcm](dist/OSS/KubernetesCcm(m).png?raw=true) | OSS/KubernetesCcm.puml
OSS | KubernetesSts </br> (Kubernetes Sts) |  |![KubernetesSts](dist/OSS/KubernetesSts(m).png?raw=true) | OSS/KubernetesSts.puml
OSS | KubernetesNetpol </br> (Kubernetes Netpol) |  |![KubernetesNetpol](dist/OSS/KubernetesNetpol(m).png?raw=true) | OSS/KubernetesNetpol.puml
OSS | KubernetesCrole </br> (Kubernetes Crole) |  |![KubernetesCrole](dist/OSS/KubernetesCrole(m).png?raw=true) | OSS/KubernetesCrole.puml
OSS | KubernetesRs </br> (Kubernetes Rs) |  |![KubernetesRs](dist/OSS/KubernetesRs(m).png?raw=true) | OSS/KubernetesRs.puml
OSS | KubernetesNode </br> (Kubernetes Node) |  |![KubernetesNode](dist/OSS/KubernetesNode(m).png?raw=true) | OSS/KubernetesNode.puml
OSS | KubernetesSecret </br> (Kubernetes Secret) |  |![KubernetesSecret](dist/OSS/KubernetesSecret(m).png?raw=true) | OSS/KubernetesSecret.puml
OSS | KubernetesNs </br> (Kubernetes Ns) |  |![KubernetesNs](dist/OSS/KubernetesNs(m).png?raw=true) | OSS/KubernetesNs.puml
OSS | KubernetesDeploy </br> (Kubernetes Deploy) |  |![KubernetesDeploy](dist/OSS/KubernetesDeploy(m).png?raw=true) | OSS/KubernetesDeploy.puml
OSS | KubernetesUser </br> (Kubernetes User) |  |![KubernetesUser](dist/OSS/KubernetesUser(m).png?raw=true) | OSS/KubernetesUser.puml
OSS | KubernetesPv </br> (Kubernetes Pv) |  |![KubernetesPv](dist/OSS/KubernetesPv(m).png?raw=true) | OSS/KubernetesPv.puml
OSS | KubernetesEp </br> (Kubernetes Ep) |  |![KubernetesEp](dist/OSS/KubernetesEp(m).png?raw=true) | OSS/KubernetesEp.puml
OSS | KubernetesSvc </br> (Kubernetes Svc) |  |![KubernetesSvc](dist/OSS/KubernetesSvc(m).png?raw=true) | OSS/KubernetesSvc.puml
OSS | KubernetesRb </br> (Kubernetes Rb) |  |![KubernetesRb](dist/OSS/KubernetesRb(m).png?raw=true) | OSS/KubernetesRb.puml
OSS | KubernetesEtcd </br> (Kubernetes Etcd) |  |![KubernetesEtcd](dist/OSS/KubernetesEtcd(m).png?raw=true) | OSS/KubernetesEtcd.puml
OSS | KubernetesIng </br> (Kubernetes Ing) |  |![KubernetesIng](dist/OSS/KubernetesIng(m).png?raw=true) | OSS/KubernetesIng.puml
OSS | KubernetesHpa </br> (Kubernetes Hpa) |  |![KubernetesHpa](dist/OSS/KubernetesHpa(m).png?raw=true) | OSS/KubernetesHpa.puml
