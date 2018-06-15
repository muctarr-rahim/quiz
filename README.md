# Quiz App
Simple EventSourcing example using .NET Core, React, Docker, Jenkins and K8s.

* run with [**docker**](https://www.docker.com/products/docker) from bash with ``.\run.sh`` 
  
  Open <http://localhost> for quiz voting and <http://localhost?results> for quiz results
  
* run with [**minikube**](https://github.com/kubernetes/minikube)

  * Start   
  
  ```minikube start --memory=4096 --cpus=4 --vm-driver=hyperkit```

  * Export the following environment variables:
  
  ```bash
  QUIZ_ENVIRONMENT='pro'
  REGISTRY=localhost:30400
  TAG=latest
  INGRESS_DOMAIN='quiz.internal'

  RABBIT_PASSWORD=changeit
  POSTGRES_PASSWORD=changeit
  JENKINS_PASSWORD=changeit

  GITHUB_REPO=netcorebcn/quiz
  GITHUB_USER=mygithubuser
  GITHUB_TOKEN='<TOKEN>'
  ```

  * Execute bash script ```./setup.sh```

  * Add ingress hosts to local host file 
  
  ```echo $(minikube ip) {jenkins,rabbit,registry}.quiz.internal quiz.internal | sudo tee -a /etc/hosts```

  **__Notes__**:
    For automatic dns wilcards resolution use [dnsmasq](https://blog.thesparktree.com/local-development-with-wildcard-dns)

  * Open <http://jenkins.quiz.internal/job/quiz/> and Build!

  * Once its build Open <http://quiz.internal> and <http://quiz.internal?results> 


  * Github integration for Pull Request workflow

    * Add Integration & Service: Manage Jenkins (GitHub plugin) 

      http://jenkins.quiz.internal/github-webhook/

    * For local jenkins integration you can use [ngrok](https://ngrok.com/) 
    
    ```bash 
    ./ngrok http jenkins.quiz.internal:80 -host-header=jenkins.quiz.internal
    ```

**Notes**: We aren't starting from the scratch. We are using ideas and code from other awesome repos.

* Running Jenkins in Docker

  <http://container-solutions.com/running-docker-in-jenkins-in-docker/>  

* K8s ingress configuration for ci cd with jenkins

  <https://github.com/kenzanlabs/kubernetes-ci-cd>

  <https://medium.com/@Oskarr3/setting-up-ingress-on-minikube-6ae825e98f82>

* Marten Event Store library for .NET and postgresql

  <https://github.com/JasperFx/marten>

* WebSockets helper classes thanks to  

  <https://github.com/radu-matei/websocket-manager>
  
* dnsmasq integrate with minikube

  <https://github.com/superbrothers/minikube-ingress-dns>
