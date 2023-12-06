# dance-standard-gitops

# Gitops Repo Patterns

This repository contains a set of gitops repository format components for use with the tad template gitops cli

# Install

To configured your `tad` cli to use this template repo use 

`tad set-repo https://github.com/redhat-appstudio/tssc-sample-gitops`

Ensure its installed 

`tad describe` which will show its location as your template source 


example output 
```
Template Repository: https://github.com/jduimovich/dance-standard-gitops.git
Template Directory: /home/john/.tad/templates/templates
```

# Example usage

## Bootstrap a new gitops repo called `reponame` and add a component

``` 
tad bootstrap reponame
cd reponame
tad describe
tad add-component c1 http
tad describe
```

The c1 component will be running 

### http 
    - contains a deployment, service and route for an image listening on port 8080
    - this matches the current RHTAP default deployment
    
### service 
    - contains a deployment, service listening on port 8080
    - this is a template which is similar to the http one, however does not expose a route, so an internal service only. 

### http-ab 
    - contains a deployment, service and route listening on port 8080
    - the route  supports A/B load splitting between two components 
    ```  
        tad set c1 service-a  80
        tad set c1 service-b  20 

## route-ab 
    - contains a route  supports A/B load splitting between two components initialized
    ```  
        tad add-component c1 service 
        tad add-component c2 service 
        tab set image c1 quay.io/jduimovich/fib-go
        tab set image c2 quay.io/jduimovich/fib-node
        tad add-component c3 route-ab
        tad set c3 service-a  80
        tad set c3 service-b  20
    ```

